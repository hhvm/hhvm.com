---
author: joelm
layout: post
title: We are the 98.5% (and the 16%)
category: blog
permalink: /blog/2813/we-are-the-98-5-and-the-16
comments:
- id: 2279
  author: Yermo
  date: '2013-12-19 10:49:24 +0000'
  date_gmt: '2013-12-19 18:49:24 +0000'
  content: |-
    May I suggest, sometime during the 2014 push, putting some efforts into improving documentation? From a users&#47;developers point of view that's the largest drawback right now and I suspect is keeping quite a few people from trying the platform.  (It took me many many hours of trial and error to get the platform running my site.)

    If more accessible and organized documentation were available, it would go a very long way to getting additional sites using the platform and would draw more help into the project.

    I would suggest the same for development docs. While the code is very well organized it is largely devoid of comments and there's little in terms of overview documentation making it quite time consuming for someone to come in and contribute meaningfully to the project. It would also pay dividends by freeing the developers from having to answer so many repeat questions. :)
- id: 2285
  author: juicybacon
  date: '2013-12-19 10:55:34 +0000'
  date_gmt: '2013-12-19 18:55:34 +0000'
  content: One question. Did the tests fail because some functions are not coded&#47;broken
    or just general runtime borkyness?
- id: 2291
  author: Joel Marcey
  date: '2013-12-19 10:58:19 +0000'
  date_gmt: '2013-12-19 18:58:19 +0000'
  content: 'That is a high priority item for the HHVM team in 2014 and, actually,
    my personal #1 (or at least #1A) priority item. I will be diving neck deep into
    documentation come January.'
- id: 2297
  author: Nick
  date: '2013-12-19 11:06:53 +0000'
  date_gmt: '2013-12-19 19:06:53 +0000'
  content: Very impressed with how much effort is being put into this.  MUCH better
    than HipHop.  Keep up the good work!
- id: 2303
  author: Yermo
  date: '2013-12-19 11:10:39 +0000'
  date_gmt: '2013-12-19 19:10:39 +0000'
  content: Excellent!
- id: 2309
  author: Paul Tarjan
  date: '2013-12-19 11:11:59 +0000'
  date_gmt: '2013-12-19 19:11:59 +0000'
  content: Mostly some functions haven't been written yet, or don't behave the same
    way in corner cases.
- id: 2315
  author: asad hasan
  date: '2013-12-19 11:38:05 +0000'
  date_gmt: '2013-12-19 19:38:05 +0000'
  content: Great Job!!! keep up the good work guys.
- id: 2321
  author: Marco Pivetta
  date: '2013-12-19 12:08:18 +0000'
  date_gmt: '2013-12-19 20:08:18 +0000'
  content: "I'm starting to introduce HHVM in all my build matrixes - works awesome
    except for edge cases! \n\nKeep up with the good work!"
- id: 2327
  author: Riku
  date: '2013-12-19 13:04:45 +0000'
  date_gmt: '2013-12-19 21:04:45 +0000'
  content: Very interested in this, keep up the good work guys!
- id: 2333
  author: dandy
  date: '2013-12-19 13:10:59 +0000'
  date_gmt: '2013-12-19 21:10:59 +0000'
  content: This is good. but where is Wordpress?
- id: 2339
  author: Louis
  date: '2013-12-19 14:09:49 +0000'
  date_gmt: '2013-12-19 22:09:49 +0000'
  content: I expect WordPress already has 100% or nearly so. When the HHVM blog first
    started, they gave plenty of instructions on how to get Wordpress running on HHVM.
    In addition, they use Wordpress to power the blog and they also use HHVM for the
    site. So... Wordpress is kind of a given ;-)
- id: 2345
  author: Jeremy Wilson
  date: '2013-12-19 14:25:32 +0000'
  date_gmt: '2013-12-19 22:25:32 +0000'
  content: I'd like to see Redis and PostgreSQL support.
- id: 2351
  author: Brandon DuRette
  date: '2013-12-19 14:39:19 +0000'
  date_gmt: '2013-12-19 22:39:19 +0000'
  content: WordPress is functional on HHVM, but the test suite is not at 100%. However,
    that's only part of the story. Plugins and themes in the WordPress ecosystem also
    depend on PHP parity. The testing matrix for the entire WP ecosystem blows up
    pretty quickly.
- id: 2357
  author: Joel Marcey
  date: '2013-12-19 15:05:59 +0000'
  date_gmt: '2013-12-19 23:05:59 +0000'
  content: 'Yeah, we know Wordpress is quite important and quite popular. :) The reason
    it did not make the cut for this round was the more complicated configuration.
    The testing requires an extra config file + database setup and access. We tried
    to stick with popular frameworks that ran phpunit tests "straight out of the box"
    so to speak, with minimal configuration changes. Our test runner that we created
    and used didn''t handle that case... but we will get it there. Mediawiki initially
    had this problem, but then they showed us an --exclude-group=Database option that
    we used. Btw, I am getting the unit tests for Wordpress from here: https:&#47;&#47;github.com&#47;kurtpayne&#47;wordpress-unit-tests
    which seemed to be the best mirror I could find on Github.'
- id: 2363
  author: Paul M. Jones
  date: '2013-12-19 15:29:00 +0000'
  date_gmt: '2013-12-19 23:29:00 +0000'
  content: |-
    I'd like to get the Aura components ( https:&#47;&#47;github.com&#47;auraphp&#47; ) included in this suite. How does one do so?

    Many thanks to everyone involved here.
- id: 2369
  author: Simon
  date: '2013-12-19 17:10:37 +0000'
  date_gmt: '2013-12-20 01:10:37 +0000'
  content: Redis support is already available and there's a <a href="https:&#47;&#47;github.com&#47;pocketRent&#47;hhvm-pgsql"
    rel="nofollow">PostgreSQL<&#47;a> extension you can use.
- id: 2375
  author: Nitin
  date: '2013-12-19 19:55:39 +0000'
  date_gmt: '2013-12-20 03:55:39 +0000'
  content: You guys did a awesome Job !! I would suggest you to work on its documentation,
    This is the only thing HHVM needs. You Rock!
- id: 2381
  author: Paul Tarjan
  date: '2013-12-19 20:17:57 +0000'
  date_gmt: '2013-12-20 04:17:57 +0000'
  content: Send us a pull request for the test script we linked to.
- id: 2387
  author: Joel Marcey
  date: '2013-12-19 20:22:45 +0000'
  date_gmt: '2013-12-20 04:22:45 +0000'
  content: Documentation is high priority for the team in 2014, starting in January
    :-)
- id: 2393
  author: wwbmmm
  date: '2013-12-19 20:27:01 +0000'
  date_gmt: '2013-12-20 04:27:01 +0000'
  content: 赞！
- id: 2399
  author: Randall Helzerman
  date: '2013-12-19 21:01:45 +0000'
  date_gmt: '2013-12-20 05:01:45 +0000'
  content: "Congrats on meeting your goals!   We don't do PHP, but we do have some
    big C++ programs; are there any generic tools optimizing the cache profile of
    your executable?  \n\nHow exactly did you guys do that?   Sounds like an interesting
    story, if its not a secret of the guild."
- id: 2405
  author: Aris Setyawan
  date: '2013-12-19 21:35:47 +0000'
  date_gmt: '2013-12-20 05:35:47 +0000'
  content: |-
    Hi,

    So a PHP framework which doesn't have PHPUnit base unit-testing, can't join HHVM parity test?
- id: 2411
  author: 'Facebooks PHP-Compiler HipHop 2.3 schneller und kompatibler | Klaus Ahrens:
    News, Tipps, Tricks und Fotos'
  date: '2013-12-20 01:50:08 +0000'
  date_gmt: '2013-12-20 09:50:08 +0000'
  content: "[&#8230;] 2.3 hat HHVM jetzt in Sachen Kompatibilit&auml;t einen weiteren
    gro&szlig;en Schritt nach vorn gemacht und absolviert rund 98,58 Prozent aller
    Unit-Tests von 21 verschiedenen PHP-Projekten. Immer mehr der Open-Source-Projekte
    unterst&uuml;tzt HHVM zu 100 [&#8230;]"
- id: 2417
  author: Joeri
  date: '2013-12-20 02:43:40 +0000'
  date_gmt: '2013-12-20 10:43:40 +0000'
  content: |-
    Really nice to see hhvm improving. As someone who has been programming php professionally for almost a decade it's great to see all the refreshing new ideas going on now in the php landscape.

    Are there plans to support oci8? I'm curious to see how hhvm handles our AutoCAD to SVG conversion code, but it's tied pretty deep to our oracle DB. I would also be interested to take our whole app for a spin, but it's 500 kloc of oracle-based code so again i can't do anything useful until there is oci8 support.
- id: 2423
  author: CeBe
  date: '2013-12-20 09:10:05 +0000'
  date_gmt: '2013-12-20 17:10:05 +0000'
  content: Great news! Once travis-ci has fixed some issues with PHPUnit I am going
    to run <a href="https:&#47;&#47;github.com&#47;yiisoft&#47;yii" rel="nofollow">yii<&#47;a>
    and <a href="https:&#47;&#47;github.com&#47;yiisoft&#47;yii2" rel="nofollow">yii2<&#47;a>
    against hhvm again and will report all things that are stopping us from having
    100% test passing! :-)
- id: 2429
  author: Paul Tarjan
  date: '2013-12-20 18:14:14 +0000'
  date_gmt: '2013-12-21 02:14:14 +0000'
  content: When I cut 2.3.2 I'll include the fix for phpunit
- id: 2435
  author: Bert Maher
  date: '2013-12-20 18:24:35 +0000'
  date_gmt: '2013-12-21 02:24:35 +0000'
  content: Yes!  We actually built a pretty nice toolchain for optimizing our binary
    layout, which we will (hopefully) write up here pretty soon.  I do have some hope
    that it will apply to other big executables besides HHVM.
- id: 2441
  author: Kevin
  date: '2013-12-21 07:44:55 +0000'
  date_gmt: '2013-12-21 15:44:55 +0000'
  content: |-
    Running Drupal

    http:&#47;&#47;translate.google.com&#47;translate?sl=auto&amp;tl=en&amp;js=n&amp;prev=_t&amp;hl=en&amp;ie=UTF-8&amp;u=http%3A%2F%2Fweb-rocker.de%2F2013%2F12%2Fdrupal-7-hhvm-vs-php-55-zend-opcache
- id: 2447
  author: Darren L
  date: '2013-12-22 18:28:16 +0000'
  date_gmt: '2013-12-23 02:28:16 +0000'
  content: This seems pretty damn awesome and fun!
- id: 2453
  author: Yii-Framework unter HHVM &rsaquo; isFett.com
  date: '2013-12-27 14:02:47 +0000'
  date_gmt: '2013-12-27 22:02:47 +0000'
  content: "[&#8230;] Laut&nbsp;http:&#47;&#47;www.hhvm.com&#47;blog&#47;2813&#47;we-are-the-98-5-and-the-16
    vom 19.12.2013 werden 99,11% aller Unit-Tests mit dem Yii-Framework fehlerfrei
    abgeschlossen. Ein Grund mehr sich hier die Performance-Unterschiede anzusehen.
    Daf&uuml;r erstellen wir ein kleines Test-Projekt. [&#8230;]"
- id: 2459
  author: Magento-Neuigkeiten der Wochen 51&#47;52 2013
  date: '2013-12-28 23:13:05 +0000'
  date_gmt: '2013-12-29 07:13:05 +0000'
  content: "[&#8230;] nicht nur weiter an der Performance und Kompatibilit&auml;t
    geschraubt, es wurde auch Magento 2 in die Liste der getesteten Software aufgenommen.
    Au&szlig;erdem kann HHVM nun auch als FastCGI-Modul hinter einem herk&ouml;mmlichen
    Webserver [&#8230;]"
- id: 2465
  author: Grim
  date: '2013-12-30 03:20:34 +0000'
  date_gmt: '2013-12-30 11:20:34 +0000'
  content: How about symfony2? I try use hhvm fastcgi mode ,but it's not ok. How use
    symfony2 on hhvm?
- id: 2471
  author: Sascha
  date: '2014-01-01 03:35:43 +0000'
  date_gmt: '2014-01-01 11:35:43 +0000'
  content: |-
    Can you clarify what tests you were running with Drupal and which version?

    I currently have two failing PHPUnit tests, created an issue on our side to improve&#47;track HHVM compatibility: https:&#47;&#47;drupal.org&#47;node&#47;2165377
- id: 2477
  author: HHVM HipHop Virtual Machine vs Apache2 |
  date: '2014-01-02 14:24:49 +0000'
  date_gmt: '2014-01-02 22:24:49 +0000'
  content: "[&#8230;] Warum also nicht sofort komplett auf HHVM umstellen? Die Frage
    ist leicht beantwortet, da unter HHVM noch nicht alle Module und Plattformen kompatibel
    sind. Eine aktuelle &Uuml;bersicht findet ihr hier. [&#8230;]"
- id: 2483
  author: Ajinkya
  date: '2014-01-09 22:29:56 +0000'
  date_gmt: '2014-01-10 06:29:56 +0000'
  content: PHP is quite underrated, mostly from Java guys, but look at numbers, its
    the king.
- id: 2489
  author: qianzhihe
  date: '2014-01-11 01:12:11 +0000'
  date_gmt: '2014-01-11 09:12:11 +0000'
  content: Great news!  thank you
- id: 2495
  author: How will HHVM influence PHP? &laquo; {5} Setfive &#8211; Talking to the
    World
  date: '2014-01-14 10:27:54 +0000'
  date_gmt: '2014-01-14 18:27:54 +0000'
  content: "[&#8230;] the last few weeks, there&#8217;s been a slew of HHVM related
    news from the &#8220;We are the 98.5%&#8221; post from the HHVM team to the Our
    HHVM Roadmap from the Doctrine team. With the increasing [&#8230;]"
- id: 2501
  author: Christopher Svanefalk
  date: '2014-01-15 23:02:33 +0000'
  date_gmt: '2014-01-16 07:02:33 +0000'
  content: "Fantastic work guys! \n\nMy company is already optimising our PHP codebase
    for full HHVM compatibility, and we plan to deploy it on our production servers
    before summer 2014.\n\nYou are doing great things for PHP and the community, and
    I very much look forward to see how HHVM will progress during the year :)"
- id: 2507
  author: ming
  date: '2014-01-22 12:56:30 +0000'
  date_gmt: '2014-01-22 20:56:30 +0000'
  content: |-
    Great stuffs.

    BTW, your tests include phpmyadmin, but, I get only blank screen using the latest build running as fastcgi daemon?  Is there special configuration?
- id: 2513
  author: Paul Tarjan
  date: '2014-01-22 21:49:30 +0000'
  date_gmt: '2014-01-23 05:49:30 +0000'
  content: There are fixed in trunk and not in the release that should make it work.
    Can you try the `hhvm-nightly` package and see if that works for you?
- id: 2519
  author: Ming
  date: '2014-01-23 09:10:28 +0000'
  date_gmt: '2014-01-23 17:10:28 +0000'
  content: "Thanks Paul. \n\nThe nightly build works and seems mostly functional.
    \ There is a segmentation fault and I will file that to the bugs forum.\n\nAnother
    question.  I understand that HHVM does not implement every modules and&#47;or
    drivers that PHP offers, how do I know what is &#47; is not included, and, is
    there any tools to check against the webapp codes?"
- id: 2525
  author: Paul Tarjan
  date: '2014-01-23 14:17:08 +0000'
  date_gmt: '2014-01-23 22:17:08 +0000'
  content: function_exists() is a nice to know, and if you like to trust docs you
    can try https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;wiki&#47;Extensions
- id: 2531
  author: Facebook HHVM 团队封闭开发三周的成果展 &#124; 我爱互联网
  date: '2014-01-29 01:13:24 +0000'
  date_gmt: '2014-01-29 09:13:24 +0000'
  content: "[&#8230;] 　　英文原文：we-are-the-98-5-and-the-16 [&#8230;]"
- id: 2537
  author: 'HHVM: The Next Six Months &laquo; HipHop Virtual Machine'
  date: '2014-02-24 17:27:56 +0000'
  date_gmt: '2014-02-25 01:27:56 +0000'
  content: "[&#8230;] We&rsquo;ve been making steady progress on HHVM&rsquo;s compatibility&nbsp;with&nbsp;PHP&nbsp;in
    the wild, but we still have a lot of work ahead of us. We&rsquo;re using&nbsp;unit
    test pass rates&nbsp;as a proxy for success measurement, but you can help by&nbsp;adding
    HHVM to your Travis configuration, and reporting bugs and issues through&nbsp;GitHub.
    We are resourced&nbsp;to help support a couple of major HHVM deployments, which
    we hope has the side effect of exposing us to &#8220;non-Facebook&#8221; deployment
    and maintenance challenges. [&#8230;]"
- id: 2543
  author: Implementing MySQLi &laquo; HipHop Virtual Machine
  date: '2014-02-26 12:12:21 +0000'
  date_gmt: '2014-02-26 20:12:21 +0000'
  content: "[&#8230;] After warming up with the parser, I was ready to start my big
    project: implement MySQLi. This has been a long requested feature for HHVM. And,
    this extension is required to help meet our compatibility goals. [&#8230;]"
- id: 2549
  author: Tracking Parity &laquo; HipHop Virtual Machine
  date: '2014-03-03 14:53:07 +0000'
  date_gmt: '2014-03-03 22:53:07 +0000'
  content: "[&#8230;] runner are a nice representative sample of real world PHP (and
    we are adding more). We showed a static snapshot of our test parity to these frameworks
    late last year. As HHVM is continually developed, it is [&#8230;]"
- id: 3491
  author: 赵伊凡&#8217;s blog：Facebook推出编程语言&mdash;&mdash;Hack | 赵伊凡&#039;s Blog
  date: '2014-03-21 07:40:54 +0000'
  date_gmt: '2014-03-21 14:40:54 +0000'
  content: "[&#8230;] HHVM仍然是一个PHP运行平台，我们打算继续保持这种方式。事实上，我们正努力达到PHP-5的标准。其中HHVM的首要任务是能够运行未经修改的PHP
    5的源代码，不仅是为了社区，也因为我们依赖许多第三方PHP底层库。 HHVM现在是一个能同时运行PHP和Hack的平台，所以你可以逐渐体验Hack所带来的新特性。
    [&#8230;]"
- id: 404339
  author: Adeel Ahmad
  date: '2015-03-07 09:22:12 +0000'
  date_gmt: '2015-03-07 17:22:12 +0000'
  content: Although you have made progress with PHP compatibility, its a hard hitting
    fact that still you have to go a long way.  I am using HHVM and still it requires
    much to be done.
- id: 480701
  author: 'PHP 6: Zend Engine oder HHVM? - entwickler.de'
  date: '2015-05-08 02:19:58 +0000'
  date_gmt: '2015-05-08 09:19:58 +0000'
  content: "[&#8230;] ohne Unterlass daran, die Abdeckung der wichtigsten Frameworks
    und Tools weiter zu steigern &ndash; zahlreiche Projekte sind bereits zu 100 Prozent
    mit der HHVM kompatibel. Doch auch die Projekte selbst unternehmen gro&szlig;e
    Anstrengungen, ihre Codebasis f&uuml;r HipHop zu [&#8230;]"
- id: 480737
  author: HHVM in der echten PHP-Welt - entwickler.de
  date: '2015-05-08 02:27:24 +0000'
  date_gmt: '2015-05-08 09:27:24 +0000'
  content: "[&#8230;] runner are a nice representative sample of real world PHP (and
    we are adding more). We showed a static snapshot of our test parity to these frameworks
    late last year. As HHVM is continually developed, it is [&#8230;]"
- id: 806135
  author: Si desarrollas en PHP y tienes un rato, prueba HHVMSopa de bits
  date: '2016-02-23 03:24:50 +0000'
  date_gmt: '2016-02-23 11:24:50 +0000'
  content: "[&#8230;] el pasado 19 de Diciembre se publicaba en el blog de HHVM un
    art&iacute;culo sobre la ejecuci&oacute;n de pruebas unitarias de diversos frameworks
    en HHVM. Desde el inicio de esas pruebas hasta el resultado final, la mejora ha
    sido notable en algunos [&#8230;]"
- id: 806141
  author: HHVM en Magento y SymfonySopa de bits
  date: '2016-02-23 03:25:07 +0000'
  date_gmt: '2016-02-23 11:25:07 +0000'
  content: "[&#8230;] m&aacute;s estrellas en GitHub, es otro de los agraciados&nbsp;con
    la mejora de rendimiento. Adem&aacute;s de las mejoras publicadas en los tests
    del blog de HHVM, hay otras pruebas m&aacute;s b&aacute;sicas realizadas con ApacheBench.
    Digna de menci&oacute;n es esta [&#8230;]"
---

On November 4th, the HHVM team went on a [3-week performance and parity lockdown](http://www.hhvm.com/blog/1499/locking-down-for-performance-and-parity). The lockdown officially ended on November 22nd. Overall, this lockdown was a qualified success. Success was measured on 3 vectors:


<!--truncate-->

  1. Did we meet our 99% average unit test pass percentage goal for the 21 open-source frameworks we tested against?


  2. Did we meet the 15% across the board performance improvement gains?


  3. Were the razors put away for the entirety of the three weeks?


![The HHVM Team at the post-lockdown party](/static/images/posts/postlockdown21.png)
<center><i>The HHVM Team at the post-lockdown party</i></center>

## Parity


Going into lockdown, the team knew that awesome performance alone would not suffice in making HHVM a viable PHP runtime to be used out in the wild. It actually had to run real, existing PHP code reliably. So we made that a first class work item (as it will continue to be into 2014). Our first step into improving PHP parity was to look at [Github](https://github.com/), see which [PHP projects were being used by many people](https://github.com/search?l=php&q=stars%3A%3E1&s=stars&type=Repositories) (via their "star" rating) and make sure their unit tests would run successfully on HHVM.


### Parity Results

Let's just get to the numbers. After over **125 diffs**, here are the results of the parity portion of our 3-week lockdown.

[Recall the table of parity](/blog/2013/09/12/wow-hhvm-is-fast-too-bad-it-doesnt-run-my-code.html) before the lockdown. Now, here is our graph of improvement after the lockdown:

![The updated unit test parity results after our 3-week lockdown](/static/images/posts/Screenshot-2013-12-17-12.35.361.png)
<center><i>The updated unit test parity results after our 3-week lockdown</i></center>

As you probably can see by the graph, we were successful in our efforts to improve unit test parity nearly across the board:

  1. The team **doubled** the number of open source projects with unit tests that pass at 100% on HHVM (from 4 to 8). And we have 4 more that are very close in the 99%+ range.


  2. We had > 10% gains in Assetic, Symfony, Yii and CodeIngiter (I am not counting the Pear gain here since we did not have a nice baseline number to begin with).


  3. And all 21 frameworks are above 90% in overall unit test pass percentage.


Many of the diffs and updates that enabled our unit test parity increase are part of the [HHVM 2.3 package](http://www.hhvm.com/blog/2393/hhvm-2-3-0-and-travis-ci). Some key improvements that had significant impact on our unit test results were:

  1. Make array not an instanceof `Traversable`


  2. `Internationalization` support


  3. `PDO::sqliteCreateFunction()` implementation


  4. The beginning of real `php.ini` support


However, there are a few curiosities...


  1. **Why did PhpMyAdmin regress?** We are not convinced this is a regression in the "we are failing more tests than before because of some code we broke" sense. This actually may have to do with our testing framework script not actually loading all of the tests properly initially. We fixed this mid-stream. That said, we are looking into the root cause of this regression, just in case we broke something.


  2. **Why the 90 degree cliff drop-off around November 24th?** We submitted a diff that we thought was going to push a framework to 100%, but instead [segfaulted the runtime](https://github.com/facebook/hhvm/commit/c6d99f1e8eb869a2c16449d057af66eca266fc7b). It was [fixed soon thereafter](https://github.com/facebook/hhvm/commit/2d4f9ee46bfc20b34e77ccd93816c2d6cfd8a26c).


### Testing Framework


The 21 open source projects that were used as our initial baseline to increase our unit test parity were, as stated above, chosen on popularity. However, they were also chosen based on their use of PHPUnit and on how well they would work with our testing framework. Given the sheer number of unit tests that come with some of these projects (e.g., Symfony and ZF2 each have over 10K tests), we needed to come up with a testing framework that would allow us to run the tests for all of the projects in a speedy manner. So the team developed a script that would download, install and run the unit tests for all of the 21 open source projects in parallel. The script is still a work in progress, but it allowed us to run all 50K+ unit tests in 30 minutes to 1 hour (depending if the JIT is on) vs the many hours it would take to the unit tests serially. That script is located in the [HHVM Github repository](https://github.com/facebook/hhvm/blob/master/hphp/test/frameworks/run.php).

You may also notice that ***your*** favorite open source project is not currently in the list above. There are a couple of reasons for that. First, we couldn't cover all open source projects in a 3-week span. Secondly, while open source projects like CakePHP are very important, and we will add them to our testing framework, there were some setup and configuration problems (e.g., requiring of a database) that wouldn't allow us to add them in a short manner.

Finally, as discussed in our pre-lockdown blog post, the HHVM team created a bunch of "[stickies](http://hhvm.com/wp-content/uploads/2013/11/2013-10-31-17.33.041.jpg)" to help guide our work. The stickies were placed on a "number of failing tests associated with this sticky task" vs. "number of days to implement". So, we generally worked from top left to bottom right to get the most bang for our buck.


### Assumptions and Caveats


It is worth pointing out some of the assumptions and caveats that went into to coming up with the statistics above.




  - The final, overall unit test pass percentage (98.5%) is a straight, unweighted average of the individual open source project unit test pass percentages (i.e., add all of the percentages and divide by 21). So, a project like Paris which has 50 unit tests carries the same percentage weight as Symfony which has 10K unit tests. If we weighted these percentages (where Symfony and Zf2 carried more weight than Paris and Idiorm), the overall pass percentage would see a minimal drop (minimal because of the small variance in pass percentages for all of the open source projects).


  - There are some unit tests that fail in HHVM, but also fail with PHP 5.5.x. We called these tests "clowny" and disregarded them in our testing framework.

![Sometimes there is clowniness when it comes to PHP](/static/images/posts/2013-11-21-12.17.301.jpg)
<center><i>Sometimes there is clowniness when it comes to PHP</i></center>


  - There are some unit tests that actually caused problems with our testing framework script (deadlocks, etc.). We "blacklisted" these tests and counted them as failures in terms of our pass percentage.


### Submitted Project Pull Requests


There were times when code changes were necessary to the actual open source project in order to successfully run all of its unit tests. For example, a change may have been necessary in order to support our parallel testing framework. In other cases, there were actual bugs in the unit tests. A real pleasant surprise during our lockdown was how awesome the project owners/maintainers were in reviewing and, in most cases, accepting our pull requests.


### Travis Integration


The [announcement of HHVM 2.3](http://www.hhvm.com/blog/2393/hhvm-2-3-0-and-travis-ci) talked a bit about Travis CI Integration. Now that we are starting to consistently pass unit tests for open source projects, some have added HHVM to their Travis CI build (awesome!). Here are some open source frameworks that have added us to their CI build:




  * [PHPUnit](https://github.com/sebastianbergmann/phpunit/pull/1072)


  * [Yii](https://github.com/yiisoft/yii/pull/3109)


  * [Doctrine 2](https://github.com/doctrine/doctrine2/pull/873)


  * [Laravel](https://github.com/laravel/framework/pull/2973)


Thanks to the above for adding us so quickly. And we have [many pull requests outstanding](https://github.com/search?q=Try+running+unit+tests+on+HHVM+&ref=cmdform&type=Issues) for other open source frameworks to do the same.


## Performance


The performance team blew through their lockdown performance goal of 15% and ended up at 16% for running facebook.com.

![The updated performance results after our 3-week lockdown](http://hhvm.com/wp-content/uploads/2013/12/Screenshot-2013-12-18-09.54.181.png)
<center><i>The updated performance results after our 3-week lockdown</i></center>

This can only mean good things for other PHP code out in the wild. The performance gains came from lots of small improvements, and a few big ones. Some of the biggest wins were:




  1. Generating code for unusual function call patterns. HHVM already generates good code for ordinary function and method calls, so some less-common patterns had started to show up in our performance profile data. The two biggest ones were [`call_user_func()`](http://php.net/manual/en/function.call-user-func.php) and `static::` method calls, which were both handled by the interpreter. Now we generate optimized machine code for each of those call types.


  2. Optimizing the layout of the HHVM binary. HHVM is a big program: the compiled C++ code of HHVM clocks in at just under 100 MB. The CPU's caches work better when the hot code footprint is small, instead of spread out across the address space, so we put the hottest functions together in one part of the binary. For an extra boost to [I-TLB](http://en.wikipedia.org/wiki/Translation_lookaside_buffer) performance, we then mapped that part using [huge pages](http://en.wikipedia.org/wiki/Page_%28computer_memory%29#Huge_pages).


  3. Using the interpreter to detect hot functions. HHVM interprets the first several requests to avoid wasting time and space compiling startup code. We added logic to the interpreter to find the hottest functions and compile them to a special part of the translation cache. Like the last optimization, this one improves code locality, this time for the dynamically generated code.


  4. Upgrading our regular expression library. Newer versions of [PCRE](http://www.pcre.org/) include a JIT compiler for regular expressions, which gives HHVM a nice performance boost.




## Hygiene


I am sure you are thinking to yourself, "all these gains and statistics are nice and everything, but what about the beards?!?" Right, you then remember that in our [beginning the lockdown](http://www.hhvm.com/blog/1499/locking-down-for-performance-and-parity) post that "shaving was discouraged". I am happy to report that we also succeeded in maintaining a state of minimal facial hygiene throughout the lockdown. And here are the pictures to prove it.

![SaraG had a beard in spirit](/static/images/posts/2013-11-22-16.11.241.jpg)
<center><i>SaraG had a beard in spirit</i></center>

![The HHVM team has their razors in hand ready to clean up](/static/images/posts/2013-11-22-16.15.431.jpg)
<center><i>The HHVM team has their razors in hand ready to clean up</i></center>


## Did we meet our goals?


Remember the three success vectors that were posed at the beginning of this blog post?




  1. Did we meet our parity improvement goals for the 21 open-source frameworks we tested against => 99% average unit test parity?


  2. Did we meet performance improvement goals => 15% across the board performance gain?


  3. Were the razors put away for the entirety of the three weeks?


Here are your answers:


  1. **Close YES!** (using rounding to our advantage)


  2. **Resounding YES!** (no rounding needed)


  3. **YES!** Some of us are grayer than others.


## The Future (2014)


Performance improvements will always be a core mantra for the HHVM team. That said, parity will be 1A on the priority scale for the team. We really do care about open source and the PHP community. 2014 will be a year where we go to great lengths to make HHVM first-class when it comes to **both** performance and parity. More unit tests passing for more open source projects and frameworks. Real world testing for PHP code out in the wild. Stay tuned for further updates on our progress and plans. Until then, Happy Holidays and Happy New Year!
