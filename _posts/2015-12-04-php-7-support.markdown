---
author: jwatzman
layout: post
title: PHP 7 Support
category: blog
permalink: /blog/10859/php-7-support
comments:
- id: 724343
  author: milliondollarserver
  author_email: lugh@live.ca
  author_url: http://milliondollarserver.com
  date: '2015-12-05 19:05:50 +0000'
  date_gmt: '2015-12-06 03:05:50 +0000'
  content: This is exciting! Looking forward to see how nightly works.
- id: 724823
  author: najbolji hosting
  author_email: info@sceko.com
  author_url: http://www.oklop.me/
  date: '2015-12-06 08:09:49 +0000'
  date_gmt: '2015-12-06 16:09:49 +0000'
  content: nice, php 7 is amazing
- id: 728957
  author: Danny van Kooten
  author_email: danny@ibericode.com
  author_url: http://dvk.co/
  date: '2015-12-09 23:46:43 +0000'
  date_gmt: '2015-12-10 07:46:43 +0000'
  content: Neat, still happily running HHVM with no intention to switch to PHP7 anytime
    soon. To hear that you'll be supporting all PHP7 features is reassuring! :)
- id: 748991
  author: PHP7 atau HHVM ? | KMKLabs Blog
  author_email: ''
  author_url: http://blog.kmklabs.com/2015/12/05/php7-atau-hhvm/
  date: '2016-01-03 23:25:21 +0000'
  date_gmt: '2016-01-04 07:25:21 +0000'
  content: "[&#8230;] Josh Watzman dari Facebook ada mengeluarkan blog post&nbsp;bahawa
    release HHVM 3.11 akan dimundurkan untuk &nbsp;memastikan &nbsp;semua fitur baru
    yang ada di PHP7 [&#8230;]"
- id: 767711
  author: Orhaan
  author_email: orhanfirik@gmail.com
  author_url: http://eksisozluk.com
  date: '2016-01-19 12:13:52 +0000'
  date_gmt: '2016-01-19 20:13:52 +0000'
  content: Well done we're very excited about that :)
- id: 849569
  author: Elian
  author_email: eli.asraf@gmail.com
  author_url: http://www.webxfactor.com
  date: '2016-03-28 06:55:07 +0000'
  date_gmt: '2016-03-28 13:55:07 +0000'
  content: i have a question guys is there any compatibility problems with the php
    7 versions? i have applications running the 5.5 and if i start working on the
    7 might be any issues on files i add on ?
- id: 852785
  author: Joel Marcey
  author_email: joelm@fb.com
  author_url: ''
  date: '2016-03-29 11:46:22 +0000'
  date_gmt: '2016-03-29 18:46:22 +0000'
  content: "Elian, what type of compatibility problems are you referring to? With
    HHVM's PHP 7 support, you currently have to opt-in for any of the breaking changes
    that might occur. So, if you use new features, you can use those without opting
    in and we attempted to be as  compatible with PHP 7 as possible.\r\n\r\nAre you
    running into anything in particular?"
---

For those that haven't been following along, the next version of the PHP language, version 7.0.0, [was very recently released](http://php.net/archive/2015.php#id2015-12-03-1). Those of us working on HHVM offer our congratulations to all the contributors to this latest release! We're all really excited to see this release come out the door, and for what it means for the future of PHP.

<!--truncate-->

The release has implications for HHVM as well. PHP 7 contains [many new and exciting language features](http://php.net/manual/en/migration70.new-features.php), such as [anonymous classes](http://php.net/manual/en/language.oop5.anonymous.php) and [generator delegation](http://php.net/manual/en/language.generators.syntax.php#control-structures.yield.from). The HHVM project is committed to continuing to support the evolving PHP language, and as such we are proud to announce that the current [nightly releases](http://docs.hhvm.com/hhvm/installation/linux#other-packages) have support for all major PHP 7 features, and the [upcoming 3.11.0 stable release](https://github.com/facebook/hhvm/wiki/Release%20Schedule) will be the first release of HHVM with support for the major PHP 7 features.

A small number of the changes in PHP 7 are [not backwards compatible](http://php.net/manual/en/migration70.incompatible.php), and we don't want to leave behind our many users relying on our solid PHP 5 support and who may, for good reason, not want to upgrade immediately. Therefore, HHVM will continue to simultaneously support PHP 5 and PHP 7 for the foreseeable future. This is the way the simultaneous support works:




  * Features that pose no compatibility issues are just always available. For example, anonymous classes require no special configuration to use — they work by default.


  * Similarly, features which were removed in PHP 7, such as [alternative open tags](https://wiki.php.net/rfc/remove_alternative_php_tags), will just continue to work in HHVM for the foreseeable future.


  * The INI option `hhvm.php7.all = 1` enables the PHP 7 behavior for backwards-incompatible changes. (PHP 5 behavior will remain the default still for a while.) Each major compatibility break has its own option, if you want to turn them on one by one. See [our INI documentation](http://docs.hhvm.com/hhvm/configuration/INI-settings#php-7-settings) for details.


The language features of PHP 7.0 are of course just the start. As PHP 7.1 and onward develop, we will keep adding the new PHP features into HHVM, to continue having parity with the language.

Please give the nightly builds a try and [let us know about any issues](https://github.com/facebook/hhvm/issues) so we can fix them before the 3.11.0 release! All the major features are working and pass PHP 7's own test suites, but there are certain to be edge cases and minor features we're missing. We want to make sure that 3.11.0 is as solid a release as possible for our new PHP 7 support!
