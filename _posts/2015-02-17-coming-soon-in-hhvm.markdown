---
author: jwatzman
layout: post
title: Coming Soon in HHVM
category: blog
permalink: /blog/8405/coming-soon-in-hhvm
comments:
- id: 380381
  author: Casey
  date: '2015-02-17 14:10:35 +0000'
  date_gmt: '2015-02-17 22:10:35 +0000'
  content: You guys are killing it. Thanks for all your work!
- id: 380387
  author: Elliot
  date: '2015-02-17 14:17:23 +0000'
  date_gmt: '2015-02-17 22:17:23 +0000'
  content: These is a really exciting change-set. I'm desperate to get my hands on
    all of these things already!
- id: 380399
  author: Anatoly
  date: '2015-02-17 14:24:31 +0000'
  date_gmt: '2015-02-17 22:24:31 +0000'
  content: Oh, GC of cyclic references! Really looking forward for this!
- id: 380417
  author: John
  date: '2015-02-17 14:45:16 +0000'
  date_gmt: '2015-02-17 22:45:16 +0000'
  content: What about other rdbms, like PostgreSQL and&#47;or SQLite? Is support for
    them considered or the demand is too low?
- id: 380441
  author: Josh Watzman
  date: '2015-02-17 14:55:49 +0000'
  date_gmt: '2015-02-17 22:55:49 +0000'
  content: We haven't had significant demand for them, at least not to the level of
    MySQL. If you'd like to see it, feel free to file an issue on GitHub. I can't
    promise we'll be able to get to it soon, but it will definitely be good to have
    a place to track demand. (And if you, or someone else, wants to build support
    for us, we'd be happy to discuss there about what a good PR would look like! Definitely
    the way to ensure support gets added soonest.)
- id: 380447
  author: Dominic Watson
  date: '2015-02-17 15:21:35 +0000'
  date_gmt: '2015-02-17 23:21:35 +0000'
  content: Woo! As soon as OSX support hits, I'm jumping on board with this.
- id: 380513
  author: Paul M
  date: '2015-02-17 16:57:03 +0000'
  date_gmt: '2015-02-18 00:57:03 +0000'
  content: "Awesome news about async for mysql and memcached.\r\n\r\nWhat about using
    APC as a key&#47;value store?  I'm doing that right now.  Can async functionality
    be extended to that as well?\r\n\r\nThanks"
- id: 380525
  author: Josh Watzman
  date: '2015-02-17 17:01:50 +0000'
  date_gmt: '2015-02-18 01:01:50 +0000'
  content: My understanding is that APC is local to the PHP&#47;HHVM process, and
    never goes off-box, and so should always be very fast to access. If this isn't
    always the case, or you have some other use case for async APC, please file an
    issue on GitHub so we can track demand!
- id: 381185
  author: Kurre
  date: '2015-02-18 05:34:31 +0000'
  date_gmt: '2015-02-18 13:34:31 +0000'
  content: I've tried HHVM on my upcoming site and I must say that it is super fast!
    But I need support for MSSQL connection before I can launch my site, any chance
    that you are working on this? :)
- id: 381275
  author: Josh Watzman
  date: '2015-02-18 09:32:28 +0000'
  date_gmt: '2015-02-18 17:32:28 +0000'
  content: There's an issue open with some interest (https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;issues&#47;1579)
    but I'm not aware of anyone actively working on it, unfortunately.
- id: 381353
  author: Lukas
  date: '2015-02-18 12:43:06 +0000'
  date_gmt: '2015-02-18 20:43:06 +0000'
  content: both are important but SQLite is imho critical since its so huge to have
    a powerful DB right out of the box. Many applications use this to enable quick
    setup of their example apps.
- id: 382307
  author: Scott Arciszewski
  date: '2015-02-19 08:47:23 +0000'
  date_gmt: '2015-02-19 16:47:23 +0000'
  content: "Are you going to implement some of the PHP7 changes in HHVM? \r\n\r\nIn
    particular, the migration of mcrypt from libmcrypt (which is abandonware) into
    a openssl shim, cache-timing-safe character encoding functions, an updated hash
    extension (adding: SHA-512&#47;256, SHA-3, BLAKE2b, etc.) are features I plan
    on committing to PHP 7 that HHVM users may benefit from too.\r\n\r\nIf you need
    me to manually submit these separately, just let me know."
- id: 382763
  author: Scott Arciszewski
  date: '2015-02-19 11:08:42 +0000'
  date_gmt: '2015-02-19 19:08:42 +0000'
  content: I'm very surprised there isn't already a lot of demand for PostgreSQL.
    :)
- id: 382823
  author: Josh Watzman
  date: '2015-02-19 11:37:09 +0000'
  date_gmt: '2015-02-19 19:37:09 +0000'
  content: "There's been some demand for a general postgres plugin. One is provided
    by a third-party (who we've worked closely with a few times), it's at https:&#47;&#47;github.com&#47;PocketRent&#47;hhvm-pgsql,
    and that has been more than good enough for most people. If you haven't seen it
    before, you should give it a try!\r\n\r\nThere hasn't been any demand yet for
    *async* versions of those functions, at least that I've seen."
- id: 382835
  author: Josh Watzman
  date: '2015-02-19 11:39:33 +0000'
  date_gmt: '2015-02-19 19:39:33 +0000'
  content: "Yep, we want to continue being compatible with PHP, and that includes
    the upcoming PHP7. I don't think we've started work on implementing any of the
    features yet, but we've definitely discussed how to go about several of them --
    and PHP7 is still far enough away that we have plenty of time.\r\n\r\nIf you want
    to contribute fixes for us, we'd love to take the PRs as well!"
- id: 385967
  author: Andris
  date: '2015-02-20 20:25:13 +0000'
  date_gmt: '2015-02-21 04:25:13 +0000'
  content: Async query support would come handy with PDO too.
- id: 386765
  author: episode 123 &#8211; fastclick, hhvm, node-io split | WebDevRadio
  date: '2015-02-21 09:42:15 +0000'
  date_gmt: '2015-02-21 17:42:15 +0000'
  content: "[&#8230;] &#8211; http:&#47;&#47;hhvm.com&#47;blog&#47;8405&#47;coming-soon-in-hhvm
    async mysql [&#8230;]"
- id: 390179
  author: episode 123 &ndash; fastclick, hhvm, node-io split | PHP Podcasts
  date: '2015-02-23 00:43:49 +0000'
  date_gmt: '2015-02-23 08:43:49 +0000'
  content: "[&#8230;] &#8211; http:&#47;&#47;hhvm.com&#47;blog&#47;8405&#47;coming-soon-in-hhvm
    async mysql [&#8230;]"
- id: 407621
  author: castarco
  date: '2015-03-10 17:12:57 +0000'
  date_gmt: '2015-03-11 00:12:57 +0000'
  content: "Automatically updated (via APT) a server with a wordpress blog and owncloud
    installed (from HHVM 3.5 to HHVM 3.6) and now the server only responds with HTTP
    404 error codes: \"404 File Not Found\" :( .\r\n\r\nAny idea to solve it? Thanks
    for yout time!"
- id: 407651
  author: Josh Watzman
  date: '2015-03-10 17:32:07 +0000'
  date_gmt: '2015-03-11 00:32:07 +0000'
  content: Can you please file a bug report at https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;issues,
    with as many details about your application, how it's configured, what else (if
    anything) you changed as part of the 3.6 upgrade, etc, as you know? Much easier
    to track bugs there than on our blog post :)
- id: 480827
  author: HHVM &ndash; die Roadmap f&uuml;r 2015 - entwickler.de
  date: '2015-05-08 02:41:33 +0000'
  date_gmt: '2015-05-08 09:41:33 +0000'
  content: "[&#8230;] Einen detaillierten &Uuml;berblick &uuml;ber alle neuen Features
    sowie weiterf&uuml;hrende Links f&uuml;r Early Adaptors findet man in der offiziellen
    Ank&uuml;ndigung. [&#8230;]"
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
