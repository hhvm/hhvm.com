---
author: wizkid
comments: true
layout: post
title: Implementing MySQLi
category: blog
redirect_from:
  - /blog/3689/implementing-mysqli
---

I joined the HHVM team right before Christmas for a [hackamonth](https://www.facebook.com/notes/facebook-engineering/hackamonth-mixing-things-up/10150161285048920) (or, in my case, a hack-a-two-months).


## Getting My Feet Wet


To prepare for what was to be my big project, I rewrote the `ini` parser to better match Zend. This was released in HHVM 2.4.0. Interestingly, the parser was going to be shipped with HHVM 2.3.0; but when we tested the RC (release candidate), we noticed that we had a bunch of `ini` files at Facebook that the parser failed upon. So, I had to fix those files before we could release the new one.


## MySQLi


![MySQLi](/static/images/posts/MySQLi-logo1.png)

After warming up with the parser, I was ready to start my big project: implement [`MySQLi`](https://github.com/facebook/hhvm/tree/master/hphp/runtime/ext/mysql). This has been a[ long requested feature](https://github.com/facebook/hhvm/issues/362) for HHVM. And, this extension is required to help meet our [compatibility goals](http://www.hhvm.com/blog/2813/we-are-the-98-5-and-the-16).


### Preparation


`MySQLi` is not a trivial extension. As a PHP developer, I am so glad that [SaraG](http://www.hhvm.com/blog/author/sgolemon) has created [HNI](https://github.com/facebook/hhvm/blob/master/hphp/runtime/vm/native.h) (HHVM Native Interface), which makes it possible to write extensions in PHP directly instead of writing them in C++. Also, SaraG created a tool called [docskel.php](https://github.com/facebook/hhvm/blob/master/hphp/tools/docskel/docskel.php), which uses the [raw XML](https://svn.php.net/repository/phpdoc/en/trunk/reference/mysqli/mysqli/) that forms the [php.net](http://php.net) documentation to stub out the appropriate HNI-based signatures for extensions. While the documentation can be wrong sometimes when it comes to return types and parameter types, the stub generation saves a ton of time. After the stub generation, essentially the only work left  is to implement all the required functions.


### Implementation


For many of the MySQLi methods, it was simply a matter of essentially passing through calls to the older MySQL equivalent implementations. For example,[ `mysqli::real_escape_string()` just calls the implementation for `mysql_real_escape_string()`](https://github.com/facebook/hhvm/blob/8b0eacb8600240e01fef637c4efa650adf30babb/hphp/runtime/ext/mysql/ext_mysqli.php#L651-657).

`MySQLi` has both a procedural and an object-oriented interface. However, because we can write part of the extension in PHP, I could implement almost all of the procedural interface in PHP by just having it call the object-oriented interface. For example, [the procedurual function `mysqli_real_escape_string()` just calls the object-oriented function `mysqli::real_escape_string()`](https://github.com/facebook/hhvm/blob/8b0eacb8600240e01fef637c4efa650adf30babb/hphp/runtime/ext/mysql/ext_mysqli.php#L2174-2176).


### Testing


To test the correctness of my implementation, I used the [Zend test suite](https://github.com/php/php-src/tree/master/ext/mysqli/tests). There are about 300 tests in this test suite. However, these tests are not meant to be run in parallel. Many tests uses the same database table which, when running in parallel, will randomly make the test fail because some other test touched the same table at the same time. Running the tests in serial wasn't a great option because that would make development of `MySQLi` a lot slower. So, instead, I updated our [Zend import script](https://github.com/facebook/hhvm/blob/master/hphp/tools/import_zend_test.py#L1042-1265) to fix the tests to use different tables, thus avoiding the conflicts when running in parallel.

Another testing issue came with what we call [`ZendParamMode`](https://github.com/facebook/hhvm/commit/506f21c4b51c59b42e0997b0e25ba94e7d58149d). `ZendParamMode` is our flag to indicate the calling convention that Zend uses. In short, when using `ZendParamMode`, if a function is called with a parameter of the wrong type, a warning is logged and the function returns `null`. The problem is that functions in `HNI` that are implemented in PHP do not currently support `ZendParamMode`. So even if the function was doing everything correct, except how it handled `ZendParamMode`, the test would fail. This made it very hard to see what was implemented correctly and what was incorrect or missing. But, since making the function actually have correct behavior is more important than supporting `ZendParamMode`, I just changed the import script to remove most of the cases where `ZendParamMode` was tested.

After fixing the above issues, I was able to perform the normal "where does the test fail and fix it" methodology. This often included reading [Zend's `MySQLi` source code](https://github.com/php/php-src/tree/master/ext/mysqli) to determine what the right behavior should be.


### Overcoming Roadblocks


The most difficult part of the `MySQLi` implementation was [`mysqli_stmt::bind_param()`](https://github.com/facebook/hhvm/blob/3a1e50ab41b7597429a6a6bd66180bd97db28f23/hphp/runtime/ext/mysql/mysql_common.cpp#L1012) and [`mysqli_stmt::bind_result()`](https://github.com/facebook/hhvm/blob/3a1e50ab41b7597429a6a6bd66180bd97db28f23/hphp/runtime/ext/mysql/mysql_common.cpp#L1022). These methods take a variable number of arguments that are passed by reference. And, at the time, `HNI` did not support either. First SaraG added support for [variable number of arguments](https://github.com/facebook/hhvm/commit/1da26219aee94c96e5dd49f0f7cb757db7054a71), and then I added support for [variables as references](https://github.com/facebook/hhvm/commit/bee2a659c1fce24e4f095aec9a877d02ed43877a#diff-5efcf94e8073f338f5526fda610e797eL1116).

[`mysqli_multi_query()`](https://github.com/facebook/hhvm/blob/8b0eacb8600240e01fef637c4efa650adf30babb/hphp/runtime/ext/mysql/ext_mysqli.php#L1982) (and its friends [`mysqli_more_results()`](https://github.com/facebook/hhvm/blob/8b0eacb8600240e01fef637c4efa650adf30babb/hphp/runtime/ext/mysql/ext_mysqli.php#L1967) and [`mysqli_next_result()`](https://github.com/facebook/hhvm/blob/8b0eacb8600240e01fef637c4efa650adf30babb/hphp/runtime/ext/mysql/ext_mysqli.php#L1993)) were initially going to be a bit tricky since they were not part of Zend. However, just the opposite occurred. The reason for that is that HHVM already had implementations for `mysql_multi_query()`, `mysql_more_results()` and `mysql_next_result()`, so all I had to do was essentially do a pass through call to those functions.


## Current Status


We currently pass 182 of the Zend `MySQLi` tests. We fail 114. However, many of those 114 tests are failures are what I call "technicality" failures. For example, when we `var_dump()` a `double`, we print more digits which makes our output different from Zend.

For real-world compatibility, we pass 100% of [doctrine/dbal unit tests](https://github.com/doctrine/dbal) and we pass 100% of the [CodeIgniter unit tests](https://github.com/EllisLab/CodeIgniter) when running on MySQL.


## Missing Pieces


The biggest missing pieces when it comes to passing all Zend tests are:




  * Bugs that comes from the interaction between `MySQLi` and `php.ini`. Reading default values from `php.ini` is currently missing (but is being developed).


  * Sometimes we output different error messages which confuses the test runner when it compares output.


  * Zend has two different `MySQL` drivers. One is the normal `MySQL` C API and one is their own `MySQL` Native Driver. Because HHVM uses the `MySQL` C API we, don't support the functions that require the `MySQL` Native Driver. We may be able to work around this issue for some functions, but, for now, we don't support any of the functions that require `MySQL` Native Driver.


  * What happens when something goes wrong may be different between HHVM and Zend.




## What’s next?






  * Support `ZendParamMode` for PHP functions in HNI.


  * Make more of the 114 failing Zend tests pass.


  * The plan is to release `MySQLi` in [HHVM 2.5.0](https://github.com/facebook/hhvm/wiki/Release-Schedule). Please test the implementation as much as possible before the 2.5.0 release (you can [use a nightly](http://www.hhvm.com/blog/3203/nightly-packages)), so we can continue to fix bugs.
