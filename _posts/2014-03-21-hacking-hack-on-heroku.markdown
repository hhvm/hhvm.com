---
author: ptarjan
comments: true
layout: post
title: Hacking Hack on Heroku
category: blog
redirect_from:
  - /blog/4325/hacking-hack-on-heroku
---

Yesterday, after our [Hack announcement,](http://hhvm.com/blog/4223/introducing-hack-a-programming-language-for-hhvm) we sat down with the heroku team to get Hack working on Heroku. And success! Read all about it over on the [heroku blog](https://blog.heroku.com/archives/2014/3/21/hacking_hack_on_heroku).

<!--truncate-->

First make an `index.php` file:


    <code><?hh

    echo "Hello from HHVM ".HHVM_VERSION;
    </code>


Then create a git repo, add the file, create our Heroku app and deploy away:


    <code>$ git init .
    Initialized empty Git repository in /tmp/myhackapp/.git/
    $ git add index.php
    $ git commit -m 'initial'
    [master (root-commit) 024f2b1] initial
     1 file changed, 3 insertions(+)
     create mode 100644 index.php
    $ heroku create --buildpack https://github.com/hhvm/heroku-buildpack-hhvm
    Creating stormy-crag-8213... done, stack is cedar
    BUILDPACK_URL=https://github.com/hhvm/heroku-buildpack-hhvm
    http://stormy-crag-8213.herokuapp.com/ | git@heroku.com:stormy-crag-8213.git
    …
    </code>


And then we can check and see that it worked:


    <code>$ heroku open
    </code>


Send any issues to us on our [buildpack repo](https://github.com/hhvm/heroku-buildpack-hhvm).
