---
title: The Future of HHVM
author: mwang
layout: post
category: blog
---

Several months ago, PHP [officially announced][php5eol] the end-of-life for
PHP5.

The HHVM team is happy about the direction PHP has taken with PHP7, and we're
proud of the role we've played in pushing the language and runtime to where
they are today.  Since the PHP community is finally saying goodbye to PHP5,
we've decided to do so as well.

<!--truncate-->

Our next LTS release, 3.24, will be cut [about four months from now][lts] and
will receive support for one year thereafter.  It will also be the **last HHVM
release that commits to PHP5 support**.  This aligns with PHP's own timeline of
sunsetting PHP5 at the end of 2018.  HHVM users should note that while we won't
drop support for every PHP5-specific quirk immediately, they will all be up for
removal after the 3.24 release cut---and compatibility features like
ext\_zend\_compat will eventually be deprecated and deleted.

It's clear, however, that PHP7 represents a substantive departure from PHP5.
It changes a number of behaviors, some of which are not backward-compatible.
At Facebook, meanwhile, we've used HHVM for years almost exclusively to run
Hack.  Hack had already addressed many of PHP5's shortcomings that PHP7 also
fixes (as well as others that it does not), though Hack's solutions don't
always match PHP7's.

PHP7 is charting a new course away from PHP5, and we want to do the same, via a
renewed focus on Hack.  Consequently, **HHVM will not aim to target PHP7**.
The HHVM team believes that we have a clear path toward making Hack a fantastic
language for web development, untethered from its PHP origins.  We'd do
ourselves and our users a disservice by positioning HHVM as an uncommon, less
well-documented, less compatible PHP7 runtime.

We want to make HHVM and Hack a much better---and even more
performant---developer experience.  Our team has lots of features, libraries,
and performance opportunities in the pipeline, and we want to take the rest of
this post to share them with our community.

## Hack to the Future

We've laid out some realistic goals for better supporting Hack on HHVM, and our
three top-level objectives are as follows:

1. **Reinvest in open source.**  It's clear that having engineers dedicated to
   working directly with the community on its needs is a hard requirement if we
   want to provide even our biggest external users the requisite support.  We
   have begun building up these efforts, and you should start seeing clear
   improvement in the directions outlined below in the coming months.
2. **Set clearer expectations and communicate more openly.**  We want our users
   to have a clear understanding of our plans, goals, and priorities, so that
   they can make the best technical decisions for their products.  We'll aim to
   bring Hack users into conversations about upcoming features and language
   changes much earlier in the process.
3. **Stay focused and don't overextend.**  Trying to support both PHP7 and Hack
   would lead to undesirable compromises on both fronts.  We plan to decouple
   ourselves even more from PHP, so that we can make Hack great without having
   to account for all of the oldest, darkest corners of PHP's design.  We want
   the freedom to make Hack even more performant, and ultimately make it the
   best web application language available.

To complement these goals, we have one explicit non-goal:

1. **We do not intend to be the runtime of choice for folks with pure PHP7
   code.**  We expect Hack and PHP7 to retain a good deal of overlap for the
   time being, and many users may find success using the runtimes
   interchangeably in the short term.  But for those who want to be on the
   newest version of PHP7 and to make use of new behaviors, HHVM will not be
   the most suitable platform.

## Upcoming Changes

So what do these goals mean for our users in practice?

Ironically, they mean **better PHP7 compatibility in the short term**.
Although our open source efforts will focus on Hack, the fact of the matter is
that Hack was designed and built on top of the PHP ecosystem.  In order to
build any nontrivial applications in “pure Hack,” developers need either to
rely on major PHP frameworks or to build their own from scratch.  While the
latter option might be available to a medium-sized company with sufficient
resources, it's currently impractical for most potential Hack adopters.  We
want to change this.

We've begun working toward these goals by **making HHVM compatible with current
versions of major PHP tools** like Composer and PHPUnit, and we expect this
work to continue, directed by the needs of the Hack community and our major
users.  This is not compatibility for compatibility's sake, however.  We'll
cherry-pick features and bug-for-bug compatibilities based on need, and we
won't be targeting any specific PHP 7.x version.  Our eventual goal is for Hack
to have its own ecosystem of core frameworks, whether built by our team or by
others, such that writing a “pure Hack” project is just as easy as writing in
“pure PHP”---but with better performance and developer experience.  We're also
**building tools and libraries designed specifically for Hack**, such as:

- [The Hack Standard Library][hsl], providing a consistent and type-safe
  standard library with full support for the dict, keyset, and vec types.  We
  expect to release a stable v1.0 before HHVM 3.23.
- [TypeAssert][type-assert], which safely converts untyped data (e.g., database
  results or JSON data) into fully typed data.
- [Hack Codegen][hack-codegen], providing a type-safe alternative to magic
  methods such as `__call()`.
- [XHP-Lib][xhp-lib] v2, with full support from the Hack typechecker.
- An [autoloader][autoload] with support for autoloading classes, type aliases,
  functions, and constants.
- An AST-based library with tools for linting and automatically editing code.
  We're expecting to release an early version of this within the next few
  weeks.

While supporting Hack users currently still entails supporting some PHP
libraries, we will not be targeting PHP software beyond such libraries after
the 3.24 release.

We'll aim to align all these efforts with changes to the Hack language.  As we
depart from PHP and our framework dependencies, we'll open up opportunities to
make major performance and design improvements to the Hack language.  Here are
some examples of what our team is working on:

- **Finishing up Hack arrays.**  We've developed explicitly specialized
  array-like data structures in `vec[]`, `dict[]`, and `keyset[]` that are
  easier to typecheck and open up new performance opportunities.  These have
  been available for experimentation in the runtime for several months, and
  will soon be ready for official release.
- **Eliminating destructors.**  Deterministic object destruction is the reason
  why nonscalar PHP values require precise reference counting.  This
  requirement has long been, and continues to be, a sizable performance
  bottleneck in our optimized JIT-compiled code.  Using garbage collection
  instead could unlock measurable performance improvements, and the behavior of
  destructors could be closely imitated by a combination of try/finally and
  other new language constructs.
- **Eliminating references.**  PHP references have unusual semantics, where the
  function specifies the binding of parameters with no indication at the
  callsite.  Moreover, reffiness is not a part of function interfaces, and a
  parent method can be overridden in a derived class with different reference
  binding in any or all parameters.  This is both confusing and
  performance-degrading, and a more disciplined reference-like construct (such
  as in/out function parameters) could be both more useful and more efficient.

As we conceive of and develop such plans, our team will prioritize
communicating these potential changes to our users.  We consider this a vital
prerequisite for iterating on the Hack language more aggressively: We _must_
have good processes in place for helping our users to juggle releases and to
prepare for what's coming next.

Our team will also tackle some longstanding issues raised by many of our
largest users, such as writing better and more complete documentation for HHVM
configuration; communicating release-to-release changes more clearly; and
improving cross-platform builds and testing---all with an eye towards improving
the developer experience of Hack.

If you're running HHVM and have questions, concerns, or enthusiasm about our
direction that you'd like to share, please reach out to us in the [HHVM
General][fb-group] group on Facebook.  As we ramp up this effort over the
coming months, we'll do our best to give you our ear, and we'll make sure to
keep you in the loop once we get rolling.


[php5eol]:      http://php.net/supported-versions.php
[lts]:          https://docs.hhvm.com/hhvm/installation/release-schedule
[hsl]:          https://github.com/hhvm/hsl
[type-assert]:  https://github.com/hhvm/type-assert
[hack-codegen]: https://github.com/hhvm/hack-codegen
[xhp-lib]:      https://github.com/facebook/xhp-lib
[autoload]:     https://github.com/hhvm/hhvm-autoload
[fb-group]:     https://www.facebook.com/groups/hhvm.general/
