---
author: oyamauchi
layout: post
title: 'Announcing our book: “Hack & HHVM”'
category: blog
permalink: /blog/8981/announcing-our-book-hack-hhvm
comments:
- id: 475571
  author: Kristian
  author_email: kristianoye@gmail.com
  author_url: ''
  date: '2015-05-04 13:21:13 +0000'
  date_gmt: '2015-05-04 20:21:13 +0000'
  content: "I am a big fan of PHP and so far I love most of the changes I see in Hack.
    \ I am curious to know if the editor used in the tutorial is available as source
    code (with the nifty intellisense-like funcionality).  \r\n\r\nThe reason I ask:
    I got on the net&#47;learned to code back in 1993 when I discovered text-based
    MUDs.  I learned C&#47;C++ after falling in love with LPC (the interpreted language
    of the MUD I was on).  I would like to create a new generation of web-based MUD
    using a restricted subset of Hack where other users can alter&#47;extend the codebase
    on-line."
- id: 475691
  author: Josh Watzman
  author_email: jwatzman@fb.com
  author_url: https://www.facebook.com/jwatzman
  date: '2015-05-04 15:07:06 +0000'
  date_gmt: '2015-05-04 22:07:06 +0000'
  content: "We're working on a full-featured Hack IDE. There's more information at
    http:&#47;&#47;nuclide.io&#47;.\r\n\r\nThe tutorial demo is a really really really
    basic web editor. I certainly wouldn't want to use it as an IDE! If you want to
    play around with it, though, it's made of a few components:\r\n\r\n- The editor
    itself is CodeMirror.\r\n- The typechecker core is a JS cross-compile of the actual
    Hack typechecker. Source for the JS bits are here https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;tree&#47;master&#47;hphp&#47;hack&#47;src&#47;js
    but most of it is just the normal Hack typechecker.\r\n- It's glued together with
    a bit of JS webworker magic, see http:&#47;&#47;hacklang.org&#47;wp-content&#47;themes&#47;hack&#47;demo&#47;hack_demo.js
    and http:&#47;&#47;hacklang.org&#47;wp-content&#47;themes&#47;hack&#47;demo&#47;hack_demo_worker.js\r\n\r\nBut
    I'd just wait for Nuclide :)"
- id: 484481
  author: PHP Annotated Monthly &ndash; May 2015 | JetBrains PhpStorm Blog
  author_email: ''
  author_url: http://blog.jetbrains.com/phpstorm/2015/05/php-annotated-monthly-may-2015/
  date: '2015-05-11 00:28:11 +0000'
  date_gmt: '2015-05-11 07:28:11 +0000'
  content: "[&#8230;] Hack &amp; HHVM book by&nbsp;Owen Yamauchi has reached early
    release stage, so if you&#8217;re interested in using Hack&#47;HHVM in your projects,
    that might be a good read. [&#8230;]"
---

![Book cover](/static/images/posts/rc_cat.gif)

We’d like to get more developers in the community using Hack. But we know there’s been something lacking: a good, consolidated resource for learning Hack and getting the most use out of it. We have documentation online, but it’s more of a reference than a tutorial.

<!--truncate-->

I have good news on that front: for the past few months, I’ve been writing a book about Hack and HHVM, and starting today, you can get [an early look](http://shop.oreilly.com/product/0636920037194.do) at it through our publisher, O’Reilly Media.

This is an Early Release — it’s not finished yet. Not all of the chapters are available yet, and the ones that are available might still change before final publication. The technical content is solid, though, so you should be able to read what’s there and go start writing Hack. The book is about HHVM/Hack version 3.6 LTS, which was [released in March](http://hhvm.com/blog/8849/hhvm-3-6-0).

Buying now gets you an ebook with the content as it is now, plus ongoing updates as more chapters become available, and the final ebook when it’s published this summer.

We’d like your feedback on the early release! Questions, comments, concerns: all welcome. If you’re still confused about anything after reading about it in the book, please let us know so we can make it better. Send your feedback to [book@hacklang.org](mailto:book@hacklang.org).
