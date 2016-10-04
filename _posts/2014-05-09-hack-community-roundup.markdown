---
author: jwatzman
layout: post
title: Hack Community Roundup
category: blog
permalink: /blog/4811/hack-community-roundup
comments:
- id: 84641
  author: Utomo
  date: '2014-05-09 18:00:20 +0000'
  date_gmt: '2014-05-10 01:00:20 +0000'
  content: "How about releasing tools to convert php script to hack? \r\nOr help popular
    opensource to migrate.  Such as opencart"
- id: 85427
  author: Nino
  date: '2014-05-09 23:24:39 +0000'
  date_gmt: '2014-05-10 06:24:39 +0000'
  content: 'Not that big yet, but not to forget: the german speaking hack and hhvm
    support forum. www.fbhack.de'
- id: 85715
  author: Florian Zemke
  date: '2014-05-10 01:13:21 +0000'
  date_gmt: '2014-05-10 08:13:21 +0000'
  content: There's hackificator. On YouTube you will also find a presentation of some
    Facebookers who talk about migrating PHP to Hack.
- id: 87851
  author: Josh Watzman
  date: '2014-05-10 10:58:35 +0000'
  date_gmt: '2014-05-10 17:58:35 +0000'
  content: I actually wasn't aware of that one, thanks for pointing it out! I sadly
    don't speak German myself, but I'm pretty sure at least one member of our team
    does, so we'll make sure to have someone check it out.
- id: 87893
  author: Josh Watzman
  date: '2014-05-10 11:03:34 +0000'
  date_gmt: '2014-05-10 18:03:34 +0000'
  content: "Indeed -- my presentation is on YouTube https:&#47;&#47;www.youtube.com&#47;watch?v=5tEnAL_Fad4&list=PLb0IAmt7-GS2fdbb1vVdP8Z8zx1l2L8YS
    and the tools I talk about and demo are all available in the Debian packages,
    with the source code alongside Hack in the HHVM github repository.\r\n\r\nIf you
    or anyone is running into any problems, please let us know! For bugs and problems,
    feel free to file an issue on github. For general questions, we monitor the \"hacklang\"
    StackOverflow tag, and members of the Hack team are also typically on IRC (#hhvm
    on Freenode) during the workday US Pacific time."
- id: 95339
  author: 'The first micro framework written in Hack is there: hack-mvc ! - Dev Metal'
  date: '2014-05-12 06:09:05 +0000'
  date_gmt: '2014-05-12 13:09:05 +0000'
  content: "[&#8230;] awesome news about Hack and HipHop in the current blog post
    of the official HipHop&#47;HHVM dev [&#8230;]"
- id: 101693
  author: Adrian Budau
  date: '2014-05-13 16:10:29 +0000'
  date_gmt: '2014-05-13 23:10:29 +0000'
  content: Would you consider added polling to hh_server next to inotify? Virtualbox
    shared folders don't trigger inotify notifications properly so this would be very
    useful :-)
- id: 101987
  author: speg
  date: '2014-05-13 17:59:49 +0000'
  date_gmt: '2014-05-14 00:59:49 +0000'
  content: Is this why I have to manually restart and do hh_client check each time?
- id: 104999
  author: Josh Watzman
  date: '2014-05-14 09:36:38 +0000'
  date_gmt: '2014-05-14 16:36:38 +0000'
  content: "This is something we're considering, yes. For now, you may want to try
    http:&#47;&#47;docs.vagrantup.com&#47;v2&#47;synced-folders&#47;rsync.html --
    it will hopefully generate the right inotify events and fix the problem, though
    I haven't tried it personally. (You can also move your code out of the VirtualBox
    share.)\r\n\r\nIf you want a one-shot batch mode, we do have an implementation
    of that -- you can run \"hh_server --check path&#47;to&#47;www&#47;dir\"\r\n\r\nAre
    you using VirtualBox for any inherent reason, or are you on an unsupported OS
    and just need it to get Linux running? What OS are you using? We're trying to
    prioritize building a \"less smart\" incremental mode vs. proper OS X support.
    (Windows will come somewhat later and is more involved.)"
- id: 105005
  author: Josh Watzman
  date: '2014-05-14 09:37:47 +0000'
  date_gmt: '2014-05-14 16:37:47 +0000'
  content: Very likely, yes, sorry about that. See my response to the parent comment
    for some other things you can do.
- id: 105077
  author: Adrian Budau
  date: '2014-05-14 10:01:14 +0000'
  date_gmt: '2014-05-14 17:01:14 +0000'
  content: "I tried using rsync. With auto-sync it works more or less reliably (if
    you run scripts that modify a large number of files auto-sync is slow sometimes).\r\nI
    use VirtualBox because at this moment it is still far more easier to set up hacklang
    on ubuntu than everything else. I am on OSX on the moment. +the ability to keep
    a project completely sandboxed."
- id: 106241
  author: Adrian Budau
  date: '2014-05-14 17:56:03 +0000'
  date_gmt: '2014-05-15 00:56:03 +0000'
  content: 'It seems I can''t edit comments so I''ll make  anew one: I would not require
    this if hh_client and hh_server could be more easily installed (i.e. not require
    the whole of hhvm).'
- id: 109787
  author: speg
  date: '2014-05-15 17:03:09 +0000'
  date_gmt: '2014-05-16 00:03:09 +0000'
  content: "Thank you! I was so frustrated when I wasn't seeing the type checker catching
    my errors. I have confirmed that making changes inside my VM works. As does setting
    up the VM to sync with rsync. Though it's a bit awkward having to do the extra
    step of `vagrant rsync-auto`. \r\n\r\nI feel like I am missing something though..
    Is hh_client supposed to alert your errors as soon as a change is detected? Right
    now I am having to do `hh_client` each time I want to check. If not, how is that
    any different thant the `hh_server --check path&#47;to&#47;www&#47;dir` you mentioned
    earlier.\r\n\r\nI can't speak for the parent, but I am using vagrant &amp; virtual
    box to manage development environments that are similar to production. I'm not
    sure having proper OS X support would help much, because I would still rather
    develop on a VM so that I could stay as close to production as possible."
- id: 121685
  author: Nazar Mokrynskyi
  date: '2014-05-18 18:20:52 +0000'
  date_gmt: '2014-05-19 01:20:52 +0000'
  content: "I've looked video of talk about PHP -> Hack convertion. And I have a question
    about PhpDoc sections. As I understand - you ignore them, but most of code I write
    at least last year contains proper PhpDoc sections that you can definitely use
    during convertion.\r\n\r\nDo you have plans about supporting this at least as
    optional feature?"
- id: 124979
  author: Josh Watzman
  date: '2014-05-19 09:12:45 +0000'
  date_gmt: '2014-05-19 16:12:45 +0000'
  content: Having hh_client&#47;hh_server without HHVM isn't terribly useful, since
    you need HHVM to actually run your code! Or am I missing something about the use
    case you have in mind?
- id: 124985
  author: Josh Watzman
  date: '2014-05-19 09:15:16 +0000'
  date_gmt: '2014-05-19 16:15:16 +0000'
  content: "Running hh_client is how you check for Hack errors. It just queries the
    server for the current error list, so if you want to run it automatically, you
    need to set that up yourself. There are a couple ways to get it to run automatically:\r\n\r\n-
    You can wire it in to your editor. We have vim support https:&#47;&#47;github.com&#47;hhvm&#47;vim-hack
    and emacs support https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;tree&#47;master&#47;hphp&#47;hack&#47;editor-plugins&#47;emacs.
    This is pretty highly recommended.\r\n- You can run \"watch hh_client\" in a second
    terminal window."
- id: 125009
  author: Josh Watzman
  date: '2014-05-19 09:17:47 +0000'
  date_gmt: '2014-05-19 16:17:47 +0000'
  content: "We don't plan to typecheck them as-is right now. Here is a long thread
    where I discuss our thoughts on different conversion strategies, including docblock
    comments: https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;issues&#47;2236.
    (Short version: type-checking them isn't enforced by the runtime, which is dangerous.)\r\n\r\nUsing
    them to aide a conversion effort is potentially useful. The challenge there is
    trying to parse the docblock comments, since everyone writes them slightly differently,
    and then get that into a format that makes sense in the Hack type system."
- id: 125411
  author: Adrian Budau
  date: '2014-05-19 11:01:58 +0000'
  date_gmt: '2014-05-19 18:01:58 +0000'
  content: "I have hhvm installed in my VM (with all of its dependencies). That's
    where my server is set up. But I'm coding from my master OS (from outside). Here
    I don't need the whole power of HHVM, just the type checker. \r\n\r\nI hope was
    clear enough :-)"
- id: 480755
  author: Was wurde eigentlich aus &hellip; Hack? - entwickler.de
  date: '2015-05-08 02:34:40 +0000'
  date_gmt: '2015-05-08 09:34:40 +0000'
  content: "[&#8230;] zu PHP, auch in der Community existieren zahlreiche spannende
    Projekte, die Josh Watzman jetzt im offiziellen Hack-Blog vorgestellt hat. Die
    spannendsten davon m&ouml;chten wir euch an dieser Stelle kurz [&#8230;]"
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
