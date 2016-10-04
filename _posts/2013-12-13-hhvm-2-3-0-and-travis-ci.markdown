---
author: ptarjan
layout: post
title: HHVM 2.3.0 and Travis CI
category: blog
permalink: /blog/2393/hhvm-2-3-0-and-travis-ci
comments:
- id: 2213
  author: slurm
  date: '2013-12-13 15:13:12 +0000'
  date_gmt: '2013-12-13 23:13:12 +0000'
  content: Keep up the good work, curious to see how parity percentages looks for
    this version.
- id: 2219
  author: Joel Marcey
  date: '2013-12-13 16:10:27 +0000'
  date_gmt: '2013-12-14 00:10:27 +0000'
  content: The lockdown results post should be out mid-late next week. Stay tuned.
- id: 2225
  author: Matthieu
  date: '2013-12-14 02:08:36 +0000'
  date_gmt: '2013-12-14 10:08:36 +0000'
  content: 'Awesome! Though there''s still a few issues to fix on Travis side: https:&#47;&#47;github.com&#47;travis-ci&#47;travis-ci&#47;issues&#47;1749'
- id: 2231
  author: HHVM 2.3.0 支援 FastCGI&#8230; | Gea-Suan Lin&#039;s BLOG
  date: '2013-12-14 18:22:06 +0000'
  date_gmt: '2013-12-15 02:22:06 +0000'
  content: "[&#8230;] 在 HHVM 官方的 blog 上看到 2.3.0 的消息：「HHVM 2.3.0 and Travis CI」。 [&#8230;]"
- id: 2237
  author: Sandeep
  date: '2013-12-15 01:33:29 +0000'
  date_gmt: '2013-12-15 09:33:29 +0000'
  content: |-
    Thanks for the updates. Could you please provide the source packages for fedora and ubuntu. We've built one for Centos 6, but it would be more helpful if you can provide the fedora SRPM, so we can make it parity with it.
    http:&#47;&#47;yum.gleez.com&#47;6&#47;x86_64&#47;repoview&#47;hhvm.html
- id: 2243
  author: Alex
  date: '2013-12-16 03:49:16 +0000'
  date_gmt: '2013-12-16 11:49:16 +0000'
  content: |-
    Wonderful work! I'm just about to test it in our dev environment , hopefully someday we will be able to migrate to HHVM too :))

    Thanks guys!
- id: 2249
  author: Corey Ballou
  date: '2013-12-16 06:22:42 +0000'
  date_gmt: '2013-12-16 14:22:42 +0000'
  content: One thing I'd be interested in seeing with each release blog post is an
    updated framework support graph. You've clearly added a number of additions and
    fixes which would affect the overall framework unit tests.
- id: 2255
  author: Paul Tarjan
  date: '2013-12-16 14:59:42 +0000'
  date_gmt: '2013-12-16 22:59:42 +0000'
  content: Coming up this week.
- id: 2261
  author: We are the 98.5% (and the 16%) &laquo; HipHop Virtual Machine
  date: '2013-12-19 11:18:39 +0000'
  date_gmt: '2013-12-19 19:18:39 +0000'
  content: "[&#8230;] of the diffs and updates that enabled our unit test parity increase
    are part of the HHVM 2.3 package. Some key improvements that had significant impact
    on our unit test results [&#8230;]"
- id: 2267
  author: Facebook HHVM 团队封闭开发三周的成果展 | zengine
  date: '2014-01-28 18:29:51 +0000'
  date_gmt: '2014-01-29 02:29:51 +0000'
  content: "[&#8230;] 大部分文件更改已包含在HHVM 2.3版本中，以下是一些对单元测试结果有显著影响的关键改进： [&#8230;]"
- id: 2273
  author: 'HHVM: The Next Six Months &laquo; HipHop Virtual Machine'
  date: '2014-02-24 17:31:49 +0000'
  date_gmt: '2014-02-25 01:31:49 +0000'
  content: "[&#8230;] us. We&rsquo;re using&nbsp;unit test pass rates&nbsp;as a proxy
    for success measurement, but you can help by&nbsp;adding HHVM to your Travis configuration,
    and reporting bugs and issues through&nbsp;GitHub. We are resourced&nbsp;to help
    support a couple of major [&#8230;]"
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
