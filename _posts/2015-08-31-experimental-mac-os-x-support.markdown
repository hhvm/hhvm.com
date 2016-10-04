---
author: jwatzman
layout: post
title: Experimental Mac OS X Support
category: blog
permalink: /blog/10043/experimental-mac-os-x-support
comments:
- id: 721331
  author: Christer Eckermann
  date: '2015-12-03 10:39:02 +0000'
  date_gmt: '2015-12-03 18:39:02 +0000'
  content: Currently we run HHVM on an Ubuntu VM on a Mac Mini server. Will be great
    to be able to skip the VM, so I'll be looking forward to hear more about the OS
    X progress for HHVM.
- id: 721337
  author: Josh Watzman
  date: '2015-12-03 10:42:22 +0000'
  date_gmt: '2015-12-03 18:42:22 +0000'
  content: Give it a shot now -- as far as we know, most things work. File issues
    on github for the stuff that doesn't -- that's the best way for us to figure out
    what's broken and what of that is important to people.
- id: 732353
  author: Rob Lewis
  date: '2015-12-13 10:59:46 +0000'
  date_gmt: '2015-12-13 18:59:46 +0000'
  content: Are there any special requirements for running HHVM on the Server version
    of Mac OS? This would seem to be a logical target platform.
- id: 733355
  author: Fred Emmott
  date: '2015-12-14 11:05:06 +0000'
  date_gmt: '2015-12-14 19:05:06 +0000'
  content: "As I understand it, OSX server is no longer a separate version, merely
    a collection of applications&#47;packages that gets installed on standard OSX
    from the App Store; I wouldn't expect there to be any special requirements.\r\n\r\nThat
    said, we've not tested it, and we still consider the OSX support to be experimental."
- id: 921695
  author: Hosting
  date: '2016-05-07 00:53:03 +0000'
  date_gmt: '2016-05-07 07:53:03 +0000'
  content: dumb question, wordpress can run on HHVM if the server support it, but
    all plug in developed for wordpress, too?
- id: 923699
  author: Josh Watzman
  date: '2016-05-09 03:48:06 +0000'
  date_gmt: '2016-05-09 10:48:06 +0000'
  content: It depends on the plug in and what PHP features it uses. HHVM strives for
    full PHP compatibility, so the vast majority are going to work without modification,
    and anything that doesn't work is considered a bug in HHVM. We are only tracking
    major frameworks, and there are far too many Wordpress plugins for us to track
    them all anyway. But do file an issue on GitHub if something doesn't work.
---

We're happy to announce official Mac OS X support in HHVM, with version 3.9! If you use [Homebrew](http://brew.sh/) and want to get started now, the steps to use our [official tap](https://github.com/hhvm/homebrew-hhvm) are really simple:

```bash
$ brew tap hhvm/hhvm
$ brew install hhvm
```

<!--truncate-->

If you don't use Homebrew or want to build HHVM yourself, [take a look at our wiki page for directions](https://github.com/facebook/hhvm/wiki/Building-and-installing-HHVM-on-OSX-10.10). Building HHVM is a very resource-intensive and slow process -- be prepared to devote a few gigabytes of RAM and a couple of hours to letting it compile. (The Homebrew formula doesn't have a bottle yet, so the same applies to whether you use Homebrew or not.)

Keep in mind that OS X support is still _experimental_ at this point. Most things seem to work -- it passes most of our test suite, and is able to run both a simple Drupal 7 and WordPress installation when I briefly tested it. However, it hasn't been extensively battle-tested! For example, there are a couple of failures in our own test suite when running on OS X. It's good enough to use for local development work, but I don't recommend a production deployment on anything but Linux quite yet. Information about supported Linux distributions is [available on our wiki](https://github.com/facebook/hhvm/wiki/Prebuilt%20Packages%20for%20HHVM).

Let us know how it goes! It's been a long road getting here, and inevitably some bumps in the road still ahead (for example, I'm pretty sure as of this writing master doesn't build on OS X and am working on fixing it). But OS X support is very important to us and to our community; we are committed to supporting it long-term. In particular, this means that we will make sure HHVM continues to improve on OS X in the future, so that later releases can be less and less experimental. Note that for the 3.9 LTS specifically, although we will continue to backport security patches into the branch, after the release of 3.10, users of the Homebrew formula will be upgraded to 3.10 and we won't provide the usual [LTS-specific packaging](https://github.com/facebook/hhvm/wiki/Long-term-support-%28LTS%29) for OS X. We don't anticipate this being a problem since no one should be using the 3.9 OS X release in production anyways, and you can always manually build out of the 3.9 branch if you really need to.

Finally, I'd be remiss without calling out a few key community contributors, without whose work this port would never have happened. A special thank you to:




  * [Daniel Sloof](https://github.com/facebook/hhvm/commits?author=danslo), who did most of the initial port to OS X.


  * [Jingyi Wei](https://github.com/facebook/hhvm/commits?author=wjywbs), who contributed many useful OS X fixes, including finally getting the JIT itself working.


  * All of the contributors to the various unofficial Homebrew HHVM packages, most especially [this one](https://github.com/mcuadros/homebrew-hhvm); although for various reasons we ended up building our own formula, the unofficial ones were enormously helpful to peek at.


As always, if you run into issues, please [file them on GitHub](https://github.com/facebook/hhvm/issues)!
