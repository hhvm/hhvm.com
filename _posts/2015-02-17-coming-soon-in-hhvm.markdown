---
author: jwatzman
comments: true
layout: post
title: Coming Soon in HHVM
category: blog
permalink: /blog/8405/coming-soon-in-hhvm
---

The next HHVM release, 3.6, is on the horizon. We expect it to be released [at the very end of February or in early March](https://github.com/facebook/hhvm/wiki/Release%20Schedule). It's going to be a big release. Not only will it be our second release with [long-term support](https://github.com/facebook/hhvm/wiki/Long-term-support-%28LTS%29), but it will contain several exciting new features -- and lay the groundwork for continued development later this year.

<!--truncate-->

**New features in 3.6:**


  * Long-awaited MySQL support for async functions in Hack! [Hack's async functions](http://docs.hhvm.com/manual/en/hack.async.php) allow an application to continue executing code while fetching data, which can dramatically reduce the time it spends waiting for IO. We blogged a few weeks ago about [async curl support](http://hhvm.com/blog/7091/async-cooperative-multitasking-for-hack), and with 3.6, MySQL will be usable with Hack's async functions as well. This support comes from a new MySQL client library from the [WebScaleSQL](http://webscalesql.org/) project; this is built-in to HHVM and will work with any recent MySQL server. Full documentation will be ready by the actual 3.6 release, but for early adopters, [here is the internal API header](https://github.com/facebook/hhvm/blob/master/hphp/runtime/ext/async_mysql/ext_async_mysql.php).

  * While we're at it, we added async support for memcache as well. Much of the code for this comes from the [mcrouter open-source project](https://github.com/facebook/mcrouter), though again it does not require mcrouter and will work with any recent memcache server. [Here's the internal API header](https://github.com/facebook/hhvm/blob/master/hphp/runtime/ext/mcrouter/ext_mcrouter.php) while we prepare documentation for this feature too for the 3.6 release.

  * A restructuring of the FastCGI server, which fixed several memory leaks and reliability issues, especially under very high load.

  * A multitude of other crash and memory leak fixes.

  * Native property handlers, an HHVM-internal feature for compatibility with existing PHP code. Previously, some PHP which used edge cases around `__set`/`__get` and sub-classing certain internal classes wouldn't work on HHVM. With the addition of native property handlers in 3.6, it will work without modification.

  * Speaking of compatibility, 3.6 contains many fixes to make HHVM [even more compatible with existing PHP code](http://www.hhvm.com/frameworks/). As always, HHVM strives to maintain full compatibility with PHP. If your existing code doesn't work on HHVM, please [file an issue on GitHub](https://github.com/facebook/hhvm/issues)!

  * Improved typechecking support for [XHP](http://docs.hhvm.com/manual/en/hack.xhp.php) in Hack.


**Update 2015-02-18:** if you can't wait for the 3.6 official release, the above features are now available in any [prebuilt nightly package](https://github.com/facebook/hhvm/wiki/Prebuilt%20Packages%20for%20HHVM) dated 2015-02-18 or later.

But what's coming out soon is only part of the story. The 3.6 release lays the groundwork for even more impressive components, which will let us continue making HHVM a highly performant, feature-rich PHP runtime.

**HHVM roadmap for 2015:**





  * Integration of [LLVM](http://llvm.org/) as a further optimization step to make the hottest code run even faster on HHVM.

  * Continued experiments with support for 64-bit ARM platforms to increase deployment options for HHVM.

  * Improvements to the garbage-collection scheme for HHVM. This will start with collecting cyclic references and move into experiments with a full mark-and-sweep garbage collector, built on top of a pluggable GC interface.

  * Other general memory usage improvements, including investigation into several longstanding memory and stability issues.

  * First-class OS X support.

  * Even tighter integration of the Hack typechecker with HHVM, leading to an even easier experience [getting started with and using Hack](http://docs.hhvm.com/manual/en/install.hack.bootstrapping.php).

  * Full support for all configuration options in INI files (most are already supported), killing the HHVM-specific HDF files.

  * Releasing the 100% Hack [XHP 2.0 library](https://github.com/facebook/xhp-lib).

  * Continued compatibility fixes to make even more existing PHP code work without modification on HHVM.


So 3.6 will be an exciting release, and 2015 is shaping up to be an exciting year! As always, contributions of any kind are extremely welcome -- whether they be questions, suggestions, bug reports, or code -- and will always be viewed constructively. Check out the links in the sidebar to the right to get involved!
