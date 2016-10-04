---
author: paulbiss
layout: post
title: Lockdown Results and HHVM Performance
category: blog
permalink: /blog/9293/lockdown-results-and-hhvm-performance
comments:
- id: 518891
  author: RobW
  date: '2015-06-09 10:45:48 +0000'
  date_gmt: '2015-06-09 17:45:48 +0000'
  content: Can you link to the drupal bug about searching the file system that you
    fixed with a db change?
- id: 518903
  author: Tim Siebels
  date: '2015-06-09 10:49:44 +0000'
  date_gmt: '2015-06-09 17:49:44 +0000'
  content: "Great article! I really like that you explained what setup was used in
    detail. Reading the issue's comments during lockdown was fun, as you could see
    progress.\r\nFurthermore you included performance gains for PHP which shows that
    this isn't a fight with vanilla PHP but is a healthy competition. :)\r\nKeep getting
    more open, I like it! :)"
- id: 518909
  author: Fred Emmott
  date: '2015-06-09 10:52:21 +0000'
  date_gmt: '2015-06-09 17:52:21 +0000'
  content: 'Thanks :) For reference (sorry we forgot to include it in the post) the
    MediaWiki issue with full results is here: https:&#47;&#47;phabricator.wikimedia.org&#47;T99740'
- id: 518921
  author: Fred Emmott
  date: '2015-06-09 10:53:36 +0000'
  date_gmt: '2015-06-09 17:53:36 +0000'
  content: Sorry, this was from an external contributor and we don't have the source
    handy. We've asked for details and will get back to you :)
- id: 518927
  author: Joel Marcey
  date: '2015-06-09 10:59:54 +0000'
  date_gmt: '2015-06-09 17:59:54 +0000'
  content: Thanks Tim!
- id: 518939
  author: Kazanir
  date: '2015-06-09 11:04:55 +0000'
  date_gmt: '2015-06-09 18:04:55 +0000'
  content: "What happened here was that devel_generate was used to generate the content
    in the database dump, but the module wasn't actually disabled or uninstalled.
    Then the database dump was used to drive a codebase that lacked that module. This
    results in a \"zombie\" entry in Drupal's system table where a module is recorded
    as enabled despite not existing. (This is a known issue on the Drupal side.) This
    results in each page request seeing the \"missing\" module and scanning the entire
    filesystem below modules&#47; to try to find it on every request.\r\n\r\nOops."
- id: 519047
  author: Esa
  date: '2015-06-09 12:36:49 +0000'
  date_gmt: '2015-06-09 19:36:49 +0000'
  content: You are leading the whole php community. Mark should be proud of you. You
    deserve the whole php community comes and welcome you due to your achievements.
- id: 519221
  author: mikeytown2
  date: '2015-06-09 15:31:37 +0000'
  date_gmt: '2015-06-09 22:31:37 +0000'
  content: There are a couple of async MySQL Drupal modules out there, but they are
    using mysqlng &amp; mysqli &amp; MYSQLI_ASYNC instead of HHVM async as it wasn't
    available when the code was developed. See https:&#47;&#47;www.drupal.org&#47;project&#47;apdqc
    &amp; https:&#47;&#47;www.drupal.org&#47;sandbox&#47;gielfeldt&#47;2422171
- id: 519227
  author: mikeytown2
  date: '2015-06-09 15:37:09 +0000'
  date_gmt: '2015-06-09 22:37:09 +0000'
  content: I believe this is the issue - https:&#47;&#47;www.drupal.org&#47;node&#47;1081266
- id: 519443
  author: Meserlian
  date: '2015-06-10 00:12:01 +0000'
  date_gmt: '2015-06-10 07:12:01 +0000'
  content: This is awesome testing. Looking forward for the Async test for WP.
- id: 519449
  author: Nemo
  date: '2015-06-10 00:18:21 +0000'
  date_gmt: '2015-06-10 07:18:21 +0000'
  content: Thanks for your testing. From several things mentioned, it seems you tested
    an older release of MediaWiki (1.24?) with vanilla settings. For higher realism,
    it would probably have been more useful to test the settings commonly used by
    any "serious" MediaWiki wiki, see https:&#47;&#47;www.mediawiki.org&#47;wiki&#47;Manual:Performance_tuning
    for the basics.
- id: 519497
  author: Radu Murzea
  date: '2015-06-10 01:55:24 +0000'
  date_gmt: '2015-06-10 08:55:24 +0000'
  content: "I really love the incredible amount of detail in this post and, obviously,
    the impressive results of your improvements.\r\n\r\nI'm really curious to see
    how these tweaks affect performance of a much broader collection of PHP frameworks
    and CMS-es."
- id: 519515
  author: Peter
  date: '2015-06-10 02:42:11 +0000'
  date_gmt: '2015-06-10 09:42:11 +0000'
  content: Awesome, I really fell in love with HHVM over the last couple of months.
    I can't wait for 3.8.
- id: 519701
  author: Fred Emmott
  date: '2015-06-10 09:01:13 +0000'
  date_gmt: '2015-06-10 16:01:13 +0000'
  content: "We're on a slightly older version as:\r\n - it's only one minor version
    behind\r\n - we're not aware of significant performance changes\r\n - if there
    are any, we would expect them to mostly benefit HHVM anyway, as that's the engine
    that Wikipedia have recently switched to\r\n - updating releases has a high cost:
    as well as the basic mechanics, we need to make sure the results are still consistent,
    re-profile to make sure there's not been any changes in the defaults that are
    good for 'just works' but aren't realistic (the documentation is not good enough
    for this), etc\r\n\r\nIt is not vanilla:\r\n - we use a custom file-based localization
    cache (which is an improvement over Mediawiki's file cache and MySQL caches),
    which is an improvement on PHP5, PHP7, and HHVM: http:&#47;&#47;cl.ly&#47;image&#47;3I2m2a190G3N\r\n
    - we disable view counters\r\n\r\nIn general, we aim to optimize and reconfigure
    by profiling and looking for bottlenecks, rather than trusting often-incorrect
    or outdated documentation. The Mediawiki docs were good though, so to address
    them:\r\n\r\n - opcode caching is enabled by default in all recent versions of
    PHP, and irrelevant in HHVM. Our benchmarking script makes sure it is enabled
    when running PHP5 or PHP7\r\n - memcached is not used both because object caching
    does not show up as significant in profiles, and because there is not yet a sufficiently
    complete and stable implementation for PHP7\r\n - output caching is not used as
    this would be nearly a no-op with an HTTP cache in place, and roughly turn the
    benchmark into 'Hello, world'. The uncached Barack Obama page is representative
    of the load on Wikipedia's application servers\r\n- HTTP caching: again, turns
    it into 'hello, world'. While this does mean that our numbers are not representative
    of the RPS you'd get on the whole system, presumably if you're looking at PHP
    performance, performance of the application servers are what you want to focus
    on\r\n\r\n - mbstring is enabled in PHP5, PHP7, and HHVM\r\n - FastStringSearch
    is not used because it is not available for PHP7, disabling like-for-like comparisons\r\n
    - the MySQL lock options do not have an affect, and should not be particularly
    relevant as our benchmark does not include writes\r\n - We have plenty of RAM
    for MySQL, $PHP_IMPLEMENTATION, and nginx."
- id: 522191
  author: HHVM Demonstrated to be 18.7% Faster Than PHP 7 on a WordPress Workload
  date: '2015-06-12 10:47:28 +0000'
  date_gmt: '2015-06-12 17:47:28 +0000'
  content: "[&#8230;] week HHVM developers shared the results of their first ever
    open source performance lockdown. HHVM is Facebook&#8217;s open source PHP execution
    engine, originally created to help make its [&#8230;]"
- id: 522197
  author: Guilherme Cardoso
  date: '2015-06-12 10:58:35 +0000'
  date_gmt: '2015-06-12 17:58:35 +0000'
  content: "Sorry for asking this here. ATM attributes are available at class level
    and methods.\r\n\r\nIs it in the roadmap to include them as well on properties
    or is something impossible thanks to PHP dynamic nature?\r\n\r\nWhen looking for
    web frameworks features, implementing attributes in properties allow us to define
    most common configs (entities mapping, validations mappings, etc) in a good way,
    similar to C# attributes features. ATM i'm doing it in properties getters which
    is ugly of course."
- id: 522389
  author: Nemo
  date: '2015-06-12 13:54:26 +0000'
  date_gmt: '2015-06-12 20:54:26 +0000'
  content: "Thanks for the clarifications, in particular on localisation cache; it
    was not clear to me what you meant by &laquo;we&rsquo;ve specifically turned them
    off&raquo; before reading https:&#47;&#47;github.com&#47;hhvm&#47;oss-performance&#47;blob&#47;master&#47;README.md#mediawiki
    .\r\n\r\nI still wonder about the effect of some other standard configurations
    you may have missed, like $wgJobRunRate."
- id: 524369
  author: 'HHVM Performance Lockdown: Is HHVM Reaching Its Limit?'
  date: '2015-06-14 03:15:34 +0000'
  date_gmt: '2015-06-14 10:15:34 +0000'
  content: "[&#8230;] latest HHVM blogpost is all about getting performance gains
    from HHVM in real-life situations. With a noticeable increase for MediaWiki, all
    other frameworks are [&#8230;]"
- id: 525377
  author: 'L&rsquo;hebdo de l&rsquo;&eacute;cosyst&egrave;me WordPress #22'
  date: '2015-06-15 01:04:58 +0000'
  date_gmt: '2015-06-15 08:04:58 +0000'
  content: "[&#8230;] vous suivez la guerre que se livre PHP et HHVM pour optimiser
    les performances de leur interpr&eacute;teur PHP respect&#8230;, hhvm a publi&eacute;
    cette semaine leurs derni&egrave;res [&#8230;]"
- id: 525761
  author: Josh Watzman
  date: '2015-06-15 09:49:44 +0000'
  date_gmt: '2015-06-15 16:49:44 +0000'
  content: No fundamental reason why we haven't allowed it, just haven't gotten around
    to building it :) I just filed https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;issues&#47;5493
    for you. In the future, GitHub issues or IRC are, respectively, better ways of
    filing feature requests or asking questions than a comment on a random blog post
    :)
- id: 530213
  author: Jani Tarvainen
  date: '2015-06-23 10:24:52 +0000'
  date_gmt: '2015-06-23 17:24:52 +0000'
  content: "I strapped the HTTP&#47;2 capable H2O web server to HHVM to go ahead and
    make it serve like they do in 2020 :)\r\n\r\nhttps:&#47;&#47;www.symfony.fi&#47;entry&#47;serving-php-on-http-2-with-h2o-and-hhvm-symfony-wordpress-drupal"
- id: 537869
  author: wwbmmm
  date: '2015-06-30 22:51:18 +0000'
  date_gmt: '2015-07-01 05:51:18 +0000'
  content: You had optimized for RepoAuthoritative mode with proxygen server. What
    about non RepoAuthoritative mode and fastcgi server? This is more popular use
    case (except facebook) and is more compatible with zend php.
- id: 537875
  author: Paul Bissonnette
  date: '2015-06-30 23:02:34 +0000'
  date_gmt: '2015-07-01 06:02:34 +0000'
  content: "The numbers are based on proxygen running behind nginx, we found that
    it showed a small performance bump when compared to fastcgi behind nginx, but
    the difference was very small.\r\n\r\nWe have in the past published numbers based
    on non-RepoAuthoratative mode, and will continue to track and improve its performance.
    For a variety of reasons running in RepoAuthoratative mode will always be a substantial
    performance benefit. Put simply the use of whole program analysis allows a host
    of powerful optimizations that depend on the knowledge that all execution paths
    are both known and stable.\r\n\r\nIt is worth noting that even in non-RepoAuthoratative
    mode we are quite performant, and the performance benefit from this mode is probably
    only going to be important to those operating at a sufficiently large scale. We
    are aware of other large deployments that use or are exploring the future use
    of this setting. We've also added tooling to make it easier to experiment with
    RepoAuthoritative mode (mentioned in the article).\r\n\r\nObviously there is no
    one ideal configuration that will work for every installation, but we feel strongly
    that the configuration presented here is a good choice for large sites that deeply
    care about this kind of performance. The article was already complicated enough
    with one set of configuration options so we chose the ones that would matter most
    to anyone operating at scale."
- id: 537989
  author: wwbmmm
  date: '2015-07-01 00:54:50 +0000'
  date_gmt: '2015-07-01 07:54:50 +0000'
  content: Are you going to do some optimization for non-RepoAuthoratative mode? My
    profiling shows that ExecutionContext::lookupPhpFile cost 11% inclusive cpu in
    non-RepoAuthoratative mode. Those who says "php7 is faster than hhvm" only compare
    php7 with hhvm-no-repo.
- id: 538001
  author: Paul Bissonnette
  date: '2015-07-01 01:06:16 +0000'
  date_gmt: '2015-07-01 08:06:16 +0000'
  content: "We're committed to improving both modes, though at the end of the day
    the metric we watch most carefully is repo-mode performance.\r\n\r\nWe've done
    a fair bit of profiling in non-repo mode and have made some important improvements.
    I've never seen lookupPhpFile in any of the profiles I've examined, and the function
    doesn't appear to be present in master, 3.3, 3.6, or 3.7 (are you benchmarking
    an old version of hhvm?). I'd be curious to hear more details about how you're
    performing this profiling and I'd be happy to work with the data to make improvements
    or review pull-requests.\r\n\r\nThere's been a lot of confusion about how to benchmark
    PHP engines in a fashion that's representative of a production environment. A
    good portion of this article has been about trying to formalize some of the lessons
    we learned. The hope is that we might provide a sane hhvm configuration as well
    as a framework for simulating a production environment for others who wish to
    run their own benchmarks.\r\n\r\nI've seen some of the numbers being passed around
    but so little has been shared of the methodology that I can't really comment on
    the accuracy of those results."
- id: 538019
  author: wwbmmm
  date: '2015-07-01 01:38:32 +0000'
  date_gmt: '2015-07-01 08:38:32 +0000'
  content: I have profiled in 3.0&#47;3.6, 3.6 is slightly faster. Do you have email
    address? I can send you more details.
- id: 538043
  author: Paul Bissonnette
  date: '2015-07-01 01:49:21 +0000'
  date_gmt: '2015-07-01 08:49:21 +0000'
  content: 'Sure, paulbiss (at) fb.com, you can also find me on our Freenode channels
    #hhvm and #hhvm-dev (I''m usually around during normal business hours in California).
    Thanks!'
- id: 538607
  author: HHVM Now Faster than PHP 7 | Hackers Media
  date: '2015-07-01 11:51:06 +0000'
  date_gmt: '2015-07-01 18:51:06 +0000'
  content: "[&#8230;] to the report, various setups were tested, with technologies
    like WordPress, Drupal, and MediaWiki used in a [&#8230;]"
- id: 547421
  author: Craig Carnell
  date: '2015-07-14 02:15:20 +0000'
  date_gmt: '2015-07-14 09:15:20 +0000'
  content: Where are the Magento results? :)
- id: 547703
  author: Fred Emmott
  date: '2015-07-14 09:58:45 +0000'
  date_gmt: '2015-07-14 16:58:45 +0000'
  content: "Magneto1:\r\n\r\nHHVM 3.7: 119.73 RPS\r\nHHVM 3.8: 124.47 RPS\r\nImprovement:
    4%\r\n\r\nMagento2: pull requests welcome ;) https:&#47;&#47;github.com&#47;hhvm&#47;oss-performance"
- id: 547709
  author: Fred Emmott
  date: '2015-07-14 09:59:24 +0000'
  date_gmt: '2015-07-14 16:59:24 +0000'
  content: We didn't include them in the post as Magento wasn't part of the lockdown.
---

The HHVM team has concluded its first ever open source performance lockdown, and we're very excited to share the results with you. During our two week lockdown, we've made strides optimizing builtin functions, dynamic properties, string concatenation, and the file cache. In addition to improving HHVM, we also looked for places in the open source frameworks where we could contribute patches that would benefit all engines. Our efforts centered around maximizing requests per second (RPS) with Wordpress, Drupal 7, and MediaWiki, using our [oss-performance](https://github.com/hhvm/oss-performance) benchmarking tool.

<!--truncate-->

## Summary


During lockdown we achieved a 19.4% RPS improvement for MediaWiki workloads, and a 1.8% RPS improvement for Wordpress. We demonstrated that HHVM is 55.5% faster than PHP 7 on a MediaWiki workload, 18.7% faster on a Wordpress workload, and 10.2% faster on a Drupal 7 workload. Improvements made to HHVM to better serve open source frameworks will ship with the next release. As a part of our lockdown effort a patch showing a promising performance improvement for all PHP engines was submitted to MediaWiki. The raw data, configuration settings, and summary statistics are available [here](http://dl.hhvm.com/resources/lockdown-data/).

Lockdowns are always a great opportunity to get the whole community involved, and we're thrilled with the participation this time around. Our #hhvm and #hhvm-dev channels on Freenode were quite active and a number of contributors even chimed in on [GitHub issues](https://github.com/facebook/hhvm/issues). Special thanks to [Christian Sieber](https://github.com/Kazanir) for [contributing support](https://github.com/hhvm/oss-performance/commit/65983c56be0beaf708a4e974c55dba46e9d1cedb) for Drupal 8 to our benchmarking tool.

Throughout the lockdown we have made improvements to our benchmarking tools, and optimized our configuration. We're pleased to report that these frameworks all ran successfully using the high performance [RepoAuthoritative](https://github.com/facebook/hhvm/wiki/Performance-Tuning#use-repoauthoritative---20) compilation mode, and file-cache we deploy with at Facebook. New [tooling](https://github.com/facebook/hhvm/commit/4bbae3bab9aae9647588637af5518f37f4091fc4) will make it easier to take advantage of these powerful tools in the upcoming 3.8 release.


## Methodology


While no benchmark will ever perfectly capture the performance profiles of the disparate live sites it seeks to approximate, great care was taken in constructing this tool. We feel that it's important to carefully explain the decisions we've made and the effects they've had on performance. Hopefully these notes will shed light on the numbers that we've shared, and help others to configure their benchmarking suites or to optimize their sites. Inquiries regarding the benchmarking methodology can be made directly on our [oss-performance](https://github.com/hhvm/oss-performance) repository, pull-requests for new features and fixes are also most welcome.

Our hardware setup featured [Mac Pro](https://www.apple.com/mac-pro/) computers running a minimal installation of [Ubuntu](http://www.ubuntu.com) 14.04 (no virtualization or other layers which would add uncontrolled variables). We chose the Mac Pro because, while being convenient to work with, they also contain components that are representative of hosting servers, including Xeon processors, an abundance of RAM, and flash storage. They are also readily available in an identical configuration (see notes for details). The configuration offered ample RAM to avoid the possibility of swapping, and an SSD to reduce the effect of latency reading from disk. The minimalistic software installation ensured that results were consistent between runs and that benchmarks were run in near isolation.

For HHVM, we choose to run in RepoAuthoritative mode, using the file cache to construct a virtual in-memory file system, and with the [proxygen webserver](https://github.com/facebook/hhvm/commit/8039dc9e321905441141592bfbd3c6d78158911e). This setup closely mirrors the configuration we use to run Facebook, and has been highly optimized. Traffic was proxied through an nginx webserver to allow for a fair comparison with PHP running FastCGI through nginx. We chose a high thread-count, as many frameworks were I/O-bound. For a CPU-bound application, we generally recommend a thread-count no higher than twice the number of available cores.

Our PHP 5 and 7 setups were quite similar; we enabled the opcache, and chose settings tuned for performance. For all engines tested, error reporting and logging were disabled to limit log spew and maximize performance. In production we generally favor a sampling approach that allows for data to still be collected about warnings and notices. For benchmarking, we felt no logging was most appropriate.

The benchmarking tool performs a sanity check once the engine and webserver have started accepting traffic to ensure that the framework is sending reasonable responses on the URLs being benchmarked. We also collect a count of the various HTTP response codes, average bytes received, and failed requests. This data is manually inspected after data collection is complete to ensure that the results from the server are reasonable. Note that some of the URLs benchmarked return non-200 response codes to approximate a realistic distribution of requests to a live server. For all results presented here this sanity check information is available in the raw JSON data provided in the notes.

![cartoon](/static/images/posts/cartoon.png)

Each framework we benchmarked was configured with a sample dataset designed to approximate an average installation. For Wordpress and Drupal 7, bundled tools were used to construct demo sites for benchmarking. MediaWiki was benchmarked using the Barack Obama page from Wikipedia, as was recommended by an engineer from Wikimedia foundation as representative of their load. For Wordpress, the URLs queried were based on data extracted from the [hhvm.com](http://hhvm.com) access logs. Drupal 7 query URLs mirrored similar access patterns to Wordpress as access logs from live sites were not readily available. The MediaWiki URL list was generated to stress the Barack Obama page.

Drupal 8 was benchmarked in a manner similar to Drupal 7, including the use of bundled tooling to generate the sample site. A consensus has not developed as to whether the page cache should be used when measuring Drupal 8 performance so for our benchmarking suite we support cached and uncached Drupal 8 as separate targets. An additional setup step was performed to pre-populate Drupal 8 Twig templates so that benchmarking could be performed in RepoAuthoritative mode. This is an ahead of time optimization any sufficiently large deployment of this framework would be likely to benefit from. For both versions of Drupal a small number of additional tweaks were carried out to make the sample data more realistic. The [details](https://github.com/hhvm/oss-performance/blob/master/README.md) of these changes as well as details about the configurations of the various other frameworks are available on our oss-performance repository.

When running each engine, we sent both a set of single threaded and a set of concurrent warmup requests to each site before we began measuring performance data. We did this to allow hardware caches to warm up, PHP's opcache to fill, and HHVM's JIT compilation to complete. The number and duration of these warmup periods was chosen by examining performance profiles to look for steady state and monitoring the size and growth of the HHVM translation cache to ensure that compilation was largely completed. As we decided to run HHVM in RepoAuthoritative mode, a setup step was also included to build and optimize the bytecode repository using whole-program analysis, and construct the static content portion of the file-cache for efficient in-memory file system access.

Benchmarking requests were sent from 200 concurrent users, using the siege benchmarking tool. A high number of concurrent users best approximated the maximum possible RPS of a server under high load. Ideally concurrency should be the highest number of users possible before requests began to queue, as this was not possible with siege a high number was selected to ensure reliable RPS data. Note that as a consequence of this decision the response time metric now includes time spent queued. A realistic load balancer would prevent such queueing from occurring on machines serving live traffic.

We discovered that, by default, MediaWiki will store a view counter in MySQL, as well as a cache of each translatable string on any given page. Any large-scale deployment of MediaWiki would need to disable these options; so we've specifically turned them off. We've confirmed that these settings are also disabled in production for Wikipedia. A patch has been submitted to MediaWiki to cache translations more efficiently. The view counters have been deprecated, and will likely be removed entirely in a future release. These particular inefficiencies were discovered by analyzing the queries sent to MySQL by MediaWiki during a single request.

In our initial testing with Drupal 7, we noticed that every request was triggering a scan of the Drupal document root, making the is_dir(), opendir(), and readdir() functions incredibly hot. It has since been brought to our attention that a known bug in Drupal was causing the extension used to generate the sample data to be treated as missing, thus triggering a complete filesystem scan for each request. Currently the only fix for this issue is to manually remove references to the uninstalled extension from the database. After patching the database time spent accessing the filesystem drops substantially and the resulting site behaves identically to a fresh installation of Drupal 7 with manually entered data.


## Results


Our results compare pre- and post-lockdown HHVM, and separately PHP 5, 7, and post-lockdown HHVM. We used PHP 5.6.9, and commits from PHP, and HHVM master (see notes below). For the pre- and post-lockdown comparison stable releases of MediaWiki, Drupal 7, and Wordpress were used, post-lockdown numbers include [a patch](https://github.com/hhvm/oss-performance/blob/master/targets/mediawiki/patches/0001-LCStoreStaticArray.patch) to MediaWiki that was written during the lockdown. The second set of comparisons uses the same stable releases, with the MediaWiki patch applied for all engines. Data for each engine, framework pair was collected in ten independent runs, and RPS was quantified.

We observed low variability between runs and have a great deal of confidence in the reproducibility of these results. The raw output of each run in JSON form has been made available in the notes below along with the batch run settings used to configure the benchmark tool. The canonical field in the output indicates whether non-standard options were passed during the test run. The only non-standard option passed during our test runs was to apply the MediaWiki patch. All passed options are available in the [configuration JSON](http://dl.hhvm.com/resources/lockdown-data/batch-run-config.json).

In the lockdown, we were able to improve MediaWiki performance by 19.4%, and Wordpress by 1.8%. Unfortunately, Drupal wins were no longer measurable once the Drupal database was patched to fix the aforementioned plugin bug. In addition, we increased RPS for simple pages by 5.2% (this was mostly a measure of the overhead incurred by a request). The lockdown offered an opportunity to evaluate our methodology, and work with the community on realistic configurations for the sample data used in our benchmarking. A number important changes to the benchmarking tools and framework configurations were made throughout the course of the lockdown. The results of the lockdown are summarized below, normalized to pre-lockdown RPS numbers. Drupal 8 was not part of our lockdown and is therefore not measured here.

![](/static/images/posts/lockdown-fixed2.png)

Across the board we found that HHVM performs best on applications where CPU time is maximized. In particular we're 1.55 times faster than PHP 7 on a MediaWiki workload, 1.1 times faster on a Drupal 7 workload, and 1.19 times faster on a Wordpress workload. As none of these frameworks take advantage of the asynchronous I/O architecture available in HHVM (i.e., async), it's not surprising that the greatest performance benefits come from the efficient execution of PHP code possible with a JIT compiler. The following figure summarizes the performance difference between PHP 5, PHP 7, and HHVM. Results were normalized to PHP 5 RPS, and Drupal 8 has been included. We benchmarked Drupal 8 with caching both enabled and disabled. In general the results for Drupal 8 were more stable with the cache disabled.

![](/static/images/posts/engines-fixed.png)

For all benchmarks we performed ten independent runs and used the mean RPS result. We also measured standard deviation (see error bars). Standard deviation was highly consistent between runs, and we're confident that with the proper configuration and hardware these results should be easy to reproduce.

As an exercise, we evaluated the benefits of [async MySQL](https://github.com/facebook/hhvm/tree/master/hphp/runtime/ext/async_mysql) in the Wordpress environment. By modifying portions of Wordpress to take advantage of the async capabilities offered by Hack and HHVM, we were able to examine the potential for performance gains through async execution. In our test environment we separated the MySQL and PHP hosting to separate machines within the same datacenter to approximate a realistic Wordpress stack. The introduction of asynchronous query execution can demonstrate performance gains in both RPS and response time. We'll be writing separately about this in the near future.


## Lockdown Optimizations


By sharing the details of some select successes and failures from lockdown we'd like to provide a window into the work we've been doing and offer a guide to anyone considering working on performance related patches for HHVM. Lockdown issues are available on the HHVM GitHub repository and have been [tagged](https://github.com/facebook/hhvm/issues?q=is%3Aopen+is%3Aissue+label%3Alockdown) with “lockdown.” They include our running commentary and notes about our findings as we implemented and measured them.

The issues we focused on fell broadly into several categories: builtin functions, extensions, function dispatch, memory model, JIT compilation, and framework specific patches. In addition to exploring these optimizations we also experimented with introducing async into Wordpress to measure its benefit.

The optimizations to builtin functions included get_object_vars() ([#5287](https://github.com/facebook/hhvm/issues/5287)), implode() ([#5289](https://github.com/facebook/hhvm/issues/5289)), function_exists() ([#5288](https://github.com/facebook/hhvm/issues/5288)), and defined() ([#5290](https://github.com/facebook/hhvm/issues/5290)). The first two optimizations were quite fruitful for both Wordpress and MediaWiki. We had previously predicted that function_exists() and defined() would be good targets for Drupal 7. Unfortunately defined() was not hot enough to have a measurable performance effect, and function_exists() was primarily called with non-static strings making it difficult to optimize.

We also looked at optimizing string concatenation in the JIT using a specialized bytecode for multi-string concatenations ([#5304](https://github.com/facebook/hhvm/issues/5304)). Although this is a valuable optimization we were unable to measure a performance benefit in any of these frameworks. The majority of multi-string concatenations were in places that retained a reference to the internally joined strings, this prevented an important feature of the optimization allowing reuse of consumed string buffers. A further potential JIT optimization was object destruction ([#5281](https://github.com/facebook/hhvm/issues/5281)). Experimentation led us to the conclusion that it would not be worthwhile to explore changes to the object destruction path. Building a non-refcounted garbage-collector is an ongoing HHVM project and may offer more substantial performance benefits in this area.

Several important enhancements to builtin function dispatch were made ([#5276](https://github.com/facebook/hhvm/issues/5276), [#5277](https://github.com/facebook/hhvm/issues/5277)) and several more have been planned ([#5267](https://github.com/facebook/hhvm/issues/5267), [#5292](https://github.com/facebook/hhvm/issues/5292)). The optimizations now completed have allowed for faster inline dispatch to functions with variadics and improved support for static method dispatch for builtin classes. These changes have already showed measurable performance gains in Wordpress, and we expect a tangible benefit from the remaining patches once they are ready to be merged.

Currently we build using libpcre despite the availability of libpcre2. We decided to see if this new pcre library was any more performant ([#5302](https://github.com/facebook/hhvm/issues/5302)). Unfortunately the results here were not encouraging. Further discussions with the maintainers of libpcre2 have led us to conclude that the changes were largely surrounding the API and that optimizing performance was not a goal. In the future we may explore the optional use of a different regular expression processing library for compatible expressions (though to remain feature complete we will always need to provide libpcre as a fallback).

Profiling has demonstrated that dynamic property access is a hot code-path for Wordpress, therefore we worked to optimize dynamic properties and object cloning for objects with such properties ([#5285](https://github.com/facebook/hhvm/issues/5285), [#5286](https://github.com/facebook/hhvm/issues/5286), [#5287](https://github.com/facebook/hhvm/issues/5287)). In HHVM dynamic properties are stored in arrays, which had previously been eagerly copied during calls to clone() and get_object_vars(). By allowing copy-on-write behavior for these property arrays, similar to the behavior of regular PHP arrays, we measured performance improvements in Wordpress.

Some of our largest wins have come from examining the frameworks themselves. In particular, reconfiguring MediaWiki to move translatable string caching out of MySQL showed a 14% performance win using HHVM and a 21% win when using PHP 7. We created an alternative implementation that improved RPS by an additional 22% and 5% respectively - bringing the total improvement for HHVM and PHP 7 to 39% and 33%. We're happy to be able to contribute back to another open source project and are working to upstream these changes.

There are some notable wins that disappeared as we tuned our benchmarking methodology and patched the frameworks themselves. For MediaWiki optimizing str_replace() was a major win, but the hot-path for str_replace() was elided in the subsequent patch to fix localization caching. Likewise optimizations to the file cache showed a great deal of promise for Drupal 7 ([#5284](https://github.com/facebook/hhvm/issues/5284)) until it was discovered that the document tree scanning behavior of Drupal was a bug, which we were able to fix with a database change.

Work continues on a number of these changes ([#5264](https://github.com/facebook/hhvm/issues/5264), [#5269](https://github.com/facebook/hhvm/issues/5269), [#5270](https://github.com/facebook/hhvm/issues/5270), [#5299](https://github.com/facebook/hhvm/issues/5299)), and others have been completed post-lockdown ([#5300](https://github.com/facebook/hhvm/issues/5300), [#5279](https://github.com/facebook/hhvm/issues/5279)). Of the notable post-lockdown completions, work to speedup memcpy showed major performance gains for our internal workload.

We're all quite thrilled with the progress made during the lockdown and the lessons learned. In particular, we feel that we've been able to validate the importance of both JIT compilation and asynchronous execution for optimizing PHP performance. From Amdahl's law, we know that any attempt to optimize execution efficiency of PHP will be undercut by I/O-bound applications. Async offers us the opportunity to shift latency back to the CPU by improving I/O performance, increasing the importance of efficient PHP execution through JIT compilation. By combining async and JIT compilation, we're able to run applications such as Facebook at scale.


## Technical Notes


*Frameworks used* — Collected statistics came from stable releases and betas of several popular frameworks. For Drupal we measured [7.31](https://www.drupal.org/drupal-7.31-release-notes) and [8.0.0-beta11](https://www.drupal.org/node/2496019). For MediaWiki and Wordpress, version [1.24.0](https://git.wikimedia.org/tag/mediawiki%2Fcore.git/29427008e6971268de6a81cf0b8f1a641959b100) and [4.2.0](https://core.svn.wordpress.org/tags/4.2/) were used. Data for Wordpress was generated using the demo-data-creator version 1.3.2. The patch developed for MediaWiki and used in cross-engine comparisons and with post-lockdown HHVM is [available](https://github.com/hhvm/oss-performance/blob/master/targets/mediawiki/patches/0001-LCStoreStaticArray.patch) on the oss-performence repository. **Update:** this has now [been merged into Mediawiki](https://github.com/wikimedia/mediawiki/commit/c403d4838dc8662d62902ced3713c1d9be6309cc).

*Hardware details* - Benchmark statistics were collected on a late 2013 Mac Pro (MD878LL/A). The machine features a 6-core 3.5 GHz Xeon processor with 64 GB of RAM and a 512 GB SSD.

*Siege* - When benchmarking frameworks we used [Siege 2.78](http://download.joedog.org/siege/siege-2.78.tar.gz), currently all versions of Siege 3 have known problems. In particular Siege 3.0.0 to 3.0.7 send incorrect HOST headers to ports other than 80, and 443, and Siege 3.0.8 and 3.0.9 occasionally send bad paths due to incorrect redirect handling.

*Nginx* - All requests were proxied through nginx, this was required as Siege is unable to talk directly to a FastCGI server. We used nginx 1.4.6. The [configuration settings](https://github.com/hhvm/oss-performance/blob/master/conf/nginx/nginx.conf.in) for nginx are available in the oss-performance repository.

*Engines Benchmarked* - To compare pre- and post- lockdown performance of HHVM we measured a build of HHVM master from [May 11th](https://github.com/facebook/hhvm/commit/a70e46bba40ae1f64dbebee26ebd86c820fd0d67) and [May 22nd](https://github.com/facebook/hhvm/commit/7c3639aed1143d155397cd3d6e0b7945cc0b8af0). For PHP/HHVM comparisons post-lockdown HHVM, PHP stable [release 5.6.9](http://php.net/downloads.php#v5.6.9), and PHP 7 master from [May 22nd](https://github.com/php/php-src/commit/c63467fe6e92d664d6f51369be821c60d8eead6f) were used.

*Result Details* - For all data used here we've made the [raw JSON output](http://dl.hhvm.com/resources/lockdown-data/raw-results.tgz) of each run of the oss-performance tool available and the [settings](http://dl.hhvm.com/resources/lockdown-data/batch-run-config.json) we used, we strongly recommend that anyone wishing to release results from this tool make this diagnostic data available. We are also making available the [summary statistics](http://dl.hhvm.com/resources/lockdown-data/batch-run-results.csv) computed across runs.

*Response Time* - We haven't included response times in this report as lockdown optimizations focused on RPS. Response time is a more important metric for many smaller sites and the numbers we collected are available in the raw data. We hope to make improvements to the benchmarking tool to generate concurrency/response time and concurrency/RPS curves.

*Sugar CRM* - There has been some interest in the SugarCRM performance of the various PHP engines. We were unable to provide these numbers as could not find a recent version of PHP 7 that could execute SugarCRM without encountering a segmentation fault. Hopefully it will be possible to collect these numbers in the future as PHP 7 becomes more mature.
