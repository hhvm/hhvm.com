---
author: paulbiss
layout: post
title: HHVM Lockdown
category: blog
permalink: /blog/9089/hhvm-lockdown
comments:
- id: 481445
  author: Wim Leers
  date: '2015-05-08 16:47:30 +0000'
  date_gmt: '2015-05-08 23:47:30 +0000'
  content: "Awesome, can't wait to see the results! :)\r\n\r\nIt'd be particularly
    interesting to see how much faster the upcoming version 8 of Drupal will be, since
    PHP 7 is significantly faster than HHVM there: http:&#47;&#47;lerdorf.com&#47;d8.html#&#47;drupalbench.\r\n\r\nFeel
    free to ping me if you have questions regarding Drupal 8 :)"
- id: 481793
  author: Ross
  date: '2015-05-09 01:05:25 +0000'
  date_gmt: '2015-05-09 08:05:25 +0000'
  content: "http:&#47;&#47;editingandwritingservices.com&#47;a-or-an-before-words-beginning-with-h&#47;\r\n\r\nSeen
    the mistake a few times in this blog! It's 'a HHVM'."
- id: 482135
  author: z88
  date: '2015-05-09 08:45:26 +0000'
  date_gmt: '2015-05-09 15:45:26 +0000'
  content: "I'm wondering, do any shared host support HHVM&#47;Hack? I can't find
    any. Is this something that shared hosts may do in future or would HHVM be a bad
    idea in shared environment?\r\n\r\nI love Hack, but I want my applications to
    reach masses, masses use shared hosting."
- id: 482405
  author: Paul Bissonnette
  date: '2015-05-09 12:05:46 +0000'
  date_gmt: '2015-05-09 19:05:46 +0000'
  content: Our benchmarking suite was setup with Drupal 7. I'll see about making sure
    we get some numbers for 8 as well. Thanks for the suggestion!
- id: 482417
  author: Paul Bissonnette
  date: '2015-05-09 12:07:47 +0000'
  date_gmt: '2015-05-09 19:07:47 +0000'
  content: "It's pronounced aitch-aitch-vee-em.\r\n\r\nhttp:&#47;&#47;blog.apastyle.org&#47;apastyle&#47;2012&#47;04&#47;using-a-or-an-with-acronyms-and-abbreviations.html"
- id: 482447
  author: Paul Bissonnette
  date: '2015-05-09 12:13:41 +0000'
  date_gmt: '2015-05-09 19:13:41 +0000'
  content: "I know that both WP Engine and Kinsta host wordpress sites using HHVM
    but I don't think Hack would be an option in those cases.\r\n\r\nHeroku currently
    hosts HHVM sites and you should be able to write Hack there, I may be missing
    others."
- id: 484493
  author: PHP Annotated Monthly &ndash; May 2015 | JetBrains PhpStorm Blog
  date: '2015-05-11 00:34:00 +0000'
  date_gmt: '2015-05-11 07:34:00 +0000'
  content: "[&#8230;] is available in the changelog. HHVM Open Source team is continuing
    a tradition of lockdowns&nbsp;announcing&nbsp;the&nbsp;first ever open source
    performance lockdown. They&nbsp;plan to focus their efforts on performance [&#8230;]"
- id: 485495
  author: Ewan Valentine
  date: '2015-05-11 12:46:14 +0000'
  date_gmt: '2015-05-11 19:46:14 +0000'
  content: Any news on Doctrine compatibility?
- id: 487241
  author: Josh Watzman
  date: '2015-05-12 15:23:16 +0000'
  date_gmt: '2015-05-12 22:23:16 +0000'
  content: "It's passing about 99% of its own unit tests on HHVM: http:&#47;&#47;www.hhvm.com&#47;frameworks&#47;\r\n\r\nMost
    of the remaining failures are minor issues that don't come up in real-world code,
    e.g., HHVM differing very slightly in the wording of error messages, things like
    that. If you're hitting a real issue, please file an issue on GitHub: https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;issues\r\n\r\nBut
    most things are expected to work nowadays. :)"
- id: 488249
  author: Spudley
  date: '2015-05-13 05:25:21 +0000'
  date_gmt: '2015-05-13 12:25:21 +0000'
  content: "Don't be a grammar nazi. Even the article you linked to closes on a pragmatic
    note:\r\n\r\n> No mat&shy;ter. Just do your best to be a good com&shy;mu&shy;ni&shy;ca&shy;tor
    and move on!"
- id: 488741
  author: Paul M
  date: '2015-05-13 10:16:44 +0000'
  date_gmt: '2015-05-13 17:16:44 +0000'
  content: "So wrt releases 3.8 will be the release to watch out for when it comes
    to a performance increase?\r\n\r\nThanks"
- id: 490049
  author: Danny van Kooten
  date: '2015-05-14 01:38:43 +0000'
  date_gmt: '2015-05-14 08:38:43 +0000'
  content: Awesome - I love this tradition. Have been running HHVM for about a year
    now, about time I start giving back. I'll be keeping an eye on the issue list!
    :)
- id: 490607
  author: Ewan Valentine
  date: '2015-05-14 10:08:20 +0000'
  date_gmt: '2015-05-14 17:08:20 +0000'
  content: Excellent, thanks for that! :)
- id: 517121
  author: Andr&eacute; R.
  date: '2015-06-08 06:08:22 +0000'
  date_gmt: '2015-06-08 13:08:22 +0000'
  content: Any news on this? or was it a Paul only lock down? *(given activity on
    issue tracker)* :)
- id: 517205
  author: Paul Bissonnette
  date: '2015-06-08 08:23:50 +0000'
  date_gmt: '2015-06-08 15:23:50 +0000'
  content: "Hi Andr&eacute;!\r\n\r\nI can assure you it was not a solo effort! We're
    putting together some detailed notes on what we worked on, how we did, and how
    things are looking overall. Thanks for your interest!"
---

![Neon Lockdown Sign](/static/images/posts/10537187_10152729686506660_886816697495269948_o-1.jpg)

It's that time of year again! Next week the HHVM Open Source team is beginning a lockdown. The next two weeks will feature beards, long hours, and performance wins. We're excited to announce that this will be our first ever open source performance lockdown.

<!--truncate-->

During lockdown we plan to focus our efforts on performance wins for Wordpress, Drupal, and MediaWiki. We're confident these gains will translate to many other popular frameworks. We will be tracking our efforts through [github issues](https://github.com/facebook/hhvm/labels/lockdown), and measuring performance using our [benchmarking tool](https://github.com/hhvm/oss-performance).

Throughout the next two weeks we will continue to review pull requests and respond to issues, and will be prioritizing those related to performance. In particular we're soliciting pull requests for any of our lockdown issues, as well as novel performance tasks we hadn't thought to add. We hope you'll join in and help us make this lockdown a success.

Performance lockdowns have been an HHVM tradition for many years, and we can't wait to get the rest of the community involved. In addition to optimizing HHVM performance we're also looking at ways we may be able to contribute back to these frameworks, and exploring the best practices for [configuring HHVM](http://hhvm.com/blog/4061/go-faster) to run each framework efficiently.
