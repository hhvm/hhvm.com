---
author: ptarjan
comments: true
layout: post
title: HHVM on Heroku
category: blog
redirect_from:
  - /blog/1379/hhvm-on-heroku
---

Do you use [heroku](http://heroku.com) to host your PHP app and want to save 2x-10x dynos? Or serve user requests 2x-10x faster? I'm happy to announce that you can now use HHVM on heroku. You should clone your app and try it out before pushing to production as HHVM doesn't support [every possible use of PHP](http://www.hhvm.com/blog/875/wow-hhvm-is-fast-too-bad-it-doesnt-run-my-code) (yet).

To use it with a new app:


    heroku create --buildpack https://github.com/hhvm/heroku-buildpack-hhvm


Or to convert your existing PHP app (once you tested it works on HHVM):


    heroku config:set BUILDPACK_URL=https://github.com/hhvm/heroku-buildpack-hhvm
    <make some git change and commit it>
    git push


The hardest part of this whole endeavor was getting HHVM to compile on [Ubuntu 10.04](https://github.com/facebook/hhvm/wiki/Building-and-installing-on-Ubuntu-10.04-LTS), but once that worked it was smooth sailing. If you want to dive into the nitty gritty details you can [read the source](https://github.com/hhvm/heroku-buildpack-hhvm).

A huge thanks to [@pvh](https://twitter.com/pvh) for hosting us at heroku and hacking on this for a day. And to[ Claudiu Ceia](https://www.facebook.com/wtf.no.username) for writing the .hdf linter and all his work throughout this project.

If you have any issues with the heroku part, open issues on the [heroku buildpack issue tracker](https://github.com/hhvm/heroku-buildpack-hhvm/issues) and if you have any issues with HHVM running your code open issues on the [HHVM issue tracker.](https://github.com/facebook/hhvm/issues) And if you can make this integration better in any way, please fork and send pull requests.
