---
author: joelm
comments: true
layout: post
title: Faster GitHub Commits
category: blog
permalink: /blog/5399/faster-github-commits
---

The HHVM community is awesome, particularly when it comes to directly helping us fix HHVM through [pull requests](https://github.com/facebook/hhvm/pulls?direction=desc&page=1&sort=created&state=closed). Until now, the actual pushing of commits (both our internal code and your pull requests) back to the [master HHVM branch on GitHub](https://github.com/facebook/hhvm/commits/master) has been a manual process, and takes more time than we would prefer (and I am sure may have frustrated you from time to time).

<!--truncate-->

Initially, the entire process was manual. We would `curl` the pull request and pipe it to `git am`, then manually prepare the diff for review internally. After it was accepted, we would manually prepare the internal commit to be usable externally by GitHub, then manually build and test the new code, and finally `git push`.

Great scripts by [ptarjan](https://github.com/ptarjan) and [sgolemon](https://github.com/sgolemon) to help get and prepare pull requests for review and then prepare the commits for GitHub have alleviated some of this manual process. However, in the end, someone still had to manually build, test and then push the code to the world.

![We are moving just a bit faster....](/static/images/posts/357klxj.jpg)
<center><i>We are moving just a bit faster....</i></center>

Those that keep track of the [HHVM GitHub repo](https://github.com/facebook/hhvm) may have noticed a higher frequency of commits being pushed than in the past. This is not due to someone having too much time on their hands; we are all still very busy hopefully [making HHVM better](http://www.hhvm.com/frameworks/). Instead, we have set up what generally amounts to a sophisticated cron job where a user called [`facebook-github-bot`](https://github.com/facebook-github-bot) pushes any new internal HHVM code to GitHub every 30 minutes. So, once your pull request has been accepted and committed internally, your code should be live on GitHub in, at most, 30 minutes later (unless the job catches a failure, like a build error). In addition, this also allows the individual diffs that we write internally to be pushed to you much faster, closer to real-time, instead of in one sweeping push with a bunch of the day's diffs.

This job syncs all new code from the time of the last GitHub commit, does some git commit message housekeeping to prepare it for GitHub, builds and tests the code automatically, and, assuming all went well in those previous steps, [pushes the code to the master branch](https://github.com/facebook/hhvm/commits/master).

Not every pull request is accepted. And there are times when pull requests take a while to get reviewed (either due to issues with the code changes in general or with issues internally on our end). However, we hope those cases are the exceptions. We want to accept as many pull requests as provided to us (either as-is or with some modification). And we believe that getting your code into the master branch quickly will hopefully help show how much we appreciate your contributions.

Now, if there was only a way we could get your pull requests reviewed faster and more openly.... Hmmm... ;)
