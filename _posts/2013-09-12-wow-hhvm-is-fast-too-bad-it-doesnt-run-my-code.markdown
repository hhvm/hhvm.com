---
author: joelm
comments: true
layout: post
title: Wow HHVM is fast...too bad it doesn’t run my code
category: blog
redirect_from:
  - /blog/875/wow-hhvm-is-fast-too-bad-it-doesnt-run-my-code
---

HHVM is a highly performant PHP runtime. In fact, it is nearly 40% faster than [HPHPc](http://en.wikipedia.org/wiki/HipHop_for_PHP#History_Before_HHVM), and only getting faster. For example, the HHVM team just rewrote the JIT to use an [SSA intermediate representation (IR)](https://github.com/facebook/hiphop-php/blob/master/hphp/doc/ir.specification). HHIR (HipHop Intermediate Representation) is a strongly typed, SSA-form intermediate representation, positioned between HHBC (HipHop Bytecode) and machine code. It allows HHVM to perform optimizations that were very difficult to perform with the old JIT, using the context of the current runtime environment (e.g., reference counting elision).

![HHVM Performance with addition of IR](/static/images/posts/ir_chart-e13788785293871.png)
<center><i>HHVM Performance with addition of IR</i></center>

Facebook continues to use fewer resources because of the continual performance increases provided by HHVM. However, there is a problem...

![HHVM fatals on Laravel unit tests.](/static/images/posts/hhvm_fatal-e13788786622871.png)
<center><i>HHVM fatals on Laravel unit tests.</i></center>

Performance is critical, but it isn’t everything. In order to gain broader adoption for HHVM, being able to run popular frameworks is a must; in other words, we can have the highest performing PHP runtime, but if doesn’t run real-world code without a lot of pain, then it won’t be used widely. Understanding this, we are putting serious resources around parity with the PHP runtime.

The table below shows the team’s current progress towards parity with [20+ of the most popular frameworks used with PHP today](https://github.com/search?l=php&q=stars%3A%3E1&s=stars&type=Repositories). These frameworks come with unit tests that are run via [PHPUnit](https://github.com/sebastianbergmann/phpunit/). The unit tests provide a good indication of how well a framework will ultimately run when used in production. The unit tests were run on CentOS 6 from the latest branch of the framework from GitHub, on the latest development build of HHVM.

Framework | % Unit Tests Pass on HHVM | % Unit Tests Failing on HHVM | % Unit Tests Causing HHVM to Fatal/Seg Fault [1]
--------- | ------------------------- | ---------------------------- | ------------------------------------------------
[PHPUnit](https://github.com/sebastianbergmann/phpunit) [2] | 90 | 10 | 0
[Composer](https://github.com/composer/composer) | 97 | 3 | < 1
[Symfony](https://github.com/symfony/symfony) | 91 | 9 | < 1
[CakePHP](https://github.com/cakephp/cakephp) | 0 | Tests won't run [3] | Tests won't run
[Wordpress](https://github.com/kurtpayne/wordpress-unit-tests) | 76 | 24 | < 1
[Joomla](https://github.com/joomla/joomla-platform) | 0 | Tests won't run [4] | Tests won't run
[phpBB](https://github.com/phpbb/phpbb3) | 0 | 100 [5] | 0
[PHPMyAdmin](https://github.com/phpmyadmin/phpmyadmin) | 0 | Tests won't run [6] | Tests won't run
[Laravel](https://github.com/laravel/laravel) | 95 | 3 | 2
[zf2](https://github.com/zendframework/zf2) | 0 | Tests won't run [7] | Tests won't run
[yii](https://github.com/yiisoft/yii) | 92 | 8 | <1
[Slim](https://github.com/codeguy/Slim) | 99 | 1 | 0
[Facebook PHP SDK](https://github.com/facebook/facebook-php-sdk) | 100 | 0 | 0
[Doctrine](https://github.com/doctrine/doctrine2) | 0 | Tests won't run [8] | Tests won't run
[Assetic](https://github.com/kriswallsmith/assetic) | 80 | 20 | 0
[Twig](https://github.com/fabpot/Twig) | 78 | 22 | 0
[Drupal](https://github.com/drupal/drupal) | 98 | 2 | 0
[Paris](https://github.com/j4mie/paris) [9] | 100 | 0 | 0
[Idiorm](https://github.com/j4mie/idiorm) [9] | 100 | 0  | 0
[CodeIgniter](https://github.com/EllisLab/CodeIgniter) | 81 | 19 | < 1
[Magento](https://github.com/magento/magento2) | 0 | Tests won't run [10] | Tests won't run

It is clear that HHVM is lacking in full support for these frameworks. The first step is to implement the functionality that is causing the HHVM to fatal with some of these unit tests. From the results, in addition to bugs, the HHVM team now knows that it is lacking in support for:


  * Intl (internationalization), MySQLi, ZipArchive, RegexIterator


  * Unimplemented functions such as `str_getcsv`, `stream_context_get_options`


  * Richer DOM, Phar and FileInfo support


  * Support for php.ini and associated options


  * Better autoloading support


After ensuring that all unit tests can be run to completion (i.e. no more fatals), the team will continue to implement the functionality that is causing the tests to fail. In parallel, the team will be working to implement any functionality required to allow these frameworks to run on HHVM in the real world (e.g., ensuring the base cases and tutorials can run). Blog posts will be coming soon on how to run the unit tests for each framework on HHVM and/or getting the actual frameworks to run on HHVM (hopefully with less and less workarounds as functionality is implemented).

The HHVM team’s goal is to reach at least parity with the PHP runtime on these (and other) frameworks (the PHP runtime passes the unit tests anywhere from 95-100%) [11]. Plans are in the works to have a near-live dashboard showing the progress on reaching this goal. If you do not see an important framework in our list that should be added to our testing, please comment below and we will add it.

Moving forward, the HHVM team is going to increase the amount of information around the status of HHVM. Parity status is just one piece of this puzzle. Here is an idea of the plans for the HHVM team in the next 6-12 months:


  * Top PHP Framework parity


  * Updated HHVM documentation


  * First class support for open source contributions


  * Easy install of HHVM on Linux


  * PHP language improvements (e.g., type hints for scalars)


While our small team is aggressively trying to improve HHVM, we know that we cannot address all compatibility concerns as quickly as we would like. Thus, [we sincerely welcome contributions](https://github.com/facebook/hiphop-php#contributing), particularly any that can help HHVM reach parity with your desired workload(s). The team will be happy to review and assist with pull requests. Particular thanks to [Daniel Sloof](https://github.com/danslo), [Markus Staab](https://github.com/staabm), [Vadim Borodavko](https://github.com/javer), [Kristaps Kaupe](https://github.com/kristapsk), [huzhiguang](https://github.com/huzhiguang), and the many others in the community currently pushing commits to our source base.

If you do not have a specific workload or application in mind, but still would like to be involved in HHVM, please look at the issues tagged _[zend incompatibility](https://github.com/facebook/hiphop-php/issues?labels=zend+incompatibility&page=1&state=open)_ for known conflicts with the PHP runtime. Tests can be added easily (see the [README](https://github.com/facebook/hiphop-php/blob/master/hphp/test/README.md)) and [Travis-CI](https://travis-ci.org/) is integrated, which provides quick and reliable test results on commits. Visit us on IRC channel [#hhvm on freenode](http://webchat.freenode.net/?channels=hhvm) if you need further guidance.

We know there is work to do, but the HHVM team’s #1 priority right now is being able to run all the (sane) PHP code in the wild.


#### Footnotes


1. Tests that cause HHVM to fatal were commented out and replaced with a return of `$this->fail("HHVM Fatals");` which causes the test to fail, but allow the test suite to continue running.

2. The PHPUnit self-check tests were not run with PHPUnit directly; rather it comes with a self install test that was run, from the source root, via a command similar to ‘`hhvm phpunit.php --verbose`’. Also, as of now, the tests will only complete when provided with a `--debug` or `--verbose` flag; otherwise there is a segmentation fault. That said, PHPUnit does run well enough to be used to execute the unit tests for all the other frameworks.

3. CakePHP has a class named `String`. HHVM does not allow, by default, for classes to have names of primitives. HHVM has other bugs around `preg_replace_callback()` and autoloading of classes ([https://github.com/facebook/hiphop-php/pull/959](https://github.com/facebook/hiphop-php/pull/959)).

4. The Joomla unit tests do not currently run because of autoloading issues related to: [https://github.com/facebook/hiphop-php/pull/959](https://github.com/facebook/hiphop-php/pull/959)

5. All 2010 phpBB unit tests fail, and all fail for one reason. There is a method called `setValue()` that takes two parameters, but throughout the testing only one parameter is provided (and no default value for the second parameter is given). HHVM does not allow this.

6. PHPMyAdmin requires mysqli immediately, and HHVM does not support this.

7. zf2 requires the Intl (internationalization) extension, and HHVM does not support this.

8. Doctrine2 has certain classes that implement interfaces, but these classes do not implement these interfaces fully. HHVM requires classes that implement interfaces to be compatible with the interfaces they implement.

9. A pull request was made for Paris and Idiorm to change their tests to better support HHVM, but to also be more correct: [https://github.com/j4mie/idiorm/pull/143](https://github.com/j4mie/idiorm/pull/143)

10. Magento fatals immediately with the following error message: "HipHop Fatal error: Class Mock_Mage_Core_Controller_Varien_ActionAbstract_839dc612 contains abstract method (dispatch) and must therefore be declared abstract or implement the remaining methods". We believe it is a problem with the HHVM `ReflectionMethod` implementation.


10. The PHP runtime tests were run with a source-code compiled version of PHP 5.5.4 on CentOS 6, with the following configuration:

`./configure --prefix=/home/joelm/php55 --with-mysql --with-pdo-mysql --with-curl --with-openssl --with-mcrypt --enable-mbstring --enable-pcntl --with-mysqli --enable-intl --with-pdo-pgsql --with-pgsql --with-libxml-dir --enable-opcache --enable-calendar --enable-sockets --enable-zip --enable-soap --with-zlib --with-gd --with-bz2`
