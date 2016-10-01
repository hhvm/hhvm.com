---
author: ptarjan
comments: true
layout: post
title: Nightly Packages
category: blog
redirect_from:
  - /blog/3203/nightly-packages
---

If you just can't wait to get your hands on the latest HHVM code, but you don't want to spend the time to compile it, we have a present for you.

<!--truncate-->

Every midnight, we [run a script](https://github.com/hhvm/packaging/blob/master/hhvm/deb/package) that pulls whatever is in [master](https://github.com/facebook/hhvm/commits/master), compiles it, does a sanity check, builds a package and sends it off to the repo. You can then use it by adding the [HHVM repo normally](https://github.com/facebook/hhvm/wiki#installing-pre-built-packages-for-hhvm) and then installing the "`hhvm-nightly`" package instead of the "`hhvm`" package. The nightly package should work identically to the current [8 week release cycle](https://github.com/facebook/hhvm/wiki/Release-Schedule) package; it will just have all the most recent commits with much less of the testing and hardening (so beware). While we pride ourselves in having master always passing the full test suite, bugs can obviously creep in, so please don't run your production site on a nightly. When you are about to report an issue, please check that it hasn't already been fixed by the nightly package.

(Update) All our [supported distros](https://github.com/facebook/hhvm/wiki/Prebuilt%20Packages%20for%20HHVM) now have nightlies.

For now, there are only Ubuntu LTS (12.04), Ubuntu most recent (13.10) and Debian stable (7). We will consider others if there is enough desire. Comment below if you want another distro and would actively use "`hhvm-nightly`".

For Ubuntu 12.04:


    sudo add-apt-repository ppa:mapnik/boost
    wget -O - http://dl.hhvm.com/conf/hhvm.gpg.key | sudo apt-key add -
    echo deb http://dl.hhvm.com/ubuntu precise main | sudo tee /etc/apt/sources.list.d/hhvm.list
    sudo apt-get update
    sudo apt-get install hhvm-nightly


For Ubuntu 13.10:


    wget -O - http://dl.hhvm.com/conf/hhvm.gpg.key | sudo apt-key add -
    echo deb http://dl.hhvm.com/ubuntu saucy main | sudo tee /etc/apt/sources.list.d/hhvm.list
    sudo apt-get update
    sudo apt-get install hhvm-nightly


For Debian 7:


    wget -O - http://dl.hhvm.com/conf/hhvm.gpg.key | sudo apt-key add -
    echo deb http://dl.hhvm.com/debian wheezy main | sudo tee /etc/apt/sources.list.d/hhvm.list
    sudo apt-get update
    sudo apt-get install hhvm-nightly
