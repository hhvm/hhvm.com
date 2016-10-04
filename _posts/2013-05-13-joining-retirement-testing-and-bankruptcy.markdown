---
author: ptarjan
layout: post
title: Joining, Retirement, Testing, and Bankruptcy
category: blog
permalink: /blog/575/joining-retirement-testing-and-bankruptcy
comments:
- id: 479
  author: Joseff B
  date: '2013-05-17 20:49:33 +0000'
  date_gmt: '2013-05-18 03:49:33 +0000'
  content: Hi I'm wondering if Mongo DB is supported now since you closed all the
    Mongo DB tickets.
- id: 485
  author: Rocky Sharma
  date: '2013-06-28 08:16:32 +0000'
  date_gmt: '2013-06-28 15:16:32 +0000'
  content: URL-Rewriting at some point is ache !
---

First of all, hi. I recently joined the team as you could probably see from my [plethora](https://github.com/facebook/hiphop-php/graphs/contributors) of commits to github. I first fixed up [closures a bit](https://github.com/facebook/hiphop-php/commit/4d7004e955c764c5e7474c4b366d3606348f61eb) and moved our "PHP tests in C++" [to have one fewer language](https://github.com/facebook/hiphop-php/commit/eca135cb31b54c4e69fc09f73c8756846f18b935). I'll be doing many exciting things for hiphop but I'll be mostly caring about making it incredibly easy for anyone to use for any PHP code. So please bug me if it doesn't run your favorite piece of code.

<!--truncate-->

As you can see from our [graphs](https://github.com/facebook/hiphop-php/graphs/code-frequency), lots of code has been flowing lately. The first major thing, is we deleted almost all of HPHPc. It has been [fully replaced](https://www.facebook.com/notes/facebook-engineering/speeding-up-php-based-development-with-hiphop-vm/10151170460698920) by HHVM. We no longer do source level transforms to C++, instead the backend is now a just-in-time compiled virtual machine. It is faster, allows for iterative development, and opens us up for many optimizations in the future. If there is leftover dead code, please send in pull requests.

The was also a major addition in the graphs. We imported almost all of php.net's tests. [8446 in total](https://github.com/facebook/hiphop-php/tree/master/hphp/test/zend). We want to keep an eye on how we compare, and we'll work hard over the next few months to move more from [bad](https://github.com/facebook/hiphop-php/tree/master/hphp/test/zend/bad) to [good](https://github.com/facebook/hiphop-php/tree/master/hphp/test/zend/good). We aren't trying for parity on error messages but we are striving to be able to run all major PHP software. If you fix a compatibility issue, please move the test from bad to good.

As you can see, we have over 300 issues on github. We've been keeping abreast of the current issues and pull requests, but we just haven't gotten into our backlog. Many of them are for HPHPc, and many others don't have good repro cases. To help us not end up in [broken window syndrome](http://en.wikipedia.org/wiki/Broken_windows_theory), we're going to be closing all bugs older than 2 months. If yours is still an issue, please re-open it, and in order of goodness:




  1. Give detailed repro steps


  2. Write a test case in [hphp/tests/quick](https://github.com/facebook/hiphop-php/tree/master/hphp/test/quick) (run it with [hphp/tests/run](https://github.com/facebook/hiphop-php/blob/master/hphp/test/run)) and send the pull request


  3. Fix it in a pull request




On that note, I'd like to chat briefly about pull requests. For hiphop to accept your code, you must fill out the [CLA](https://developers.facebook.com/opensource/cla). It is super quick and you only have to fill it out once for all our open source projects. Also, we don't directly merge in your code. We copy it into our internal [code review](http://phabricator.org/) tool, do a ton of perf and unit testing, and then it will appear as a commit authored by you after that. It is just much easier and safer for us to run all our internal testing on it before merging it in.


Thanks for listening. I hope this helps keep issues that are current at the front of our minds as we improve hiphop. Please keep sending issues and pull requests as much as possible.
