---
author: joelm
comments: true
layout: post
title: 'Locking Down for Performance and Parity '
category: blog
redirect_from:
  - /blog/1499/locking-down-for-performance-and-parity
---

The HHVM team, along with our wonderful [open source](https://github.com/facebook/hhvm) contributors, is constantly trying to [improve the runtime](http://www.hhvm.com/blog/1301/hhvm-2-2-0). We know, however, that there is work to do to [run the world's PHP code reliably and consistently](http://www.hhvm.com/blog/875/wow-hhvm-is-fast-too-bad-it-doesnt-run-my-code).

<!--truncate-->

Every 6 months or so, the HHVM team goes into _lockdown_. Lockdown is a Facebook tradition where a team picks a few concentrated areas and pushes hard on them. The team is huddled together. No meetings. Specific task focused. Shaving is discouraged.

The HHVM team's latest Lockdown started on Monday. It is a 3-week effort focused entirely on two things: performance and parity.

![We want performance to rise even further](/static/images/posts/Screen-Shot-2013-11-06-at-5.16.45-PM1.png)
<center><i>We want performance to rise even further</i></center>

![We want to pass unit tests for as many frameworks as possible](/static/images/posts/Screen-Shot-2013-11-06-at-5.29.58-PM1.png)
<center><i>We want to pass unit tests for as many frameworks as possible</i></center>

The first graph is our performance graph. The second graph is our parity graph, and the percentages are unit tests passing per framework. Simply put, by the end of the three weeks, we want to have had each graph move up and to the right. (_Note_: The dip you see in the parity graph is our [unit test script](https://github.com/facebook/hhvm/tree/master/hphp/test/frameworks) misbehaving. The script is being continuously modified to make our testing better and more valuable).

The stickies below are an example of the individual tasks to get us there. We have prioritized them by impact (e.g., number of unit tests that will pass upon completion of the task) and length (how many days the task will take to complete). If these stickies are moved to the "Done" column, the graphs should respond favorably.

![If we finish these tasks, we will meet our parity goal](/static/images/posts/2013-10-31-17.33.041.jpg)
<center><i>If we finish these tasks, we will meet our parity goal</i></center>


The HHVM team really cares about maintaining a high quality runtime for PHP. At the end of the three weeks, the no shaving mantra having fully taken hold, we are hoping you see a much better HHVM in terms of being able to accurately run a broader array of PHP code, very fast. Stay tuned for the results of this lockdown.

![Here are some of the team members during the first week of lockdown. The no shaving mantra is being adhered to.](/static/images/posts/2013-11-07-14.11.131.jpg)
<center><i>Here are some of the team members during the first week of lockdown. The no shaving mantra is being adhered to.</i></center>
