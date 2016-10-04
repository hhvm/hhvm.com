---
author: jwatzman
layout: post
title: 'Hack Community Roundup #2'
category: blog
permalink: /blog/5429/hack-community-roundup-2
comments:
- id: 225227
  author: Raju
  author_email: raju.sriramoju@shoregrp.com
  author_url: ''
  date: '2014-08-26 06:07:26 +0000'
  date_gmt: '2014-08-26 13:07:26 +0000'
  content: "Hi,\r\n\r\nI am a php developer, new to HHVM HACK, i would like to learn
    HHVM HACK language, we are using Linux-Ubunto 13.10,\r\n\r\nI have few questions,
    Please help me out.\r\n1) What is the text editor (IDE) to use hhvm hack language
    and how to download for ubunto 13.10 ?\r\n2) how to complile hack code before
    exicute.?\r\n3) do we have any coverter to convert existing php project to hhvm
    hack.?\r\n\r\nquick response is highly appreciated, thanks in advance,\r\n\r\nRaju,\r\nemai
    : raju.sriramoju@shoregrp.com"
- id: 226811
  author: Josh Watzman
  author_email: jwatzman@fb.com
  author_url: https://www.facebook.com/jwatzman
  date: '2014-08-27 10:46:56 +0000'
  date_gmt: '2014-08-27 17:46:56 +0000'
  content: "Hey Raju!\r\n\r\n1. This was answered at http:&#47;&#47;stackoverflow.com&#47;questions&#47;23582444&#47;what-ides-have-support-for-the-hack-language.
    Facebook also has our own IDE, FBIDE, that we are going to release at some point.\r\n\r\n2.
    The directions on http:&#47;&#47;hhvm.com&#47; are pretty good. Once you have
    HHVM working, http:&#47;&#47;docs.hhvm.com&#47;manual&#47;en&#47;install.hack.bootstrapping.php
    is how you start with Hack code.\r\n\r\n3. This was answered at http:&#47;&#47;stackoverflow.com&#47;questions&#47;22541250&#47;how-would-you-migrate-from-php-to-hack."
---

Since the [last roundup](http://hhvm.com/blog/4811/hack-community-roundup), our community has continued to produce some really cool projects using Hack. I'm really excited to have another long list to share with all of you!

<img src="/static/logo.svg" alt="Hack Logo" style="width: 200px;"/>

<!--truncate-->

## Github Projects

  * Nathan Davidson is [porting his "groundwork" framework to Hack](https://github.com/ndavison/groundwork-hacklang). He describes groundwork as "a lightweight RESTful-like framework ... designed to quickly get a backend communicating with a backbone.js, or equivalent, frontend."

  * Brian Scaturro posted ["Hacktions", a simple framework for sending messages to observers](https://github.com/HackPack/hacktions). It sits in his "HackPack" alongside [HackUnit](https://github.com/HackPack/HackUnit) which I mentioned last roundup.

  * Tobias Nyholm [wrote a small twig filter](https://github.com/HappyR/ExcerptBundle) to "take a HTML string as input and make it shorter without breaking the HTML". He also [wrote a short blog post](http://developer.happyr.com/symfony-bundle-using-hack) on the plugin.

  * The prismic.io team [ported their PHP kit to Hack](https://github.com/prismicio/hack-kit), as well as [a simple Hack starter project](https://github.com/prismicio/hack-plain-starter). See [their blog post about it](https://blog.prismic.io/U5bUnTkAACwAN-rs/using-hack-language-prismicio) for more information.

  * Andy Hawkins of Bombsquad [released Link-Hack](https://github.com/bmbsqd/Link-Hack), a "version of Amanpreet Singh's minimal PHP Router".


## Blog Posts / Other

  * The Hack team and knowledgeable community members monitor the [StackOverflow](http://stackoverflow.com/) tag "hacklang" for questions, and we've gotten some good ones. In particular, I loved [this question about converting some PHP code to Hack](http://stackoverflow.com/questions/23580272/writing-a-ioc-container-in-hack). It's an extremely good question about thinking about how to write well-structured Hack strict-mode code; make sure to read the author's comment on my answer about why the author's code was structured that way.

  * In the same vein, as part of his groundwork framework rewrite mentioned above, Nathan Davidson wrote [a great blog post about his experience with the conversion](http://www.nathandavison.com/article/21/adventure-time-with-hack-and-hhvm), including some insightful discussion of the finer points of a Hack conversion and what it means to be well-typed.

  * Knecht Rootrecht has started a [German language Hack forum](http://www.fbhack.de/).


One reminder for anyone thinking of starting a new project in Hack: the type system itself is enforced by a separate typechecker, not by HHVM itself, so make sure you [follow the directions on getting it set up](http://docs.hhvm.com/manual/en/install.hack.bootstrapping.php), otherwise you're missing out on a huge amount of the power of Hack!

Leave your thoughts down in the comments. In particular, please let me know what I've missed so I can feature it in the next post!
