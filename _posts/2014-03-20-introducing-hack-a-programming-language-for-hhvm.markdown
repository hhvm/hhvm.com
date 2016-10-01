---
author: julienv
comments: true
layout: post
title: Introducing Hack - A Programming Language for HHVM
category: blog
redirect_from:
  - /blog/4223/introducing-hack-a-programming-language-for-hhvm
---

As you [may have heard or seen already](https://code.facebook.com/posts/264544830379293/hack-a-new-programming-language-for-hhvm/), the [Hack programming language](http://hacklang.org) has been released for HHVM. Hack reconciles the fast development cycle of PHP with the discipline provided by static typing, while adding many features commonly found in other modern programming languages.

<!--truncate-->

We have deployed Hack at Facebook and it has been a great success. Over the last year, we have migrated nearly our entire PHP codebase to Hack, thanks to both organic adoption and a number of homegrown refactoring tools.

We are proud to release [an open source version of Hack](https://github.com/facebook/hhvm/tree/master/hphp/hack) to the public as part of our HHVM runtime platform, which will now support both Hack and PHP.

It is important to note that we have developed Hack to interoperate as seamlessly as possible with PHP. In fact, it is a [stated goal of the HHVM team](http://hhvm.com/blog/2014/02/24/hhvm-the-next-six-months/) to continue to grow compatibility with the many existing PHP frameworks. The top 20 open source frameworks on Github run on HHVM. We currently pass <del>9</del> [10 of the top 20](http://hhvm.com/frameworks) at 100% on their unit tests. Most of the others are passing at or above 90%. We, of course, are working hard to ensure every framework is at or near 100%.

You can [view the complete Hack language announcement](https://code.facebook.com/posts/264544830379293/hack-a-new-programming-language-for-hhvm/) or go directly to [http://hacklang.org](http://hacklang.org) to find out more. Enjoy!
