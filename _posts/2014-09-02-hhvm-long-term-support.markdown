---
author: ender
comments: true
layout: post
title: HHVM Long Term Support
category: blog
redirect_from:
  - /blog/6083/hhvm-long-term-support
---

HHVM is known for its very intense and quick development pace: currently we ship to GitHub the exact same code we use to run the Facebook site within minutes of every commit, and we release a full version every 8 weeks. That is great and at the same time scary if you are trying to build a business or infrastructure around it.

The HHVM team at Facebook understands that in order to reach every corner of the PHP landscape our users need to have some sort of commitment, in order to plan their deployments accordingly and to know how upstream will react to security and stability fixes in already released versions, for example.


## The deal


For these and other reasons, starting with HHVM 3.3, the HHVM team will support two source releases at all times (that we will call LTS, Long-Term Support), separated by roughly 6 months (24 weeks apart to be exact), to have an effective support cycle of nearly a year. As an example, HHVM 3.3, which is scheduled for 11th Sept 2014, will be supported until 3.9 is released (8x6=48 weeks later, about 11 months). Accordingly, 3.6 (hopefully released 24 weeks after 3.3) will be supported for 6 releases (until 3.12 or equivalent sees the light). Confused? Let's try a table!


Version name | Intended Release Date | LTS? | End of support
------------ | --------------------- | ---- | --------------
**3.3** | **11 Sep 2014** | **yes** | **13 Aug 2015**
3.4* | 6 Nov 2014 | no |
3.5* | 1 Jan 2015 | no |
**3.6*** | **26 Feb 2015** | **yes** | **28 Jan 2016**
3.7* | 23 Apr 2015 | no |
3.8* | 18 Jun 2015 | no |
**3.9*** | **13 Aug 2015**	| **yes** | **14 Jul 2016**
3.10* | 8 Oct 2015 | no |
3.11* | 3 Dec 2015 | no |
**3.12*** | **28 Jan 2016** | **yes** | **29 Dec 2016**
3.13* | 24 Mar 2016 | no |
3.14* | 19 May 2016 | no |
**3.15** | **14 Jul 2016** | **yes** | **15 Jun 2017**

<center><i>* Release names uncertain, but you get the idea.</i></center>


## What about official distribution packages?


Additionally to the above, we are pushing really hard to get official Debian packages into the main archive, which would make their way into Debian stable, Ubuntu semiannual releases, as well as any Debian derivatives. We are aware of the long support cycles of those distributions and we intend to support whichever version is released with Debian and Ubuntu stable versions for security-related fixes for as long as that version is supported in Debian/Ubuntu.

We are trying to come up with plans for other distributions like Fedora, but our resources are limited for now and while we will keep releasing packages for many distributions, we may not cover them with LTS.  This doesn't mean that we are not going to have the usual RPMs or DEBs for various distros in every release, but they will not be residing in official repos.


## What type of updates I may expect in LTS releases?


This can easily be a hot topic for the community and at the same time become a burden for the team, so let's be clear. The answer is _it depends_.

It depends on the severity of the problem we want to fix and intrusiveness of the patch to apply. Security issues? _Absolutely!_ Big regressions? _Sure, why not, if they don't imply re-architecting a big chunk of code._ Small patches that can drive that version to 100% completeness on some framework? _Let's do it._ But observe that the longer an LTS release is out there, the less likely we will be doing major surgery on it. Security fixes will have absolute priority, and the rest of issues will need to be studied by balancing the amount of work patching and testing vs. the benefit and the risk of getting it out of the door. We expect you, the users, to guide us with PRs or features that you would like to have in the current LTS releases.

We are finalizing the plan and we may need to make adjustments to it. Do you have any questions or suggestions? Please comment!

_Ender works in Facebook as Security Engineer and has a passion for packaging. He's been a Debian Developer since 2001._
