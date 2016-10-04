---
author: joelm
layout: post
title: Wow HHVM is fast...too bad it doesn’t run my code
category: blog
permalink: /blog/875/wow-hhvm-is-fast-too-bad-it-doesnt-run-my-code
comments:
- id: 515
  author: Pasquale Vazzana
  author_email: pvazzana@medialeader.it
  author_url: ''
  date: '2013-09-12 18:48:58 +0000'
  date_gmt: '2013-09-13 01:48:58 +0000'
  content: Keep up the good work!
- id: 521
  author: Yermo
  author_email: yml@yml.com
  author_url: http://miles-by-motorcycle.com
  date: '2013-09-12 21:53:09 +0000'
  date_gmt: '2013-09-13 04:53:09 +0000'
  content: "I've found the members of your team in IRC extremely helpful and open
    to bug reports and questions. I confess I was surprised.  \n\nI was convinced
    there was no way hhvm could run my codebase, a framework&#47;platform not that
    unlike Drupal,  because of how large, involved and most depressingly old it is.
    To my shock and amazement it runs almost 100%, and I'm confident with a little
    more effort it will be 100%. And it's <b>FAST</b>.\n\nWhat's simply nuts is
    the assertion that in some cases the JIT compiler does a better job (i.e. is faster)
    than a static C++ compiler can, something that I still have a hard time wrapping
    my brain around."
- id: 527
  author: Bnaya
  author_email: me@bnaya.net
  author_url: ''
  date: '2013-09-13 03:42:04 +0000'
  date_gmt: '2013-09-13 10:42:04 +0000'
  content: I hope namespaces is also on the loop. Thank you for that great project!!
- id: 533
  author: aleksandar
  author_email: office@ajankovic.com
  author_url: http://ajankovic.com
  date: '2013-09-13 03:50:19 +0000'
  date_gmt: '2013-09-13 10:50:19 +0000'
  content: |-
    I am sure that including Magento in the "top frameworks" list will be appriciated by it's large community.

    In case u need help with unit tests let us know :-)
- id: 539
  author: Lelala
  author_email: lelala@gmx.net
  author_url: http://www.lelala.ch
  date: '2013-09-13 04:24:02 +0000'
  date_gmt: '2013-09-13 11:24:02 +0000'
  content: |-
    The performance issue isn't quite that important, usually can throw more (cheap today)hardware at the problem.
    Sure, in a datacenter there may be an issue, but in real world, there is not...
- id: 545
  author: Joseph Redfern
  author_email: joseph@redfern.me
  author_url: http://blog.redfern.me/
  date: '2013-09-13 04:36:31 +0000'
  date_gmt: '2013-09-13 11:36:31 +0000'
  content: Awesome stuff. FYI, the sorting on the table doesn't work - seems to be
    treating the numbers as strings.
- id: 551
  author: Ilmari Oranen
  author_email: ilmari.oranen@gmail.com
  author_url: ''
  date: '2013-09-13 05:40:02 +0000'
  date_gmt: '2013-09-13 12:40:02 +0000'
  content: "I'm very excited to see when Drupal unit test pass reaches 100%. \n\nSupporting
    the gazillion modules is a different thing, but could be possible with the support
    of the Drupal community  :-)"
- id: 557
  author: yosef
  author_email: yosef_cool_ha@hotmail.com
  author_url: http://duckgamer.com
  date: '2013-09-13 06:26:11 +0000'
  date_gmt: '2013-09-13 13:26:11 +0000'
  content: "What would be very neat of you to add is to make it similar to php5-fpm
    as possible(allowing us to just as easily add hhvm to replace the php5-fpm) or
    to simpley run as a seperate server from php5-fpm and await requests of our NGINX.
    \nso far HHVM configuration has been more confusing than that of PHP5-FPM and
    I fail to configure it on my own.\nmy setup is simple, if the file extension is
    php then just send it to a unix  socket of php5-fpm.sock, the php5-fpm doesn't
    care from what folder it is sent to, however hhvm seems like it cares of the paths
    and folders which makes it quite difficult to figure out how to configure, good
    work tho and hope you get it beyond your expectations."
- id: 563
  author: Lukas
  author_email: smith@pooteeweet.org
  author_url: http://pooteeweet.org
  date: '2013-09-13 06:59:46 +0000'
  date_gmt: '2013-09-13 13:59:46 +0000'
  content: |-
    "Doctrine2 has certain classes that implement interfaces, but these classes do not implement these interfaces fully. HHVM requires classes that implement interfaces to be compatible with the interfaces they implement."

    could you explain a bit more what you mean by that? see also https:&#47;&#47;twitter.com&#47;jmikola&#47;status&#47;378374068648419328
- id: 569
  author: Jose Diaz-Gonzalez
  author_email: hhvm@josediazgonzalez.com
  author_url: http://josediazgonzalez.com
  date: '2013-09-13 07:49:28 +0000'
  date_gmt: '2013-09-13 14:49:28 +0000'
  content: |-
    It would be nice if you included the methodology for running tests here. I am part of the CakePHP core team, and we'd love to have full compatibility with HipHop, though we can't do that without knowing how you did setup&#47;ran test :)

    Feel free to ping me if you have any questions.
- id: 575
  author: Ahemd Enan
  author_email: enandev@gmail.com
  author_url: ''
  date: '2013-09-13 09:08:02 +0000'
  date_gmt: '2013-09-13 16:08:02 +0000'
  content: Great Stuff  !,  i think wordpress is the most important cms&#47;framework
    for php  and it's have very large community from different language , please  lets
    us know more about unit tests  even we can make especial one for hhvm
- id: 581
  author: Joel Marcey
  author_email: joelm@fb.com
  author_url: https://www.facebook.com/JoelMarcey
  date: '2013-09-13 11:37:18 +0000'
  date_gmt: '2013-09-13 18:37:18 +0000'
  content: aleksandar, thanks for your comment. I have added Magento to the table
    with a footnote as to why the unit tests won't run. We are pretty sure it is a
    bug on our end. Once that is fixed, we will see what other failures we may have
    :)
- id: 587
  author: Joel Marcey
  author_email: joelm@fb.com
  author_url: https://www.facebook.com/JoelMarcey
  date: '2013-09-13 11:38:56 +0000'
  date_gmt: '2013-09-13 18:38:56 +0000'
  content: Jose Diaz-Gonzalez, I am planning to update our GitHub wiki with information
    on the setup and processes we used to run these tests. I hope to get that documented
    very soon.
- id: 593
  author: Sam
  author_email: sam.artioli@disney.com
  author_url: ''
  date: '2013-09-13 12:25:08 +0000'
  date_gmt: '2013-09-13 19:25:08 +0000'
  content: |-
    How about Guzzle?

    http:&#47;&#47;guzzlephp.org&#47;
- id: 599
  author: Slavin
  author_email: slytael@gmail.com
  author_url: http://www.geckod.com
  date: '2013-09-13 14:12:55 +0000'
  date_gmt: '2013-09-13 21:12:55 +0000'
  content: I honestly fail to see the whole idea of keep trying to make PHP fast.
    It's not used in enterprise projects, nor was it intended to be. I have nothing
    but respect for building (or almost) a blazing fast VM. PHP got so popular because
    of it's ease of installation. Take that away and there's nothing left. Having
    said that, I do hope that this project actually goes somewhere.
- id: 605
  author: ENTERPRISE OR GTFO
  author_email: admin@localhost.dev.com
  author_url: ''
  date: '2013-09-13 16:11:40 +0000'
  date_gmt: '2013-09-13 23:11:40 +0000'
  content: |-
    Enterprise projects? You sound like Ballmer.

    You can remove these:
    - Wordpress
    - Joomla
    - PHPBB
    - Drupal (< 8)
    - Magento

    Nobody that would care about scaling an application would use such bloated, insecure and poorly architected applications.
- id: 611
  author: Jeff
  author_email: krypto.jeff@gmail.com
  author_url: ''
  date: '2013-09-13 23:03:17 +0000'
  date_gmt: '2013-09-14 06:03:17 +0000'
  content: Looking forward to Magento support!
- id: 617
  author: Alex
  author_email: alex@nodex.co.uk
  author_url: http://www.nodex.co.uk
  date: '2013-09-14 02:30:27 +0000'
  date_gmt: '2013-09-14 09:30:27 +0000'
  content: |-
    +1 To Enterprise or GTFO.

    And forget supporting frameworks - what about MongoDB, Postgres support ?
- id: 623
  author: Daniel Lowrey
  author_email: rdlowrey@gmail.com
  author_url: ''
  date: '2013-09-14 08:29:30 +0000'
  date_gmt: '2013-09-14 15:29:30 +0000'
  content: |-
    <blockquote>Unimplemented functions such as str_getcsv, stream_context_options<&#47;blockquote>

    Uh, there's no such thing as a <code>stream_context_options<&#47;code> function. I assume this refers to an inability to use <i>any<&#47;i> stream context functionality? If so, this is a major shortcoming for support in my own work.

    <b>Can you please clarify this point?</b>
- id: 629
  author: Joel Marcey
  author_email: joelm@fb.com
  author_url: https://www.facebook.com/JoelMarcey
  date: '2013-09-14 08:57:21 +0000'
  date_gmt: '2013-09-14 15:57:21 +0000'
  content: Good catch, thanks. It should have been <code>stream_context_get_options<&#47;code>.
    I fixed it.
- id: 635
  author: Noticias 14-10-2013 - La Web de Programaci&oacute;n
  author_email: ''
  author_url: http://kartones.net/blogs/lawebdeprogramacion/archive/2013/09/14/noticias-14-10-2013.aspx
  date: '2013-09-14 12:56:29 +0000'
  date_gmt: '2013-09-14 19:56:29 +0000'
  content: "[&#8230;] La m&aacute;quina virtual de Facebook para PHP va aumentando
    su rendimiento a muy buen ritmo, aunque todav&iacute;a no tenga soporte total
    del lenguaje. [&#8230;]"
- id: 641
  author: Yonni
  author_email: yonmanm@gmail.com
  author_url: ''
  date: '2013-09-14 23:02:12 +0000'
  date_gmt: '2013-09-15 06:02:12 +0000'
  content: What about Zend Framework 1 &amp; Zend Framework 2? Any relevant test runs
    with those?
- id: 647
  author: Marco Pivetta
  author_email: ocramius@gmail.com
  author_url: http://ocramius.github.io/
  date: '2013-09-15 16:48:05 +0000'
  date_gmt: '2013-09-15 23:48:05 +0000'
  content: |-
    I've been playing around with HHVM today and it really looks promising!

    The only "hard stop" I had so far is PHPUnit containing un-recognized syntax such as:

    <code>HipHop Fatal error: syntax error, unexpected '(', expecting T_LNUMBER or ';' in &#47;vagrant&#47;ProxyManager&#47;vendor&#47;phpunit&#47;phpunit&#47;PHPUnit&#47;Util&#47;XML.php on line 825<&#47;code>

    Had other problems such as the constant <code>PHP_VERSION_ID<&#47;code> not being undefined, or missing classes such as <code>RecursiveArrayIterator<&#47;code> or missing implementations for the reflection API (mainly seems to crash when you extend internal classes).

    That's unfortunate, but I can see HipHop VM is now really something easy to install and to use! That surely helps in getting the community to report issues!

    As for the installers: please start signing your .deb packages :-)
- id: 653
  author: Lucas Costa
  author_email: lucas@ezlike.com.be
  author_url: ''
  date: '2013-09-15 19:15:20 +0000'
  date_gmt: '2013-09-16 02:15:20 +0000'
  content: Thanks! Hope to see you guys around here often!
- id: 659
  author: Joel Marcey
  author_email: joelm@fb.com
  author_url: https://www.facebook.com/JoelMarcey
  date: '2013-09-16 08:17:07 +0000'
  date_gmt: '2013-09-16 15:17:07 +0000'
  content: We have zf2 in the table. It won't run because of the lack of internationalization
    support by HHVM. However, we are working on that aspect and working with people
    who may modify the test suite to help us exit more gracefully than a fatal with
    the lack of that extension.
- id: 665
  author: raciloni
  author_email: raciloni@gmail.com
  author_url: ''
  date: '2013-09-16 16:47:34 +0000'
  date_gmt: '2013-09-16 23:47:34 +0000'
  content: Can you add <a href="http:&#47;&#47;fatfreeframework.com&#47;home" rel="nofollow">Fat-Free
    framework<&#47;a> to your table, It's a realy promising micro-framework, and I'd
    like to see it supported by HHVM.
- id: 671
  author: RouteXL
  author_email: info@routexl.com
  author_url: http://www.routexl.com/
  date: '2013-09-17 13:43:04 +0000'
  date_gmt: '2013-09-17 20:43:04 +0000'
  content: I can't get my Slim project to run on HHVM. Were there any specific configurations
    made for this framework, or was it ran plain vanilla? I guess there are some rewriterules
    required to redirect custom endpoints...
- id: 677
  author: John
  author_email: rrrrr@gmail.com
  author_url: ''
  date: '2013-09-18 04:56:24 +0000'
  date_gmt: '2013-09-18 11:56:24 +0000'
  content: I agree with Alex. The only reason I can't use HHVM is because it lacks
    MongoDB support. There was a promise from Sarah (a year ago or so) that you guys
    will try to make php extensions easily compilable to HHVM, but still, nothing
    happened.
- id: 683
  author: Brian Cavanagh
  author_email: brian@designedtoscale.com
  author_url: http://designedtoscale.com
  date: '2013-09-18 18:39:55 +0000'
  date_gmt: '2013-09-19 01:39:55 +0000'
  content: If you could only get New Relic Integrated into this I would start transitioning
    clients tomorrow!  I would be scared to lose all the diagnostic information that
    NR provides my Enterprise Clients
- id: 689
  author: Rod
  author_email: rsala004@gmail.com
  author_url: ''
  date: '2013-09-21 13:53:01 +0000'
  date_gmt: '2013-09-21 20:53:01 +0000'
  content: Why throw money at a problem instead of using this if you can, for free?
    I at least hope it's your own money and not someone else's.
- id: 695
  author: Дайджест интересных новостей и материалов из мира PHP за последние две недели
    (8&mdash;22 сентября 2013) | Juds
  author_email: ''
  author_url: http://www.juds.com.ua/php-digest21/
  date: '2013-09-23 00:54:27 +0000'
  date_gmt: '2013-09-23 07:54:27 +0000'
  content: "[&#8230;] HHVM быстр&hellip; жаль мой код не запускается&nbsp;&mdash;
    Не смотря на заманчивую производительность, HHVM поддерживает далеко не все возможности
    PHP. В посте приведена таблица со списком фреймворков и информацией об их работоспособности
    в HHVM на основе данных о выполнимости юнит-тестов. Приоритетная цель для команды
    HHVM &mdash; обеспечить 100% работу этих фреймворков на HHVM. Помощь контрибьюторов&nbsp;приветствуется.
    [&#8230;]"
- id: 701
  author: 'PHP: Installing HipHop PHP on Ubuntu &laquo; {5} Setfive &#8211; Talking
    to the World'
  author_email: ''
  author_url: http://shout.setfive.com/2013/09/23/php-installing-hiphop-php-on-ubuntu/
  date: '2013-09-23 07:37:35 +0000'
  date_gmt: '2013-09-23 14:37:35 +0000'
  content: "[&#8230;] couple of weeks ago, a blog post came across &#47;r&#47;php
    titled Wow HHVM is fast&hellip;too bad it doesn&rsquo;t run my code. The post
    is pretty interesting, it takes a look at what the test pass % is for a variety
    of PHP [&#8230;]"
- id: 707
  author: ivan panfilov
  author_email: vault58@hotmail.com
  author_url: ''
  date: '2013-09-23 07:52:18 +0000'
  date_gmt: '2013-09-23 14:52:18 +0000'
  content: "I love this project. But really don't waste time for frameworks and other
    bullshit stuff. Coz 100% this is not help for improviing performace. Support only
    standart PHP for people who really needed in perfomance and who writing application
    \nwithaout 100 tons of boilerplate crap."
- id: 713
  author: RouteXL
  author_email: info@routexl.com
  author_url: http://www.routexl.com/
  date: '2013-09-25 05:04:52 +0000'
  date_gmt: '2013-09-25 12:04:52 +0000'
  content: |-
    Referring to my previous question regarding the Slim framework, I got it to work using this config:

    <code>
    Server {
      SourceRoot = &#47;var&#47;www
      DefaultDocument = index.php
    }

    VirtualHost {
      www {
        Pattern = .*
        ServerVariables {
            PHP_SELF = &#47;index.php
            SCRIPT_NAME = &#47;index.php
        }
        RewriteRules {
          index {
            pattern = ^(.*)$
            to = index.php&#47;$1
            qsa = true
          }
        }
      }
    }
    <&#47;code>
- id: 719
  author: Jakub
  author_email: Bukaj.kelo@gmail.com
  author_url: ''
  date: '2013-09-25 23:55:30 +0000'
  date_gmt: '2013-09-26 06:55:30 +0000'
  content: "I would love to see passing tests for media wiki. \n\nThanks for a great
    project."
- id: 725
  author: Benchmarking HipHopVM against PHP 5.3 on Ubuntu 12.04 | LeaseWeb Labs
  author_email: ''
  author_url: http://www.leaseweblabs.com/2013/09/benchmarking-hiphopvm-php-5-3-ubuntu-12-04/
  date: '2013-09-26 00:35:11 +0000'
  date_gmt: '2013-09-26 07:35:11 +0000'
  content: "[&#8230;] The differences were smaller and less consistent than I expected.
    Also I was disappointed that HipHopVM did not run my code. [&#8230;]"
- id: 731
  author: Fabien
  author_email: fabien@symfony.com
  author_url: http://twig.sensiolabs.org/
  date: '2013-09-28 04:35:21 +0000'
  date_gmt: '2013-09-28 11:35:21 +0000'
  content: Just for your information, I've just finished making Twig compatible with
    HHVM; at least, all tests pass now.
- id: 737
  author: Ryan Kopf
  author_email: ryan@ryankopf.com
  author_url: http://ryankopf.com
  date: '2013-10-01 21:59:05 +0000'
  date_gmt: '2013-10-02 04:59:05 +0000'
  content: SilverStripe would be another important Framework to test on. SilverStripe
    powers quite a few government, political, insurance company, and other large websites.
- id: 743
  author: Remo
  author_email: remo.laubacher@gmail.com
  author_url: http://www.codeblog.ch
  date: '2013-10-03 07:11:03 +0000'
  date_gmt: '2013-10-03 14:11:03 +0000'
  content: |-
    It seems like concrete5 has a similar problem like CakePHP. There's a class called "Collection" which causes HHVM to fail with:

    <code>
    HipHop Fatal error: Class Concrete5_Model_Page may not inherit from interface (Collection) in &#47;home&#47;remo&#47;concrete5&#47;web&#47;concrete&#47;core&#47;models&#47;page.php on line 12<&#47;code>
- id: 749
  author: Bert-Jan
  author_email: info@bert-jan.com
  author_url: ''
  date: '2013-10-09 04:14:24 +0000'
  date_gmt: '2013-10-09 11:14:24 +0000'
  content: I would love to see Propel added to the table.. it's a very popular ORM
    (like Doctrine) used (among others) in symfony &amp; symfony2, but also stand-alone
    in other projects.
- id: 755
  author: Andrey Tserkus
  author_email: zerkyn@gmail.com
  author_url: ''
  date: '2013-10-09 16:18:43 +0000'
  date_gmt: '2013-10-09 23:18:43 +0000'
  content: |-
    Can you also add Magento 2 to the list?
    It is a newer version under development, it has more unit tests.

    GitHub link:
    https:&#47;&#47;github.com&#47;magento&#47;magento2

    Thanks!
- id: 761
  author: Greg
  author_email: gholland85@gmail.com
  author_url: ''
  date: '2013-10-11 10:25:35 +0000'
  date_gmt: '2013-10-11 17:25:35 +0000'
  content: Would love to see Guzzle and the AWS SDK  supported. Great work so far,
    very excited to see what the future holds for this project!
- id: 767
  author: grim
  author_email: dudoenin@mail.com
  author_url: ''
  date: '2013-10-12 02:18:27 +0000'
  date_gmt: '2013-10-12 09:18:27 +0000'
  content: Symconf 2 Go~!
- id: 773
  author: HHVM 2.2.0 &laquo; HipHop Virtual Machine
  author_email: ''
  author_url: http://www.hhvm.com/blog/1301/hhvm-2-2-0
  date: '2013-10-17 17:02:49 +0000'
  date_gmt: '2013-10-18 00:02:49 +0000'
  content: "[&#8230;] was a 17% CPU reduction for running facebook.com compared to
    HHVM 2.1.0. It also supports many more frameworks out of the box&nbsp;like Symfony,
    CodeIgniter, Laravel, and many [&#8230;]"
- id: 779
  author: Corey Ballou
  author_email: corey@coreyballou.com
  author_url: https://pop.co
  date: '2013-10-22 06:37:43 +0000'
  date_gmt: '2013-10-22 13:37:43 +0000'
  content: In future updates, it'd be great if you included the framework version
    numbers just for reference. Major release versions of frameworks often include
    substantial changes. For instances, I can see you're using Laravel 4 for this
    which was still very much in development at the time so I'm wondering how Laravel
    3 faired.
- id: 785
  author: Ivan Mosiev
  author_email: i.k.mosev@gmail.com
  author_url: ''
  date: '2013-10-27 03:13:10 +0000'
  date_gmt: '2013-10-27 10:13:10 +0000'
  content: |-
    Please don't write silly comments. HHVM should support all features of modern PHP, does not matter is it required for frameworks or not. For example we have ArrayAccess interface wich is part of standard PHP library. Unfortunately HHVM does not work correctly with this code:
    <code>
    $array = new ArrayObject();
    $array['foo'] = 'bar';
    array_key_exists('foo', $array);
    <&#47;code>
    This bug break some tests in PHPUnit and other frameworks and if would like to use ArrayAccess in your code will also break your code too. I think frameworks is used there first of all because of huge amount of unit tests that can be used to verify that HHVM supports all existing PHP features. However, if you mean that you don't need OOP in PHP at all you are free to use kPHP anaunced not so long time ago, as I know it supports only old school procedural approach.
- id: 791
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2013-10-28 11:24:06 +0000'
  date_gmt: '2013-10-28 18:24:06 +0000'
  content: Have you reported the bug on github? And we would love a pull request :)
- id: 797
  author: Ivan Mosiev
  author_email: i.k.mosev@gmail.com
  author_url: ''
  date: '2013-10-28 14:29:19 +0000'
  date_gmt: '2013-10-28 21:29:19 +0000'
  content: Report no problem, but about pull request I'm unsure. I'm not so good in
    C++
- id: 803
  author: sachin
  author_email: sachitaware21@gmail.com
  author_url: ''
  date: '2013-10-31 03:39:28 +0000'
  date_gmt: '2013-10-31 10:39:28 +0000'
  content: Can I use it with Core PHP(Procedural style) in any way.I am not using
    any specific Framework for my application but have a custom built mini framework
    to perform basic operations.
- id: 809
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2013-10-31 10:40:56 +0000'
  date_gmt: '2013-10-31 17:40:56 +0000'
  content: 'Yes'
- id: 815
  author: Fernando
  author_email: f.j.mota13@gmail.com
  author_url: ''
  date: '2013-11-07 15:47:21 +0000'
  date_gmt: '2013-11-07 23:47:21 +0000'
  content: |-
    What about Kohana Framework tests? http:&#47;&#47;kohanaframework.org

    WIll be great to see it!
- id: 821
  author: Furicane
  author_email: furi@cane.com
  author_url: ''
  date: '2013-11-17 09:50:36 +0000'
  date_gmt: '2013-11-17 17:50:36 +0000'
  content: Rod, HHVM doesn't work in real world (yet). There are numerous extensions
    PHP has that are in use which HHVM doesn't support and might not support at all.
    That means you can't use it. If you have a busy website, that assumes it makes
    money. Investing money in infrastructure to get several times more back is called
    smart investing. I just hope no one hired you so far, you seem way too green for
    real world work.
- id: 827
  author: bob
  author_email: rsanchez1990@gmail.com
  author_url: ''
  date: '2013-11-18 07:58:37 +0000'
  date_gmt: '2013-11-18 15:58:37 +0000'
  content: Using this is far from free. You don't have to pay for a product, but you
    do have to pay for development time taken to implement this. Then there's the
    opportunity cost of taking a few hours (or more) to implement HHVM rather than
    taking less than an hour to throw more hardware at the problem and using the saved
    time to do something else.
- id: 833
  author: Josh
  author_email: josh@qaribou.com
  author_url: http://qaribou.com
  date: '2013-12-16 18:01:13 +0000'
  date_gmt: '2013-12-17 02:01:13 +0000'
  content: |-
    Just tested this on 2.3.0 w&#47; concrete5 5.6.1.3 - same issue. I'm pretty sure you're right, it's colliding due to Collection being a reserved name, as evidenced on line 930 here:
    https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;blob&#47;master&#47;hphp&#47;runtime&#47;vm&#47;class.cpp#L930

    So Collection is already a defined class name and it won't let you define another (indeed that codepath has instantiated Collection objects of its own already.) If I had to choose, I'd say that the "Collection" is the most fundamental part of Concrete5, so it's not something easily refactored. It's old fashioned, but maybe the HHVM guys should consider a prefix to their own naming conventions. hhvmCollection is much less likely to be defined in a PHP script than Collection would be, after all.
- id: 839
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: ''
  date: '2013-12-17 11:39:20 +0000'
  date_gmt: '2013-12-17 19:39:20 +0000'
  content: Collection should already be namespaced. Maybe it didn't make it into 2.3.0.
    Can you try it again with trunk?
- id: 845
  author: Rafi B.
  author_email: justRafi@gmail.com
  author_url: ''
  date: '2013-12-17 16:21:35 +0000'
  date_gmt: '2013-12-18 00:21:35 +0000'
  content: "+1 for Kohana, would be interesting."
- id: 851
  author: Philipp Gampe
  author_email: philipp.gampe@typo3.org
  author_url: ''
  date: '2013-12-20 11:59:25 +0000'
  date_gmt: '2013-12-20 19:59:25 +0000'
  content: |-
    Any time plan for mysqli support? Mysql is deprecated as of PHP 5.5 and many applications move mysqli.
    http:&#47;&#47;www.php.net&#47;manual&#47;en&#47;intro.mysql.php

    Also consider adding TYPO3 CMS to the list of tested frameworks - it is the fifth most widely used CMS.
    Unit test examples can be found on travis.
- id: 857
  author: Philipp Gampe
  author_email: philipp.gampe@typo3.org
  author_url: ''
  date: '2013-12-20 12:17:35 +0000'
  date_gmt: '2013-12-20 20:17:35 +0000'
  content: |-
    I just checked ... old stable TYPO3 CMS Version 4.5 LTS runs with hhvm <3 in frontend context.

    This is really fast.
- id: 863
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2013-12-20 18:13:50 +0000'
  date_gmt: '2013-12-21 02:13:50 +0000'
  content: mysqli support will land in the next month or two
- id: 869
  author: Josh
  author_email: josh@qaribou.com
  author_url: http://qaribou.com
  date: '2013-12-24 10:15:39 +0000'
  date_gmt: '2013-12-24 18:15:39 +0000'
  content: I found the issue https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;issues&#47;1003
    , and it looks like it just missed the cutoff on 2.3.1. Trunk (and everything
    I see that's going in to 2.3.2) has this fix included. I'm visiting family for
    the holidays for the next week, but will definitely test once I'm back to work.
    It does look like it will all work though - Concrete5's parity remains to be seen,
    but this is a huge amount of progress.
- id: 875
  author: HipHop VM reaches 100% green Unit Tests in Laravel, Drupal, Slim, CodeIgniter
    etc. | Dev Metal
  author_email: ''
  author_url: http://www.dev-metal.com/hiphop-vm-reaches-100-green-unit-tests-in-laravel-drupal-slim-codeigniter-etc/
  date: '2013-12-27 22:58:34 +0000'
  date_gmt: '2013-12-28 06:58:34 +0000'
  content: "[&#8230;] September 2013 the PHP HipHop VM dev team wrote a very interesting
    article [1] about failing Unit Tests of most PHP frameworks when running inside
    the HipHop VM (HHVM). The [&#8230;]"
- id: 881
  author: Loyd
  author_email: loydromano@gmail.com
  author_url: http://www.sample.com
  date: '2014-02-02 07:55:29 +0000'
  date_gmt: '2014-02-02 15:55:29 +0000'
  content: "My programmer is trying to convince me to move to .net from PHP.\nI have
    always disliked the idea because of the expenses.\n\nBut he's tryiong none the
    less. I've been using Movable-type on a number of websites for about a \nyear
    and am anxious about switching to another platform.\n\nI have heard excellent
    things about blogengine.net.\nIs there a way I can transfer all my wordpress posts
    into it?\nAny kind of help would be really appreciated!"
- id: 887
  author: HHVM and WordPress | Keita&#039;s Blog
  author_email: ''
  author_url: http://kkob.us/2014/02/09/hhvm-and-wordpress/
  date: '2014-02-14 02:22:24 +0000'
  date_gmt: '2014-02-14 10:22:24 +0000'
  content: "[&#8230;] Wow HHVM is fast&hellip;too bad it doesn&rsquo;t run my code&#8617;
    [&#8230;]"
- id: 893
  author: 'HHVM: The Next Six Months &laquo; HipHop Virtual Machine'
  author_email: ''
  author_url: http://www.hhvm.com/blog/3743/hhvm-the-next-six-months
  date: '2014-02-24 17:23:24 +0000'
  date_gmt: '2014-02-25 01:23:24 +0000'
  content: "[&#8230;] 20+ top PHP frameworks have 100% unit tests passing [&#8230;]"
- id: 899
  author: besei
  author_email: com@com.com
  author_url: ''
  date: '2014-03-14 16:41:06 +0000'
  date_gmt: '2014-03-14 23:41:06 +0000'
  content: |-
    I got to be able to run, "HHVM" program somehow.
    There was an error of, "mysqli" startup screen "phpmyadmin". I've found the cause of the error.
    Thank you.
    Plan and would like to run for example "CakePHP", "CodeIgniter", "FuelPHP".

    These comments, is the google translation.
- id: 13085
  author: Facebook's Hack, HHVM, and the Future of PHP - Programming - O'Reilly Media
  author_email: ''
  author_url: http://programming.oreilly.com/2014/04/facebooks-hack-hhvm-and-the-future-of-php.html
  date: '2014-04-03 05:01:45 +0000'
  date_gmt: '2014-04-03 12:01:45 +0000'
  content: "[&#8230;] engine. This is necessary because Facebook&#8217;s existing
    codebase is largely existing PHP code. There are a few exceptions since HHVM is
    not 100% compatible with the PHP Zend Engine; there are a few language features
    (like [&#8230;]"
- id: 182045
  author: Hubnest &raquo; What is HHVM?
  author_email: ''
  author_url: http://new.hubnest.com/what-is-hhvm/
  date: '2014-06-22 12:26:47 +0000'
  date_gmt: '2014-06-22 19:26:47 +0000'
  content: "[&#8230;] not for everybody. Although it runs all our codes out of the
    box, HHVM&#8217;s PHP implementation&nbsp;isn&#8217;t complete enough&nbsp;to
    run many popular PHP frameworks. One of the issues&nbsp;is the server requirements
    &#8211; HHVM is [&#8230;]"
- id: 182903
  author: Pavel
  author_email: devibalast@sbcglobal.net
  author_url: ''
  date: '2014-06-24 05:00:45 +0000'
  date_gmt: '2014-06-24 12:00:45 +0000'
  content: Looks very promising but a bit diffucult to deal with some configuration
    problems. We need to disable php native soapclient because we use nusoap. We failed
    miserably. Is there a way to disable some soap or some other modules? Traditional
    way does not work. Is there something fundamental we are missing?
- id: 239603
  author: Major
  author_email: major@fanando.com
  author_url: ''
  date: '2014-09-14 01:15:16 +0000'
  date_gmt: '2014-09-14 08:15:16 +0000'
  content: "+1 for Kohana!!!!!"
- id: 241679
  author: John Sutton
  author_email: jsutton@littlerock.org
  author_url: ''
  date: '2014-09-17 09:09:35 +0000'
  date_gmt: '2014-09-17 16:09:35 +0000'
  content: I used HPHPc and I liked it. Then HHVM came along and I was disappointed
    since it no longer compiled to C, but that decision wasn't mine. I avoided HHVM
    as long as I could, but because of Ubuntu upgrades I eventually installed HHVM
    and FastCGI. When I tried it I discovered HHVM does not support ODBC_CONNECT -
    a very commonly used function. I have many PHP webservices that pull data using
    ODBC. I am really disappointed.
- id: 268151
  author: Theodore R. Smith
  author_email: theodore@phpexperts.pro
  author_url: http://www.phpexperts.pro/
  date: '2014-10-04 05:45:27 +0000'
  date_gmt: '2014-10-04 12:45:27 +0000'
  content: Hey John, the many database-specific functions from the 1990s are no longer
    wise to rely on. Indeed, they're starting to be deprecated by Zend PHP itself.
    Today, in 2014, you really really ought to migrate to PDO (which does support
    ODBC), the de facto standard for database access.
- id: 465065
  author: k0d3g3ar
  author_email: vlad@lanpartyheads.com
  author_url: ''
  date: '2015-04-27 05:50:04 +0000'
  date_gmt: '2015-04-27 12:50:04 +0000'
  content: How about losing the personal attacks here and actually contributing something
    that we all can benefit from.  Telling someone that they shouldn't be hired or
    are too green makes you look like someone I would never hire - not a team player.
- id: 465077
  author: k0d3g3ar
  author_email: vlad@lanpartyheads.com
  author_url: ''
  date: '2015-04-27 05:52:27 +0000'
  date_gmt: '2015-04-27 12:52:27 +0000'
  content: It is used in enterprise projects - lots of them.  Also PHP lacks in any
    form of true compilation to hide source code.  This is a highly needed and valuable
    project.
- id: 465083
  author: k0d3g3ar
  author_email: vlad@lanpartyheads.com
  author_url: ''
  date: '2015-04-27 05:52:48 +0000'
  date_gmt: '2015-04-27 12:52:48 +0000'
  content: "+1"
- id: 476627
  author: HHVM will kompatibel mit den h&auml;ufigsten PHP Frameworks werden - entwickler.de
  author_email: ''
  author_url: https://entwickler.de/online/php/hhvm-will-kompatibel-mit-den-haeufigsten-php-frameworks-werden-136998.html
  date: '2015-05-05 05:26:25 +0000'
  date_gmt: '2015-05-05 12:26:25 +0000'
  content: "[&#8230;] man in den vergangenen Monaten gro&szlig;e Fortschritte bei
    der Performance gemacht hat, wie aus der aktuellen Meldung hervorgeht, will man
    nun mit h&ouml;chster Priorit&auml;t an der Kompatibilit&auml;t zu Anwendungen
    aus der [&#8230;]"
---

HHVM is a highly performant PHP runtime. In fact, it is nearly 40% faster than [HPHPc](http://en.wikipedia.org/wiki/HipHop_for_PHP#History_Before_HHVM), and only getting faster. For example, the HHVM team just rewrote the JIT to use an [SSA intermediate representation (IR)](https://github.com/facebook/hiphop-php/blob/master/hphp/doc/ir.specification). HHIR (HipHop Intermediate Representation) is a strongly typed, SSA-form intermediate representation, positioned between HHBC (HipHop Bytecode) and machine code. It allows HHVM to perform optimizations that were very difficult to perform with the old JIT, using the context of the current runtime environment (e.g., reference counting elision).

<!--truncate-->

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
