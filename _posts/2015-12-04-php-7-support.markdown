---
author: jwatzman
comments: true
layout: post
title: PHP 7 Support
category: blog
redirect_from:
  - /blog/10859/php-7-support
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
