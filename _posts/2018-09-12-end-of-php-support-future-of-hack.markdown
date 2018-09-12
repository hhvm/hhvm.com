
---
title: "Ending PHP Support, and The Future Of Hack"
layout: post
author: fe
category: blog
---

# Ending Support for PHP

HHVM v3.30 will be the last release series where HHVM aims to support PHP. The key dates are:

* 2018-12-03: branch cut: expect PHP code to stop working with master and nightly builds after this date
* 2018-12-17: expected release date for v3.30.0
* 2019-01-28: expected release date for v4.0.0, without PHP support
* 2019-11-19: expected end of support for v3.30

Ultimately, we recommend that projects either migrate entirely to the Hack language, or entirely to PHP7 and the PHP runtime.

We expect support for real-world PHP code to break rapidly: for example, we are likely to replace reference parameters (`&$foo`) to builtins with `inout` parameters, make `INT64_MAX + 1 === INT64_MIN` (instead of a float),  among other changes. In the short term, we expect it to be fairly straightforward to migrate code to deal with these changes, but this will require that any dependencies written in PHP are either forked and migrated to Hack, or migrated away from.

We're extremely grateful to the users and developers of PHP, and are glad to have been part of those communities.

# The Future Of Hack

We are proud of Hack, but there are still many areas where we want to make major improvements to the language; during the next 2-3 years, we will be working towards making Hack a language that builds on the best parts of its' heritage to produce:

* a consistent, statically typed language
* the development speed and ease-of-use that's traditionally associated with dynamically typed languages

During these 2-3 years, aggressive growth of our user base is not a primary goal: we want most people's first exposure to Hack to be the improved language that we are working towards. However, we will be increasing our investment in Hack/HHVM open source, to continue to support our existing users, and aim to build a community ready to support growth in the future.

As we expect the language to evolve rapidly, we **strongly** recommend using the regular releases instead of the LTS releases for large projects; while this does mean you need to upgrade more often, both us and our users have found that it is generally easier to catch up on 2 months worth of changes 3 times as often than 6 months of changes in one go. We will also be re-evaluating the length of our release cycle; one possibility is that we will move to releases every 4 weeks, with these releases being supported for 6-8 weeks.

For this time period, most of Facebook's Hack libraries and tools on GitHub will only target the latest release, not LTS versions; branches and fixes will be made as-needed, but these branches will be community supported, except for security issues reported via [Facebook's Whitehat Program](https://www.facebook.com/whitehat).

# Open Source Hack in 2018

The priorities of the Hack/HHVM open source team are to support our existing users, and to reduce the pain of the removal of PHP support. This will involve creating additional projects, and polishing several existing projects to reach a state suitable for v1.x.

Currently, plans include:

* [hh-apidoc](https://github.com/hhvm/hh-apidoc): improve ease of use, integrate with existing projects, improve readability and formatting of produced documents
* [hacktest](https://github.com/hhvm/hacktest): improve ease of use, documentation, and use as a replacement for PHPUnit in all our existing projects
* [hack-router](https://github.com/hhvm/hack-router), [hack-router-codegen](https://github.com/hhvm/hack-router-codegen): [remove the dependency on PSR-7](https://github.com/facebookexperimental/hack-http-request-response-interfaces/), revisit the API design for current best practices, improve documentation
* we are investigating migrating away from Composer and Packagist; it currently seems likely that this is going to be a set of best practices or extensions to [Yarn](https://yarnpkg.com/), using the NPM repository, with the goal of using a single package manager for both the JS and Hack parts of web-based projects.

We hope to help the community build what is needed; please get in contact via [Facebook], [Reddit], [Twitter], or in #hhvm on irc.freenode.net.

In 2019, we expect this work to continue and expand in scope, and to provide more automated migrations to update code to deal with language changes.

[Facebook]: https://www.facebook.com/groups/hhvm.general/
[Reddit]: https://www.reddit.com/r/hacklang
[Twitter]: https://twitter.com/hacklang/
