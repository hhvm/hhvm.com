---
author: sgolemon
layout: post
title: Getting WordPress running on HHVM
category: blog
permalink: /blog/3095/getting-wordpress-running-on-hhvm
comments:
- id: 17
  author: Sandeep
  date: '2012-10-08 16:21:12 +0000'
  date_gmt: '2012-10-08 23:21:12 +0000'
  content: Nice blog and well documented.
- id: 23
  author: Go Faster! | HipHop for PHP
  date: '2012-10-22 11:40:06 +0000'
  date_gmt: '2012-10-22 18:40:06 +0000'
  content: "[...] Post navigation &larr; Previous [...]"
- id: 29
  author: Vadim Sigaev
  date: '2012-11-13 17:43:04 +0000'
  date_gmt: '2012-11-14 01:43:04 +0000'
  content: |-
    Very nice post, but please tell, where i can find documentation on HHVM for future reading?
    First of all, is it somewhere specification about hhvm.hdf structure?
    And also it's very interesting to read about debugging features.
- id: 35
  author: sgolemon
  date: '2012-11-14 17:24:23 +0000'
  date_gmt: '2012-11-15 01:24:23 +0000'
  content: |-
    At the moment, all the real documentation is in git under the doc&#47; directory, but it's a bit dry and hard to read casually.

    I plan to publish a version of the PHP manual with HipHop details merged in where appropriate (particularly under configuration and runtime variances).

    https:&#47;&#47;github.com&#47;facebook&#47;hiphop-php&#47;tree&#47;master&#47;doc
- id: 41
  author: heinhtetaung
  date: '2012-11-16 10:13:52 +0000'
  date_gmt: '2012-11-16 18:13:52 +0000'
  content: "i did everything you say ..\nafter that src&#47;hhvm&#47;hhvm --mode daemon
    --user web --config &#47;etc&#47;hhvm.hdf\nnothing happend. \ni try other \nsrc&#47;hhvm&#47;hhvm
    test.php --mode s --port 8080\nmapping self...n\nmapping self took 0'00\" (36559
    us) wall timen\nloading static content...n\nsearching all files under source root...\nanalyzing
    9526 files under source root...\nloaded 0 bytes of static content in total\nloading
    static content took 0'00\" (75376 us) wall timen\ncould not allocate 1210089471
    bytes for translation cache\nwhat's wrong ?"
- id: 47
  author: sgolemon
  date: '2012-11-16 15:58:52 +0000'
  date_gmt: '2012-11-16 23:58:52 +0000'
  content: |-
    In the case of the first attempt, can you define: "Nothing happened"?  Nothing should appear to happen on the command line since you're starting up the server and it's sitting around waiting for web requests.  Does `ps ax` show it running? Do you get anything when trying to browse to that server with your webbrowser?

    On the second one, you're mixing verbs.  You've selected `--mode server` which is going to make HHVM try to load up a whole directory full of files (though you haven't specified which directory).  What you have done is a pass a single file name with is more appropriate to just running as a command-line script (without passing the --mode server flag).
- id: 53
  author: heinhtetaung
  date: '2012-11-16 18:53:58 +0000'
  date_gmt: '2012-11-17 02:53:58 +0000'
  content: "thank you for your reply , i already check `ps ux ` . i dont see that
    process and any listen port 80 . i try mode server ,  \n src&#47;hhvm&#47;hhvm
    --mode s --user web --config &#47;etc&#47;hhvm.hdf\ncould not allocate 1210089471
    bytes for translation cache"
- id: 59
  author: rynop
  date: '2012-11-29 18:27:25 +0000'
  date_gmt: '2012-11-30 02:27:25 +0000'
  content: First off thanks for all the hard work.  Do you have a list of the php
    extensions you support? I'm wondering if things like APC, cURL, memcache, pdo
    MySQL etc are supported. I found https:&#47;&#47;github.com&#47;facebook&#47;hiphop-php&#47;wiki&#47;Extensions-and-modules-roadmap
    but its a bit outdated (last mod 2yrs ago).
- id: 65
  author: Steve McNally
  date: '2012-11-29 18:45:13 +0000'
  date_gmt: '2012-11-30 02:45:13 +0000'
  content: 'Thanks for sharing this with the community.  I''m reading the more general
    hhvm update info, too.  Q: the hhvm is concerned "exclusively" with php execution
    time? are there db-layer improvements, too?'
- id: 71
  author: Lewis Cowles
  date: '2012-11-30 00:06:44 +0000'
  date_gmt: '2012-11-30 08:06:44 +0000'
  content: |-
    Are there many benefits to using Wordpress under HHPHP? Any stats? Also what about other libraries like Codeigniter.

    Lastly what version of PHP is HHPHP compatible with?
- id: 77
  author: Nick_vh
  date: '2012-11-30 03:53:22 +0000'
  date_gmt: '2012-11-30 11:53:22 +0000'
  content: |-
    Well, I tried to get it running with Drupal, but somehow it seems to be lacking a lot of verbose output to help you understand where it goes wrong

    I documented the whole process below and used vagrant to made sure that my machine was not corrupt.
    http:&#47;&#47;nickveenhof.be&#47;blog&#47;getting-drupal-7-almost-running-hhvm

    The server started in daemon mode, and then shows a message "Not Found". It also does not report anything in the error.log (while it does have write access)

    I'd appreciate if there were more runtime debug modes? Perhaps it could be ran in --mode server and show the errors in the terminal? Perhaps I'm not seeing the obvious?
- id: 83
  author: Nick_vh
  date: '2012-11-30 04:13:53 +0000'
  date_gmt: '2012-11-30 12:13:53 +0000'
  content: "Ok, I played with it even more and it seems that it might be that HHVM
    does not support some php extensions yet such as PDO? Is that right?\n\nAfter
    figuring out how to debug it, I posted the stacktrace in my blog mentioned above\n\nFor
    others : \nsudo hhvm --config &#47;etc&#47;hhvm.hdf --user YOUR_WEB_USER --mode
    daemon -v \"Log.Level=Verbose\" -v \"Log.NoSilencer=on\" -v \"Log.Header=on\"\ntail
    -f &#47;var&#47;log&#47;hhvm&#47;error.log\n\nDon't forget to kill to process
    if you want to try it again."
- id: 89
  author: rynop
  date: '2012-11-30 14:10:16 +0000'
  date_gmt: '2012-11-30 22:10:16 +0000'
  content: "Here they are: https:&#47;&#47;github.com&#47;facebook&#47;hiphop-php&#47;tree&#47;master&#47;src&#47;runtime&#47;ext\n\nI'm
    trying to start via:\nryan: sudo &#47;usr&#47;bin&#47;hhvm --mode daemon --user
    \"www-data\" --config &#47;etc&#47;hhvm.hdf\n\nBut I keep getting the following
    errors:\ncat error.log \nFailed to initialize central HHBC repository at '&#47;home&#47;ryan&#47;.hhvm.hhbc'\nFailed
    to initialize central HHBC repository at '&#47;var&#47;www&#47;.hhvm.hhbc'\n\nGot
    any pointers on where I can read about how to configure where this .hhvm.hhbc
    goes?  its not in index.php?file=options.compiled . Also why is it trying to write
    anything to the user im logged in as dir? i specified --user \"www-data\" and
    am launching cmd via sudo..."
- id: 95
  author: Rod Salazar
  date: '2012-12-01 02:04:58 +0000'
  date_gmt: '2012-12-01 10:04:58 +0000'
  content: "It's pretty clear what is wrong, there is not enough memory for the translation
    cache, as specified by that error! \n\n'could not allocate 1210089471 bytes for
    translation cache'\n\nThe hhvm daemon is also spitting out that error except you
    can't see it because it is a daemon process."
- id: 101
  author: rynop
  date: '2012-12-01 17:39:36 +0000'
  date_gmt: '2012-12-02 01:39:36 +0000'
  content: http:&#47;&#47;www.hiphop-php.com&#47;wp&#47;?p=257 explains all about
    hhbc. Sorry for all the posts. Hopefully this saves the next person time in connecting
    the dots.
- id: 107
  author: sgolemon
  date: '2012-12-03 16:00:26 +0000'
  date_gmt: '2012-12-04 00:00:26 +0000'
  content: Yeah, sounds like you got it figured out.  Sorry for the delay getting
    back to you.
- id: 113
  author: sgolemon
  date: '2012-12-03 16:02:22 +0000'
  date_gmt: '2012-12-04 00:02:22 +0000'
  content: Correct.  HipHop is just about speeding up the PHP execution time portion
    of the stack.  db-layer speed-ups (which is the first thing anyone should address)
    are out of scope, but I'm sure you'll find many posts on technique involving memcached,
    judicious use of indexes, etc... for that.
- id: 119
  author: sgolemon
  date: '2012-12-03 16:06:02 +0000'
  date_gmt: '2012-12-04 00:06:02 +0000'
  content: |-
    Our (unpublished) stats say that facebook.com would require aproximately 6x as many front-end machines if we were using stock PHP. ((Note that the FB codebase is tightly tuned to HipHop))  I've also got some numbers showing hiphop&#47;repojit performing at about 4:1 for more generic codebases like Wordpress.

    Beyond speed, there's the differences in what we're doing with the language syntax itself.  HipHop had generators long before PHP (php.net just added these for 5.5), and we've got a strict typing implementation on its way down the pipe which should improve development a bit.
- id: 125
  author: sgolemon
  date: '2012-12-03 16:07:10 +0000'
  date_gmt: '2012-12-04 00:07:10 +0000'
  content: |-
    As replied on your blog (and twitter), I didn't see the same issues as you, primarily because I ran into other problems at an earlier stage with the lack of support for custom stream wrappers.

    Short version: Yes, drupal and hiphop aren't friends at this point.  We'll have to do some work there.
- id: 131
  author: rynop
  date: '2012-12-03 18:48:24 +0000'
  date_gmt: '2012-12-04 02:48:24 +0000'
  content: Np. Prob not the right place to ask this question is - but wondering if
    you could touch on the following topics in future blog posts  1) how does FB store
    session data across nodes? You back your sessions with memcache?  2) Also wondering
    how you roll out code updates and "warm" up the cache&#47;clear old cache without
    disrupting incoming requests.  With apc+fpm I just clear the opcode and requests
    in flight are not impacted, while new requests get the code updates. I'm still
    not clear on how this works in the wild with HHVM+JIT. Do you just run '&#47;usr&#47;bin&#47;hhvm-analyze'
    , copy the &#47;tmp&#47;hphp_XXXXX&#47;hhvm.hhbc.sq3 to 'Repo {  Central {    Path'
    and kill&#47;start the &#47;usr&#47;bin&#47;hhvm?
- id: 137
  author: sgolemon
  date: '2012-12-07 19:22:55 +0000'
  date_gmt: '2012-12-08 03:22:55 +0000'
  content: |-
    Yeah, this isn't the spot to going into it, besides I'm sure it's already been covered on the Facebook Engineering Blog: https:&#47;&#47;www.facebook.com&#47;Engineering?sk=notes

    If you still have trouble finding it, I'll ask around for some more specific links.
- id: 143
  author: Victor
  date: '2013-01-27 15:03:02 +0000'
  date_gmt: '2013-01-27 23:03:02 +0000'
  content: Is there any way to create a friendly url's system using HHVM? I've changed
    the RewriteRule but I could only call the GET of the page, with no success in
    calling css and js's files and folders. Is there any solution to the directives
    &ldquo;RewriteCond %{SCRIPT_FILENAME} !-f&rdquo; and &ldquo;RewriteCond %{SCRIPT_FILENAME}
    !-d&rdquo; on HHVM?
- id: 149
  author: Eric
  date: '2013-02-25 01:37:44 +0000'
  date_gmt: '2013-02-25 09:37:44 +0000'
  content: |-
    I'm using Ubuntu 12.10 and compiled HHVM using the guide at the wiki.
    I tend to use the laravel framework for my webpages; however, functons such as function_exists()&#47;class_exists() isn't supported.

    I saw that they were supported using the --hphp -v "AllVolatile=true" option. But that requires me to use "old" hphp, right? Which isn't going to be supported after mid 2013?

    Is there by any chanse, possible, to use those functions, using HHVM?
- id: 155
  author: Alex Babira
  date: '2013-04-13 07:01:26 +0000'
  date_gmt: '2013-04-13 14:01:26 +0000'
  content: "I used the pre built binary to get hip hop from here\n\nhttps:&#47;&#47;github.com&#47;facebook&#47;hiphop-php&#47;wiki&#47;Prebuilt-packages-on-ubuntu-12.04\n\nof
    course i run it on ubuntu 12.04 lts. The problem is hhvm is not starting \nsudo
    &#47;usr&#47;bin&#47;hhvm --mode daemon --user \"my user\" --config &#47;etc&#47;hhvm.hdf
    \ndoes nothing..... \"netstat -tulpn\" does not display anything waiting on port
    80 or whatever port I assign to HHVM via the conf file, \"ps aux\" does not display
    any processes related to hhvm, the wierd thing is that when i try to run hhvm
    in verbose mode i get some messages in my error.log but they dont seem to be errors
    here are the lines that get printed\n\n[Sat Apr 13 23:01:06 2013] [hphp] [2526:7f7369430e40:0:000001]
    [] mapping self...\n[Sat Apr 13 23:01:06 2013] [hphp] [2526:7f7369430e40:0:000002]
    [] mapping self took 0'00\" (55495 us) wall time\n[Sat Apr 13 23:01:06 2013] [hphp]
    [2526:7f7369430e40:0:000003] [] loading static content...\n[Sat Apr 13 23:01:06
    2013] [hphp] [2526:7f7369430e40:0:000004] [] searching all files under source
    root...\n[Sat Apr 13 23:01:06 2013] [hphp] [2526:7f7369430e40:0:000005] [] analyzing
    1 files under source root...\n[Sat Apr 13 23:01:06 2013] [hphp] [2526:7f7369430e40:0:000006]
    [] loaded 0 bytes of static content in total\n[Sat Apr 13 23:01:06 2013] [hphp]
    [2526:7f7369430e40:0:000007] [] loading static content took 0'00\" (2442 us) wall
    time\n\nI am guessing that's because of the log level,(Note that the root in this
    case is just a simple index.php file containing an echo statement, not wordpress)."
- id: 161
  author: Facebook&#8217;s HipHop Engine, When to Use it, and Getting it to Work with
    CodeIgniter | Kyle Boddy
  date: '2013-05-02 15:31:18 +0000'
  date_gmt: '2013-05-02 22:31:18 +0000'
  content: "[...] After that, test your chops by downloading, installing, and configuring
    WordPress with hhvm. [...]"
- id: 167
  author: Adrian
  date: '2013-05-06 15:33:57 +0000'
  date_gmt: '2013-05-06 22:33:57 +0000'
  content: "Pardon my ignorance on this but I have a pretty basic question. \nDoes
    running an application on hiphop require Apache (or other web server) and php
    installed or hiphop provides that functionality.\n\nSo Install Apache, install
    php, install mysql - then install hiphop?"
- id: 173
  author: sgolemon
  date: '2013-05-11 09:34:40 +0000'
  date_gmt: '2013-05-11 16:34:40 +0000'
  content: |-
    Well, HipHop *is* an implementation of PHP, so no: You don't need PHP installed.

    It's also got it's own web server built in.  Notice how the "Configuring" section talks about port numbers and virtual hosts and logging?  So no to that as well.  You *can* put Apache in front of HipHop if you need access to some of the additional feature Apache has, but in that case Apache would just be proxying to HipHop's web server.
- id: 179
  author: sgolemon
  date: '2013-05-11 09:35:55 +0000'
  date_gmt: '2013-05-11 16:35:55 +0000'
  content: Where did you get the idea they weren't supported?
- id: 185
  author: Adrian
  date: '2013-05-20 22:44:03 +0000'
  date_gmt: '2013-05-21 05:44:03 +0000'
  content: |-
    I compile and installed word press the other day. It was much certainly quicker.
    I am assuming that under load it would continue to outperform standard php and apache installs. It will be interesting to watch it mature over the next few years.
- id: 191
  author: Adrian
  date: '2013-05-20 22:45:38 +0000'
  date_gmt: '2013-05-21 05:45:38 +0000'
  content: that link is broken
- id: 197
  author: George Jempty
  date: '2013-06-11 06:53:00 +0000'
  date_gmt: '2013-06-11 13:53:00 +0000'
  content: |-
    options.compiled link is broken, it's now here:

    https:&#47;&#47;github.com&#47;facebook&#47;hiphop-php&#47;blob&#47;master&#47;hphp&#47;doc&#47;options.compiled
- id: 203
  author: Denis
  date: '2013-06-13 12:43:27 +0000'
  date_gmt: '2013-06-13 19:43:27 +0000'
  content: Please make bench comparing to APC.
- id: 209
  author: Dylan R Madisetti
  date: '2013-06-24 22:40:53 +0000'
  date_gmt: '2013-06-25 05:40:53 +0000'
  content: "So I got Wordpress running on HipHop. Woop woop! I admit, I cheated and
    used the binaries, but it was a fairly painless process on Ubuntu 13.2 (I built
    from scratch on Debian squeeze the other day and it was killer.)  In addition
    to the post you have here, I had to add \n  DefaultDocument = index.php\nto the
    server block and\n  JitASize = 67108864\n  JitAStubsSize = 67108864\n  JitGlobalDataSize
    = 16777216\nto the eval block (My poor VM couldn't take it otherwise)\n\njust
    playing around with this it seems wordpress defined rewrite rules don't work.
    Considering trying to run hhvm with nginx as detailed here https:&#47;&#47;github.com&#47;facebook&#47;hiphop-php&#47;wiki&#47;Using-nginx-as-Front-Server-to-HipHop
    to see if I can get something to give.\n\nor is there a way to do this solely
    with hiphop?"
- id: 215
  author: Joe Wang
  date: '2013-07-03 03:50:20 +0000'
  date_gmt: '2013-07-03 10:50:20 +0000'
  content: "Dear Sara,\n\nThank you for the great guide! Got a problem though, its
    not working for me...\nI just created a new AWS EC2 Ubuntu 12.04 LTS instance
    and installed a prebuilt package of Hiphop VM (v2.0.2). I applied the Object declaration
    fix and forgo the other Wordpress tweaks as they appear to be striked out. \nHowever
    Wordpress (brand new 3.4.2 installtion) still won't run. I can visit separate
    pages via MY_DOMAIN&#47;wordpress&#47;php-page.php (must have the .php suffix,
    otherwise chrome will just display \"Not found\"), but Wordpress as a whole just
    doesn't run. The error that I see are either \"web page not available\" or simply
    \"not found\".\nI tried to run the server with and w&#47;out the config or user
    settings to the same results."
- id: 221
  author: Dylan R Madisetti
  date: '2013-07-22 06:11:15 +0000'
  date_gmt: '2013-07-22 13:11:15 +0000'
  content: |-
    Wordpress works by hitting [WordpressDirectory]&#47;index.php which the loads everything else. Depending on the referring url, Wordpress will spit up various pages.
    If you default hiphop in the server block of the configuration with
    DefaultDocument = index.php

    then you should be good to run. You will not be able to use permalinks, but leaving posts in their ?p=number form should let you spit up pages&#47;posts.

    I have not found much documentation on making this working with fully formed slugs, but I'm looking into it. Ideally I want to be running a multisite wordpress from hiphop.
- id: 227
  author: David Michael
  date: '2013-07-29 08:43:23 +0000'
  date_gmt: '2013-07-29 15:43:23 +0000'
  content: Joe, I am getting the same issue you are. I was able to install correctly
    but when trying to go to site&#47;index.php i get a not found error.
- id: 233
  author: Zijin Zhang
  date: '2013-07-30 02:05:39 +0000'
  date_gmt: '2013-07-30 09:05:39 +0000'
  content: |-
    I followed this tutorial.When I requested &#47;wp-admin everything worked perfectly.However,when I requested &#47;,I was simply notified 'not found'.So I looked into error log,nothing wrong.Then I looked into access log,I fount that when I requested &#47;,hhvm responded 301 or 302.

    Can someone shed some light on this?
- id: 239
  author: Frank
  date: '2013-09-01 11:54:09 +0000'
  date_gmt: '2013-09-01 18:54:09 +0000'
  content: |-
    I tried to get around this problem with an nginx front end but could not get it to work using proxy_pass, despite it working fine for php5-fpm using fcgi_pass. Very frustrating.

    I'd switch to hphp and ditch php5-fpm+xcache+opcache tomorrow for Wordpress if it could do clean URLs.
- id: 245
  author: Al
  date: '2013-10-25 12:45:06 +0000'
  date_gmt: '2013-10-25 19:45:06 +0000'
  content: |-
    Don't forget about owner of <b>"SourceRoot = &#47;var&#47;www&#47;</b>:

    <i>chown web &#47;var&#47;www -R</i>
- id: 251
  author: 更换WordPress运行环境为HHVM | Lance&#039;blog
  date: '2013-12-06 20:51:47 +0000'
  date_gmt: '2013-12-07 04:51:47 +0000'
  content: "[&#8230;] + PHP.现在我向使用HHVM重新搭建WordPress运行环境，HHVM官方也有一片搭建教程Getting WordPress
    running on HHVM，我就参考这篇文章搭建一下。&nbsp;HHVM [&#8230;]"
- id: 257
  author: HHVM revisited - SitePoint
  date: '2013-12-21 11:00:10 +0000'
  date_gmt: '2013-12-21 19:00:10 +0000'
  content: "[&#8230;] and most of them are rather self explanatory and straightforward.
    In fact, if you follow HHVM&#039;s excellent WordPress tutorial from a while back,
    you&#039;ll see how simple a basic server configuration [&#8230;]"
- id: 263
  author: HHVM revisited | WarWebDev
  date: '2013-12-22 10:45:25 +0000'
  date_gmt: '2013-12-22 18:45:25 +0000'
  content: "[&#8230;] and most of them are rather self explanatory and straightforward.
    In fact, if you follow HHVM&#039;s excellent WordPress tutorial from a while back,
    you&#039;ll see how simple a basic server configuration [&#8230;]"
- id: 269
  author: Case insensitive constant names are not supported in HipHop | Christian
    Berendt
  date: '2014-01-14 06:15:50 +0000'
  date_gmt: '2014-01-14 14:15:50 +0000'
  content: "[&#8230;] More details about running WordPress on HHVM are available in
    the HHVM blog. [&#8230;]"
- id: 275
  author: การใช้งาน WordPress บน HipHop Virtual Machine for PHP
  date: '2014-01-17 09:19:43 +0000'
  date_gmt: '2014-01-17 17:19:43 +0000'
  content: "[&#8230;] Ref -&nbsp;hhvm.com [&#8230;]"
- id: 281
  author: Clotilde Roes
  date: '2014-01-21 22:47:08 +0000'
  date_gmt: '2014-01-22 06:47:08 +0000'
  content: This is really great and awesome.
- id: 287
  author: HHVM and WordPress | Keita&#039;s Blog
  date: '2014-02-08 16:56:31 +0000'
  date_gmt: '2014-02-09 00:56:31 +0000'
  content: "[&#8230;] Getting WordPress running on HHVM &laquo; HipHop Virtual Machine&#8617;
    [&#8230;]"
- id: 293
  author: Announcing Transaction Traces for the Agent SDK - New Relic blog
  date: '2014-02-11 14:20:40 +0000'
  date_gmt: '2014-02-11 22:20:40 +0000'
  content: "[&#8230;] Getting WordPress running on HHVM [&#8230;]"
- id: 299
  author: xyz
  date: '2014-02-12 03:11:22 +0000'
  date_gmt: '2014-02-12 11:11:22 +0000'
  content: |-
    Hi,
    I am a  new bee, i tried to configure hhvm with the above steps and finally succedded to execute simple hello world through command prompt, but fail to execute the same *.php file through URL by using the above "&#47;etc&#47;hhvm.hdf " config file. Can anybody help me. I already wasted my 4days with boost version....:(

    Thanks in Advance
- id: 305
  author: Vasken Hauri
  date: '2014-03-03 16:00:42 +0000'
  date_gmt: '2014-03-04 00:00:42 +0000'
  content: As of r27377 of WordPress, the lower-case constant issue has been fixed
    for the purpose of hhvm compatibility (thanks to Andrew Nacin). https:&#47;&#47;core.trac.wordpress.org&#47;changeset&#47;27377
- id: 311
  author: Joel Marcey
  date: '2014-03-03 16:04:48 +0000'
  date_gmt: '2014-03-04 00:04:48 +0000'
  content: Yay! :)
- id: 8861
  author: Scalable WordPress Hosting | The Coloured Keyboard
  date: '2014-03-31 11:06:59 +0000'
  date_gmt: '2014-03-31 18:06:59 +0000'
  content: "[&#8230;] I would like to test WordPress running on&nbsp;HHVM&nbsp;but
    to date there isn&#8217;t a hosting solution out there that supports this out
    of the [&#8230;]"
- id: 18797
  author: WordPress on HHVM | Rob Fahrni
  date: '2014-04-06 21:25:12 +0000'
  date_gmt: '2014-04-07 04:25:12 +0000'
  content: "[&#8230;] HHVM Blog: &#8220;As of WordPress 3.9, and HHVM 2.0 the following
    changes aren&rsquo;t necessary as WP have updated their codebase to play nice
    with HHVM, and HHVM has updated itself to support more PHP stuff.&#8221; [&#8230;]"
- id: 42935
  author: WordPress, Heroku and HHVM | Useful Stuff
  date: '2014-04-27 07:18:58 +0000'
  date_gmt: '2014-04-27 14:18:58 +0000'
  content: "[&#8230;] supports major PHP open source projects like WordPress. Running
    this&nbsp;project on seems&nbsp;really easy. A little modification was needed
    but last version (3.9) no longer need this.&nbsp;HHVM&nbsp;can also run [&#8230;]"
- id: 103361
  author: Philip John
  date: '2014-05-14 01:19:18 +0000'
  date_gmt: '2014-05-14 08:19:18 +0000'
  content: 'As of last night there is a HHVM config available for Varying Vagrant
    Vagrants (VVV): https:&#47;&#47;github.com&#47;johnjamesjacoby&#47;hhvvvm'
- id: 186095
  author: MRoeling
  date: '2014-07-01 06:49:52 +0000'
  date_gmt: '2014-07-01 13:49:52 +0000'
  content: "Updated list: \r\nhttps:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;tree&#47;master&#47;hphp&#47;runtime&#47;ext"
- id: 264239
  author: 博客迁移到HHVM@Openshift ; 论野生技术&amp;二次元
  date: '2014-09-28 19:14:10 +0000'
  date_gmt: '2014-09-29 02:14:10 +0000'
  content: "[&#8230;] 配置hhvm，参考http:&#47;&#47;hhvm.com&#47;blog&#47;3095&#47;getting-wordpress-running-on-hhvm，将以下内容填入~&#47;app-root&#47;repo&#47;config&#47;hhvm.d&#47;config.hdf
    \  wordpress + hhvm.hdf YAML [&#8230;]"
- id: 300869
  author: James
  date: '2014-11-19 19:35:05 +0000'
  date_gmt: '2014-11-20 03:35:05 +0000'
  content: "Sorry for raising this posts from death but I can't find the aforementioned
    post. Most specifically \"how does FB store session data across nodes\".\r\n\r\nWe
    are looking into deploying hhvm in a load balanced scenario."
- id: 302267
  author: Cesar Falcao
  date: '2014-11-22 10:22:59 +0000'
  date_gmt: '2014-11-22 18:22:59 +0000'
  content: "I got it working fine Nginx+MariaDB10 and Wordpress, but the performance
    is dead slow. I got 1500 concurrent users, but now I can't get more than 50 and
    its all very long response times, timeout and errors.\r\n\r\nI got JIT on, I can't
    find any info about what to do."
- id: 302273
  author: Cesar Falcao
  date: '2014-11-22 10:24:29 +0000'
  date_gmt: '2014-11-22 18:24:29 +0000'
  content: 'EDIT: 1500 concurrent users with PHP 5 in the same VPS, 123 ms avg response.'
- id: 317717
  author: WordPress on NGINX + HHVM with Heroku Buildpacks - xyu.io
  date: '2014-12-15 13:31:12 +0000'
  date_gmt: '2014-12-15 21:31:12 +0000'
  content: "[&#8230;] buildpack with nginx and HHVM built in. Much progress have also
    been made both HHVM and WordPress to make both compatible with each other. So
    it seems like now is as good a time as any to update the stack this site is running
    [&#8230;]"
- id: 350453
  author: Blake
  date: '2015-01-27 08:42:52 +0000'
  date_gmt: '2015-01-27 16:42:52 +0000'
  content: 'Just an FYI: HHVM no longer supports the built-in webserver as of 3.0.0.
    Please use your own webserver (nginx or apache) talking to HHVM over fastcgi.
    https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;wiki&#47;FastCGI'
---

This article aims to walk through the installation process for getting WordPress running on HHVM (HipHop Virtual Machine).

<!--truncate-->

## Installing HHVM

For the sake of this case-study, I used Ubuntu "Precise" 12.04 as my linux distribution since I'd be able to [install from a simple binary package](https://github.com/facebook/hiphop-php/wiki/Prebuilt-packages-on-ubuntu-12.04).  Instructions are currently available for [building for Ubuntu 12.04](https://github.com/facebook/hiphop-php/wiki/Building-and-installing-HHVM-on-Ubuntu-12.04) yourself, or [building for CentOS 6.3](https://github.com/facebook/hiphop-php/wiki/Building-and-installing-HHVM-on-CentOS-6.3).  Other distros will probably work with some effort, and you're encouraged to try.

## Unpacking Wordpress

Head to [wordpress.org/download](http://wordpress.org/download) to grab the [latest tar.gz](http://wordpress.org/latest.tar.gz) version of Wordpress and unpack it in a suitable location.  For the purposes of this post, I'll be using _/var/www/wp/_


     $ cd /var/www
     $ wget 'http://wordpress.org/latest.tar.gz'
     $ tar -zxf latest.tar.gz
     $ mv wordpress wp

##  Making a few... tweaks

**Update:** As of WordPress 3.9, and HHVM 2.0 the following changes aren't necessary as WP have updated their codebase to play nice with HHVM, and HHVM has updated itself to support more PHP stuff.  Isnt' Open Source awesome? :)

<del>Wordpress doesn't quite work "right out of the box" with HHVM because a few of HipHop's behaviors differ from the PHP it was built for.</del>

<del>First, case-insensitive constants are simply not supported by HipHop.  They're a bit silly, rarely used, and are more expensive (computationally) than they're worth.  Fortunately, wordpress only uses this feature in one place (to maintain BC with older plugins), and we can work around it by defining the most common variants.</del>

<del>Open up _wp-includes/wp-db.php_ and look for the line which defines the _'OBJECT'_ constant (line 20 in my version).  We'll want to take off the third parameter saying to declare it case-insensitively, and add in the lower-case and drop-case versions as alternates. This should be enough to cover 99% of plugins out there.</del>

<pre>
<del>
define('OBJECT', 'OBJECT');
define('Object', 'OBJECT');
define('object', 'OBJECT');
</del>
</pre>


<del>The rest of the changes are actually just temporary work-arounds for fixes which will be in HipHop in the next week or so.  **I'll update this post as those fixes reach github.**</del>

<del>As of this writing,_ ini_get('post_max_size')_ will return an empty string, and _ini_get('upload_max_filesize')_ will return a size in megabytes, but without the '_M_' suffix, so it is interpreted as bytes.  Fixes for both of these are currently pending, so just set them both manually for now.</del>

<pre>
<del>
// wp-admin/includes/template.php in wp_max_upload_size()

#$u_bytes = wp_convert_hr_to_bytes(ini_get('upload_max_filesize'));
#$p_bytes = wp_convert_hr_to_bytes(ini_get('post_max_size'));
$u_bytes =
$p_bytes = 100 << 20; // 100MB, or whatever you'll be setting
</del>
</pre>


**Update**: Both _post_max_size_ and _upload_max_filesize_ have been updated to return sane values and these changes are no longer required.

<del>_magic_quotes_runtime_ is (happily) not supported by HipHop.  _get_magic_quotes_runtime_() probably should have just quietly returned false, but for whatever reason it was implemented as throwing a "not implemented" exception.  A fix for this is currently pending, so hard-code a zero (false) for now.</del>

<pre>
<del>
// wp-admin/includes/class-pclzip.php in privDisableMagicQuotes()
#$this->magic_quotes_status = @get_magic_quotes_runtime();
$this->magic_quotes_status = 0;

// wp-includes/class-phpmailer.php in EncodeFile()
#$magic_quotes = get_magic_quotes_runtime();
$magic_quotes = 0;
</del>
</pre>

**Update**: _get_magic_quotes_runtime()_ has been updated to always return 0 (false) rather than throwing an exception.  This tweak no longer needs to be made.

## Create a config file

The syntax for HipHop's web server is pretty extensive, but the following placed in _/etc/hhvm.hdf_ should be enough to get you going.  Refer to [options.compiled](https://github.com/facebook/hiphop-php/blob/master/doc/options.compiled) for other settings.


    // /etc/hhvm.hdf

    Server {
      Port = 80
      SourceRoot = /var/www/
    }

    Eval {
      Jit = true
    }
    Log {
      Level = Error
      UseLogFile = true
      File = /var/log/hhvm/error.log
      Access {
        * {
          File = /var/log/hhvm/access.log
          Format = %h %l %u %t "%r" %>s %b
        }
      }
    }

    VirtualHost {
      * {
        Pattern = .*
        RewriteRules {
          dirindex {
            pattern = ^/(.*)/$
            to = $1/index.php
            qsa = true
          }
        }
      }
    }

    StaticFile {
      FilesMatch {
        * {
          pattern = .*.(dll|exe)
          headers {
            * = Content-Disposition: attachment
          }
        }
      }
      Extensions {
        css = text/css
        gif = image/gif
        html = text/html
        jpe = image/jpeg
        jpeg = image/jpeg
        jpg = image/jpeg
        png = image/png
        tif = image/tiff
        tiff = image/tiff
        txt = text/plain
      }
    }


You may wish to add other directives and static file extensions, but this will get you started.  The RewriteRule is to accomodate the fact that HipHop does not (currently) support a DirectoryIndex style directive.  While this feature is currently in development, we can get by with a general case rewrite rule.


## Start the webserver

Pretty straight-forward, just press go:


    sudo /usr/bin/hhvm --mode daemon --user web --config /etc/hhvm.hdf


Assuming of course you have a user designated for your web server to run as named 'web'.  Rename this one as needed.

## Wordpress setup


From here, setup follows the normal "[Famous 5 Minute Installation](http://codex.wordpress.org/Installing_WordPress)".  If you run into any trouble, check that you updated system files as described above, look into your error.log, or leave a comment here or on our [Facebook Page](https://www.facebook.com/pages/HipHop-for-PHP/282425744325).
