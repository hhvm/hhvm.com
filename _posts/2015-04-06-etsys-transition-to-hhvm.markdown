---
author: jwatzman
comments: true
layout: post
title: Etsy's Transition to HHVM
category: blog
permalink: /blog/8939/etsys-transition-to-hhvm
---

Dan Miller, an engineer at Etsy, wrote an [extensive blog post detailing Etsy's transition to HHVM](https://codeascraft.com/2015/04/06/experimenting-with-hhvm-at-etsy/) on some of their production servers.

<!--truncate-->

They saw significant decrease in response time:

![HHVM vs PHP 5.5 Response Time](/static/images/posts/Screen-Shot-2015-04-05-at-8.34.13-PM-1024x572.png)

as well as a significant increase in maximum load before response time began to suffer:

![Response Time as Load Increases](/static/images/posts/Screen-Shot-2015-04-04-at-10.19.45-AM-1024x575.png)

Beyond just raw performance, the blog post also talks about some of the other features of HHVM, such as its built-in debugger and performance profiling tools. I highly recommend [reading the entire post for all the details](https://codeascraft.com/2015/04/06/experimenting-with-hhvm-at-etsy/)!

Success stories like these are why Facebook open-sourced HHVM, and continues to be committed to it as an open-source project. Helping other people and companies scale their technology helps connect the world, and is why I personally love doing what I'm doing.

[Read more at the Code as Craft blog: "Experimenting with HHVM at Etsy"](https://codeascraft.com/2015/04/06/experimenting-with-hhvm-at-etsy/)
