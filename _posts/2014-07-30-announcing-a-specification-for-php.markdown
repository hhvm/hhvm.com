---
author: joelm
comments: true
layout: post
title: Announcing a specification for PHP
category: blog
permalink: /blog/5723/announcing-a-specification-for-php
---

![PHP-logo](/static/images/posts/PHP-logo2.png)

The PHP language has been around for over 20 years and is clearly one of the most popular programming languages in the world. PHP is definitely the [lingua-franca <del>of the internet</del> for server-side web programming](http://php.net/usage.php).

<!--truncate-->

While there is extensive [user-documentation](http://php.net/manual), the PHP language has always been missing a language specification. That is not to say a specification hasn't been [thought about or discussed](http://stackoverflow.com/questions/4680119/php-language-specification). It is just that one has never really come to fruition.

The Chinese philosopher Lao Tzu stated "A journey of a thousand miles begins with a single step". We are excited to announce the initial draft of a specification for PHP.

The existence of the specification was[ announced](http://news.php.net/php.internals/75886) by [Sara](https://twitter.com/SaraMG) at OSCON 2014. The feedback to the announcement and [the sample chapter](http://dl.hhvm.com/resources/PHPSpec-SneakPeak.pdf) was [overwhelmingly positive](http://www.ralf-lang.de/2014/07/23/sara-golemon-facebook-announces-php-language-specification-for-oscon-2014/).

And now, the [entirety of the initial draft specification](https://github.com/php/php-langspec/blob/master/spec/php-spec-draft.md) has been [released to the world](http://news.php.net/php.standards/125). It is hosted on a [git repository at php.net](http://git.php.net/?p=php-langspec.git;a=summary) and this repo will be [mirrored to GitHub](https://github.com/php/php-langspec). Please have a read through the specification. Provide your [pull requests](https://wiki.php.net/vcs/gitworkflow) and [feedback](https://bugs.php.net/). We hope and expect that this specification will evolve over time with the help of everyone who cares about the PHP language.

Thank you to the PHP group for taking the mantle and providing the infrastructure for hosting the further development of the specification and helping shepherd this as a truly community-owned and developed project.

Special thanks must be given to [Rex Jaeschke](https://github.com/RexJaeschke), who lead the actual writing of the specification, and [Drew Paroski](https://github.com/paroski), who was pivotal in the review effort and helped Rex shape the spec into its initial form. Thanks to [Paul Tarjan](https://github.com/ptarjan), [Sara Golemon](https://github.com/sgolemon), [Fred Emmott](https://github.com/fredemmott), [Josh Watzman](https://github.com/jwatzman) and the rest of the [HHVM](http://hhvm.com) team for their awesome contributions and feedback. And thank you to [Stanislav Malyshev](https://github.com/smalyshev) and [Nikita Popov](https://github.com/nikic), who had an early look at the specification and provided valuable feedback.

Language specifications may not be flashiest things in the world of programming, but, in my humble opinion, this is an exciting day for the PHP language. [Read on](https://github.com/php/php-spec/tree/master/spec)!!
