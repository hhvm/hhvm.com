---
author: ptarjan
layout: post
title: HHVM on Heroku
category: blog
permalink: /blog/1379/hhvm-on-heroku
comments:
- id: 1205
  author: Dennis
  author_email: magnusbizus@gmail.com
  author_url: ''
  date: '2013-10-30 12:28:40 +0000'
  date_gmt: '2013-10-30 19:28:40 +0000'
  content: Do you have plans for HHVM on OpenShift?
- id: 1211
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com/
  date: '2013-10-30 13:03:19 +0000'
  date_gmt: '2013-10-30 20:03:19 +0000'
  content: I haven't used OpenShift before, but if get it working there, please let
    us know.
- id: 1217
  author: Dean Herbert
  author_email: pe@ppy.sh
  author_url: ''
  date: '2013-11-25 01:17:14 +0000'
  date_gmt: '2013-11-25 09:17:14 +0000'
  content: I'm always curious when reading the performance comparisons to base php
    &ndash; are you using a bytecode compiler like OpCache in 5.5 for these comparisons?
    That makes a huge difference.
- id: 1223
  author: Jared Kip
  author_email: jared@jaredkipe.com
  author_url: http://jaredkipe.com
  date: '2013-12-04 18:19:58 +0000'
  date_gmt: '2013-12-05 02:19:58 +0000'
  content: |-
    You guys have done really good work on this project.
    I found a pretty big parity issue in the magic method abilities (vs Zend anyway).
    http:&#47;&#47;jaredkipe.com&#47;blog&#47;website-development&#47;silverstripe-on-hhvm-part-two&#47;
- id: 1229
  author: Дайджест интересных новостей и материалов из мира PHP (20 октября &mdash;
    10 ноября 2013) | Juds
  author_email: ''
  author_url: http://www.juds.com.ua/php-digest24/
  date: '2013-12-15 01:02:49 +0000'
  date_gmt: '2013-12-15 09:02:49 +0000'
  content: "[&#8230;] HHVM на Heroku&nbsp;&mdash; Использование HHVM теперь возможно
    на популярной облачной платформе Heroku. [&#8230;]"
- id: 9527
  author: HHVM vs Zend | Feng&#039;s Blog
  author_email: ''
  author_url: http://f-xj.org/?p=143
  date: '2014-03-31 18:53:26 +0000'
  date_gmt: '2014-04-01 01:53:26 +0000'
  content: "[&#8230;] flexibility that PHP provides. HHVM runs much of the world&rsquo;s&nbsp;existing
    PHP.&nbsp;Developers&nbsp;and&nbsp;hosts&nbsp;are adopting HHVM.&nbsp;We are aware
    of&nbsp;minor incompatibilities (please&nbsp;open issues&nbsp;when you find [&#8230;]"
- id: 183839
  author: Teng
  author_email: tengyifei88@gmail.com
  author_url: http://www.thinkingandcomputing.com/
  date: '2014-06-26 09:11:27 +0000'
  date_gmt: '2014-06-26 16:11:27 +0000'
  content: 'I made a OpenShift cartridge consisting of HHVM in FastCGI mode and Nginx.
    Please kindly take a look at it: https:&#47;&#47;github.com&#47;tengyifei&#47;openshift-cartridge-nginx-hhvm'
---

Do you use [heroku](http://heroku.com) to host your PHP app and want to save 2x-10x dynos? Or serve user requests 2x-10x faster? I'm happy to announce that you can now use HHVM on heroku. You should clone your app and try it out before pushing to production as HHVM doesn't support [every possible use of PHP](http://www.hhvm.com/blog/875/wow-hhvm-is-fast-too-bad-it-doesnt-run-my-code) (yet).

<!--truncate-->

To use it with a new app:


    heroku create --buildpack https://github.com/hhvm/heroku-buildpack-hhvm


Or to convert your existing PHP app (once you tested it works on HHVM):


    heroku config:set BUILDPACK_URL=https://github.com/hhvm/heroku-buildpack-hhvm
    <make some git change and commit it>
    git push


The hardest part of this whole endeavor was getting HHVM to compile on [Ubuntu 10.04](https://github.com/facebook/hhvm/wiki/Building-and-installing-on-Ubuntu-10.04-LTS), but once that worked it was smooth sailing. If you want to dive into the nitty gritty details you can [read the source](https://github.com/hhvm/heroku-buildpack-hhvm).

A huge thanks to [@pvh](https://twitter.com/pvh) for hosting us at heroku and hacking on this for a day. And to[ Claudiu Ceia](https://www.facebook.com/wtf.no.username) for writing the .hdf linter and all his work throughout this project.

If you have any issues with the heroku part, open issues on the [heroku buildpack issue tracker](https://github.com/hhvm/heroku-buildpack-hhvm/issues) and if you have any issues with HHVM running your code open issues on the [HHVM issue tracker.](https://github.com/facebook/hhvm/issues) And if you can make this integration better in any way, please fork and send pull requests.
