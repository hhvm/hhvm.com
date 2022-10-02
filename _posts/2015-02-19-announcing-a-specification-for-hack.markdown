---
author: joelm
layout: post
title: Announcing a Specification for Hack
category: blog
permalink: /blog/8537/announcing-a-specification-for-hack
comments:
- id: 382847
  author: Miles Johnson
  date: '2015-02-19 11:51:21 +0000'
  date_gmt: '2015-02-19 19:51:21 +0000'
  content: This is fantastic. Thanks a lot for all the hard work guys!
- id: 382925
  author: Paul M
  date: '2015-02-19 12:19:20 +0000'
  date_gmt: '2015-02-19 20:19:20 +0000'
  content: Yeah definitely.  You guys keep doing what you are doing :)
- id: 384329
  author: Clement Wong
  date: '2015-02-19 22:21:46 +0000'
  date_gmt: '2015-02-20 06:21:46 +0000'
  content: Why is Hack not subnet of PHP like asm.js of JS?
- id: 384905
  author: Fred
  date: '2015-02-20 05:22:28 +0000'
  date_gmt: '2015-02-20 13:22:28 +0000'
  content: Amazing, this will help to spread Hack even more and it deserves it. Hack
    is already so much better than PHP!
- id: 385001
  author: Joel Marcey
  date: '2015-02-20 08:22:49 +0000'
  date_gmt: '2015-02-20 16:22:49 +0000'
  content: Hack is neither a subset or a superset of PHP. You can view it as a dialect
    of PHP, with roots from the language but with added features (and some features
    removed).
- id: 385643
  author: 'Links 20&#47;2&#47;2015: Android Studio v1.1, GDB 7.9 | Techrights'
  date: '2015-02-20 17:25:52 +0000'
  date_gmt: '2015-02-21 01:25:52 +0000'
  content: "[&#8230;] Announcing a Specification for Hack [&#8230;]"
- id: 394553
  author: Clement Wong
  date: '2015-02-25 10:40:15 +0000'
  date_gmt: '2015-02-25 18:40:15 +0000'
  content: "Hi Joel,\r\n\r\nBut couldn't it be made as a subnet from the beginning
    like what Mozilla did to asm.js?\r\n(assuming the main reason of creating hack-lang
    is to avoid type checking as far as I understood?)"
- id: 395057
  author: Joel Marcey
  date: '2015-02-25 20:02:26 +0000'
  date_gmt: '2015-02-26 04:02:26 +0000'
  content: "Hi Clement,\n\nAre you asking whether Hack can be a subnet as in domain
    subnet? Like hack.php.com or something? Or are you asking if Hack can be made
    a subset of PHP? If the former, Hack and PHP are two different projects. They
    are worked on by different teams. If subset, then I explained that below as Hack
    is not really a strict subset of PHP. It is both a subset and superset in ways
    --- i.e., we call it a dialect. \n\nAnd a main reason we created Hack was not
    to avoid type-checking, but to enable quick, reliable type checking. :)"
- id: 407015
  author: PHP Annotated Monthly &ndash; March 2015 | JetBrains PhpStorm Blog
  date: '2015-03-10 04:00:43 +0000'
  date_gmt: '2015-03-10 11:00:43 +0000'
  content: "[&#8230;] talk about Hack and HHVM: the first one got a new initial specification,
    as well as PHP&nbsp;a few months ago. Hack developers produced a specification
    for the language [&#8230;]"
---

![Hack Logo](/static/images/posts/Screenshot-2015-02-18-10.07.47.png){:loading="lazy"}

Today we are excited to announce the availability of the [initial specification for the Hack programming language](https://github.com/hhvm/hack-langspec/blob/master/spec/00-specification-for-hack.md).

<!--truncate-->

When we [announced Hack](http://hhvm.com/blog/4223/introducing-hack-a-programming-language-for-hhvm), we were very excited for the community to get their hands on a programming language that has helped Facebook engineers become more productive in their day-to-day development and became, alongside PHP, the language used when developing applications running on [HHVM](http://hhvm.com). At the time of release, we had [documentation](http://docs.hhvm.com) geared for the programmer using Hack to develop applications. However, we did not have official documentation for those that might want to create a Hack implementation of their own or something like a Hack conformance test-suite. This [specification](https://github.com/hhvm/hack-langspec/blob/master/spec/00-specification-for-hack.md) fills that gap. It is _the_ document for the Hack implementer, and an excellent supplemental document for the Hack user.

Hack's roots are from PHP. Last year, we announced the [development of a specification for PHP](http://hhvm.com/blog/5723/announcing-a-specification-for-php). The fine folks at the [PHP Project](http://php.net/credits.php) have since taken over control of that specification and have shepherded it on [GitHub](https://github.com/php/php-langspec) to the tune of hundreds of commits, over 100 pull requests and many general improvements. It was very important, and extremely helpful, that we had a PHP specification when creating the Hack specification. You will see many similarities between the two specifications, along with many new [fea](https://github.com/hhvm/hack-langspec/blob/master/spec/05-types.md#types)[tur](https://github.com/hhvm/hack-langspec/blob/master/spec/14-generic-types-methods-and-functions.md)[es](https://github.com/hhvm/hack-langspec/blob/master/spec/21-attributes.md) and [differences](https://github.com/hhvm/hack-langspec/blob/master/spec/23-differences-from-php.md).

We are hosting the new Hack specification on GitHub. We are eager for you to [explore the specification](https://github.com/hhvm/hack-langspec), provide us [feedback](https://github.com/hhvm/hack-langspec/issues) and [pull requests](https://github.com/hhvm/hack-langspec/pulls). Given that Hack is still a relatively new language, we will continue to evolve the specification with new features. We encourage you to ping us with comments on direction, possible feature requests, etc -- check out the links in the sidebar to the right to see how to get involved.

Special thanks must be given to [Rex Jaeschke](https://github.com/RexJaeschke), who, as with the PHP specification, led the actual writing. In addition, [Julien Verlaguet](https://github.com/pikatchu), [Josh Watzman](https://github.com/jwatzman), [Eugene Letuchy](https://github.com/elgenie), [Fred Emmott](https://github.com/fredemmott), [Sara Golemon](https://github.com/sgolemon), and [Drew Paroski](https://github.com/paroski) helped ensure the specification's accuracy. And, of course, sincere thanks to the community that has used Hack since its inception, providing invaluable input and feedback.

[Enjoy](https://github.com/hhvm/hack-langspec/blob/master/spec/00-specification-for-hack.md)!
