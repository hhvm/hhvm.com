---
author: julienv
layout: post
title: Introducing Hack - A Programming Language for HHVM
category: blog
permalink: /blog/4223/introducing-hack-a-programming-language-for-hhvm
comments:
- id: 3101
  author: James Pearce
  author_email: jpearce@fb.com
  author_url: ''
  date: '2014-03-20 14:34:46 +0000'
  date_gmt: '2014-03-20 21:34:46 +0000'
  content: This is very exciting. Congratulations to all involved.
- id: 3107
  author: Facebook&#8217;s Hack for PHP | Coding Aloud
  author_email: ''
  author_url: http://coding.simon.geek.nz/2014/03/21/facebooks-hack-for-php/
  date: '2014-03-20 14:56:33 +0000'
  date_gmt: '2014-03-20 21:56:33 +0000'
  content: "[&#8230;] has just released the Hack documentation and tools that we have
    been using on some projects and our Hack-specific [&#8230;]"
- id: 3149
  author: Tarwin Stroh-Spijer
  author_email: tarwin@gmail.com
  author_url: http://blog.touchmypixel.com/
  date: '2014-03-20 16:57:58 +0000'
  date_gmt: '2014-03-20 23:57:58 +0000'
  content: "First, congratulations!\r\n\r\nIs there a performance difference between
    using pure PHP and Hack? I'm wondering if it is worth making Hack a Haxe target?
    [now that is confusing]"
- id: 3443
  author: patlecat
  author_email: seppli@gmx.li
  author_url: ''
  date: '2014-03-21 06:15:46 +0000'
  date_gmt: '2014-03-21 13:15:46 +0000'
  content: Can you please support openSUSE? I need it with Yii-Framework. Windows
    would be nice too for development (with XAMPP).
- id: 3503
  author: Omar Jackman
  author_email: hhvm@omarjackman.com
  author_url: http://omarjackman.com
  date: '2014-03-21 08:20:43 +0000'
  date_gmt: '2014-03-21 15:20:43 +0000'
  content: "I think this is very cool but why did you choose this syntax versus the
    java style approach of: \r\n\r\npublic string function foo(){\r\n    return 'Some
    String';\r\n}\r\n\r\nI'm not saying it's wrong, bad or anything else negative
    I'm just wondering what swayed you in this irreversible direction versus another."
- id: 3521
  author: Marco Pivetta
  author_email: ocramius@gmail.com
  author_url: http://ocramius.github.io/
  date: '2014-03-21 10:03:40 +0000'
  date_gmt: '2014-03-21 17:03:40 +0000'
  content: "Probably the most expected feature from the HHVM team :-)\r\n\r\nI'm waiting
    for integration with my favorite IDE, but will indeed start experimenting with
    HACK in the next days. Awesome, thanks!"
- id: 3605
  author: Julien Verlaguet
  author_email: julien.verlaguet@fb.com
  author_url: ''
  date: '2014-03-21 14:56:40 +0000'
  date_gmt: '2014-03-21 21:56:40 +0000'
  content: "Omar:\r\n\r\nThere was multiple options, let's review them.\r\nint function
    foo() ...\r\n\r\nThis option would have been consistent with the C tradition.
    The problem is that we have closures too, and it would have been very hard to
    make the type annotation fit in that particular place for closures.\r\n\r\nWhen
    one writes:\r\n$x = int function( ...\r\nThat's difficult to parse, especially
    if the type can be something complex like Vector etc ...\r\nWe knew that we wanted
    to expand the type-system, add new types and that each time, adapting the parser
    for closures would be painful. So we decided not to put them there.\r\n\r\nSecond
    option: function int foo(...)\r\nInternally, we have many people and tools \"grepping\"
    for functions, the way they do that is by typing: grep \"function foo\".\r\nIt
    would not have been the end of the world to put it there, but it would have been
    somewhat painful.\r\n\r\nThat's why we put the type annotation last. I hope this
    answers your question."
- id: 4031
  author: Isaac
  author_email: isaac.z.foster@gmail.com
  author_url: ''
  date: '2014-03-22 15:01:20 +0000'
  date_gmt: '2014-03-22 22:01:20 +0000'
  content: Do you have any plugins for Eclipse or other IDEs that provide the hh_client's
    feedback inline with your code?
- id: 4217
  author: Radu
  author_email: sobolanx@gmail.com
  author_url: ''
  date: '2014-03-23 01:59:21 +0000'
  date_gmt: '2014-03-23 08:59:21 +0000'
  content: "Hey guys, small issue: your blog's RSS feed URL (http:&#47;&#47;hhvm.com&#47;blog&#47;feed&#47;)
    doesn't work anymore.\r\n\r\nWas it changed to something else ? If yes, where
    can I find it ?\r\n\r\nThanks."
- id: 4895
  author: Adrian Budau
  author_email: budau.adi@gmail.com
  author_url: ''
  date: '2014-03-24 14:30:47 +0000'
  date_gmt: '2014-03-24 21:30:47 +0000'
  content: "Is there support for hack with libphutil? I suspect not considering I
    ahven't seen any big updates to the XHPAST parser.\r\n\r\nSo if not, will there
    be added in the future?\r\n\r\nThanks :-)"
- id: 4943
  author: Paul Tarjan
  author_email: pt@fb.com
  author_url: http://paultarjan.com
  date: '2014-03-24 18:53:44 +0000'
  date_gmt: '2014-03-25 01:53:44 +0000'
  content: Open a bug against them.
- id: 5519
  author: Paul
  author_email: paul.sijpkes@gmail.com
  author_url: ''
  date: '2014-03-25 20:28:20 +0000'
  date_gmt: '2014-03-26 03:28:20 +0000'
  content: I second this, a plugin for Eclipse would be gold, otherwise I might stick
    with PHP
- id: 8549
  author: 'Facebook Unveils New Programming Language: Hack | 3BSG Network'
  author_email: ''
  author_url: http://3bsg.wordpress.com/2014/03/31/facebook-unveils-new-programming-language-hack/
  date: '2014-03-31 05:58:16 +0000'
  date_gmt: '2014-03-31 12:58:16 +0000'
  content: "[&#8230;] is faster, as it uses a just-in-time compilation approach. Details
    are offered in a post on the HHVM blog. Read more at [&#8230;]"
- id: 70031
  author: Ap&eacute;ro PHP &#8211; mardi 27 mai &agrave; 19h | AFUP Lyon
  author_email: ''
  author_url: http://lyon.afup.org/2014/05/06/apero-php-mardi-27-mai-a-19h/
  date: '2014-05-06 02:26:33 +0000'
  date_gmt: '2014-05-06 09:26:33 +0000'
  content: "[&#8230;] d&eacute;but de soir&eacute;e, &nbsp;Pascal Martin&nbsp;nous
    parlera d&rsquo;HHVM et de Hack. Il nous fera un petit historique d&rsquo;HHVM,
    puis indiquera la fa&ccedil;on de l&rsquo;installer et de [&#8230;]"
- id: 177785
  author: Joseph Rex
  author_email: joerex@ostrich-dev.com
  author_url: http://josephrex.me
  date: '2014-06-12 15:15:25 +0000'
  date_gmt: '2014-06-12 22:15:25 +0000'
  content: I find this really interesting as you guys at Facebook are making great
    contributions to the open source community
- id: 201287
  author: Amachree
  author_email: emiglobetrotting@yahoo.co.uk
  author_url: ''
  date: '2014-07-31 06:51:25 +0000'
  date_gmt: '2014-07-31 13:51:25 +0000'
  content: I don't like the semantic of this language
- id: 232253
  author: Bart Schouten
  author_email: forum@xenhideout.nl
  author_url: http://www.xenhideout.nl
  date: '2014-09-03 16:39:41 +0000'
  date_gmt: '2014-09-03 23:39:41 +0000'
  content: "\"Hack\" is not a new programming language. It is an annotation-based
    type-checking and type-tracking system on top of PHP that has no runtime implications
    save for the collection classes being added. No matter how much it integrates
    with PHP syntax, and no matter how much weird stuff it introduces (Nullable types?
    Really?) there are no changes to the runtime of PHP and these features (like the
    Nullables) just serve to confuse any programmer who no longer can intuit what
    his code is REALLY doing.\r\n\r\nAnd the problem is not the type-checking. It
    is not even the hideous generics (like in Java). It is not even the Nullables.
    It is the fact that the presentation of these features is done in a way that makes
    people believe (or tries to confuse them into believing) that these are really
    additions to the PHP language when they are not.\r\n\r\nAnd this also has implications
    (much like in Java) for the way these syntaxes are developed and chosen. The syntax
    itself can serve to confuse people into believing that we are talking about core
    language features.\r\n\r\nAnd it is just a type-tracking type-checking warning-generating
    system. Nothing more. I haven't checked all of the features thoroughly (like Shapes)
    but all of it seems parse-time and most of it seems incongruent and ill-designed
    because of the initial, basic, erroneous decision to treat it as a \"language\"
    instead of as an \"annotation system\" for that language (which is PHP)."
- id: 242261
  author: The king
  author_email: eliehashesho@gmail.com
  author_url: http://www.alotbooks.com
  date: '2014-09-18 09:59:14 +0000'
  date_gmt: '2014-09-18 16:59:14 +0000'
  content: "Probably the most expected feature from the HHVM team :-)\r\n\r\nI&rsquo;m
    waiting for integration with my favorite IDE, but will indeed start experimenting
    with HACK in the next days. Awesome, thanks!"
- id: 301373
  author: zaxebo1
  author_email: zaxebo1@gmail.com
  author_url: ''
  date: '2014-11-20 17:01:29 +0000'
  date_gmt: '2014-11-21 01:01:29 +0000'
  content: "excellent work.\r\n\r\nfeedback:\r\n1) there is no mention of \"wordpress\"
    software compaitibility percentage on the page http:&#47;&#47;hhvm.com&#47;frameworks&#47;\r\n\r\n2)
    please make \"acquia Drupal\" and \"wordpress\" HUNDRED PERCENT compatible As
    soon as possible. That will give us a solid confidence in the platform too."
- id: 436367
  author: Announcing a Specification for Hack - IT Sprite
  author_email: ''
  author_url: http://www.itsprite.com/announcing-a-specification-for-hack/
  date: '2015-04-01 08:45:35 +0000'
  date_gmt: '2015-04-01 15:45:35 +0000'
  content: "[&#8230;] we announced Hack, we were very excited for the community to
    get their hands on a programming language that has [&#8230;]"
- id: 454463
  author: Mateus
  author_email: mateus_zanatta@hotmail.com
  author_url: http://hacklangbrasil.blogspot.com
  date: '2015-04-16 23:48:00 +0000'
  date_gmt: '2015-04-17 06:48:00 +0000'
  content: It may help you http:&#47;&#47;hacklangbrasil.blogspot.com&#47;2014&#47;11&#47;hack-plugin-to-sublime-text.html?m=1
- id: 839363
  author: Rubeesh
  author_email: evilhseebur@yahoo.com
  author_url: http://hhvm.com/blog/4223/introducing-hack-a-programming-language-for-hhvm
  date: '2016-03-22 05:56:02 +0000'
  date_gmt: '2016-03-22 12:56:02 +0000'
  content: What approach hack use,Is it object-oriented or strutured approach?
---

As you [may have heard or seen already](https://code.facebook.com/posts/264544830379293/hack-a-new-programming-language-for-hhvm/), the [Hack programming language](http://hacklang.org) has been released for HHVM. Hack reconciles the fast development cycle of PHP with the discipline provided by static typing, while adding many features commonly found in other modern programming languages.

<!--truncate-->

We have deployed Hack at Facebook and it has been a great success. Over the last year, we have migrated nearly our entire PHP codebase to Hack, thanks to both organic adoption and a number of homegrown refactoring tools.

We are proud to release [an open source version of Hack](https://github.com/facebook/hhvm/tree/master/hphp/hack) to the public as part of our HHVM runtime platform, which will now support both Hack and PHP.

It is important to note that we have developed Hack to interoperate as seamlessly as possible with PHP. In fact, it is a [stated goal of the HHVM team](http://hhvm.com/blog/2014/02/24/hhvm-the-next-six-months/) to continue to grow compatibility with the many existing PHP frameworks. The top 20 open source frameworks on Github run on HHVM. We currently pass <del>9</del> [10 of the top 20](http://hhvm.com/frameworks) at 100% on their unit tests. Most of the others are passing at or above 90%. We, of course, are working hard to ensure every framework is at or near 100%.

You can [view the complete Hack language announcement](https://code.facebook.com/posts/264544830379293/hack-a-new-programming-language-for-hhvm/) or go directly to [http://hacklang.org](http://hacklang.org) to find out more. Enjoy!
