---
author: ptarjan
layout: post
title: WP Engine and Box now use HHVM
category: blog
permalink: /blog/6989/wp-engine-and-box-now-use-hhvm
comments:
- id: 480797
  author: Online-Services remade? Mehr Services setzen auf Facebooks Programmiertools
    - entwickler.de
  author_email: ''
  author_url: https://entwickler.de/online/tools/online-services-remade-mehr-services-setzen-auf-facebooks-programmiertools-140384.html
  date: '2015-05-08 02:39:53 +0000'
  date_gmt: '2015-05-08 09:39:53 +0000'
  content: "[&#8230;] &Uuml;ber 1,35 Milliarden Nutzer weltweit verzeichnet Facebook
    mittlerweile. Das bedeutet Unmengen an Traffic, der von dem sozialen Netzwerk
    bew&auml;ltigt werden muss &ndash; und der dazu gef&uuml;hrt hat, dass Facebook
    ein komplett neues Fundament f&uuml;r sein Netzwerk entwickeln musste. Seitdem
    ist HHVM jedoch nicht nur f&uuml;r Facebook eine M&ouml;glichkeit, PHP effizienter
    auszuf&uuml;hren, auch zahlreiche andere Online-Services setzen mittlerweile auf
    die Virtual Machine. Mit dem File-Sharing-Start-up Box und der WordPress-Hosting-Seite
    wp-engine gaben nun zwei weitere Dienste ihren Support von HHVM bekannt. [&#8230;]"
- id: 554075
  author: Pavel
  author_email: pndeschamps@gmail.com
  author_url: http://perfectasalud.org/
  date: '2015-07-21 17:18:57 +0000'
  date_gmt: '2015-07-22 00:18:57 +0000'
  content: "That's some great news for me as I'm planning to migrate from PHP-FPM
    architecture to HHVM + FastCGI. I have a Dedicated Server running WHM&#47;cPanel.
    I need precompiled packages of HHVM for Centos 6.6. \r\n\r\nWhat I'm going to
    do is download the Centos 6.6 (64bit) iso to make a compilation and thus create
    the RPM packages for the production (live) server."
---

Two big announcements back to back.

[Box announced](http://tech.blog.box.com/2014/11/box-on-hhvm/) that they did their cutover to HHVM yesterday seeing their latency drop by **3x**. I did a [Q & A about HHVM](https://tech.blog.box.com/2014/11/hhvm-q-and-a/) today.

<!--truncate-->

The wordpress hosting site [wp-engine announced](http://wpengine.com/2014/11/19/hhvm-project-mercury/) their support for HHVM today seeing a **5.6x** speedup on their bbPress app, and **3.9x** on their custom wordpress installs.

One of the main reasons I put so much time into HHVM is for these kinds of stories. I'm very proud of how far we've come and where we're going.

![](/static/images/posts/WPE-bbPress-hhvm.jpg)
