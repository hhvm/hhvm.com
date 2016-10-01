---
author: fred
comments: true
layout: post
title: Tracking Parity
category: blog
redirect_from:
  - /blog/3611/tracking-parity
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
