---
author: jwatzman
comments: true
layout: post
title: Hack Community Roundup
category: blog
permalink: /blog/4811/hack-community-roundup
---

In the weeks since the Hack open source launch and the Hack developer day, there has been a lot of information, code, blog posts, etc coming from our nascent community. To us on the team, it's been incredible and encouraging to see the community reception to Hack. Here are some of the highlights of the things we've seen come out of our community. (And we almost certainly haven't seen everything, so please let us know in the comments what we've missed!)

<img src="/static/logo.svg" alt="Hack Logo" style="width: 200px;"/>

<!--truncate-->

## Github Projects


  * The folks at PocketRent, some of the earliest adopters of Hack, have [a small Hack framework](https://github.com/PocketRent/beatbox). Even if you aren't interested in using it directly, there are great examples of everything from XHP to async functions.


  * Victor Berchet has released a [Vagrant configuration](https://github.com/vicb/hhvm-vagrant) to help get HHVM and Hack up and running in a VM as quickly as possible. Many folks have had trouble getting HHVM and Hack up and running, and while we're trying to improve that process moving forward, if you're one of those folks, you may want to give it a try.


  * Emre Sokullu built and released [hack-mvc](https://github.com/esokullu/hack-mvc), a small MVC framework for Hack. He also [wrote a blog post](https://medium.com/p/b0acd5bcd135) discussing his motivation behind using HHVM and Hack.


  * Brian Scaturro has begun work on [HackUnit, an xUnit testing framework](https://github.com/brianium/hack-unit) written in Hack.


  * For deployment, the folks at Heroku have [first-class support for HHVM and Hack](https://blog.heroku.com/archives/2014/4/29/introducing_the_new_php_on_heroku), and have [contributed instructions to our Hack example site](https://github.com/hhvm/hack-example-site#example-setup-for-heroku) on how to get it running on Heroku.




## Presentations






  * For the visually inclined, Charles Zink has made a [YouTube video demonstrating how to get HHVM, Hack, and Nginx all playing nice on Debian 7](https://www.youtube.com/watch?v=1mxry6KRBEQ).


  * Christian Stocker gave a presentation on [HHVM, Hack, and his experiences using them in production](https://speakerdeck.com/chregu/hiphop-virtual-machine-hhvm-for-php-and-the-hack-language).




## Blog Posts






  * Several folks posted their reactions to our Hack dev day. Jeremy Mikola wrote [an extensive summary of each of the talks](http://jmikola.net/blog/hack-dev-day/), which is highly recommended if you don't have time to watch [all of the videos](https://www.youtube.com/watch?v=BnJQJNGkUdM&index=3&list=PLb0IAmt7-GS2fdbb1vVdP8Z8zx1l2L8YS). On the other hand, Michael Curry has [a nice short post picking out just his highlights from the day](http://kernelcurry.com/blog/facebooks-hack-developer-day-2014/).


  * Before the Hack release, Victor Berchet wrote a series on the Hack language ([part 1](http://www.sitepoint.com/hhvm-hack-part-1/), [part 2](http://www.sitepoint.com/look-hack-php-replacement-hhvm/)). He's got lots of good information on the Hack type system and what it might mean for current PHP developers. Just keep in mind it was written before the official release, and so many of the things listed as "not documented" should in fact now [be well documented](http://docs.hhvm.com/manual/en/index.php).


  * Davey Shafik at EngineYard wrote an excellent [survey of Hack language features](https://blog.engineyard.com/2014/hhvm-hack-php) as the third part in a blog series about HHVM ([part 1](https://blog.engineyard.com/2014/hhvm-hack), [part 2](https://blog.engineyard.com/2014/hhvm-hack-part-2)).


  * FastCompany Labs [ran a nice story on Hack and its motivation](http://www.fastcolabs.com/3028778/why-facebook-invented-a-new-php-derived-language-called-hack), including interviews with Hack tech lead Julien Verlaguet and HHVM tech lead Ed Smith. Similarly, O'Reilly Programming [ran a blog post discussing Hack and its coexistence with PHP](http://programming.oreilly.com/2014/04/facebooks-hack-hhvm-and-the-future-of-php.html). Finally, Programmable Web [ran a short overview of Hack](http://blog.programmableweb.com/2014/04/10/facebooks-hack-language-speeds-up-development-cycle/), also including quotes from Hack tech lead Julien Verlaguet.


Again, thanks to everyone who has created the information above, and to everyone who is already trying Hack. I've personally always been excited for what this technology could do to improve developers' lives, and am looking forward to helping to grow the fledgling Hack community.
