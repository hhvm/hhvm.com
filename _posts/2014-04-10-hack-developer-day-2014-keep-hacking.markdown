---
author: joelm
comments: true
layout: post
title: 'Hack Developer Day 2014: Keep Hacking'
category: blog
redirect_from:
  - /blog/4685/hack-developer-day-2014-keep-hacking
---

A few weeks ago, the Hack language was [launched to the world](http://hhvm.com/blog/4223/introducing-hack-a-programming-language-for-hhvm). Yesterday, we held the first [Hack Developer Day](https://www.facebook.com/groups/hackdevday14/) in Menlo Park, California. 150+ Members of the PHP and developer community came to Facebook headquarters and joined over 2000 people online for presentations by the engineers of Hack and HHVM. Afterwards we held a five hour hackathon, where the attendees worked with those engineers to write Hack code, either by converting current codebases or writing new code from scratch. By the way, bonus points to anyone who can decrypt the [commit message](https://github.com/facebook/hhvm/commit/d50dd15bc34c60a4bcc02dc6bd95fdf32effc54b) used when [Josh](https://github.com/jwatzman) originally pushed Hack to open source.

For those who couldn't attend, here are the videos of all the presentations...

[![Hack Developer Days](/static/images/posts/hack-dev-days.png)](https://www.youtube.com/embed/videoseries?list=PLb0IAmt7-GS2fdbb1vVdP8Z8zx1l2L8YS)

... and [click here for the PDFs of the slides](https://www.facebook.com/groups/hackdevday14/permalink/1438148983090884/).

There is [an official recap of the event](https://code.facebook.com/posts/683726355017955/hack-developer-day-recap/) on the Facebook Engineering blog, but let me try to provide you a few points that really resonated with me, and I hope many of the attendees:


  * We really strived to make Hack as unobtrusive as possible by providing a lot statically typed functionality without negatively impacting your fast workflow.


  * Hack features like [Collections](http://docs.hhvm.com/manual/en/hack.collections.php) and [async/await](http://docs.hhvm.com/manual/en/hack.async.php) were received very well and I believe will end up being an integral part of a Hack developer's toolbox.


  * Tools such as the [Hackificator](https://github.com/facebook/hhvm/tree/master/hphp/hack/tools), while not a panacea, can really help you with code conversions.


  * We are working super hard to make HHVM a really great runtime for PHP. Just check out our[ frameworks compatibility page](http://hhvm.com/frameworks/) to understand how serious we are.


  * Our community is awesome. Plain and simple. And we want to make working with Hack and HHVM awesome for them. So we are doing all we can to be even more open (e.g., we are implementing an open review process; bye-bye pull requests).


  * Let it not be forgotten that we are always trying to make HHVM more efficient and run your code faster.


  * FBIDE is really nice, and can make learning and using Hack so much easier. I am really looking forward to its release. What is FBIDE, you might ask? See the [video](https://www.youtube.com/watch?v=UCR4Ac6z_l0&list=PLb0IAmt7-GS2fdbb1vVdP8Z8zx1l2L8YS&index=9) or [recap](https://code.facebook.com/posts/683726355017955/hack-developer-day-recap/) to learn more about this nugget of information.


Simply put, the day was good times all around. And, as one attendee put it, "Keep Hacking!"
