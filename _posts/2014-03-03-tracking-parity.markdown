---
author: fred
layout: post
title: Tracking Parity
category: blog
permalink: /blog/3611/tracking-parity
comments:
- id: 2885
  author: T.J. L
  date: '2014-03-03 15:57:38 +0000'
  date_gmt: '2014-03-03 23:57:38 +0000'
  content: The fact that the graphs don't have a common "floor" (and that the bottom
    of the Y axis is simply the recent min) makes the results look a lot more volatile
    than they are, and makes it hard to "compare."
- id: 2891
  author: Fred Emmott
  date: '2014-03-03 16:03:57 +0000'
  date_gmt: '2014-03-04 00:03:57 +0000'
  content: It makes it hard to directly compare one framework to another, but we found
    it made it easier to see regressions&#47;improvements within a framework, which
    was more important to us.
- id: 2897
  author: Nano
  date: '2014-03-03 18:53:03 +0000'
  date_gmt: '2014-03-04 02:53:03 +0000'
  content: I love to see PhalconPHP working with HHVM.
- id: 2903
  author: Martin
  date: '2014-03-04 03:30:21 +0000'
  date_gmt: '2014-03-04 11:30:21 +0000'
  content: I'd love so see also the percent of the "skipped" tests.
- id: 2909
  author: Fred Emmott
  date: '2014-03-05 10:08:32 +0000'
  date_gmt: '2014-03-05 18:08:32 +0000'
  content: |-
    C extension compatibility is something that's being worked on, but is currently lower priority than PHP frameworks.

    Additionally, I'd expect PhalconPHP to be less performant than pure-PHP frameworks under HHVM - pure PHP ends up as highly optimized x64 machine code, and the overhead of calling a C&#47;C++ function (pushing stuff onto the stack instead of just using registers, etc) is likely to be more than any benefits of the C code; it's also likely that the JIT could make more efficient code from PHP than GCC can from C, as we might be able to optimize-away type checks&#47;conversions, depending on usage.
- id: 2915
  author: Nano
  date: '2014-03-12 22:39:18 +0000'
  date_gmt: '2014-03-13 05:39:18 +0000'
  content: |-
    Well, maybe in terms of speed PhalconPHP dont get much benefit from hhvm, but is clearly the most competitive framework atm.

    Absolutly all my projects (PHP) are build with PhalconPHP, so, hope in a future be available.

    http:&#47;&#47;www.techempower.com&#47;benchmarks&#47;previews&#47;round9&#47;#section=data-r9&amp;hw=peak&amp;test=json&amp;l=sg

    Anyway, thanks for you work.
- id: 5627
  author: Sumbobyboys
  date: '2014-03-26 03:41:45 +0000'
  date_gmt: '2014-03-26 10:41:45 +0000'
  content: "This page is really cool but seems to be broken right now ! (\"test-charts.js\"
    missing)\r\n\r\nThanks for all your hard work !"
---

HHVM has a [large suite of unit tests](https://github.com/facebook/hhvm/tree/master/hphp/test) that must pass in several build configurations before a commit reaches master. Unfortunately, this test suite passing doesn't tell you if HHVM can be used for anything useful - so we periodically run the test suites for popular, open source frameworks.

<!--truncate-->

![Test Results](/static/images/posts/frameworks_post_screenshot1.png)


[The frameworks test page](http://www.hhvm.com/frameworks) is now public, as is [the JSON data](http://graph.facebook.com/hhvm_oss_tests) backing it (which you're welcome to use).


## What's tested


We aim to test the latest stable version of each framework, with a few exceptions:




  * if fixes are required, we use the earliest version of `master` or `develop` that includes them


  * if recent changes make it significantly easier to run the tests - e.g., a framework switching from a custom test runner to just '`run phpunit`'


At the moment, the framework versions in our test runner are fairly consistent with our above philosophy, but we will continue to fine tune them as needed. You can see the exact versions we use in [hphp/test/frameworks/frameworks.yaml](https://github.com/facebook/hhvm/blob/master/hphp/test/frameworks/frameworks.yaml).


## How it works


The test runner and configuration is in [`hphp/test/frameworks`/](https://github.com/facebook/hhvm/tree/master/hphp/test/frameworks); once an hour, a script fetches the latest version of HHVM from GitHub, does a clean debug build, and runs the framework tests in `--csv` mode (with JIT, not RepoAuthoritative) . This data is then imported into a fairly standard MySQL+Memcached system, and made available via a[ JSON AP](http://graph.facebook.com/hhvm_oss_tests)I. The results page is built on top of that API using HHVM, XHP, and the Google Charts API.

The runner runs all tests in parallel - including tests within a framework; this is needed for the tests to complete in a reasonable amount of time, but unfortunately leads to noisy data, as some tests have implicit interdependencies.


## Motivation


We believe the current frameworks in the test runner are a nice representative sample of real world PHP (and we are adding more). We showed a [static snapshot](http://www.hhvm.com/blog/2813/we-are-the-98-5-and-the-16) of our test parity to these frameworks late last year. As HHVM is continually developed, it is paramount that the community knows whether there is progression or regression in how HHVM can run code. Having a live snapshot of unit test pass percentage progress helps "keep us honest".

Also, HHVM has [a growing developer community](https://github.com/facebook/hhvm/graphs/contributors), including passionate [OpenAcademy](https://www.facebook.com/OpenAcademyProgram) students; snapshots of this data have been invaluable for finding and prioritizing issues (combined with data from [GitHub](https://github.com/search?o=desc&q=PHP&ref=cmdform&s=stars&type=Repositories) and [VersionEye](https://www.versioneye.com/PHP)). As such, moving from occasional framework unit test snapshots to continuous data was an obvious step in making it easy for new contributors to find effective ways to contribute.
