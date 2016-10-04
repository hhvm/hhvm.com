---
author: jwatzman
comments: true
layout: post
title: LTS Updates
category: blog
permalink: /blog/7349/lts-updates
---

I just pushed HHVM 3.3.2 (and 3.4.2) onto the Debian and Ubuntu repositories. It contains fixes backported from PHP for several security issues that HHVM was also vulnerable to, as well as a fix for CVE-2014-9370, which is a header injection issue affecting only the deprecated built-in webserver. Most users of HHVM use FastCGI, which was not affected by CVE-2014-9370.

<!--truncate-->

Normally minor version updates wouldn't warrant a blog post, but we've had a lot of questions about how to stick to a particular [LTS release](http://hhvm.com/blog/6083/hhvm-long-term-support), since our current setup will always upgrade you to the newest stable release, with no way to stick to an LTS and still get its updates! This is particularly important given the security content of this release.

To fix this, I've recently defined several extra "distributions" in our Debian and Ubuntu repos on `dl.hhvm.com`. In order to use them, suffix your normal distribution with `-lts-3.3`. So, for example, if you are using Ubuntu 14.04 "trusty", you will have a line like this in your `/etc/apt/sources.list`:



`$ deb http://dl.hhvm.com/ubuntu trusty main`

To stay with the 3.3 LTS and get only LTS updates, change it to:


`$ deb http://dl.hhvm.com/ubuntu trusty-lts-3.3 main`


[Full information on our LTS releases is on the GitHub wiki.](https://github.com/facebook/hhvm/wiki/Long-term-support-%28LTS%29)
