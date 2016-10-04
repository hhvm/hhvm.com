---
author: ptarjan
layout: post
title: Debug Packages
category: blog
permalink: /blog/4601/debug-packages
comments:
- id: 19283
  author: bob
  date: '2014-04-07 15:26:18 +0000'
  date_gmt: '2014-04-07 22:26:18 +0000'
  content: Why no freebsd package?
- id: 19439
  author: Paul Tarjan
  date: '2014-04-08 00:05:10 +0000'
  date_gmt: '2014-04-08 07:05:10 +0000'
  content: Because I haven't gotten many requests for it and I don't know how to build
    for it. If you want to become the maintainer please add it to the wiki.
- id: 19757
  author: Jorge G
  date: '2014-04-08 08:18:30 +0000'
  date_gmt: '2014-04-08 15:18:30 +0000'
  content: Why no MacOS package?
- id: 20189
  author: Luke
  date: '2014-04-08 19:51:12 +0000'
  date_gmt: '2014-04-09 02:51:12 +0000'
  content: Thanks for making it easier for us to help improve this project!
- id: 66095
  author: My Journey with HHVM-Pt.2 - Tech Samurais
  date: '2014-05-04 22:40:49 +0000'
  date_gmt: '2014-05-05 05:40:49 +0000'
  content: "[&#8230;]  HHVM Blog  [&#8230;]"
- id: 177905
  author: Thomas
  date: '2014-06-12 22:02:37 +0000'
  date_gmt: '2014-06-13 05:02:37 +0000'
  content: "Log trace can be found in &#47;tmp with the following format\r\n&#47;tmp&#47;stacktrace..log"
---

![](/static/images/posts/1218.png)

We try our best to be a stable dependable runtime, but if you are reaching into the deep dark abyss of the PHP language, you might stumble upon a dark corner where we segfault or assert. First of all, we are sorry. Secondly, we would love you to [report the issue](https://github.com/facebook/hhvm/issues), and if you can put together a small test case that is best. If it only reproduces under the full moon when you hold your head to the side and hop on one leg, then a stacktrace would be next best.

<!--truncate-->

Before today, you had to compile the code by hand to get a useful stack trace. No longer! Using the [same repo](https://github.com/facebook/hhvm/wiki#installing-pre-built-packages-for-hhvm) you normally use, add `-dbg` to the name of your package.


    sudo apt-get install hhvm-dbg  # old faithful
    sudo apt-get install hhvm-nightly-dbg  # the new hotness


The package is much larger, slower and has a bajillion asserts in it, so please don't use it in production. Please DO use it for reporting stack traces and for diving into HHVM with gdb. Happy debugging.
