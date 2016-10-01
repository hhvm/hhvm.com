---
author: ptarjan
comments: true
layout: post
title: HHVM 2.3.0 and Travis CI
category: blog
redirect_from:
  - /blog/2393/hhvm-2-3-0-and-travis-ci
---

We released a new version of HHVM today. This one includes all the hard work from our lockdown (detailed post to follow) and the ability to use [HHVM with FastCGI](http://www.hhvm.com/blog/1817/fastercgi-with-hhvm).


<!--truncate-->

  * [Ubuntu 12.04](https://github.com/facebook/hhvm/wiki/Prebuilt-Packages-on-Ubuntu-12.04)  / [13.10](https://github.com/facebook/hhvm/wiki/Prebuilt-Packages-on-Ubuntu-13.10)


  * [Debian 7](https://github.com/facebook/hhvm/wiki/Prebuilt-Packages-on-Debian-7)


  * [Fedora 20](https://github.com/facebook/hhvm/wiki/Prebuilt-Packages-on-Fedora-20)


I want to share with you our new release process. Instead of just arbitrarily cutting the source tree at a certain point, we are going to exactly mirror the internal Facebook release. That means the open source release will benefit from the week of internal testing and cherry-picks that are done getting hhvm ready to run facebook.com. Facebook does an hhvm push every 2 weeks, but this is a bit too fast for most distributions. So, for now, we are going push distro packages every 8 weeks and adjust if needed. We also want to do nightly package releases, so expect those to come out when we get some time (or complain loudly if you want them sooner).

As always, if you want to become the packager for a distro, great! Bundle it up and then update the [wiki](https://github.com/facebook/hhvm/wiki#installing-pre-built-packages-for-hhvm).


## Travis CI Support


I also have a really exciting announcement: [Travis CI](https://travis-ci.org/) now supports HHVM by default! It is [really](https://github.com/kriswallsmith/assetic/pull/548) [easy](https://github.com/yiisoft/yii/pull/3109) [to](https://github.com/codeguy/Slim/pull/698) [test](https://github.com/phpbb/phpbb/pull/1932) [your](https://github.com/joomla/joomla-cms/pull/2677) [projects](https://github.com/doctrine/doctrine2/pull/873) [against](https://github.com/EllisLab/CodeIgniter/pull/2766) [HHVM](https://github.com/j4mie/idiorm/pull/168), [just](https://github.com/sebastianbergmann/phpunit/pull/1072) [add](https://github.com/j4mie/paris/pull/81)


    php:
      - hhvm


to your [.travis.yml](http://about.travis-ci.org/docs/user/languages/php/) file and now every diff will ensure your project works on HHVM. If you notice any problems, please open an [HHVM issue](https://github.com/facebook/hhvm/issues) for language problems or [Travis CI issue](https://github.com/travis-ci/travis-ci/issues?labels=php&page=1&state=open) for testing problems. In the meantime, you can special case for hhvm by adding the following to your code:


    if (defined('HHVM_VERSION')) {
      // do clowny hack while your issue/pull request is being worked on
    }


And now for the 2.3 goods. It is exciting to note that this release was ~20% CPU reduction for running facebook.com compared to HHVM 2.2.0.

Here is the full changelog for your enjoyment:




  * Implement `ZipArchive`


  * `preg_replace /e` support


  * `get_mem_usage()` no longer can be negative


  * Userland file system support


  * Implement `fileinfo` extension


  * `wordwrap()` fixes


  * `PDO::sqliteCreateFunction()`


  * Implement `NumberFormatter`


  * Implement `Locale`


  * Implement `DatePeriod`


  * Many reflection fixes


  * Stub out `PharData`


  * A ton of performance fixes


  * A ton of open source framework fixes


  * FastCGI Server Support


  * Teach `implode()` about collections


  * fix ini parsing leak


  * Make array not an instanceof `Traversable`


  * Log when a nullable (e.g. `?int`) is incorrect


  * Direct invocation of callable arrays: `$f = [$cls_or_instance, 'method']; $f()`
