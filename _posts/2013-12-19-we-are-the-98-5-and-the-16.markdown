---
author: joelm
comments: true
layout: post
title: We are the 98.5% (and the 16%)
category: blog
redirect_from:
  - /blog/2813/we-are-the-98-5-and-the-16
---

On November 4th, the HHVM team went on a [3-week performance and parity lockdown](http://www.hhvm.com/blog/1499/locking-down-for-performance-and-parity). The lockdown officially ended on November 22nd. Overall, this lockdown was a qualified success. Success was measured on 3 vectors:


<!--truncate-->

  1. Did we meet our 99% average unit test pass percentage goal for the 21 open-source frameworks we tested against?


  2. Did we meet the 15% across the board performance improvement gains?


  3. Were the razors put away for the entirety of the three weeks?


![The HHVM Team at the post-lockdown party](/static/images/posts/postlockdown21.png)
<center><i>The HHVM Team at the post-lockdown party</i></center>

## Parity


Going into lockdown, the team knew that awesome performance alone would not suffice in making HHVM a viable PHP runtime to be used out in the wild. It actually had to run real, existing PHP code reliably. So we made that a first class work item (as it will continue to be into 2014). Our first step into improving PHP parity was to look at [Github](https://github.com/), see which [PHP projects were being used by many people](https://github.com/search?l=php&q=stars%3A%3E1&s=stars&type=Repositories) (via their "star" rating) and make sure their unit tests would run successfully on HHVM.


### Parity Results

Let's just get to the numbers. After over **125 diffs**, here are the results of the parity portion of our 3-week lockdown.

[Recall the table of parity](/blog/2013/09/12/wow-hhvm-is-fast-too-bad-it-doesnt-run-my-code.html) before the lockdown. Now, here is our graph of improvement after the lockdown:

![The updated unit test parity results after our 3-week lockdown](/static/images/posts/Screenshot-2013-12-17-12.35.361.png)
<center><i>The updated unit test parity results after our 3-week lockdown</i></center>

As you probably can see by the graph, we were successful in our efforts to improve unit test parity nearly across the board:

  1. The team **doubled** the number of open source projects with unit tests that pass at 100% on HHVM (from 4 to 8). And we have 4 more that are very close in the 99%+ range.


  2. We had > 10% gains in Assetic, Symfony, Yii and CodeIngiter (I am not counting the Pear gain here since we did not have a nice baseline number to begin with).


  3. And all 21 frameworks are above 90% in overall unit test pass percentage.


Many of the diffs and updates that enabled our unit test parity increase are part of the [HHVM 2.3 package](http://www.hhvm.com/blog/2393/hhvm-2-3-0-and-travis-ci). Some key improvements that had significant impact on our unit test results were:

  1. Make array not an instanceof `Traversable`


  2. `Internationalization` support


  3. `PDO::sqliteCreateFunction()` implementation


  4. The beginning of real `php.ini` support


However, there are a few curiosities...


  1. **Why did PhpMyAdmin regress?** We are not convinced this is a regression in the "we are failing more tests than before because of some code we broke" sense. This actually may have to do with our testing framework script not actually loading all of the tests properly initially. We fixed this mid-stream. That said, we are looking into the root cause of this regression, just in case we broke something.


  2. **Why the 90 degree cliff drop-off around November 24th?** We submitted a diff that we thought was going to push a framework to 100%, but instead [segfaulted the runtime](https://github.com/facebook/hhvm/commit/c6d99f1e8eb869a2c16449d057af66eca266fc7b). It was [fixed soon thereafter](https://github.com/facebook/hhvm/commit/2d4f9ee46bfc20b34e77ccd93816c2d6cfd8a26c).


### Testing Framework


The 21 open source projects that were used as our initial baseline to increase our unit test parity were, as stated above, chosen on popularity. However, they were also chosen based on their use of PHPUnit and on how well they would work with our testing framework. Given the sheer number of unit tests that come with some of these projects (e.g., Symfony and ZF2 each have over 10K tests), we needed to come up with a testing framework that would allow us to run the tests for all of the projects in a speedy manner. So the team developed a script that would download, install and run the unit tests for all of the 21 open source projects in parallel. The script is still a work in progress, but it allowed us to run all 50K+ unit tests in 30 minutes to 1 hour (depending if the JIT is on) vs the many hours it would take to the unit tests serially. That script is located in the [HHVM Github repository](https://github.com/facebook/hhvm/blob/master/hphp/test/frameworks/run.php).

You may also notice that ***your*** favorite open source project is not currently in the list above. There are a couple of reasons for that. First, we couldn't cover all open source projects in a 3-week span. Secondly, while open source projects like CakePHP are very important, and we will add them to our testing framework, there were some setup and configuration problems (e.g., requiring of a database) that wouldn't allow us to add them in a short manner.

Finally, as discussed in our pre-lockdown blog post, the HHVM team created a bunch of "[stickies](http://hhvm.com/wp-content/uploads/2013/11/2013-10-31-17.33.041.jpg)" to help guide our work. The stickies were placed on a "number of failing tests associated with this sticky task" vs. "number of days to implement". So, we generally worked from top left to bottom right to get the most bang for our buck.


### Assumptions and Caveats


It is worth pointing out some of the assumptions and caveats that went into to coming up with the statistics above.




  - The final, overall unit test pass percentage (98.5%) is a straight, unweighted average of the individual open source project unit test pass percentages (i.e., add all of the percentages and divide by 21). So, a project like Paris which has 50 unit tests carries the same percentage weight as Symfony which has 10K unit tests. If we weighted these percentages (where Symfony and Zf2 carried more weight than Paris and Idiorm), the overall pass percentage would see a minimal drop (minimal because of the small variance in pass percentages for all of the open source projects).


  - There are some unit tests that fail in HHVM, but also fail with PHP 5.5.x. We called these tests "clowny" and disregarded them in our testing framework.

![Sometimes there is clowniness when it comes to PHP](/static/images/posts/2013-11-21-12.17.301.jpg)
<center><i>Sometimes there is clowniness when it comes to PHP</i></center>


  - There are some unit tests that actually caused problems with our testing framework script (deadlocks, etc.). We "blacklisted" these tests and counted them as failures in terms of our pass percentage.


### Submitted Project Pull Requests


There were times when code changes were necessary to the actual open source project in order to successfully run all of its unit tests. For example, a change may have been necessary in order to support our parallel testing framework. In other cases, there were actual bugs in the unit tests. A real pleasant surprise during our lockdown was how awesome the project owners/maintainers were in reviewing and, in most cases, accepting our pull requests.


### Travis Integration


The [announcement of HHVM 2.3](http://www.hhvm.com/blog/2393/hhvm-2-3-0-and-travis-ci) talked a bit about Travis CI Integration. Now that we are starting to consistently pass unit tests for open source projects, some have added HHVM to their Travis CI build (awesome!). Here are some open source frameworks that have added us to their CI build:




  * [PHPUnit](https://github.com/sebastianbergmann/phpunit/pull/1072)


  * [Yii](https://github.com/yiisoft/yii/pull/3109)


  * [Doctrine 2](https://github.com/doctrine/doctrine2/pull/873)


  * [Laravel](https://github.com/laravel/framework/pull/2973)


Thanks to the above for adding us so quickly. And we have [many pull requests outstanding](https://github.com/search?q=Try+running+unit+tests+on+HHVM+&ref=cmdform&type=Issues) for other open source frameworks to do the same.


## Performance


The performance team blew through their lockdown performance goal of 15% and ended up at 16% for running facebook.com.

![The updated performance results after our 3-week lockdown](http://hhvm.com/wp-content/uploads/2013/12/Screenshot-2013-12-18-09.54.181.png)
<center><i>The updated performance results after our 3-week lockdown</i></center>

This can only mean good things for other PHP code out in the wild. The performance gains came from lots of small improvements, and a few big ones. Some of the biggest wins were:




  1. Generating code for unusual function call patterns. HHVM already generates good code for ordinary function and method calls, so some less-common patterns had started to show up in our performance profile data. The two biggest ones were [`call_user_func()`](http://php.net/manual/en/function.call-user-func.php) and `static::` method calls, which were both handled by the interpreter. Now we generate optimized machine code for each of those call types.


  2. Optimizing the layout of the HHVM binary. HHVM is a big program: the compiled C++ code of HHVM clocks in at just under 100 MB. The CPU's caches work better when the hot code footprint is small, instead of spread out across the address space, so we put the hottest functions together in one part of the binary. For an extra boost to [I-TLB](http://en.wikipedia.org/wiki/Translation_lookaside_buffer) performance, we then mapped that part using [huge pages](http://en.wikipedia.org/wiki/Page_%28computer_memory%29#Huge_pages).


  3. Using the interpreter to detect hot functions. HHVM interprets the first several requests to avoid wasting time and space compiling startup code. We added logic to the interpreter to find the hottest functions and compile them to a special part of the translation cache. Like the last optimization, this one improves code locality, this time for the dynamically generated code.


  4. Upgrading our regular expression library. Newer versions of [PCRE](http://www.pcre.org/) include a JIT compiler for regular expressions, which gives HHVM a nice performance boost.




## Hygiene


I am sure you are thinking to yourself, "all these gains and statistics are nice and everything, but what about the beards?!?" Right, you then remember that in our [beginning the lockdown](http://www.hhvm.com/blog/1499/locking-down-for-performance-and-parity) post that "shaving was discouraged". I am happy to report that we also succeeded in maintaining a state of minimal facial hygiene throughout the lockdown. And here are the pictures to prove it.

![SaraG had a beard in spirit](/static/images/posts/2013-11-22-16.11.241.jpg)
<center><i>SaraG had a beard in spirit</i></center>

![The HHVM team has their razors in hand ready to clean up](/static/images/posts/2013-11-22-16.15.431.jpg)
<center><i>The HHVM team has their razors in hand ready to clean up</i></center>


## Did we meet our goals?


Remember the three success vectors that were posed at the beginning of this blog post?




  1. Did we meet our parity improvement goals for the 21 open-source frameworks we tested against => 99% average unit test parity?


  2. Did we meet performance improvement goals => 15% across the board performance gain?


  3. Were the razors put away for the entirety of the three weeks?


Here are your answers:


  1. **Close YES!** (using rounding to our advantage)


  2. **Resounding YES!** (no rounding needed)


  3. **YES!** Some of us are grayer than others.


## The Future (2014)


Performance improvements will always be a core mantra for the HHVM team. That said, parity will be 1A on the priority scale for the team. We really do care about open source and the PHP community. 2014 will be a year where we go to great lengths to make HHVM first-class when it comes to **both** performance and parity. More unit tests passing for more open source projects and frameworks. Real world testing for PHP code out in the wild. Stay tuned for further updates on our progress and plans. Until then, Happy Holidays and Happy New Year!
