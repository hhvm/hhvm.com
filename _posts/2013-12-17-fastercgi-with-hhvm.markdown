---
author: julk
layout: post
title: FasterCGI with HHVM
category: blog
permalink: /blog/1817/fastercgi-with-hhvm
comments:
- id: 1457
  author: Robert Lidberg
  author_email: Robert.lidberg@duva.se
  author_url: ''
  date: '2013-12-17 13:38:49 +0000'
  date_gmt: '2013-12-17 21:38:49 +0000'
  content: |-
    This is so useful! Thanks!
    Will benchmark for comparison later this week.
- id: 1463
  author: Joseph Scott
  author_email: joseph@josephscott.org
  author_url: https://josephscott.org/
  date: '2013-12-17 14:11:57 +0000'
  date_gmt: '2013-12-17 22:11:57 +0000'
  content: Did the PHP-FPM tests use an opcode cache? Which version of PHP did the
    PHP-FPM tests use?
- id: 1469
  author: klausi
  author_email: klaus.purer@gmail.com
  author_url: ''
  date: '2013-12-17 14:15:37 +0000'
  date_gmt: '2013-12-17 22:15:37 +0000'
  content: |-
    "The following php.ini and php-fpm.ini files were used. " ==> where are those files?

    Did you run the PHP-FPM benchmark without an opcode cache? Then the results are broing, please repeat with APC enabled and clarify that in the post.
- id: 1475
  author: iwankgb
  author_email: kasztelix@gmail.com
  author_url: ''
  date: '2013-12-17 14:18:11 +0000'
  date_gmt: '2013-12-17 22:18:11 +0000'
  content: I would love to know it too. Another interesting comparison could include
    hhvm+fastcgi+webserver and hhvm on its own.
- id: 1481
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: ''
  date: '2013-12-17 14:34:14 +0000'
  date_gmt: '2013-12-17 22:34:14 +0000'
  content: |-
    Juliusz is currently back home in Poland and fast asleep. I'll get him to reply as soon as he gets up.

    If you want to re-create the benchmarks I'll happily link to your post.
- id: 1487
  author: Sandeep
  author_email: sandeepone@gmail.com
  author_url: http://gleez.com
  date: '2013-12-17 14:38:50 +0000'
  date_gmt: '2013-12-17 22:38:50 +0000'
  content: Thanks for the update. Benchmarks are good and exiting. Could you please
    provide the php and hhvm configurations you ran the test?? Anyway hhvm is promising.
- id: 1493
  author: Nick
  author_email: nickvanw@uw.edu
  author_url: ''
  date: '2013-12-17 17:35:26 +0000'
  date_gmt: '2013-12-18 01:35:26 +0000'
  content: |-
    I notice that in your examples, the HHVM appears to be serving one single site - will fcgi work across multiple virtual hosts, or will it require a single instance per?

    I know the SCRIPT_FILENAME can be changed in nginx to not use a hardcoded filename
- id: 1499
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com
  date: '2013-12-17 17:42:11 +0000'
  date_gmt: '2013-12-18 01:42:11 +0000'
  content: 'The author says yes: https:&#47;&#47;news.ycombinator.com&#47;item?id=6925278'
- id: 1505
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com
  date: '2013-12-17 17:43:23 +0000'
  date_gmt: '2013-12-18 01:43:23 +0000'
  content: It should work exactly the same as PHP FPM, so yes, it can host many sites.
- id: 1511
  author: HHVM 2.3.0 and Travis CI &laquo; HipHop Virtual Machine
  author_email: ''
  author_url: http://www.hhvm.com/blog/2393/hhvm-2-3-0-and-travis-ci
  date: '2013-12-17 17:44:25 +0000'
  date_gmt: '2013-12-18 01:44:25 +0000'
  content: "[&#8230;] We released a new version of HHVM today. This one includes all
    the hard work from our lockdown (detailed post to follow) and the ability to use
    HHVM with FastCGI. [&#8230;]"
- id: 1517
  author: Nick
  author_email: nickvanw@uw.edu
  author_url: ''
  date: '2013-12-17 17:50:10 +0000'
  date_gmt: '2013-12-18 01:50:10 +0000'
  content: Awesome! I figured it would, but I wanted to make sure!
- id: 1523
  author: Nick
  author_email: nickvanw@uw.edu
  author_url: ''
  date: '2013-12-17 17:54:01 +0000'
  date_gmt: '2013-12-18 01:54:01 +0000'
  content: "Awesome! \n\nHuge shout out to you guys, this is pretty awesome! I've
    fiddled with HHVM before, but I'm super excited about this! Thanks!"
- id: 1529
  author: Oskar Hane
  author_email: oh@oskarhane.com
  author_url: http://oskarhane.com
  date: '2013-12-17 22:51:59 +0000'
  date_gmt: '2013-12-18 06:51:59 +0000'
  content: |-
    This is great, thanks guys!
    Can't wait to try this.
- id: 1535
  author: Simon
  author_email: simon@photogabble.co.uk
  author_url: http://www.photogabble.co.uk
  date: '2013-12-18 02:16:15 +0000'
  date_gmt: '2013-12-18 10:16:15 +0000'
  content: This looks very promising, looking forward to undertaking some performance
    benchmarks myself :)
- id: 1541
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2013-12-18 02:26:55 +0000'
  date_gmt: '2013-12-18 10:26:55 +0000'
  content: Cool, I would like to link to other benchmarks, so please go ahead.
- id: 1547
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2013-12-18 02:29:42 +0000'
  date_gmt: '2013-12-18 10:29:42 +0000'
  content: |-
    So, yea, that was the first thing I checked after I run the results the first time. It was enabled in php.ini.

    After giving it some thought, the only other thing that could possibly influence the results would be the compilation flags. I followed the official building from source instructions, however I could have screwed it up obviously.

    Please, feel free to roll your own benchmarks and we will link to them from the blog post.
- id: 1553
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2013-12-18 02:32:19 +0000'
  date_gmt: '2013-12-18 10:32:19 +0000'
  content: |-
    Heh, yea. I wanted to post the files, then it turned out we don't have a good thing for posting the files so I forgot to do that.

    Let me tell what I did instead. I used the default php.ini file that came along with the PHP version that was released around September. I then made sure that opcode cache is enabled and it was. I remember retrying with it enabled explicitly.
- id: 1559
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2013-12-18 02:35:16 +0000'
  date_gmt: '2013-12-18 10:35:16 +0000'
  content: php.ini file was the one that comes bundled with PHP sources. I just made
    sure that opcode cache is enabled. I did not make any tweaks to the HHVM configuration
    so I believe it would be equivalent to what comes with the OSS sources.
- id: 1565
  author: David Carrero
  author_email: david@carrero.es
  author_url: http://carrero.es
  date: '2013-12-18 02:45:26 +0000'
  date_gmt: '2013-12-18 10:45:26 +0000'
  content: I&acute;ll try in plesk installation, do you test this ?
- id: 1571
  author: N1
  author_email: krossekrabbe@gmail.com
  author_url: ''
  date: '2013-12-18 03:37:42 +0000'
  date_gmt: '2013-12-18 11:37:42 +0000'
  content: Nice, got my symfony2 app running with hhvm-fastcgi :-) Only missing piece
    for full support seems to be Intl&#47;ICU.
- id: 1577
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2013-12-18 04:23:46 +0000'
  date_gmt: '2013-12-18 12:23:46 +0000'
  content: I ran HHVM as a webserver too. It is quite capable, since it's what runs
    FB in production. In terms of I&#47;O performance it seemed to do just slightly
    better than PHP-FPM + nginx. By that I mean that for "hello world" sites it would
    deliver about 10-15% better throughput.
- id: 1583
  author: Robin
  author_email: hhvm@square-management.nl
  author_url: ''
  date: '2013-12-18 07:59:48 +0000'
  date_gmt: '2013-12-18 15:59:48 +0000'
  content: |-
    Will you be able to provide a working vagrant box (or something like that) so the complete config is available as a working set somewhere?) This would more easily allow other projects to have a running start into checking hhvm compat as well as looking at a complete working example of the config+hhvm+project etc!

    Looking forward to it!
- id: 1589
  author: Josh Koenig
  author_email: josh@getpantheon.com
  author_url: https://www.getpantheon.com
  date: '2013-12-18 10:54:00 +0000'
  date_gmt: '2013-12-18 18:54:00 +0000'
  content: "Getting 20 req&#47;sec from a simple WP install sounds like there was
    no opcode cache enabled. \n\nIf so, these benchmarks aren't very meaningful. :"
- id: 1595
  author: Joel Marcey
  author_email: joelm@fb.com
  author_url: https://www.facebook.com/JoelMarcey
  date: '2013-12-18 11:07:51 +0000'
  date_gmt: '2013-12-18 19:07:51 +0000'
  content: 'Hi Josh -- opcode cache was turned on. This should hopefully clear things
    up a bit: https:&#47;&#47;news.ycombinator.com&#47;item?id=6925278'
- id: 1601
  author: panzi
  author_email: grosser.meister.morti@gmx.net
  author_url: ''
  date: '2013-12-18 13:16:40 +0000'
  date_gmt: '2013-12-18 21:16:40 +0000'
  content: You could make a github gist and embed it in the article.
- id: 1607
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2013-12-18 14:24:39 +0000'
  date_gmt: '2013-12-18 22:24:39 +0000'
  content: I would welcome any independent tests. I will also ask Paul to try to replicate
    the results independently. If they don't match, I will update the post with the
    new results. I will also link to any independent benchmarks that you post in the
    comments.
- id: 1613
  author: Wolf
  author_email: WKupper@powertrain.com
  author_url: ''
  date: '2013-12-18 22:04:39 +0000'
  date_gmt: '2013-12-19 06:04:39 +0000'
  content: |-
    I am getting the following error on CentOS. Does anyone know what might be causing it?

    upstream sent unsupported FastCGI protocol version: 72 while reading response header from upstream

    I am running hhvm as a daemon on port 9000 and copied the NGinx config here.
- id: 1619
  author: Miguel Clara
  author_email: miguelmclara@gmail.com
  author_url: ''
  date: '2013-12-19 05:24:02 +0000'
  date_gmt: '2013-12-19 13:24:02 +0000'
  content: |-
    I was tried to test this with nginx, but can't get past "Not found"

    location ~ .php$ {
                    fastcgi_param SCRIPT_FILENAME   &#47;var&#47;www&#47;blog$fastcgi_script_name;
                    fastcgi_pass                    127.0.0.1:9000;
                    fastcgi_index                   index.php;
                    include &#47;etc&#47;nginx&#47;fastcgi_params;
            }
- id: 1625
  author: diego
  author_email: diego@sirdiego.de
  author_url: ''
  date: '2013-12-19 05:38:57 +0000'
  date_gmt: '2013-12-19 13:38:57 +0000'
  content: Hi, on my Ubuntu 12.04 there is only apache2.2 from repos, but for mod_proxy_fcgi
    I need 2.4. Have you tested this on 12.04? Have you custom build apache2.4?
- id: 1631
  author: Miguel Clara
  author_email: miguelmclara@gmail.com
  author_url: ''
  date: '2013-12-19 05:54:05 +0000'
  date_gmt: '2013-12-19 13:54:05 +0000'
  content: |-
    *I was trying!

    Btw "root" is defined previous to the .php location, forgot to mention that!
- id: 1637
  author: lubosdz
  author_email: lubosdz@hotmail.com
  author_url: http://www.synet.sk
  date: '2013-12-19 06:34:56 +0000'
  date_gmt: '2013-12-19 14:34:56 +0000'
  content: I also doubt about objectiveness of these benchmarks. 20 requests per sec
    is something wrong with environment setup. Also configuration (socket unix&#47;tcp)
    may give different results. Even though HHVM is probably nicely performative,
    yet independent professional benchmarks would be more welcome, sorry :-)
- id: 1643
  author: Las
  author_email: adsda@dde.ee
  author_url: ''
  date: '2013-12-19 09:41:39 +0000'
  date_gmt: '2013-12-19 17:41:39 +0000'
  content: Same, how did you resolve it?
- id: 1649
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2013-12-19 11:39:19 +0000'
  date_gmt: '2013-12-19 19:39:19 +0000'
  content: Please submit a bug report indicating what happens exactly. This might
    be an easy fix, provided it's a problem.
- id: 1655
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2013-12-19 11:44:48 +0000'
  date_gmt: '2013-12-19 19:44:48 +0000'
  content: This is when you forget to start HHVM with the "-vServer.Type=fastcgi"
    option. Your sever is responding with normal "HTTP 1&#47;.0" header instead of
    the binary protocol.
- id: 1661
  author: Miguel Clara
  author_email: miguelmclara@gmail.com
  author_url: ''
  date: '2013-12-19 12:15:56 +0000'
  date_gmt: '2013-12-19 20:15:56 +0000'
  content: |-
    I was using the "hhvm-fastcgi" init script from ubuntu which points to a config file already create.

    using the shell command *AFTER* cd into the root dir it worked!

    This makes me wonder however how should I handle multiple sites... like we do with php-fpm pools, but I guess I'll have to read more about that!

    I wasn't able to run ab tests though.... hhvm process crashes...

    I see this is the log:
    perf_event_open failed with: No such file or directory
    perf_event_open failed with: No such file or directory
    perf_event_open failed with: No such file or directory
    receiving index.php
- id: 1667
  author: Carlos Icaza
  author_email: icazacarlos@gmail.com
  author_url: ''
  date: '2013-12-19 12:29:04 +0000'
  date_gmt: '2013-12-19 20:29:04 +0000'
  content: I tried to install using repository technique, but the package is missing
    for i386 architecture... Debian 7.2 - VirtualBox
- id: 1673
  author: HHVM f&aring;r FastCGI support - GOTCHA
  author_email: ''
  author_url: http://gotcha.busb.org/hhvm-far-fastcgi-support/
  date: '2013-12-19 13:28:07 +0000'
  date_gmt: '2013-12-19 21:28:07 +0000'
  content: "[&#8230;] Du kan l&aelig;se meget mere og se benchmark testene her. [&#8230;]"
- id: 1679
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2013-12-19 20:19:32 +0000'
  date_gmt: '2013-12-20 04:19:32 +0000'
  content: We don't support i386
- id: 1685
  author: Andy
  author_email: rjn143@gmail.com
  author_url: ''
  date: '2013-12-20 21:00:00 +0000'
  date_gmt: '2013-12-21 05:00:00 +0000'
  content: Could you post the hhvm-fastcgi init script ?
- id: 1691
  author: Naveen Valecha
  author_email: valecha29@gmail.com
  author_url: http://www.valechatech.co.in
  date: '2013-12-20 21:18:33 +0000'
  date_gmt: '2013-12-21 05:18:33 +0000'
  content: Thanks for the sharing this.Have anyone implemented it on windows server.
- id: 1697
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2013-12-21 12:01:51 +0000'
  date_gmt: '2013-12-21 20:01:51 +0000'
  content: https:&#47;&#47;github.com&#47;hhvm&#47;packaging&#47;blob&#47;master&#47;hhvm_fastcgi&#47;root&#47;etc&#47;init.d&#47;hhvm-fastcgi
- id: 1703
  author: Sang Le
  author_email: mr.lamphong@gmail.com
  author_url: http://www.sanglt.com
  date: '2013-12-23 00:20:22 +0000'
  date_gmt: '2013-12-23 08:20:22 +0000'
  content: |-
    When will it support multiple instance. Example support for multiple site of apache or nginx.

    Current it hardcode in the &#47;etc&#47;hhvm&#47;server.hdf, so i should copy the init.d script to another, define another port + document root for other site.
- id: 1709
  author: Mike
  author_email: miguelmclara@gmail.com
  author_url: ''
  date: '2013-12-23 20:20:40 +0000'
  date_gmt: '2013-12-24 04:20:40 +0000'
  content: Its the one that comes with the ubuntu package!
- id: 1715
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2013-12-23 23:46:04 +0000'
  date_gmt: '2013-12-24 07:46:04 +0000'
  content: I just released 2.3.2 which should fix the issue.
- id: 1721
  author: Zack Gomez
  author_email: zack.gomez@gmail.com
  author_url: ''
  date: '2013-12-24 11:51:56 +0000'
  date_gmt: '2013-12-24 19:51:56 +0000'
  content: |-
    Hi Paul,

    When will 2.3.2 prebuilt unbuntu packages be pushed?
- id: 1727
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2013-12-24 12:06:19 +0000'
  date_gmt: '2013-12-24 20:06:19 +0000'
  content: I pushed them yesterday about 12 hours ago.
- id: 1733
  author: Random Lists &raquo; PHP 5.5 vs HHVM vs Node.js
  author_email: ''
  author_url: http://letschat.info/php-5-5-vs-hhvm-vs-node-js/
  date: '2013-12-25 12:25:43 +0000'
  date_gmt: '2013-12-25 20:25:43 +0000'
  content: "[&#8230;] the HHVM team used the Fibonacci benchmark (http:&#47;&#47;www.hhvm.com&#47;blog&#47;1817&#47;fastercgi-with-hhvm)
    I tried the same. What I did was vary the number of fibonacci numbers computed
    and measured the [&#8230;]"
- id: 1739
  author: Neil Girardi
  author_email: neil.girardi@gmail.com
  author_url: ''
  date: '2013-12-25 17:00:37 +0000'
  date_gmt: '2013-12-26 01:00:37 +0000'
  content: |-
    Hi,

    On Ubuntu 13.10 after running sudo apt-get install hhvm-fastcgi I get "E: Unable to locate package hhvm-fastcgi"
- id: 1745
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2013-12-25 21:49:05 +0000'
  date_gmt: '2013-12-26 05:49:05 +0000'
  content: Sorry, I broke it when I shipped 2.3.2. It is fixed now.
- id: 1751
  author: Sandeep
  author_email: sandeepone@gmail.com
  author_url: http://Thankyou!
  date: '2013-12-26 12:29:25 +0000'
  date_gmt: '2013-12-26 20:29:25 +0000'
  content: Thank you. I just want to be sure about opcode cache. Even we got good
    results on our internal benchmarks.
- id: 1757
  author: Jim Norton
  author_email: djraaj@gmail.com
  author_url: http://ivoo.tv
  date: '2013-12-26 16:54:28 +0000'
  date_gmt: '2013-12-27 00:54:28 +0000'
  content: |-
    on apt-get update
    I get this error:

    W: GPG error: http:&#47;&#47;dl.hhvm.com precise Release: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY ....
- id: 1763
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2013-12-26 17:07:40 +0000'
  date_gmt: '2013-12-27 01:07:40 +0000'
  content: |-
    Yeah, I just signed the packages. You're going to need to do this:

    wget -O - http:&#47;&#47;dl.hhvm.com&#47;conf&#47;hhvm.gpg.key | sudo apt-key add -
- id: 1769
  author: Our Future Technology Partners | Skooppa.com
  author_email: ''
  author_url: http://www.skooppa.com/skooppa-technology-partners/
  date: '2013-12-27 01:33:25 +0000'
  date_gmt: '2013-12-27 09:33:25 +0000'
  content: "[&#8230;] own Hiphop PHP compiler, which compiles PHP into C++ code to
    make incredible performance advances compared to the regular PHP interpreter and
    moderate performance advances over opcode caching. This system is being actively
    developed and [&#8230;]"
- id: 1775
  author: Julien
  author_email: dont@spam.com
  author_url: ''
  date: '2013-12-27 01:33:45 +0000'
  date_gmt: '2013-12-27 09:33:45 +0000'
  content: |-
    This worked for me, but now it can't find hhvm-fastcgi.
    It worked last week ! I guess you pushed this version in a hurry :P
- id: 1781
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2013-12-27 09:48:05 +0000'
  date_gmt: '2013-12-27 17:48:05 +0000'
  content: Which distro?
- id: 1787
  author: Scott
  author_email: thescottrosenberg@gmail.com
  author_url: ''
  date: '2013-12-29 21:06:32 +0000'
  date_gmt: '2013-12-30 05:06:32 +0000'
  content: |-
    I'm a bit confused. Your first wordpress test shows 22 requests per second from php fpm, but my own nginx&#47;php-fpm 2GB vps does over 1300 requests per second with apache bench against example.com&#47;?p=1

    In the comments, you say php-fpm is ran with opcache, but the over 2 second response time disagree.

    My site does under 600ms pageloads with wordpress php-fpm.

    Something is wrong with your test.

    You either aren't using opcache, or your hardware is really, really bad.
- id: 1793
  author: Scott
  author_email: thescottrosenberg@gmail.com
  author_url: ''
  date: '2013-12-29 21:16:16 +0000'
  date_gmt: '2013-12-30 05:16:16 +0000'
  content: |-
    Server Software:        nginx
    Server Hostname:        localhost
    Server Port:            80

    Document Path:          &#47;?p=1
    Document Length:        0 bytes

    Concurrency Level:      50
    Time taken for tests:   15.860 seconds
    Complete requests:      1000
    Failed requests:        0
    Non-2xx responses:      1000
    Total transferred:      359000 bytes
    HTML transferred:       0 bytes
    Requests per second:    63.05 [#&#47;sec] (mean)
    Time per request:       793.023 [ms] (mean)
    Time per request:       15.860 [ms] (mean, across all concurrent requests)
    Transfer rate:          22.10 [Kbytes&#47;sec] received

    Connection Times (ms)
                  min  mean[+&#47;-sd] median   max
    Connect:        0    0   1.5      0       9
    Processing:   398  775 268.0    740    2047
    Waiting:      398  775 268.0    740    2046
    Total:        398  776 269.3    740    2055

    Percentage of the requests served within a certain time (ms)
      50%    740
      66%    796
      75%    846
      80%    884
      90%    972
      95%   1280
      98%   1871
      99%   1958
     100%   2055 (longest request)


    This is php-fpm with opcache with fastCGI cache off.

    What's odd about it, besides being drastically faster than your results, is if I increase the concurrency to 500 from 50, the requests per second goes up to 434 requests per second
- id: 1799
  author: Grim
  author_email: dudoenin@mail.com
  author_url: ''
  date: '2013-12-30 03:28:54 +0000'
  date_gmt: '2013-12-30 11:28:54 +0000'
  content: How? I same with u,but is not ok. e.g.symfony&#47;web&#47;app_dev.php&#47;demo&#47;
    is 404 not found.
- id: 1805
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2013-12-30 13:05:54 +0000'
  date_gmt: '2013-12-30 21:05:54 +0000'
  content: |-
    You have only 359 bytes per request and only 22.10 of transfer? Did you install the sample data at all? Note that in my test there seem to be much, much higher transfer, and that's despite fewer requests served. I would  expect you are hitting a different page or your page contains different data.

    Either way, I will ask somebody to re-run the test when they are free.
- id: 1811
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2013-12-30 13:28:43 +0000'
  date_gmt: '2013-12-30 21:28:43 +0000'
  content: Perhaps you're getting 302 or something like that? Let me know if I read
    the stats correctly.
- id: 1817
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2013-12-30 13:37:26 +0000'
  date_gmt: '2013-12-30 21:37:26 +0000'
  content: 'In particular, take note of that "Non-2xx responses: 1000". All results
    should be 200, and they were in my case.'
- id: 1823
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2013-12-30 14:16:26 +0000'
  date_gmt: '2013-12-30 22:16:26 +0000'
  content: See my replies below.
- id: 1829
  author: Ajinkya
  author_email: Ajinkya.shahne@gmail.com
  author_url: http://javarevisited.blogspot.com
  date: '2014-01-01 22:08:12 +0000'
  date_gmt: '2014-01-02 06:08:12 +0000'
  content: What is this hip hop virtual machine, does it do hip hop when you run any
    program on it?
- id: 1835
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2014-01-02 09:58:34 +0000'
  date_gmt: '2014-01-02 17:58:34 +0000'
  content: No, only if you hit it hard.
- id: 1841
  author: Scott
  author_email: thescottrosenberg@gmail.com
  author_url: ''
  date: '2014-01-03 12:01:16 +0000'
  date_gmt: '2014-01-03 20:01:16 +0000'
  content: |-
    You make a good point.
    I actually had a full wordpress sitting there, but apparently when apache bench is run on &#47;p=1, it's actually having 404 errors, despite the fact that going to example.com&#47;p=1 loads a real page.

    Testing with example.com&#47; works fine, example.com&#47;p=1 fails.

    I also realized I had fastCGI cache set to 1s (which sits on tmpfs), which made a crazy performance difference.

    Server Software:        nginx
    Server Hostname:        unicornuproar.com
    Server Port:            80

    Document Path:          &#47;
    Document Length:        126772 bytes

    Concurrency Level:      100
    Time taken for tests:   7.630 seconds
    Complete requests:      1000
    Failed requests:        0
    Total transferred:      127048000 bytes
    HTML transferred:       126772000 bytes
    Requests per second:    131.05 [#&#47;sec] (mean)
    Time per request:       763.048 [ms] (mean)
    Time per request:       7.630 [ms] (mean, across all concurrent requests)
    Transfer rate:          16259.83 [Kbytes&#47;sec] received

    Connection Times (ms)
                  min  mean[+&#47;-sd] median   max
    Connect:        0    0   0.4      0       2
    Processing:    31  726 149.8    757     936
    Waiting:       18  700 147.4    735     885
    Total:         33  726 149.4    757     936

    Percentage of the requests served within a certain time (ms)
      50%    757
      66%    776
      75%    794
      80%    805
      90%    839
      95%    866
      98%    892
      99%    907
     100%    936 (longest request)

    This is ab -c 100 -n 1000 http:&#47;&#47;unicornuproar.com&#47;
- id: 1847
  author: Scott
  author_email: thescottrosenberg@gmail.com
  author_url: ''
  date: '2014-01-03 12:18:23 +0000'
  date_gmt: '2014-01-03 20:18:23 +0000'
  content: |-
    I have a question.

    If you use nginx with fastCGI support, with hhvm, can you use nginx fastCGI caching?

    It should work, logically, but I'm just checking.
- id: 1853
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2014-01-03 17:41:12 +0000'
  date_gmt: '2014-01-04 01:41:12 +0000'
  content: So curious, are the updated results with or without the caching?
- id: 1859
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2014-01-03 17:43:42 +0000'
  date_gmt: '2014-01-04 01:43:42 +0000'
  content: Not sure how it works. I would have to understand what does the caching
    do on the protocol level. FastCGI is a stateful protocol, however the entire state
    is contained within a transaction. If therefore cache is used to skip an entire
    transaction I don't see any issues. Otherwise I would have to understand the internals
    to know what is needed to support it.
- id: 1865
  author: Kasper Isager
  author_email: kasperisager@gmail.com
  author_url: http://github.com/kasperisager
  date: '2014-01-04 14:14:30 +0000'
  date_gmt: '2014-01-04 22:14:30 +0000'
  content: |-
    I'm happy to announce that Vagrant LNPP now includes optional support for HHVM FastCGI: https:&#47;&#47;github.com&#47;kasperisager&#47;vagrant-lnpp

    Thanks heaps for this article, it was a great help in getting things set up!
- id: 1871
  author: mig5
  author_email: mig@mig5.net
  author_url: ''
  date: '2014-01-04 19:37:54 +0000'
  date_gmt: '2014-01-05 03:37:54 +0000'
  content: |-
    Doesn't seem to play nicely with Percona Server (drop-in replacement for MySQL) ?

    # &#47;etc&#47;init.d&#47;hhvm-fastcgi start
    &#47;usr&#47;bin&#47;hhvm: &#47;usr&#47;lib&#47;libmysqlclient.so.18: no version information available (required by &#47;usr&#47;bin&#47;hhvm)
- id: 1877
  author: slurm
  author_email: slurm@frontnet.org
  author_url: http://none
  date: '2014-01-04 23:01:44 +0000'
  date_gmt: '2014-01-05 07:01:44 +0000'
  content: "test using wordpress:\nab -c 100 -n 1000 http:&#47;&#47;localhost&#47;wordpress&#47;\n\nWithout
    hhvm: (apache 2.4.6 + modphp 5.5.3) \nRequests per second:    108.79 [#&#47;sec]
    (mean)\n\nwith apache 2.4.6 + hhvm 2.3.1:   \nRequests per second:    324.37 [#&#47;sec]
    (mean)\n\ncpu: i5 760. \n------------------------------------------------------\nServer
    Software:        Apache&#47;2.4.6\nServer Hostname:        localhost\nServer Port:
    \           80\n\nDocument Path:          &#47;wordpress&#47;\nDocument Length:
    \       7673 bytes\n\nConcurrency Level:      100\nTime taken for tests:   3.083
    seconds\nComplete requests:      1000\nFailed requests:        0\nWrite errors:
    \          0\nTotal transferred:      7914000 bytes\nHTML transferred:       7673000
    bytes\nRequests per second:    324.37 [#&#47;sec] (mean)\nTime per request:       308.293
    [ms] (mean)\nTime per request:       3.083 [ms] (mean, across all concurrent requests)\nTransfer
    rate:          2506.87 [Kbytes&#47;sec] received"
- id: 1883
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2014-01-05 12:51:31 +0000'
  date_gmt: '2014-01-05 20:51:31 +0000'
  content: Awesome, thank you. Let us know if there are any issues.
- id: 1889
  author: Paulo Figueiredo
  author_email: pjrfigueiredo@gmail.com
  author_url: http://www.digitalwhores.net
  date: '2014-01-05 18:05:54 +0000'
  date_gmt: '2014-01-06 02:05:54 +0000'
  content: |-
    I'v set up nginx with hhvm but, any file .php returns me "<b>Not found</b>" except index.php that returns me "<b>Running on HHVM version 2.3.2.</b>"

    Some of my configurations

    <b>&#47;etc&#47;nginx&#47;sites-enable&#47;default</b>

    location ~ .php$ {
            root &#47;usr&#47;share&#47;nginx&#47;www;
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME &#47;usr&#47;share&#47;nginx&#47;www$fastcgi_script_name;
            include        fastcgi_params;
    }

    <b>&#47;etc&#47;hhvm&#47;server.hdf</b>

    Server {
      Port = 80
      SourceRoot = &#47;usr&#47;share&#47;nginx&#47;www&#47;
      DefaultDocument = index.php
    }
- id: 1895
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2014-01-05 23:00:16 +0000'
  date_gmt: '2014-01-06 07:00:16 +0000'
  content: That looks right. All your other files are in "&#47;usr&#47;share&#47;nginx&#47;www&#47;"
    and the www-data user has access to read them?
- id: 1901
  author: Paulo Figueiredo
  author_email: pjrfigueiredo@gmail.com
  author_url: http://www.digitalwhores.net
  date: '2014-01-06 04:25:04 +0000'
  date_gmt: '2014-01-06 12:25:04 +0000'
  content: |-
    Setup a test environment for HipHop VM.

    The final VM will contain HHVM, Nginx, PHP, MySQL, ab.

    https:&#47;&#47;github.com&#47;javer&#47;hhvm-vagrant-vm
- id: 1907
  author: Paulo Figueiredo
  author_email: pjrfigueiredo@gmail.com
  author_url: http://www.digitalwhores.net
  date: '2014-01-06 04:26:01 +0000'
  date_gmt: '2014-01-06 12:26:01 +0000'
  content: |-
    Yes! I guess! :)

    -rwxrwxrwx 1 www-data www-data   383 Jul  7  2006 50x.html
    -rwxrwxrwx 1 www-data www-data  2759 Jan  5 14:17 default.txt
    -rwxrwxrwx 1 www-data www-data 51599 Set 27 11:47 image.php
    -rwxrwxrwx 1 www-data www-data   157 Jan  5 14:27 index.html
    -rwxrwxrwx 1 www-data www-data    22 Jan  5 14:48 index.php
    -rw-r--r-- 1 www-data www-data     5 Jan  5 16:01 www.pid
    root@rack:&#47;usr&#47;share&#47;nginx&#47;www# pwd
    &#47;usr&#47;share&#47;nginx&#47;www
- id: 1913
  author: Paulo Figueiredo
  author_email: pjrfigueiredo@gmail.com
  author_url: http://www.digitalwhores.net
  date: '2014-01-06 04:26:18 +0000'
  date_gmt: '2014-01-06 12:26:18 +0000'
  content: |-
    Yes! I guess! :)
    -rwxrwxrwx 1 www-data www-data 383 Jul 7 2006 50x.html
    -rwxrwxrwx 1 www-data www-data 2759 Jan 5 14:17 default.txt
    -rwxrwxrwx 1 www-data www-data 51599 Set 27 11:47 image.php
    -rwxrwxrwx 1 www-data www-data 157 Jan 5 14:27 index.html
    -rwxrwxrwx 1 www-data www-data 22 Jan 5 14:48 index.php
    -rw-r&ndash;r&ndash; 1 www-data www-data 5 Jan 5 16:01 http:&#47;&#47;www.pid
    root@rack:&#47;usr&#47;share&#47;nginx&#47;www# pwd
    &#47;usr&#47;share&#47;nginx&#47;www
- id: 1919
  author: Jim Walker
  author_email: jim@hackrepair.com
  author_url: http://hackrepair.com
  date: '2014-01-07 11:21:13 +0000'
  date_gmt: '2014-01-07 19:21:13 +0000'
  content: I'm guessing this is not something that could ever be installed on a cPanel
    server?
- id: 1925
  author: Scott
  author_email: thescottrosenberg@gmail.com
  author_url: ''
  date: '2014-01-08 13:24:52 +0000'
  date_gmt: '2014-01-08 21:24:52 +0000'
  content: |-
    Thank you for your response.

    I don't have the information to give you on that as I'm not a developer, just a guy who likes webservers.
- id: 1931
  author: Scott
  author_email: thescottrosenberg@gmail.com
  author_url: ''
  date: '2014-01-08 13:28:36 +0000'
  date_gmt: '2014-01-08 21:28:36 +0000'
  content: |-
    Without caching.

    The setup is:
    Wordpress 3.8.1
    Arch Linux (current, rolling distro)
    nginx-custom-dev from aur
    2GB of ram (32GB ram box, rented from weloveservers.net)
    raid 10 hard drives of some variety (unknown)
    No fastCGI cache
- id: 1937
  author: Scott
  author_email: thescottrosenberg@gmail.com
  author_url: ''
  date: '2014-01-08 13:29:20 +0000'
  date_gmt: '2014-01-08 21:29:20 +0000'
  content: I should mention, 8 virtual cores on a xeon e3 1270v3 (quadcore with hyperthreading)
- id: 1943
  author: Scott
  author_email: thescottrosenberg@gmail.com
  author_url: ''
  date: '2014-01-08 13:37:20 +0000'
  date_gmt: '2014-01-08 21:37:20 +0000'
  content: Not for a long, long time, Jim.
- id: 1949
  author: Scott
  author_email: thescottrosenberg@gmail.com
  author_url: ''
  date: '2014-01-08 13:53:16 +0000'
  date_gmt: '2014-01-08 21:53:16 +0000'
  content: |-
    How did I miss the most important parts...

    php 5.5 with opcache (the built in variation)
- id: 1955
  author: Julius Kopczewski
  author_email: julek.kopczewski@gmail.com
  author_url: ''
  date: '2014-01-09 09:25:58 +0000'
  date_gmt: '2014-01-09 17:25:58 +0000'
  content: I see, I will ask someone to rerun the test. I can't do it right now myself
    because I'm terribly busy at least until 15th. Thank you very much for doing the
    tests!
- id: 1961
  author: alexodus
  author_email: alexodus71@gmail.com
  author_url: ''
  date: '2014-01-10 04:05:20 +0000'
  date_gmt: '2014-01-10 12:05:20 +0000'
  content: "+1"
- id: 1967
  author: Drupal Tuning | Annotary
  author_email: ''
  author_url: https://annotary.com/collections/23014/drupal-tuning
  date: '2014-01-12 09:16:18 +0000'
  date_gmt: '2014-01-12 17:16:18 +0000'
  content: "[&#8230;] www.hhvm.com [&#8230;]"
- id: 1973
  author: diego
  author_email: diego@sirdiego.de
  author_url: ''
  date: '2014-01-16 05:53:51 +0000'
  date_gmt: '2014-01-16 13:53:51 +0000'
  content: Has anyone had luck with Ubuntu 12.04 and Apache2.2 now? Or is there a
    possibility to install Apache2.4 with mod_proxy_fcgi on Ubuntu 12.04? 14.04 LTS
    is not that far away, but I don't want to wait 3 month :)
- id: 1979
  author: 'mods missing in apache2 : a web developer&#039;s ...blah blah blah... blog
    :)'
  author_email: ''
  author_url: http://www.thefirmy.co.uk/mods-missing-in-apache2/
  date: '2014-01-22 01:06:21 +0000'
  date_gmt: '2014-01-22 09:06:21 +0000'
  content: "[&#8230;] guys over at Facebook. To say that it is impressive, is an understatement
    &#8211; take a look this post. They got a WordPress installation running at 23
    concurrent requests per second, all the way up to [&#8230;]"
- id: 1985
  author: 'PHP HHVM with specific virtual hosts in apache : a web developer&#039;s
    ...blah blah blah... blog :)'
  author_email: ''
  author_url: http://www.thefirmy.co.uk/php-hhvm-with-specific-virtual-hosts-in-apache/
  date: '2014-01-22 08:15:21 +0000'
  date_gmt: '2014-01-22 16:15:21 +0000'
  content: "[&#8230;] article follows on from a previous post which is here, which
    in turned followed on from this post here. I decided to write this post as I have
    a number of sites inside my development box and I wanted to [&#8230;]"
- id: 1991
  author: Migrate Wordpress to Amazon EC2 | 6tech.org | Open Source Writeups
  author_email: ''
  author_url: http://www.6tech.org/2014/01/migrate-wordpress-to-amazon-ec2/
  date: '2014-01-22 08:55:35 +0000'
  date_gmt: '2014-01-22 16:55:35 +0000'
  content: "[&#8230;] Checkout the primer here: &nbsp;HHVM [&#8230;]"
- id: 1997
  author: Bob
  author_email: bob@vanluijt.nl
  author_url: ''
  date: '2014-01-27 13:45:25 +0000'
  date_gmt: '2014-01-27 21:45:25 +0000'
  content: |-
    Hi all,

    For some unknown reason HHVM-fastcgi won't fire the mysqli() function.

    I've found that HHVM is not supporting mysqli but I thought hhvm-fastcgi was...

    Can somebody help? More info: http:&#47;&#47;stackoverflow.com&#47;questions&#47;21392048&#47;hiphop-fatal-error-class-undefined-mysqli&#47;21392106
- id: 2003
  author: HHVM revisited - SitePoint
  author_email: ''
  author_url: http://www.sitepoint.com/hhvm-revisited/
  date: '2014-01-28 06:01:50 +0000'
  date_gmt: '2014-01-28 14:01:50 +0000'
  content: "[&#8230;] on December 17th, 2013 the HHVM team announced FastCGI support.
    FastCGI is a protocol for a server&#039;s communication with the application [&#8230;]"
- id: 2009
  author: Thomas Decaux
  author_email: ebuildy@gmail.com
  author_url: http://ebuildy.com
  date: '2014-02-05 01:39:48 +0000'
  date_gmt: '2014-02-05 09:39:48 +0000'
  content: |-
    Tried to run my framework eBuildy on it, everything is working fine, except its very slow (10x more than with PHP5.5+OpCache).

    I ran a ab test, I saw my CPU grows to 100% ;(

    Is there setting to tune this?

    Thanks,
- id: 2015
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2014-02-05 13:05:00 +0000'
  date_gmt: '2014-02-05 21:05:00 +0000'
  content: Run it a few times. We take a while to warm up. Also, if you are running
    the command line, you will want `-vEval.Jit=true` to turn on the JIT.
- id: 2021
  author: Nginx + HHVM FastCGI 配置指南 | Qing&#039;s Blog
  author_email: ''
  author_url: http://leiqing.net/?p=2120
  date: '2014-02-08 04:45:52 +0000'
  date_gmt: '2014-02-08 12:45:52 +0000'
  content: "[&#8230;] FasterCGI with HHVM 由于 hhvm.com 网站被Qiang，可以通过hhvm.cn的镜像查看。 [&#8230;]"
- id: 2027
  author: HHVM, Nginx and Laravel | victor - note
  author_email: ''
  author_url: http://note.kakichung.com/?p=72
  date: '2014-02-15 07:22:51 +0000'
  date_gmt: '2014-02-15 15:22:51 +0000'
  content: "[&#8230;] Information on installing HHVM on other server distributions
    (including newer Ubuntu&#8217;s) can be&nbsp;found here. [&#8230;]"
- id: 2033
  author: A Look at Hack, the PHP Replacement in HHVM - SitePoint
  author_email: ''
  author_url: http://www.sitepoint.com/look-hack-php-replacement-hhvm/
  date: '2014-02-19 09:01:25 +0000'
  date_gmt: '2014-02-19 17:01:25 +0000'
  content: "[&#8230;] few things that are worth mentioning are the recent support
    for FastCGI and the integrated [&#8230;]"
- id: 2039
  author: cabana
  author_email: cabana@wp.eu
  author_url: ''
  date: '2014-02-21 13:32:24 +0000'
  date_gmt: '2014-02-21 21:32:24 +0000'
  content: |-
    HI
    I have a qustion. Would someone tell me why I can't upload file over ftp funcion in PHP when I'm using HHVM?
    Maybe Someone had a similar problem and would tell me how to fix it ;)
- id: 2045
  author: Nick
  author_email: nickcomodo@gmail.com
  author_url: ''
  date: '2014-02-25 08:54:28 +0000'
  date_gmt: '2014-02-25 16:54:28 +0000'
  content: |-
    I think maybe it should be mentioned that you'll need to add 'IP = 127.0.0.1' to server.hdf.
    Otherwise (and this is my experience on Debian using the repos you have above) hhvm will bind to 0.0.0.0 and not localhost.
- id: 2051
  author: Franky
  author_email: franky@techkram.de
  author_url: http://techkram.de
  date: '2014-03-04 17:34:44 +0000'
  date_gmt: '2014-03-05 01:34:44 +0000'
  content: Have you ever run performance tests how good it performs when the cached
    WordPress Template comes out of a Ramdisk?
- id: 2057
  author: Robert
  author_email: Bob_586@Yahoo.com
  author_url: ''
  date: '2014-03-08 18:03:02 +0000'
  date_gmt: '2014-03-09 02:03:02 +0000'
  content: |-
    I'm using Ubuntu 13.10 with Apache2:
    I installed HHVM and it is running on port 9000...
    I cannot find these config files:
    mod_proxy.load
    mod_proxy.conf
    mod_proxy_fcgi.load
    Where can I download them from???
- id: 2063
  author: PHP + FastCGI + HHVM | REMO Ideas
  author_email: ''
  author_url: http://www.remoideas.com/php-fastcgi-hhvm/
  date: '2014-03-08 19:20:40 +0000'
  date_gmt: '2014-03-09 03:20:40 +0000'
  content: "[&#8230;] La p&aacute;gina de como instalar hhvm oficial es esta http:&#47;&#47;www.hhvm.com&#47;blog&#47;1817&#47;fastercgi-with-hhvm
    [&#8230;]"
- id: 2069
  author: Ruben de Vries
  author_email: ruben@rubensayshi.com
  author_url: ''
  date: '2014-03-13 10:05:13 +0000'
  date_gmt: '2014-03-13 17:05:13 +0000'
  content: |-
    fast-cgi can spawn a big pile of workers, hhvm is just one process

    how does this compare?
    is this configurable somehow?
- id: 3623
  author: Hack Isn&rsquo;t PHP | Roger Stringer
  author_email: ''
  author_url: http://rogerstringer.com/2014/03/21/hack-isnt-php/
  date: '2014-03-21 15:15:35 +0000'
  date_gmt: '2014-03-21 22:15:35 +0000'
  content: "[&#8230;] and they stand to gain a lot if they can make it faster, so
    they wrote their own runtime that&rsquo;s&nbsp;much&nbsp;faster than the official
    one. This is exactly what the PHP world needed: making its already-fast [&#8230;]"
- id: 5849
  author: Geo
  author_email: cubeseo@gmail.com
  author_url: ''
  date: '2014-03-26 22:21:11 +0000'
  date_gmt: '2014-03-27 05:21:11 +0000'
  content: "Trying to send SMTP mail i get error:\r\n\r\nUndefined function: stream_socket_enable_crypto"
- id: 8219
  author: necenzurat
  author_email: necenzurat@gmail.com
  author_url: http://www.necenzurat.com
  date: '2014-03-30 18:51:58 +0000'
  date_gmt: '2014-03-31 01:51:58 +0000'
  content: same error here, but i manage to install wordpress, on it so no probem
    except the notice
- id: 13691
  author: My Journey with HHVM-Pt.1 - Tech Samurais
  author_email: ''
  author_url: http://techsamurais.com/?p=1537
  date: '2014-04-03 11:54:51 +0000'
  date_gmt: '2014-04-03 18:54:51 +0000'
  content: "[&#8230;] need to run the same tests as the ones on the HHVM blog and
    compare the results. These test will be run against our project. Let&#8217;s see
    what we get! [&#8230;]"
- id: 31463
  author: Crazyzurfer
  author_email: joadiaz@alumnos.uai.cl
  author_url: ''
  date: '2014-04-16 09:15:34 +0000'
  date_gmt: '2014-04-16 16:15:34 +0000'
  content: Doesn't work for ubuntu 14.04 :(
- id: 35471
  author: Mark Jaquith
  author_email: mark@jaquith.me
  author_url: http://markjaquith.com/
  date: '2014-04-20 20:52:39 +0000'
  date_gmt: '2014-04-21 03:52:39 +0000'
  content: Yep, it's working just fine for me. Nginx doesn't really care if it's PHP-FPM
    or HHVM it's sending the requests to. Its caching is unaffected.
- id: 51989
  author: Install HHVM | Janik von Rotz
  author_email: ''
  author_url: https://janikvonrotz.ch/2014/04/30/install-hhvm/
  date: '2014-04-30 00:26:54 +0000'
  date_gmt: '2014-04-30 07:26:54 +0000'
  content: "[&#8230;] Prebuilt Packages on Ubuntu 12.04 FasterCgi with hhvm FastCGI
    configuration on the HHVM GitHub [&#8230;]"
- id: 141959
  author: Dave Harris
  author_email: drh@itfixt.com
  author_url: ''
  date: '2014-05-23 07:19:20 +0000'
  date_gmt: '2014-05-23 14:19:20 +0000'
  content: "A PHP-FPM worker process runs under the group &amp; user IDs of the owner
    of the site being served, set by the ownership of the document root for that site.
    As I run a server supporting multiple clients, this is invaluable. Can HHVM do
    this without me having to set up one VM per site?\r\n\r\nAlso: I manage the sites
    using ISPConfig. As the latter supports configuring sites to use FastCGI, I presume
    that if HHVM is the \"other side\" of FastCGI, it should work... but if not, it
    shouldn't be too hard to make it work :) Any opinions?"
- id: 143129
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com
  date: '2014-05-23 15:35:11 +0000'
  date_gmt: '2014-05-23 22:35:11 +0000'
  content: HHVM uses threads to serve each request, where PHP5 uses processes. Sadly
    with threads we can't change UserID for each request.
- id: 155273
  author: Setup HHVM on Ubuntu 13.10
  author_email: ''
  author_url: http://hitmyserver.net/hhvm-on-ubuntu-13-10.html
  date: '2014-05-27 08:52:51 +0000'
  date_gmt: '2014-05-27 15:52:51 +0000'
  content: "[&#8230;] can follow most of the directions here at the HHVM blog however
    there are a few other things to [&#8230;]"
- id: 189977
  author: YUE
  author_email: tjuyzl@gmail.com
  author_url: ''
  date: '2014-07-10 18:37:11 +0000'
  date_gmt: '2014-07-11 01:37:11 +0000'
  content: I run the SPECWeb2009 benchmark on the SUT. And at the SUT, I use the Nginx
    + HHVM3.2.0 as server. However, the requests per second is not good, and the hhvm
    process always crashes.looking forward to your reply！
- id: 195431
  author: HHVM at it&#8217;s glance &#8211; speed comparision &#8211; Fohlen&#039;s
    Blog
  author_email: ''
  author_url: https://www.einhufer.info/2014/07/23/hhvm-at-its-glance-speed-comparision/
  date: '2014-07-23 05:48:54 +0000'
  date_gmt: '2014-07-23 12:48:54 +0000'
  content: "[&#8230;] a interesting article I found comparing HHVM with [&#8230;]"
- id: 199781
  author: ck
  author_email: ck+hhvm@bbshowcase.org
  author_url: ''
  date: '2014-07-29 17:55:22 +0000'
  date_gmt: '2014-07-30 00:55:22 +0000'
  content: "Despite the age, you guys should go back and correct this page&#47;benchmark
    for the obvious error with wordpress.\r\n\r\n\"Requests per second: 949.21\"\r\n\"Time
    per request:    1.054 [ms]\"\r\n\r\nThis never happened in reality. Something
    clearly went wrong and those are empty replies with error messages if you examine
    the html of results.\r\n\r\nMultiple independent benchmarks confirm this, even
    after \"JIT warmup\" HHVM is perhaps four times faster than php 5.5, certain never
    \"40x\" faster for wordpress."
- id: 207293
  author: Why Facebook is making a PHP renaissance &#124; KidsIL
  author_email: ''
  author_url: http://www.kidsil.net/2014/08/facebook-making-php-renaissance/
  date: '2014-08-07 10:31:24 +0000'
  date_gmt: '2014-08-07 17:31:24 +0000'
  content: "[&#8230;] performance of HHVM has been reviewed&nbsp;in a few articles,
    and it seems to have pushed the core developers of PHP, as the last versions [&#8230;]"
- id: 212915
  author: Vozidea
  author_email: zeokat@gmail.com
  author_url: http://www.vozidea.com
  date: '2014-08-14 14:51:41 +0000'
  date_gmt: '2014-08-14 21:51:41 +0000'
  content: |-
    I tried to install it on Ubuntu 14.04 and followed instructions as i describe in https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;issues&#47;3472 but i&acute;m having the 404 problem.

    Perhaps someone can help, because i can't find the solution.
- id: 255023
  author: laurens
  author_email: laurens@ilaurens.nl
  author_url: ''
  date: '2014-09-24 12:25:26 +0000'
  date_gmt: '2014-09-24 19:25:26 +0000'
  content: There is also a possiblity for one process per client. I guess. So there
    is room for changes. One per thread is the better way of doing things in my opinion.
- id: 303713
  author: xeridea
  author_email: xeridea@gmail.com
  author_url: ''
  date: '2014-11-24 22:10:52 +0000'
  date_gmt: '2014-11-25 06:10:52 +0000'
  content: "\"Only 23 requests per second seem to indicate that WordPress is computationally
    very expensive to run in an interpreter.\"\r\nThis is more a sign that WordPress
    is horribly inefficient beyond reason or repair.  Anyone even remotely concerned
    about performance should not use it.  Years and years of horrible hacks on top
    of a bad framework to begin with, the devs refusing to fix it.\r\n\r\nFibonacci?
    \ What kind of a test is this?  I am sure everyone has highly specific loops like
    this on their website.  Perhaps some better tests?\r\n\r\nThe legitimate tests
    performed by others that don't result in a thousand error pages (from you know,
    crashes, and incomplete features), show more reasonable performance boost (like
    2-4x, but HHVM performance is extremely variable).\r\n\r\nI am looking forward
    to PHPNG, which has comparable performance, with potentially more, doesn't crash,
    passes all the unit tests, is compatible with all extensions, is easy to install,
    has ALL the features, you don't wait years for features, and the best support."
- id: 307931
  author: DRJ
  author_email: server@swipemax.com
  author_url: ''
  date: '2014-12-03 09:46:57 +0000'
  date_gmt: '2014-12-03 17:46:57 +0000'
  content: Any updates on this test? Please let's know how far HHVM has gone and how
    the results stack. Thanks.
- id: 309323
  author: Fred Emmott
  author_email: fe@fb.com
  author_url: ''
  date: '2014-12-05 10:04:42 +0000'
  date_gmt: '2014-12-05 18:04:42 +0000'
  content: 'I''ll hopefully have a larger update to share soon, though you can see
    how we''re trying to investigate performance here: https:&#47;&#47;github.com&#47;hhvm&#47;oss-performance'
- id: 310031
  author: HHVM with Nginx fastcgi not working properly | Zesati Answers
  author_email: ''
  author_url: http://op4rt3.org/wordpress/zesati/2014/12/06/hhvm-with-nginx-fastcgi-not-working-properly/
  date: '2014-12-06 04:35:05 +0000'
  date_gmt: '2014-12-06 12:35:05 +0000'
  content: "[&#8230;] I&#039;ve followed a stairs mentioned here:http:&#47;&#47;www.hhvm.com&#47;blog&#47;1817&#47;fastercgi-with-hhvm
    [&#8230;]"
- id: 342509
  author: GT
  author_email: abcd@kani.hu
  author_url: ''
  date: '2015-01-18 14:56:54 +0000'
  date_gmt: '2015-01-18 22:56:54 +0000'
  content: I doubt php-fpm installation had accelerator module. At the post date maybe
    the built-in opcache module wasn't available, but for fair comparison an apc could
    be essential. I don't know anyone who using php-fpm without one of these kind
    of modules (opcache&#47;apc&#47;zendaccelerator&#47;etc.)
- id: 420497
  author: 'HHVM e Hack Language: Compartilhando experiencias | Grupo de Desenvolvedores
    de PHP de S&atilde;o Paulo'
  author_email: ''
  author_url: http://phpsp.org.br/hhvm-e-hack-language-compartilhando-experiencias/
  date: '2015-03-20 10:32:26 +0000'
  date_gmt: '2015-03-20 17:32:26 +0000'
  content: "[&#8230;] O mesmo vale para o&nbsp;HHVM, que oferece pacotes de instala&ccedil;&atilde;o
    para as principais Distros Linux e&nbsp;suporte para FastCGI, podendo ser executado&nbsp;nos
    principais&nbsp;servidores [&#8230;]"
- id: 480689
  author: HHVM bekommt FastCGI-Support und wird kompatibel mit Apache, Nginx, Lighttpd,
    ... - entwickler.de
  author_email: ''
  author_url: https://entwickler.de/online/php/hhvm-bekommt-fastcgi-support-und-wird-kompatibel-mit-apache-nginx-lighttpd-137817.html
  date: '2015-05-08 02:09:50 +0000'
  date_gmt: '2015-05-08 09:09:50 +0000'
  content: "[&#8230;] der Beschreibung der FastCGI-Implementierung wird deutlich,
    dass Facebook stark auf CPU- und RAM-Optimierung hingearbeitet hat und die Erfahrung
    [&#8230;]"
- id: 536435
  author: How to Setup HHVM on Ubuntu 14.04 Server with Apache 2.4 &#8211; Part 1
    | Runtime Reflection
  author_email: ''
  author_url: https://runtimereflection.wordpress.com/2015/06/29/how-to-setup-hhvm-on-ubuntu-14-04-server-with-apache-2-4-part-1/
  date: '2015-06-29 20:44:41 +0000'
  date_gmt: '2015-06-30 03:44:41 +0000'
  content: "[&#8230;] http:&#47;&#47;hhvm.com&#47;blog&#47;1817&#47;fastercgi-with-hhvm
    [&#8230;]"
- id: 610739
  author: Faxicon Dev
  author_email: info@faxicon.com
  author_url: http://faxicon.com
  date: '2015-09-17 20:17:47 +0000'
  date_gmt: '2015-09-18 03:17:47 +0000'
  content: I'm still fail to build this one on plesk 12 with centos 7 , return to
    normal php
- id: 768449
  author: Homsa Lomsa
  author_email: pfe.skh@gmail.com
  author_url: ''
  date: '2016-01-20 00:45:17 +0000'
  date_gmt: '2016-01-20 08:45:17 +0000'
  content: "I'm benchmarking a PHP with one database insertion per request, but it
    seems like nginx&#47;php-fpm is a bit faster than nginx&#47;hhvm\r\n\r\n~700 requests
    &#47; sec for nginx&#47;php-fpm against\r\n~500 requests &#47; sec for nginx&#47;hhvm.\r\n\r\nAny
    idea?"
- id: 770519
  author: Fred Emmott
  author_email: fe@fb.com
  author_url: ''
  date: '2016-01-21 11:22:00 +0000'
  date_gmt: '2016-01-21 19:22:00 +0000'
  content: There is not enough information here to really give an informed response
    - that said, we are often slower at small benchmarks, and we do not consider this
    a problem as long as it is not true for real world applications; in our experience,
    benchmark performance and real world performance are rarely related.
---

Today, we are happy to announce [FastCGI](http://www.fastcgi.com/drupal/) support for HHVM. FastCGI is a popular protocol for communication between an application server (e.g. running your PHP code) and a webserver. With support for FastCGI, you will be able to run HHVM behind any [popular web server](http://en.wikipedia.org/wiki/FastCGI#Web_Servers_that_implement_FastCGI) (Apache, Nginx, Lighttpd, etc). The webserver is in charge of handling all the intricate details of the HTTP protocol. HHVM is in charge of what it does best, running PHP code blazingly fast.


<!--truncate-->

If you can’t wait to get your hands on the new feature, just jump to the Installation section. If you are curious about how the new feature was baked into HHVM or just want to learn how well it performs, read on.


# How it works




FastCGI was designed to solve one crucial problem that plagued its predecessor CGI, namely: performance. The CGI protocol required that a new instance of the application be spawned on every request. Such a trade-off could have been tolerable for small native programs where start-up overhead was negligible. It is however incredibly difficult for a JIT compiler such as HHVM. The HipHop virtual machine keeps track of the code that ran in the past and reuses bytecode output whenever it sees a known file. HHVM also performs just-in-time compilation, i.e. translates snippets of the bytecode into native machine code when they are run frequently. Both of these features require that an instance of HHVM runs in server mode and lives on from request to request. FastCGI protocol enables that. Moreover, FastCGI can be configured to reuse the same connection for serving multiple requests. This involves serving both requests coming one after another and serving multiple requests in parallel. In the latter case data from multiple requests is multiplexed on a single connection.




HHVM FastCGI server uses asynchronous I/O. This means that an I/O thread will never block waiting on a single connection. Instead, system routines such as select() are used to monitor activity on multiple connections at once. When activity is detected (e.g. file descriptor becomes ready for reading or writing), an I/O thread executes the appropriate non-blocking action. This completes a single cycle of the event loop. This approach maximizes CPU use when serving I/O. Consequently, the threads spend only as much time blocked as absolutely necessary. I/O is served using multiple threads. Once the server is under heavy load, there will roughly be one I/O thread per CPU core. The incoming connections are then distributed evenly between the I/O threads using a round robin. As a result, operations on a single connection are always single-threaded and no additional synchronisation is needed.




A separate set of worker threads is used to execute PHP code. All the (partially) decoded requests are put inside a common concurrent queue. In a loop, each worker thread then pops a new request to be served. At this point, all the request headers are ready. For small requests, the request body will also typically be available. When a request is large (e.g. is a file upload), the worker thread might block waiting on more I/O to become available. The payload can be stored to a file in order to keep memory usage low. Once all the request data becomes available, PHP execution may begin. The output produced by a PHP script is buffered and sent to an I/O thread for further handling.





# Performance




We conducted benchmarks using Nginx. In the first test we ran a Wordpress instance. The second test showcases HHVM performance for computation-intensive tasks. We used a simple php script computing Fibonacci numbers.





## Wordpress




The first test was performed using the Wordpress example page. No changes were made to the wordpress deployment besides filling in mandatory database connection fields. Nginx was used as a web server. Apache bench was used for load testing using this command:





    ab -c 50 -n 1000 http://localhost/wordpress/wordpress/?p=1




### PHP-FPM


Sadly the results were pretty bad for PHP. Only 23 requests per second seem to indicate that Wordpress is computationally very expensive to run in an interpreter.


    Requests per second: 23.17 [#/sec] (mean)
    Time per request:    2157.579 [ms] (mean)
    Time per request:    43.152 [ms] (mean, across all concurrent requests)
    Transfer rate:       275.42 [Kbytes/sec] received




### HHVM FastCGI




On a cold start, HHVM still performed much better than PHP-FPM; however, there was a clear penalty associated with the initial JITing of PHP files:





    Requests per second: 184.71 [#/sec] (mean)
    Time per request:    270.689 [ms] (mean)
    Time per request:    5.414 [ms] (mean, across all concurrent requests)
    Transfer rate:       2194.38 [Kbytes/sec] received




After the initial warm-up the results got noticeably better:





    Requests per second: 949.21 [#/sec] (mean)
    Time per request:    52.676 [ms] (mean)
    Time per request:    1.054 [ms] (mean, across all concurrent requests)
    Transfer rate:       11276.46 [Kbytes/sec] received




That’s a surprisingly good result of roughly 40x higher throughput than the default PHP-FPM setting.





## Fibonacci




Next we decided to compare the two runtimes using a computationally expensive example. We wrote a simple function computing Fibonacci numbers using an exponential algorithm. Here are the results for computing Fib(N) for value N = 5, 15, 25, 30:





### PHP-FPM




    Requests per second: 13789.24 [#/sec] (mean) Fib(5)
    Requests per second: 3202.31 [#/sec] (mean)  Fib(15)
    Requests per second: 118.94 [#/sec] (mean)   Fib(25)*
    Requests per second: 8.40 [#/sec] (mean)     Fib(30)**




*only 1000 requests were performed to save time




**only 100 requests were performed to save time





### HHVM FastCGI




    Requests per second: 8842.70 [#/sec] (mean) Fib(5)
    Requests per second: 8892.66 [#/sec] (mean) Fib(15)
    Requests per second: 5581.37 [#/sec] (mean) Fib(25)
    Requests per second: 737.56 [#/sec] (mean)  Fib(30)




In case where N = 5, the page required almost no computation at all. In this case it was visible just how well optimized FPM really is. It was over 50% faster than HHVM FastCGI server which indicates that there is still a lot of room for improvement in our implementation. However at N = 15 the amount of computation already shifted the balance to HHVM’s advantage. Where for HHVM the bottleneck was still the network, FPM was clearly CPU bound at this point with a result almost 3x worse than HHVM. At N = 30, HHVM just in time compilation really shined, yielding results almost 80x faster than PHP.





# Installation




Now to the fun part: how to get HHVM FastCGI working on your machine? For popular Debian-based distros we prepared a set of pre-built packages:





### Ubuntu 12.04




    echo deb http://dl.hhvm.com/ubuntu precise main | sudo tee /etc/apt/sources.list.d/hhvm.list
    sudo apt-get update
    sudo apt-get install hhvm




### Ubuntu 13.10




    echo deb http://dl.hhvm.com/ubuntu saucy main | sudo tee /etc/apt/sources.list.d/hhvm.list
    sudo apt-get update
    sudo apt-get install hhvm




### Debian 7




    echo deb http://dl.hhvm.com/debian wheezy main | sudo tee /etc/apt/sources.list.d/hhvm.list
    sudo apt-get update
    sudo apt-get install hhvm




### Other




If your distro is not on the list, you can still run HHVM FastCGI, with slightly more work (or you can take the scripts from that package and repackage it for your distro). First, install the [latest release of HHVM](https://github.com/facebook/hhvm/wiki#installing-pre-built-packages-for-hhvm). To run the server in FastCGI mode, pass additional parameters to HHVM runtime:





    cd /path/to/your/www/root
    hhvm --mode server -vServer.Type=fastcgi -vServer.Port=9000




The server will now accept connections on localhost:9000 (only TCP sockets are supported for now). To turn the server into a daemon, change the value of mode to:





    hhvm --mode daemon -vServer.Type=fastcgi -vServer.Port=9000




All the usual options accepted by the HHVM runtime are also available in the FastCGI mode. Please make sure that HHVM runs from the directory where you wish to serve PHP files.




Once the HHVM FastCGI server is up and running, it’s time to appropriately configure your webserver of choice. As an example, we include instructions for Apache and Nginx.





## Making it work with Apache




The recommended way of integrating with Apache is using the mod_proxy_fcgi module. First, you need to enable mod_proxy and mod_proxy_fcgi modules, if you haven’t done so already. To enable the modules make sure you have the following symlinks created:





    cd /path/to/your/apache/conf
    ln -s ../mods-available/mod_proxy.load mods-enabled/mod_proxy.load
    ln -s ../mods-available/mod_proxy.conf mods-enabled/mod_proxy.conf
    ln -s ../mods-available/mod_proxy_fcgi.load mods-enabled/mod_proxy_fcgi.load




Next up, you need to insert a directive instructing Apache to send traffic to the FastCGI server. You can do so by inserting the following line in your apache.conf / httpd.conf file.





    ProxyPass / fcgi://127.0.0.1:9000/path/to/your/www/root/goes/here/




Please note that this will route _all_ the traffic to the FastCGI server. If you want to route only certain requests (e.g. only those from a subdirectory or ending *.php, you can use ProxyPassMatch, e.g.





    ProxyPassMatch ^/(.*.php(/.*)?)$ fcgi://127.0.0.1:9000/path/to/your/www/root/goes/here/$1




Consult [Apache docs](http://httpd.apache.org/docs/trunk/mod/mod_proxy_fcgi.html) for more details on how to use ProxyPass and ProxyPassMatch.





## Making it work with Nginx




The default FastCGI configuration from Nginx should work just fine with HHVM FastCGI. You will need to add the following directives inside one of your location directives:





    root /path/to/your/www/root/goes/here;
    fastcgi_pass   127.0.0.1:9000;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME /path/to/your/www/root/goes/here$fastcgi_script_name;
    include        fastcgi_params;




The traffic for the surrounding location directive will then be routed to HHVM.





# What’s next?




There are a couple of important features still missing from the initial implementation. The most notable is support for local UNIX sockets. At present, only less performant (however more flexible) TCP sockets are available. The priorities for this release were:







  * Correctness,


  * Getting the architecture of the solution right, so that performance can be improved in the future.


We haven’t really done any profiling on the new server yet. It is therefore quite likely that there is some low hanging fruit waiting to be picked. We are definitely looking forward to improving HHVM FastCGI performance in the future releases.
