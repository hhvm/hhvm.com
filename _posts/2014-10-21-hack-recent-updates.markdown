---
author: jwatzman
layout: post
title: 'Hack: Recent Updates'
category: blog
permalink: /blog/6443/hack-recent-updates
comments:
- id: 283895
  author: Carl G
  date: '2014-10-21 11:19:08 +0000'
  date_gmt: '2014-10-21 18:19:08 +0000'
  content: It would be great to get an update on IDE options for Hack. When will FBIDE
    be available?
- id: 283937
  author: Josh Watzman
  date: '2014-10-21 12:08:09 +0000'
  date_gmt: '2014-10-21 19:08:09 +0000'
  content: Really sorry that we don't have any good updates on this. The most that
    I know is that it is taking longer than we expected, but it's still in progress,
    and something we want to get out as soon as we can.
- id: 284021
  author: Ze Ze
  date: '2014-10-21 14:07:19 +0000'
  date_gmt: '2014-10-21 21:07:19 +0000'
  content: "It's impossible to find tutorials or even news about Hack lang because
    the word \"hack\" is so generic.\r\n\r\nWhen will you change the name of the language?\r\n\r\nAnd
    yes, IDE is needed. You should just make it an IntelliJ extension, as that's currently
    the smartest cross platform IDE out there."
- id: 284027
  author: Josh Watzman
  date: '2014-10-21 14:15:53 +0000'
  date_gmt: '2014-10-21 21:15:53 +0000'
  content: "Yeah, it isn't the greatest name for a language ever, but we also don't
    have any plans to change it, sorry. The community roundups linked in the post
    above are good resources for the existing blog posts, tutorials, code examples,
    etc that I at least am aware of.\r\n\r\nOn the IDE front, we of course have FBIDE
    on the way. We also have plugins for vim, emacs, and now sublime-text -- there
    are links to them at https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;tree&#47;master&#47;hphp&#47;hack&#47;editor-plugins.
    There's also a highly voted issue to add Hack support to PHPStorm, which we'd
    love to see happen, and have had a couple conversations with JetBrains to hopefully
    help make it so."
- id: 284039
  author: RouteXL
  date: '2014-10-21 14:23:44 +0000'
  date_gmt: '2014-10-21 21:23:44 +0000'
  content: Great work! How about a plugin for Eclipse?
- id: 284051
  author: Josh Watzman
  date: '2014-10-21 14:28:12 +0000'
  date_gmt: '2014-10-21 21:28:12 +0000'
  content: No one is working on one right now as far as I'm aware, but I'd be more
    than happy to accept a PR on GitHub if you or someone else wanted to write one!
    https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;tree&#47;master&#47;hphp&#47;hack&#47;editor-plugins
    is where our existing plugins live.
- id: 284081
  author: Vincent DM
  date: '2014-10-21 15:18:06 +0000'
  date_gmt: '2014-10-21 22:18:06 +0000'
  content: "Thanks for the update; looking forward on the OSX item as it would be
    a great way to quickly experiment, without spinning up yet another VM.\r\n\r\nHowever,
    reason #1 holding me back to jump into Hack is IDE support (I find the supported
    editors arcane). Learning a new language is already taxing, and I don't want to
    combine this with being dragged down by a new and unfamiliar editor.\r\n\r\nAs
    said before, IntelliJ would be the optimal IDE, since it is so popular among professional
    PHP developers (which I assume are the target audience for hack). Based on the
    ticket at Jetbrains' site, they seem to be waiting for more examples of actual
    hack projects (which seems like a chicken-or-egg approach to me), so it would
    be great if Facebook could prod them or maybe even contribute it as an externally-developed
    extension?\r\n\r\nAnyway, thanks for driving the PHP community forward. I'm glad
    that hack is fixing so many things that have bothered me for years."
- id: 284087
  author: Jordan
  date: '2014-10-21 15:18:34 +0000'
  date_gmt: '2014-10-21 22:18:34 +0000'
  content: I hope so. I want to use Hacklang badly, but I refuse without an IDE.
- id: 286877
  author: Ze Ze
  date: '2014-10-24 12:29:47 +0000'
  date_gmt: '2014-10-24 19:29:47 +0000'
  content: "I looked at the intro video about FBIDE, sorry I'm not excited about that.
    Even editors like Atom are slow as snail, can't imagine a proper IDE built with
    JS. The UI looked more like a website for tablets rather than a IDE, I guess that
    is what it's gonna be - more of an editor than IDE? I can't believe nobody in
    the adience had the stones to tell what a big of a spawn of evil JS is.\r\n\r\nPHPStorm&#47;InjelliJ
    support sounds great though."
- id: 286991
  author: noko
  date: '2014-10-24 15:57:08 +0000'
  date_gmt: '2014-10-24 22:57:08 +0000'
  content: Well the name is not worse than "C" or "Go". Just start adding "hacklang"
    for search engine friendliness, just like people use "golang".
---

A lot has happened since we announced Hack. We've already highlighted our [Hack developer day](https://www.youtube.com/playlist?list=PLb0IAmt7-GS2fdbb1vVdP8Z8zx1l2L8YS), as well as posting a series of community roundups ([one](http://hhvm.com/blog/4811/hack-community-roundup), [two](http://hhvm.com/blog/5429/hack-community-roundup-2), [three](http://hhvm.com/blog/6005/hack-community-roundup-3)) highlighting the projects that our amazing Hack community have been building.

<!--truncate-->

However, one thing we haven't talked about much is the progress and evolution of the language itself. We've been busy driving the language forward, improving its PHP base as well as adding new features requested inside and outside Facebook to further increase developers' productivity. But unless you're the sort of person that reads [every commit](https://github.com/facebook/hhvm/commits/master) going into the [HHVM github repository](https://github.com/facebook/hhvm) or every change to our [docs site](http://docs.hhvm.com/manual/en/index.php), you probably have no idea about any of these changes since we haven't talked much about them yet.

![List of Hack GitHub Commits](/static/images/posts//Screen-Shot-2014-10-21-at-9.40.09-AM.png)

Over the next few weeks, we'll be making a series of posts talking about all that has happened to the language over the previous months to continue driving it forward. Some of the things we're planning to talk about:




  * Typechecking `new static()`


  * Interface requirements and trait requirements


  * First-class enums


  * `HH_FIXME` and other error suppression mechanisms


  * Better understanding the type signatures of the PHP standard library


  * OS X support


  * Covariance


  * The nullsafe operator


In short, a lot has happened to move Hack forward since its launch, and we're excited to talk about it now -- and there's a lot more on our roadmap, so stay tuned for some of our future plans as well.
