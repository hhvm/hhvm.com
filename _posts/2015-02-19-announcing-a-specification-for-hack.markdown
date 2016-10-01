---
author: joelm
comments: true
layout: post
title: Announcing a Specification for Hack
category: blog
redirect_from:
  - /blog/8537/announcing-a-specification-for-hack
---

![Hack Logo](/static/images/posts/Screenshot-2015-02-18-10.07.47.png)

Today we are excited to announce the availability of the [initial specification for the Hack programming language](https://github.com/hhvm/hack-langspec/blob/master/spec/00-specification-for-hack.md).

When we [announced Hack](http://hhvm.com/blog/4223/introducing-hack-a-programming-language-for-hhvm), we were very excited for the community to get their hands on a programming language that has helped Facebook engineers become more productive in their day-to-day development and became, alongside PHP, the language used when developing applications running on [HHVM](http://hhvm.com). At the time of release, we had [documentation](http://docs.hhvm.com) geared for the programmer using Hack to develop applications. However, we did not have official documentation for those that might want to create a Hack implementation of their own or something like a Hack conformance test-suite. This [specification](https://github.com/hhvm/hack-langspec/blob/master/spec/00-specification-for-hack.md) fills that gap. It is _the_ document for the Hack implementer, and an excellent supplemental document for the Hack user.

Hack's roots are from PHP. Last year, we announced the [development of a specification for PHP](http://hhvm.com/blog/5723/announcing-a-specification-for-php). The fine folks at the [PHP Project](http://php.net/credits.php) have since taken over control of that specification and have shepherded it on [GitHub](https://github.com/php/php-langspec) to the tune of hundreds of commits, over 100 pull requests and many general improvements. It was very important, and extremely helpful, that we had a PHP specification when creating the Hack specification. You will see many similarities between the two specifications, along with many new [fea](https://github.com/hhvm/hack-langspec/blob/master/spec/05-types.md#types)[tur](https://github.com/hhvm/hack-langspec/blob/master/spec/14-generic-types-methods-and-functions.md)[es](https://github.com/hhvm/hack-langspec/blob/master/spec/21-attributes.md) and [differences](https://github.com/hhvm/hack-langspec/blob/master/spec/23-differences-from-php.md).

We are hosting the new Hack specification on GitHub. We are eager for you to [explore the specification](https://github.com/hhvm/hack-langspec), provide us [feedback](https://github.com/hhvm/hack-langspec/issues) and [pull requests](https://github.com/hhvm/hack-langspec/pulls). Given that Hack is still a relatively new language, we will continue to evolve the specification with new features. We encourage you to ping us with comments on direction, possible feature requests, etc -- check out the links in the sidebar to the right to see how to get involved.

Special thanks must be given to [Rex Jaeschke](https://github.com/RexJaeschke), who, as with the PHP specification, led the actual writing. In addition, [Julien Verlaguet](https://github.com/pikatchu), [Josh Watzman](https://github.com/jwatzman), [Eugene Letuchy](https://github.com/elgenie), [Fred Emmott](https://github.com/fredemmott), [Sara Golemon](https://github.com/sgolemon), and [Drew Paroski](https://github.com/paroski) helped ensure the specification's accuracy. And, of course, sincere thanks to the community that has used Hack since its inception, providing invaluable input and feedback.

[Enjoy](https://github.com/hhvm/hack-langspec/blob/master/spec/00-specification-for-hack.md)!
