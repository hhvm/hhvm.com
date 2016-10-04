---
author: wizkid
layout: post
title: Implementing MySQLi
category: blog
permalink: /blog/3689/implementing-mysqli
comments:
- id: 2921
  author: Chase Christian
  author_email: madsushi@gmail.com
  author_url: http://www.armoryplus.com
  date: '2014-02-26 13:32:32 +0000'
  date_gmt: '2014-02-26 21:32:32 +0000'
  content: |-
    Thanks WizKid! I was one of the people waiting on the MySQLi and implemented it as soon as your commits were pushed to the nightly build. It has been working great! I haven't had any issues across multiple sites using MySQLi.

    Thanks again!
- id: 2927
  author: WizKid
  author_email: hesslow@gmail.com
  author_url: ''
  date: '2014-02-26 13:57:37 +0000'
  date_gmt: '2014-02-26 21:57:37 +0000'
  content: Awesome to hear.
- id: 2933
  author: Marco Pivetta
  author_email: ocramius@gmail.com
  author_url: http://ocramius.github.io/
  date: '2014-02-26 14:32:06 +0000'
  date_gmt: '2014-02-26 22:32:06 +0000'
  content: |-
    Awesome! I have just <a>enabled HHVM+MySQLi for Doctrine DBAL<&#47;a> on <a href="https:&#47;&#47;travis-ci.org&#47;doctrine&#47;dbal&#47;jobs&#47;19685616" rel="nofollow">Travis-CI<&#47;a> as a reference :-)

    Hope to see green there soon!
- id: 2939
  author: Fred Emmott
  author_email: fe@fb.com
  author_url: ''
  date: '2014-02-26 21:44:56 +0000'
  date_gmt: '2014-02-27 05:44:56 +0000'
  content: This is currently only in the nightly builds, and master, which aren't
    supported by Travis; these tests will (hopefully :p ) start passing once 2.5.0
    is released and Travis upgrade.
- id: 2945
  author: Daniel
  author_email: danieru.dressler@gmail.com
  author_url: ''
  date: '2014-02-26 23:15:07 +0000'
  date_gmt: '2014-02-27 07:15:07 +0000'
  content: I'm looking forward to this!
- id: 2951
  author: Ulf Wendel
  author_email: ulf.wendel@phpdoc.de
  author_url: http://blog.ulf-wendel.de
  date: '2014-02-27 02:51:06 +0000'
  date_gmt: '2014-02-27 10:51:06 +0000'
  content: Glad to hear that you found the php.net ext&#47;mysqli&#47;tests to be
    that strict and picky that they make you scratch your head.... Only picky tests
    can detect changes made without documenting them.
- id: 2957
  author: ms
  author_email: mariusz.szydzik@googlemail.com
  author_url: ''
  date: '2014-02-27 03:51:05 +0000'
  date_gmt: '2014-02-27 11:51:05 +0000'
  content: Any plans for mysqlnd modules like mysqlnd_ms?
- id: 2963
  author: WizKid
  author_email: hesslow@gmail.com
  author_url: ''
  date: '2014-02-27 10:13:08 +0000'
  date_gmt: '2014-02-27 18:13:08 +0000'
  content: Didn't even know that there existed other modules for mysqlnd. Currently
    there is no plan from our side but we would be happy to take pull requests.
- id: 2969
  author: CJ
  author_email: smoogro@gmail.com
  author_url: ''
  date: '2014-02-27 14:40:35 +0000'
  date_gmt: '2014-02-27 22:40:35 +0000'
  content: '"Zend" is a company, not an implementation of PHP.'
- id: 2975
  author: Copyright Police
  author_email: police@php.net
  author_url: ''
  date: '2014-02-27 16:40:08 +0000'
  date_gmt: '2014-02-28 00:40:08 +0000'
  content: |-
    In the world of Facebook, do you not know the name of the programming languages you use?
    Or is this some sort of twisted way to rebrand PHP as Zend, and this hvvm abomination PHP?
- id: 2981
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2014-02-28 02:16:15 +0000'
  date_gmt: '2014-02-28 10:16:15 +0000'
  content: Zend is the engine that powered PHP4 and Zend 2 powers PHP5 (but most people
    just call it zend now since PHP4 is retired). https:&#47;&#47;en.wikipedia.org&#47;wiki&#47;Zend_Engine
- id: 2987
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2014-02-28 02:19:21 +0000'
  date_gmt: '2014-02-28 10:19:21 +0000'
  content: |-
    No twisting intended. What would you rather we call things? We need a name for the language (PHP) and the runtime available at php.net. Because the underlying engine is named zend, that is term we usually use: https:&#47;&#47;en.wikipedia.org&#47;wiki&#47;Zend_Engine

    Also, why do you think HHVM is an abomination? Are you just trolling or do you have some qualms with our project and there is something we should change?
- id: 2993
  author: Johannes
  author_email: johannes@schlueters.de
  author_url: http://schlueters.de
  date: '2014-02-28 11:03:55 +0000'
  date_gmt: '2014-02-28 19:03:55 +0000'
  content: |-
    For nitpicking: There is a company Zend Technologies Ltd., anengine called Zend Engine in different versions and a PHP runtie using it.
    The Zend Engine can be used for very few things in its own, but you need the PHP parts, like HTTP request handling or different PHP modules.
    Continueing to nitpick: mysqli is using APIs provided by the Zend Engine but is part of PHP. This can easily eseenin thelicenses headers. The ones in Zend&#47; say "Zend Engine, Copyright (c) 1998-2014 Zend Technologies Ltd. (http:&#47;&#47;www.zend.com)" the ones in other parts say " PHP Version 5 , Copyright (c) 1997-2014 The PHP Group" They also usedifferent licenses (Zend Engine License vs. PHP License)

    But as said this is nitpicking, inpractical terms the software is called PHP, is licensed under PHP Liense (Zend Engine License allows such relicensing) and is developed by a large comunity where even the company Zend Technologies Ltd. is just one between others.

    Historially the split was more relevant as there was a clear separation between both things and it was more possible to switch out the engine, nowadays, especially with PHP 5 OO APIs this isn't the case anymore. Also historically Zend (the company) was by far the largest contributor to the engine, that has changed and some independent contributors see it as unfair to be pulled in that way. I myself don't have thosestrictfeelings, but some do ...
- id: 2999
  author: Schien
  author_email: Schien@antradar.com
  author_url: http://www.antradar.com
  date: '2014-02-28 18:21:07 +0000'
  date_gmt: '2014-03-01 02:21:07 +0000'
  content: In Zend PHP there are benefits of using MySQLi over MySQL. Is the MySqli
    extension for HHVM just for parity I suppose? We changed the default db wrapper
    in our frameworks to MySQL so that they work with HHVM out of the box. There's
    no need to switch back to MySqli is there? Thanks.
- id: 3005
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2014-02-28 21:07:34 +0000'
  date_gmt: '2014-03-01 05:07:34 +0000'
  content: We don't mean to offend anyone, we just need names for things. What should
    we call the binary available on php.net? "The reference PHP implementation" is
    a bit long, "PHP" is confusing to the language, and "php-src" is a bit awkward
    as a noun.
- id: 3011
  author: Christopher Svanefalk
  author_email: christopher.svanefalk@gmail.com
  author_url: http://www.csvanefalk.com
  date: '2014-03-03 09:46:59 +0000'
  date_gmt: '2014-03-03 17:46:59 +0000'
  content: His name is "Copyright Police", seems like a pretty clearcut troll. Pity
    they find their way even to great project sites like this one.
- id: 3017
  author: Marco Pivetta
  author_email: ocramius@gmail.com
  author_url: http://ocramius.github.io/
  date: '2014-03-04 01:07:53 +0000'
  date_gmt: '2014-03-04 09:07:53 +0000'
  content: I already enforced DBAL to build on nightly ones - loads of tests are still
    failing though ;-)
---

I joined the HHVM team right before Christmas for a [hackamonth](https://www.facebook.com/notes/facebook-engineering/hackamonth-mixing-things-up/10150161285048920) (or, in my case, a hack-a-two-months).

<!--truncate-->

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
