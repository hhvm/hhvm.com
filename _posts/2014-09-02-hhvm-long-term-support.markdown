---
author: ender
layout: post
title: HHVM Long Term Support
category: blog
permalink: /blog/6083/hhvm-long-term-support
comments:
- id: 231227
  author: Alex Bilbie
  author_email: hello@alexbilbie.com
  author_url: http://alexbilbie.com
  date: '2014-09-02 13:34:38 +0000'
  date_gmt: '2014-09-02 20:34:38 +0000'
  content: "This is great to read.\r\n\r\nWhat plans are there to improve the HHVM
    documentation? There is a lot of inconsistent or missing or out of date documentation
    across docs.hhvm.com and the Github wiki especially around server configuration."
- id: 231239
  author: Graham Campbell
  author_email: graham@mineuk.com
  author_url: https://github.com/GrahamCampbell
  date: '2014-09-02 13:45:03 +0000'
  date_gmt: '2014-09-02 20:45:03 +0000'
  content: Will there be nightly packages for the lts branches?
- id: 231245
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com
  date: '2014-09-02 14:19:37 +0000'
  date_gmt: '2014-09-02 21:19:37 +0000'
  content: "No concrete plans from us. Please open github issues and we'll tag them
    with documentation. \r\n\r\nThe docs are in github so send us PRs to fix any problems
    you see, and the wiki is, well, a wiki. So please edit it as you see fit. If you
    don't know how open an issue or ask us on IRC."
- id: 231251
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com
  date: '2014-09-02 14:20:43 +0000'
  date_gmt: '2014-09-02 21:20:43 +0000'
  content: I wasn't planning on it. I don't think diffs will live on the branch very
    long before a release is made as they will mostly be security fixes which shouldn't
    live in the open for long.
- id: 231593
  author: Christopher Pitt
  author_email: cgpitt@gmail.com
  author_url: ''
  date: '2014-09-02 22:19:08 +0000'
  date_gmt: '2014-09-03 05:19:08 +0000'
  content: '"Mac OS X installation is currently EXPERIMENTAL and UNSUPPORTED."'
- id: 231635
  author: HHVM 的 LTS | Gea-Suan Lin&#039;s BLOG
  author_email: ''
  author_url: http://blog.gslin.org/archives/2014/09/03/5026/hhvm-%e7%9a%84-lts/
  date: '2014-09-02 23:54:54 +0000'
  date_gmt: '2014-09-03 06:54:54 +0000'
  content: "[&#8230;] 相較於 Ubuntu 的五年 LTS (Long Term Support)，HHVM 的 LTS 只有 48 周：「HHVM
    Long Term Support」。 [&#8230;]"
- id: 231731
  author: Ender
  author_email: ender@fb.com
  author_url: ''
  date: '2014-09-03 02:22:57 +0000'
  date_gmt: '2014-09-03 09:22:57 +0000'
  content: As Paul said, the LTS are mostly designed to be released as point releases,
    similar to what a stable Linux kernel is nowadays.  With that in mind, it's likely
    to have maybe release candidates for the first releases if we have more stuff
    than can be comfortable, but otherwise it wouldn't make sense to have continuous
    builds on those.
- id: 231755
  author: Xandi Ostermeyr
  author_email: ao@codesprint.de
  author_url: http://www.codesprint.de
  date: '2014-09-03 02:49:38 +0000'
  date_gmt: '2014-09-03 09:49:38 +0000'
  content: "great to read. should make it significant easier, to setup a hhvm environment
    in a company.\r\nbut like alex said, it would be great if you could provide also
    \"versioned\" documentation for the LTS releases."
- id: 233099
  author: Ender
  author_email: ender@fb.com
  author_url: ''
  date: '2014-09-04 18:55:57 +0000'
  date_gmt: '2014-09-05 01:55:57 +0000'
  content: "Hum.  That is a very interesting point, thanks for bringing it up.  Do
    you think it makes more sense to have something by release, as e.g. MySQL (which
    I find particularly overkill for HHVM if you ask me) or adding version information
    to the documentation (similar to e.g. jQuery: https:&#47;&#47;api.jquery.com&#47;ajaxSuccess&#47;).\r\n\r\nI'd
    like to hear any arguments towards or against it."
- id: 233105
  author: Ender
  author_email: ender@fb.com
  author_url: ''
  date: '2014-09-04 18:57:34 +0000'
  date_gmt: '2014-09-05 01:57:34 +0000'
  content: What do you mean with your comment?  It would be great to hear a constructive
    explanation instead of a rant. :-)
- id: 235619
  author: 'Mission statement: the new Dashboard | the rabbit hole'
  author_email: ''
  author_url: http://blog.fortrabbit.com/mission-statement-the-new-dashboard/
  date: '2014-09-08 07:12:19 +0000'
  date_gmt: '2014-09-08 14:12:19 +0000'
  content: "[&#8230;] sooner.&nbsp;We love to see that HHVM is getting more stable
    and more predictable, for instance with longtime support&nbsp;and we are looking
    to make it available in away that it can be used in [&#8230;]"
- id: 237299
  author: Ender
  author_email: ender@fb.com
  author_url: ''
  date: '2014-09-10 14:29:35 +0000'
  date_gmt: '2014-09-10 21:29:35 +0000'
  content: Given that I got 0 comments, my decision is that we will go with the jQuery
    model from now on.  I'll spread the word around that we need to add version information
    to the documentation.
- id: 237869
  author: PHP News You May Have Missed - August, September 2014
  author_email: ''
  author_url: http://www.sitepoint.com/php-news-may-missed-august-september-2014/
  date: '2014-09-11 09:00:07 +0000'
  date_gmt: '2014-09-11 16:00:07 +0000'
  content: "[&#8230;] HHVM, which we&rsquo;ve covered to a certain degree before,
    has announced Long Term Support editions. This means you can now feel safer deploying
    your production code with HHVM, due to their &ldquo;promise&rdquo; of keeping
    said version alive for the foreseeable future. The skeptics in the PHP community
    who doubted the longevity of the project can now rest assured that their code
    will keep working, BC-safe, for at least another while. You can read more about
    this here. [&#8230;]"
- id: 241763
  author: PHP Annotated Monthly &#8211; September 2014 | JetBrains PhpStorm Blog
  author_email: ''
  author_url: http://blog.jetbrains.com/phpstorm/2014/09/php-annotated-monthly-september-2014/
  date: '2014-09-17 12:05:05 +0000'
  date_gmt: '2014-09-17 19:05:05 +0000'
  content: "[&#8230;] Did you know PHP is not the only PHP interpreter? Lukas Kawhe
    Smith looks at the &#8220;alternative PHP&#8217;s&#8221; and the future of PHP&nbsp;from
    a distance. Oh, and Facebook&#8217;s HHVM now comes with long-term support. [&#8230;]"
- id: 274439
  author: PHP News You May Have Missed &ndash; August, September 2014 | AndrewRout.com
  author_email: ''
  author_url: http://andrewrout.com/blog/2014/10/php-news-you-may-have-missed-august-september-2014/
  date: '2014-10-10 22:11:39 +0000'
  date_gmt: '2014-10-11 05:11:39 +0000'
  content: "[&#8230;] HHVM, which we&rsquo;ve covered to a certain degree before,
    has announced Long Term Support editions. This means you can now feel safer deploying
    your production code with HHVM, due to their &ldquo;promise&rdquo; of keeping
    said version alive for the foreseeable future. The skeptics in the PHP community
    who doubted the longevity of the project can now rest assured that their code
    will keep working, BC-safe, for at least another while. You can read more about
    this here. [&#8230;]"
- id: 321239
  author: Ubuntu HHVM Install &raquo; Jesses Web Development Portfolio and Web Development
    Blog by Jesse Cascio
  author_email: ''
  author_url: http://jessesnet.com/development-notes/2014/ubuntu-hhvm-install/
  date: '2014-12-20 23:37:52 +0000'
  date_gmt: '2014-12-21 07:37:52 +0000'
  content: "[&#8230;] viable option for large scale, memory intensive programming
    projects. Also with the announcement of HHVM long term support, Facebook has made
    it clear it will continue to work on and perfect its PHP JIT compiler. One thing
    [&#8230;]"
- id: 334595
  author: netroby
  author_email: hufeng1987@gmail.com
  author_url: http://www.netroby.com
  date: '2015-01-07 17:21:24 +0000'
  date_gmt: '2015-01-08 01:21:24 +0000'
  content: "Your lts not really lts , Ubuntu LTS will continue several years. \r\n\r\nYou
    just support for several month.\r\n\r\nIt's not really good for who want stable
    ."
- id: 344435
  author: Aftab Naveed
  author_email: aftabnaveed@gmail.com
  author_url: ''
  date: '2015-01-20 22:05:17 +0000'
  date_gmt: '2015-01-21 06:05:17 +0000'
  content: We are using hhvm 3.3 in our production, performance has been great so
    for, but the question is all the future version will carry compatibility of code
    ? or code adjustments might be required.
- id: 344753
  author: Fred Emmott
  author_email: fe@fb.com
  author_url: ''
  date: '2015-01-21 09:16:33 +0000'
  date_gmt: '2015-01-21 17:16:33 +0000'
  content: "Any future 3.3 release should be compatible with code that worked on 3.3.0
    and any other current 3.3 release.\r\n\r\nOutside of the same release series,
    we've generally been following what PHP5 does - this is usually deprecation warnings
    before something breaks.\r\n\r\nWe've not yet decided how we're going to handle
    the breaking changes in PHP7."
- id: 480773
  author: Facebook erweitert Support f&uuml;r HHVM - entwickler.de
  author_email: ''
  author_url: https://entwickler.de/online/php/facebook-erweitert-support-fuer-hhvm-139681.html
  date: '2015-05-08 02:37:24 +0000'
  date_gmt: '2015-05-08 09:37:24 +0000'
  content: "[&#8230;] direkt auf der Facebook-Site eingesetzt, als auch auf GitHub
    zur Verf&uuml;gung gestellt werden. Daher k&uuml;ndigt das HHVM-Team auf seinem
    Blog nun einen Long Term Support f&uuml;r Source-Releases an, der einen &Uuml;berblick
    &uuml;ber die anstehenden [&#8230;]"
- id: 522905
  author: harshit
  author_email: harshit2prakash.2010@rediffmail.com
  author_url: ''
  date: '2015-06-12 22:31:02 +0000'
  date_gmt: '2015-06-13 05:31:02 +0000'
  content: "great to see this...is HHVM now available on fedora?\r\nwould be great
    if it is."
- id: 729191
  author: dipen
  author_email: dipen.ec2010@gmail.com
  author_url: http://localhost
  date: '2015-12-10 06:35:53 +0000'
  date_gmt: '2015-12-10 14:35:53 +0000'
  content: HHVM latest or after 3.9 for centos 6 64bits please ?
- id: 729305
  author: Josh Watzman
  author_email: jwatzman@fb.com
  author_url: https://www.facebook.com/jwatzman
  date: '2015-12-10 09:48:20 +0000'
  date_gmt: '2015-12-10 17:48:20 +0000'
  content: 'We unfortunately only have the resources right now to maintain Debian
    and Ubuntu packages. There are community-contributed directions here, which may
    or may not work, and aren''t supported by the team: https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;wiki&#47;Building-and-installing-HHVM-on-CentOS-6.6'
- id: 729311
  author: Josh Watzman
  author_email: jwatzman@fb.com
  author_url: https://www.facebook.com/jwatzman
  date: '2015-12-10 09:48:47 +0000'
  date_gmt: '2015-12-10 17:48:47 +0000'
  content: 'We unfortunately only have the resources right now to maintain Debian
    and Ubuntu packages. There are community-contributed directions here, which may
    or may not work, and aren''t supported by the team: https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;wiki&#47;Building-and-installing-HHVM-on-Fedora-19-or-20'
---

HHVM is known for its very intense and quick development pace: currently we ship to GitHub the exact same code we use to run the Facebook site within minutes of every commit, and we release a full version every 8 weeks. That is great and at the same time scary if you are trying to build a business or infrastructure around it.

<!--truncate-->

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
