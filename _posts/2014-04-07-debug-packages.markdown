---
author: ptarjan
comments: true
layout: post
title: Debug Packages
category: blog
redirect_from:
  - /blog/4601/debug-packages
---

![](/static/images/posts/1218.png)

We try our best to be a stable dependable runtime, but if you are reaching into the deep dark abyss of the PHP language, you might stumble upon a dark corner where we segfault or assert. First of all, we are sorry. Secondly, we would love you to [report the issue](https://github.com/facebook/hhvm/issues), and if you can put together a small test case that is best. If it only reproduces under the full moon when you hold your head to the side and hop on one leg, then a stacktrace would be next best.

<!--truncate-->

Before today, you had to compile the code by hand to get a useful stack trace. No longer! Using the [same repo](https://github.com/facebook/hhvm/wiki#installing-pre-built-packages-for-hhvm) you normally use, add `-dbg` to the name of your package.


    sudo apt-get install hhvm-dbg  # old faithful
    sudo apt-get install hhvm-nightly-dbg  # the new hotness


The package is much larger, slower and has a bajillion asserts in it, so please don't use it in production. Please DO use it for reporting stack traces and for diving into HHVM with gdb. Happy debugging.
