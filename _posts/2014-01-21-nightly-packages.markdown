---
author: ptarjan
layout: post
title: Nightly Packages
category: blog
permalink: /blog/3203/nightly-packages
comments:
- id: 2555
  author: Stuart Carnie
  author_email: stuart.carnie@gmail.com
  author_url: ''
  date: '2014-01-21 15:22:49 +0000'
  date_gmt: '2014-01-21 23:22:49 +0000'
  content: Great stuff!  Will hhvm-fastcgi-nightly become available the same way?
- id: 2561
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2014-01-21 15:30:50 +0000'
  date_gmt: '2014-01-21 23:30:50 +0000'
  content: No. `hhvm-fastcgi` doesn't actually have any binaries in it. It is just
    config files for your ngingx or apache. I'm going to work on figuring out how
    to make it not uninstall when you install the nightly, but for now, you can force
    install it or configure by hand.
- id: 2567
  author: Victor Berchet
  author_email: vberchet-all@yahoo.com
  author_url: https://github.com/vicb
  date: '2014-01-21 23:26:13 +0000'
  date_gmt: '2014-01-22 07:26:13 +0000'
  content: For those interested I have a Vagrant setup available at https:&#47;&#47;github.com&#47;vicb&#47;hhvm-vagrant.
    It comes with some HH samples and more is on the way.
- id: 2573
  author: Rasta
  author_email: mf_peppa@yahoo.com
  author_url: ''
  date: '2014-01-22 02:00:43 +0000'
  date_gmt: '2014-01-22 10:00:43 +0000'
  content: Is an Mac OS version planned? If yes, when?
- id: 2579
  author: inet
  author_email: inet2800@gmail.com
  author_url: ''
  date: '2014-01-22 04:58:48 +0000'
  date_gmt: '2014-01-22 12:58:48 +0000'
  content: Please consider builds for Amazon Linux.
- id: 2585
  author: Jacey Harker
  author_email: thyme3333@hotmail.com
  author_url: ''
  date: '2014-01-22 10:25:09 +0000'
  date_gmt: '2014-01-22 18:25:09 +0000'
  content: A nightly update for CentOS (via YUM) would be much-appreciated for our
    dev servers.
- id: 2591
  author: Vadim
  author_email: nucleusv@gmail.com
  author_url: ''
  date: '2014-01-22 10:31:31 +0000'
  date_gmt: '2014-01-22 18:31:31 +0000'
  content: Please package for  > CentOS 6.4
- id: 2597
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2014-01-22 23:27:35 +0000'
  date_gmt: '2014-01-23 07:27:35 +0000'
  content: Mac OS works in interpreter mode but the JIT doesn't work yet. Sadly that
    is the best part of HHVM so we aren't releasing on homebrew yet.
- id: 2603
  author: Bruno
  author_email: bruno@skvorc.me
  author_url: http://www.4kk.me
  date: '2014-01-23 01:20:37 +0000'
  date_gmt: '2014-01-23 09:20:37 +0000'
  content: Agreed, CentOS support would be great.
- id: 2609
  author: Mohammed
  author_email: harede0@gmail.com
  author_url: ''
  date: '2014-01-23 22:35:32 +0000'
  date_gmt: '2014-01-24 06:35:32 +0000'
  content: "I tired to install it and it works with me via command line by when I
    tried it via broswer I have no luck \n\nI amd using apache as a webserver and
    I followed the instructions in this article \nhttp:&#47;&#47;www.hhvm.com&#47;blog&#47;\nunder
    the title of \nMaking it work with Apache"
- id: 2615
  author: Souki
  author_email: soukup@simplia.cz
  author_url: ''
  date: '2014-01-24 05:10:22 +0000'
  date_gmt: '2014-01-24 13:10:22 +0000'
  content: Amazon Linux support would be great!
- id: 2621
  author: Patrick
  author_email: patrickheeney@gmail.com
  author_url: http://getprotobox.com/
  date: '2014-01-24 10:48:57 +0000'
  date_gmt: '2014-01-24 18:48:57 +0000'
  content: I added nightly support to hhvm for vagrant fans at http:&#47;&#47;getprotobox.com&#47;
    or https:&#47;&#47;github.com&#47;protobox&#47;protobox .
- id: 2627
  author: 'Programowanie w PHP &raquo; Blog Archive &raquo; HipHop Virtual Machine
    Blog: Nightly Packages'
  author_email: ''
  author_url: http://php-soft.cba.pl/?p=4382
  date: '2014-01-26 01:35:25 +0000'
  date_gmt: '2014-01-26 09:35:25 +0000'
  content: "[&#8230;] On the HipHop Virtual Machine blog today they&#8217;re announcing
    a new option for those that &#8220;just can&#8217;t wait&#8221; to get the latest
    and greatest HHVM version &#8211; nightly packages. [&#8230;]"
- id: 2633
  author: Pomyk
  author_email: pomyk@go2.pl
  author_url: ''
  date: '2014-01-27 08:37:42 +0000'
  date_gmt: '2014-01-27 16:37:42 +0000'
  content: "+1 for CentOS :)"
- id: 2639
  author: HHVM 2.4.0 &laquo; HipHop Virtual Machine
  author_email: ''
  author_url: http://www.hhvm.com/blog/3287/hhvm-2-4-0
  date: '2014-02-01 10:01:29 +0000'
  date_gmt: '2014-02-01 18:01:29 +0000'
  content: "[&#8230;] 8 week release cadence to keep everything fresh and in your
    hands. Also remember you can run the nightly packages if you want a bleeding edge
    [&#8230;]"
- id: 2645
  author: M&aacute;ximo Cuadros
  author_email: mcuadros@gmail.com
  author_url: https://github.com/mcuadros/homebrew-hhvm
  date: '2014-02-02 16:29:03 +0000'
  date_gmt: '2014-02-03 00:29:03 +0000'
  content: The OSX brew tap is update to 2.4.0
- id: 2651
  author: Cyrill Schumacher
  author_email: cyrill@schumacher.fm
  author_url: ''
  date: '2014-02-12 14:48:23 +0000'
  date_gmt: '2014-02-12 22:48:23 +0000'
  content: I would like to see nightly builds for Amazon Linux AMI :-) Thanks!
- id: 2657
  author: Pepijn Blom
  author_email: pepijn@blommail.nl
  author_url: ''
  date: '2014-02-14 06:04:06 +0000'
  date_gmt: '2014-02-14 14:04:06 +0000'
  content: |-
    About to start testing some sites with HHVM nightly. Can't wait to see the results!

    For work CentOS builds would be appreciated, for personal experimentation Debian &amp; Ubuntu will do just fine :)
- id: 2669
  author: besei
  author_email: com@com.com
  author_url: ''
  date: '2014-02-21 15:28:40 +0000'
  date_gmt: '2014-02-21 23:28:40 +0000'
  content: |-
    $sudo apt-cache show hhvm-nightly

    Hhvm-nightly package can not be found
- id: 2675
  author: Jon Deckeer
  author_email: jondecker76@gmail.com
  author_url: ''
  date: '2014-02-22 03:59:24 +0000'
  date_gmt: '2014-02-22 11:59:24 +0000'
  content: |-
    It appears that hhvm-nightly hasn't built for saucy since the 18th (though precise nightly builds seem to be working)

    http:&#47;&#47;dl.hhvm.com&#47;ubuntu&#47;pool&#47;main&#47;h&#47;hhvm-nightly&#47;
- id: 2681
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2014-02-22 17:15:34 +0000'
  date_gmt: '2014-02-23 01:15:34 +0000'
  content: Hmm, it seems the precise VM is more memory constrained than the others.
    I'll bump the parallelism from 8 to 4
- id: 2687
  author: besei
  author_email: com@com.com
  author_url: ''
  date: '2014-02-23 14:10:04 +0000'
  date_gmt: '2014-02-23 22:10:04 +0000'
  content: Why?
- id: 2693
  author: besei
  author_email: com@com.com
  author_url: ''
  date: '2014-02-25 05:13:52 +0000'
  date_gmt: '2014-02-25 13:13:52 +0000'
  content: "# sudo apt-get install hhvm\nReading package lists... Done\nBuilding dependency
    tree       \nReading state information... Done\nPackage hhvm is not available,
    but is referred to by another package.\nThis may mean that the package is missing,
    has been obsoleted, or\nis only available from another source\n\nE: Package 'hhvm'
    has no installation candidate\n\n# sudo apt-cache show hhvm\nN: Can't select versions
    from package 'hhvm' as it is purely virtual\nN: No packages found\n\n# sudo apt-cache
    show hhvm-nightly\nN: Unable to locate package hhvm-nightly\nE: No packages found"
- id: 2699
  author: besei
  author_email: com@com.com
  author_url: ''
  date: '2014-02-26 06:45:36 +0000'
  date_gmt: '2014-02-26 14:45:36 +0000'
  content: |-
    Sory.

    cpu 32bit.
    Feel disappointed.
    orz
- id: 2705
  author: besei
  author_email: com@com.com
  author_url: ''
  date: '2014-02-26 06:46:34 +0000'
  date_gmt: '2014-02-26 14:46:34 +0000'
  content: |-
    I'm sorry.
    cpu 32bit.
    Feel disappointed.
    orz
- id: 2711
  author: Implementing MySQLi &laquo; HipHop Virtual Machine
  author_email: ''
  author_url: http://www.hhvm.com/blog/3689/implementing-mysqli
  date: '2014-02-26 12:19:21 +0000'
  date_gmt: '2014-02-26 20:19:21 +0000'
  content: "[&#8230;] HHVM 2.5.0. Please test the implementation as much as possible
    before the 2.5.0 release (maybe by using a nightly), so we can continue to fix
    [&#8230;]"
- id: 4055
  author: Jason McClellan
  author_email: jason@jasonmcclellan.io
  author_url: ''
  date: '2014-03-22 16:24:21 +0000'
  date_gmt: '2014-03-22 23:24:21 +0000'
  content: Would love to see nightlies on Fedora!
- id: 4271
  author: Hemant Tiwari
  author_email: t.hemantkumar@gmail.com
  author_url: http://hemant-uniquescience.blogspot.in
  date: '2014-03-23 04:35:25 +0000'
  date_gmt: '2014-03-23 11:35:25 +0000'
  content: "I am trying to install in my local machine under categoty \"For Ubuntu
    12.04\" I got the following error :\r\n\r\nhemant@hemant-virtual-machine:~$ sudo
    apt-get install hhvm-nightly\r\nReading package lists... Done\r\nBuilding dependency
    tree       \r\nReading state information... Done\r\nE: Unable to locate package
    hhvm-nightly"
- id: 4535
  author: Souvik
  author_email: chatterjee.souvik@gmail.com
  author_url: ''
  date: '2014-03-23 22:35:24 +0000'
  date_gmt: '2014-03-24 05:35:24 +0000'
  content: How can I install Hack in Windows?
- id: 5081
  author: Tyler
  author_email: tyler.slater@joltup.com
  author_url: http://joltup.com
  date: '2014-03-25 00:07:48 +0000'
  date_gmt: '2014-03-25 07:07:48 +0000'
  content: "+1 for amazon linux...i would love to use this on elasticbeanstalk"
- id: 5729
  author: Jay
  author_email: jshampur@gmail.com
  author_url: ''
  date: '2014-03-26 12:22:39 +0000'
  date_gmt: '2014-03-26 19:22:39 +0000'
  content: "+1 for CentOS"
- id: 6251
  author: Stranger
  author_email: som@mail.ru
  author_url: ''
  date: '2014-03-28 09:38:03 +0000'
  date_gmt: '2014-03-28 16:38:03 +0000'
  content: FreeBSD would be great!
- id: 8003
  author: Maxim
  author_email: dp.maxime@gmail.com
  author_url: ''
  date: '2014-03-30 17:01:17 +0000'
  date_gmt: '2014-03-31 00:01:17 +0000'
  content: "I am having a trouble using hhvm-nightly with Google API PHP Client:\r\n\r\nWarning:
    Unknown signature algorithm. in &#47;home&#47;maxime&#47;Git&#47;google-api-php-client&#47;src&#47;Google&#47;Signer&#47;P12.php
    on line 85\r\n\r\nFatal error: Uncaught exception 'Google_Auth_Exception' with
    message 'Unable to sign data' in &#47;home&#47;maxime&#47;Git&#47;google-api-php-client&#47;src&#47;Google&#47;Signer&#47;P12.php:86\r\n\r\n\r\nThe
    troubled code in P12.php is:\r\n\r\n    if (!openssl_sign($data, $signature, $this->privateKey,
    \"sha256\")) {\r\n      throw new Google_Auth_Exception(\"Unable to sign data\");\r\n
    \   }\r\n\r\n\r\nThis code works fine with PHP on the same machine with Ubuntu
    13.10."
- id: 19355
  author: 味見部さんにお邪魔して、HACKが動く環境を作った
  author_email: ''
  author_url: http://rocky-manobi.com/blog/?p=164
  date: '2014-04-07 20:08:41 +0000'
  date_gmt: '2014-04-08 03:08:41 +0000'
  content: "[&#8230;] ココのfor For Ubuntu 13.10:のコマンドをとりあえず叩く。今の時点でこのコマンドをプロビジョニングファイルに落としたとしても明日には動かなくなってると思うのでやらない。
    [&#8230;]"
- id: 35747
  author: wasif
  author_email: wasifbinrashid@gmail.com
  author_url: ''
  date: '2014-04-21 06:10:18 +0000'
  date_gmt: '2014-04-21 13:10:18 +0000'
  content: whats about windows version ?
- id: 38879
  author: mani
  author_email: manikantasai123456789@gmail.com
  author_url: ''
  date: '2014-04-24 06:54:09 +0000'
  date_gmt: '2014-04-24 13:54:09 +0000'
  content: wat about windows8
- id: 190469
  author: Martin
  author_email: martin@majlis.cz
  author_url: http://martin.majlis.cz
  date: '2014-07-12 02:09:18 +0000'
  date_gmt: '2014-07-12 09:09:18 +0000'
  content: "Hi,\r\nI have noticed, that there is already repository for Ubuntu 14.04
    Trusty.\r\n\r\nSo, it would be possible to generalize the code for Ubuntu 13.10
    and higher such as:\r\n\r\nsudo echo 1\r\nwget -O - http:&#47;&#47;dl.hhvm.com&#47;conf&#47;hhvm.gpg.key
    | sudo apt-key add -\r\nversion=`lsb_release -a | grep Codename | cut -f2`\r\necho
    deb http:&#47;&#47;dl.hhvm.com&#47;ubuntu $version main | sudo tee &#47;etc&#47;apt&#47;sources.list.d&#47;hhvm.list\r\nsudo
    apt-get update\r\nsudo apt-get install hhvm-nightly"
- id: 192077
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com
  date: '2014-07-15 22:00:31 +0000'
  date_gmt: '2014-07-16 05:00:31 +0000'
  content: Sadly I don't want to maintain that many images that I have to build for.
    I do the latest LTS and the latest release.
- id: 195977
  author: Armin
  author_email: armingrudd@gmail.com
  author_url: ''
  date: '2014-07-24 10:51:18 +0000'
  date_gmt: '2014-07-24 17:51:18 +0000'
  content: ubuntu 14.04 LTS is the latest release. please add it.
- id: 196145
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com
  date: '2014-07-24 23:15:43 +0000'
  date_gmt: '2014-07-25 06:15:43 +0000'
  content: It is there on https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;wiki&#47;Prebuilt%20Packages%20for%20HHVM
- id: 196319
  author: Armin
  author_email: armingrudd@gmail.com
  author_url: ''
  date: '2014-07-25 13:34:49 +0000'
  date_gmt: '2014-07-25 20:34:49 +0000'
  content: "Thanks.\r\nbut I have problem with running hack files.\r\nI have apache
    enabled and hhvm installed. how can I use it?\r\nI mean I created a .php file
    with this code:\r\n\r\ncopied in my htdocs folder which I use for other projects.\r\nbut
    it doesn't work and gives me a syntax error that means it doesn't know <?hh code.\r\nI
    created .hhconfig but when running hh_client it says no hhconfig in root directory
    &#47;home&#47;user&#47;.\r\nI&#039;m confused. Where should I create my hack files
    and how can I run it?\r\nI found nothing useful in manual.\r\nplease help.\r\nThanks
    again"
- id: 235505
  author: Ben Swinburne
  author_email: ben.swinburne@gmail.com
  author_url: ''
  date: '2014-09-08 03:43:40 +0000'
  date_gmt: '2014-09-08 10:43:40 +0000'
  content: "+1 for Amazon Linux"
- id: 330671
  author: Logan
  author_email: lstellway@brighton.com
  author_url: ''
  date: '2015-01-02 14:54:58 +0000'
  date_gmt: '2015-01-02 22:54:58 +0000'
  content: A CentOS package would be great!
- id: 342089
  author: Helmut Hoffer von Ankershoffen
  author_email: hhva@20steps.de
  author_url: http://20steps.de
  date: '2015-01-18 07:08:01 +0000'
  date_gmt: '2015-01-18 15:08:01 +0000'
  content: "+1 for CentOS (7)"
- id: 480695
  author: HHVM ab sofort mit Nightly Packages - entwickler.de
  author_email: ''
  author_url: https://entwickler.de/online/php/hhvm-ab-sofort-mit-nightly-packages-138089.html
  date: '2015-05-08 02:18:54 +0000'
  date_gmt: '2015-05-08 09:18:54 +0000'
  content: "[&#8230;] und ebenfalls in den Genuss eines Nightly Packages kommen m&ouml;chte,
    soll seine W&uuml;nsche im Blogpost Nightly Packages hinterlassen. Dort findet
    man auch Installationsanleitungen f&uuml;r die angesprochenen [&#8230;]"
---

If you just can't wait to get your hands on the latest HHVM code, but you don't want to spend the time to compile it, we have a present for you.

<!--truncate-->

Every midnight, we [run a script](https://github.com/hhvm/packaging/blob/master/hhvm/deb/package) that pulls whatever is in [master](https://github.com/facebook/hhvm/commits/master), compiles it, does a sanity check, builds a package and sends it off to the repo. You can then use it by adding the [HHVM repo normally](https://github.com/facebook/hhvm/wiki#installing-pre-built-packages-for-hhvm) and then installing the "`hhvm-nightly`" package instead of the "`hhvm`" package. The nightly package should work identically to the current [8 week release cycle](https://github.com/facebook/hhvm/wiki/Release-Schedule) package; it will just have all the most recent commits with much less of the testing and hardening (so beware). While we pride ourselves in having master always passing the full test suite, bugs can obviously creep in, so please don't run your production site on a nightly. When you are about to report an issue, please check that it hasn't already been fixed by the nightly package.

(Update) All our [supported distros](https://github.com/facebook/hhvm/wiki/Prebuilt%20Packages%20for%20HHVM) now have nightlies.

For now, there are only Ubuntu LTS (12.04), Ubuntu most recent (13.10) and Debian stable (7). We will consider others if there is enough desire. Comment below if you want another distro and would actively use "`hhvm-nightly`".

For Ubuntu 12.04:


    sudo add-apt-repository ppa:mapnik/boost
    wget -O - http://dl.hhvm.com/conf/hhvm.gpg.key | sudo apt-key add -
    echo deb http://dl.hhvm.com/ubuntu precise main | sudo tee /etc/apt/sources.list.d/hhvm.list
    sudo apt-get update
    sudo apt-get install hhvm-nightly


For Ubuntu 13.10:


    wget -O - http://dl.hhvm.com/conf/hhvm.gpg.key | sudo apt-key add -
    echo deb http://dl.hhvm.com/ubuntu saucy main | sudo tee /etc/apt/sources.list.d/hhvm.list
    sudo apt-get update
    sudo apt-get install hhvm-nightly


For Debian 7:


    wget -O - http://dl.hhvm.com/conf/hhvm.gpg.key | sudo apt-key add -
    echo deb http://dl.hhvm.com/debian wheezy main | sudo tee /etc/apt/sources.list.d/hhvm.list
    sudo apt-get update
    sudo apt-get install hhvm-nightly
