---
author: fred
layout: post
title: Compatibility Update
category: blog
permalink: /blog/4841/compatibility-update
comments:
- id: 36047
  author: Yosmany
  author_email: yosmanyga@gmail.com
  author_url: ''
  date: '2014-04-21 10:18:05 +0000'
  date_gmt: '2014-04-21 17:18:05 +0000'
  content: Typo in "Symphony" word, it's "Symfony".
- id: 36053
  author: Fred Emmott
  author_email: fe@fb.com
  author_url: ''
  date: '2014-04-21 10:19:52 +0000'
  date_gmt: '2014-04-21 17:19:52 +0000'
  content: Thanks, fixed
- id: 36101
  author: Martin
  author_email: martin@olsansky.sk
  author_url: ''
  date: '2014-04-21 11:31:11 +0000'
  date_gmt: '2014-04-21 18:31:11 +0000'
  content: What about Nette?
- id: 36125
  author: Fred Emmott
  author_email: fe@fb.com
  author_url: ''
  date: '2014-04-21 11:49:43 +0000'
  date_gmt: '2014-04-21 18:49:43 +0000'
  content: We've not looked at Nette yet; https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;issues&#47;2500
    will be updated when that changes - I guess you filed that.
- id: 36143
  author: Jeremias
  author_email: j.davidmuiambo@gmail.com
  author_url: https://twitter.com/jeremiasmuiambo
  date: '2014-04-21 13:29:36 +0000'
  date_gmt: '2014-04-21 20:29:36 +0000'
  content: Amazing Job
- id: 36149
  author: Danny
  author_email: dannykopping@gmail.com
  author_url: http://infomaniac.co.za
  date: '2014-04-21 13:48:28 +0000'
  date_gmt: '2014-04-21 20:48:28 +0000'
  content: "This is really great! I'm sure a metric ass-tonne of work has gone into
    this from all parties involved! \r\nI think we should commend this big effort,
    and then and only then correct spelling mistakes and ask for more stuff, no? :)"
- id: 36215
  author: Morgan
  author_email: mkbreden@gmail.com
  author_url: ''
  date: '2014-04-21 15:21:33 +0000'
  date_gmt: '2014-04-21 22:21:33 +0000'
  content: I see you're focusing on stagnated frameworks like CodeIgniter. Any plans
    to test compatibility with more actively maintained solutions like CakePHP or
    Yii?
- id: 36221
  author: Fred Emmott
  author_email: fe@fb.com
  author_url: ''
  date: '2014-04-21 15:44:36 +0000'
  date_gmt: '2014-04-21 22:44:36 +0000'
  content: "We tried to optimize for popularity&#47;effort: we based popularity on
    github stars&#47;forks&#47;watchers, and some data from versioneye, and effort
    was a guess primarily based on how large the frameworks are.\r\n\r\nWe are testing
    Yii (it's shown on http:&#47;&#47;hhvm.com&#47;frameworks&#47;), and an OpenAcademy
    student is currently working on it.\r\n\r\nThe main reason we didn't work on CakePHP
    is because it's got a custom test runner - you can't just run 'phpunit path&#47;to&#47;test'.
    This means we'd have had to have spent a non-trivial amount of time improving
    our test runner, instead of working on improving compatibility.\r\n\r\nThis is
    something we're likely to address in the future, but we don't think it's the best
    way for us to increase the usefulness of HHVM in the short-term - we're instead
    going to be looking at specific problems reported on github."
- id: 36239
  author: Morgan
  author_email: mkbreden@gmail.com
  author_url: ''
  date: '2014-04-21 15:55:16 +0000'
  date_gmt: '2014-04-21 22:55:16 +0000'
  content: "Thanks for the insight! I'm glad to hear Yii is in your sights, and I
    didn't know about CakePHP's testing suite.\r\n\r\nGood luck and happy bug hunting!"
- id: 36257
  author: Konstantin Kudryashov
  author_email: ever.zet@gmail.com
  author_url: ''
  date: '2014-04-21 16:31:04 +0000'
  date_gmt: '2014-04-21 23:31:04 +0000'
  content: "You missed Behat v3:\r\nhttps:&#47;&#47;travis-ci.org&#47;Behat&#47;Behat&#47;jobs&#47;23445116\r\n;)"
- id: 36311
  author: Mark Story
  author_email: mark.story@gmail.com
  author_url: http://mark-story.com
  date: '2014-04-21 19:17:03 +0000'
  date_gmt: '2014-04-22 02:17:03 +0000'
  content: The custom test runner is being removed in CakePHP 3.0, and we'll be using
    the standard phpunit like other libraries. We have HHVM as build target in travis.ci,
    but we're not quite at 100%. Once we get most of the development done for 3.0
    completed, I plan on spending time to improve compatibility with HHVM.
- id: 36335
  author: Fred Emmott
  author_email: fe@fb.com
  author_url: ''
  date: '2014-04-21 20:05:21 +0000'
  date_gmt: '2014-04-22 03:05:21 +0000'
  content: That's awesome -  I'll see what it would take to add it to our runner tomorrow
    (hopefully just an edit to https:&#47;&#47;github.com&#47;facebook&#47;hhvm&#47;blob&#47;master&#47;hphp&#47;test&#47;frameworks&#47;frameworks.yaml)
    - even though we're not going to be directly working on frameworks, if you file
    issues for specific compatibility issues you find, we'll be happy to work on them
    :)
- id: 36365
  author: Joel Marcey
  author_email: joelm@fb.com
  author_url: ''
  date: '2014-04-21 20:34:30 +0000'
  date_gmt: '2014-04-22 03:34:30 +0000'
  content: Yay! That's great news! :)
- id: 36419
  author: Mark
  author_email: mark@nospam.org
  author_url: ''
  date: '2014-04-21 22:16:24 +0000'
  date_gmt: '2014-04-22 05:16:24 +0000'
  content: "sabre&#47;http, sabre&#47;event and sabre&#47;vobject are already hhvm
    compatible, too. Hope sabre&#47;dav will be really soon\r\n\r\nhhvm compatible
    (afaik):\r\nhttps:&#47;&#47;travis-ci.org&#47;fruux&#47;sabre-http\r\nhttps:&#47;&#47;travis-ci.org&#47;fruux&#47;sabre-event\r\nhttps:&#47;&#47;travis-ci.org&#47;fruux&#47;sabre-vobject\r\n\r\nNot
    yet:\r\nhttps:&#47;&#47;travis-ci.org&#47;fruux&#47;sabre-dav"
- id: 36497
  author: Julius Beckmann
  author_email: hhvm@h4cc.de
  author_url: http://hhvm.h4cc.de/
  date: '2014-04-22 00:10:34 +0000'
  date_gmt: '2014-04-22 07:10:34 +0000'
  content: "Also consider, that all the other packages installed with these frameworks
    need to be tested to.\r\n\r\nYou can check it out here: http:&#47;&#47;hhvm.h4cc.de&#47;\r\nEven
    with dependency graph analysis, for example symfony: http:&#47;&#47;hhvm.h4cc.de&#47;graphs&#47;symfony_2_4.png"
- id: 36533
  author: Josh
  author_email: joshuataylorx@gmail.com
  author_url: http://joshtaylor.id.au
  date: '2014-04-22 00:56:48 +0000'
  date_gmt: '2014-04-22 07:56:48 +0000'
  content: "HHVM has come a very long way in a very short time. Having kept a very
    close eye on HHVM, I'm quite impressed at the resources FB has put towards making
    HHVM kick ass.\r\n\r\nA great team of engineers, and public commit history makes
    FB look like a major winner.\r\n\r\nAlso helping existing AJAX calls be cut in
    half running the same code with HHVM is also a major win :)."
- id: 36635
  author: nickvergessen
  author_email: nickvergessen@phpbb.com
  author_url: ''
  date: '2014-04-22 04:01:59 +0000'
  date_gmt: '2014-04-22 11:01:59 +0000'
  content: Typo in the word "phpbb3", its "phpBB"
- id: 36689
  author: Radu Murzea
  author_email: sobolanx@gmail.com
  author_url: ''
  date: '2014-04-22 04:50:02 +0000'
  date_gmt: '2014-04-22 11:50:02 +0000'
  content: "Wow, that is great news. I never expected HHVM to grow and improve sooo
    fast. I keep a local copy of HHVM's source code on my machine and, every time
    I pull from GitHub (maybe once a week), I'm amazed at how much progress is made
    in such a short time.\r\n\r\nWhen you reach 100 % with Symfony too, it will be
    the most awesome day :) ."
- id: 36701
  author: Radu Murzea
  author_email: sobolanx@gmail.com
  author_url: ''
  date: '2014-04-22 04:53:05 +0000'
  date_gmt: '2014-04-22 11:53:05 +0000'
  content: 'Ooooh, I almost forgot. Please take a look at this when you have the time:
    https:&#47;&#47;www.facebook.com&#47;groups&#47;hackdevday14&#47;permalink&#47;1438300749742374
    . Many thanks.'
- id: 36731
  author: Dave
  author_email: drupal@davidstoline.com
  author_url: http://davidstoline.com
  date: '2014-04-22 05:55:23 +0000'
  date_gmt: '2014-04-22 12:55:23 +0000'
  content: I'm going to guess that since Drupal 7 has exactly 0 PHPUnit tests, you
    mean Drupal 8.
- id: 36767
  author: Jose
  author_email: jose.zap@gmail.com
  author_url: ''
  date: '2014-04-22 05:59:38 +0000'
  date_gmt: '2014-04-22 12:59:38 +0000'
  content: That's great news Fred! Looking forwards seeing CakePHP 3.0 in the frameworks
    testsuite
- id: 36989
  author: Fred Emmott
  author_email: fe@fb.com
  author_url: ''
  date: '2014-04-22 09:07:11 +0000'
  date_gmt: '2014-04-22 16:07:11 +0000'
  content: Thanks, fixed.
- id: 37007
  author: Joel Marcey
  author_email: joelm@fb.com
  author_url: ''
  date: '2014-04-22 09:44:17 +0000'
  date_gmt: '2014-04-22 16:44:17 +0000'
  content: 'Check and see if these work for you: https:&#47;&#47;www.facebook.com&#47;groups&#47;hackdevday14&#47;permalink&#47;1438300749742374&#47;'
- id: 37103
  author: Fred Emmott
  author_email: fe@fb.com
  author_url: ''
  date: '2014-04-22 11:50:09 +0000'
  date_gmt: '2014-04-22 18:50:09 +0000'
  content: CakePHP3 should be in our next push - it's currently at 96%
- id: 37895
  author: Knecht Rootrecht
  author_email: ninsky80@googlemail.com
  author_url: http://www.fbhack.de
  date: '2014-04-23 11:56:51 +0000'
  date_gmt: '2014-04-23 18:56:51 +0000'
  content: "Just set up a german speaking support forum for Hack and HHVM. \r\n\r\nwww.fbhack.de\r\n\r\nHope
    some PHP devs interested in Hack&#47;HHVM will find it useful!"
- id: 39845
  author: Automated twitter compilation up to 25 April 2014 | David Goodwin
  author_email: ''
  author_url: http://codepoets.co.uk/2014/automated-twitter-compilation-up-to-25-april-2014/
  date: '2014-04-25 10:01:42 +0000'
  date_gmt: '2014-04-25 17:01:42 +0000'
  content: "[&#8230;] have finally hit 100% PHPUnit test passing for 20 popular frameworks..
    and getting close on more. hhvm.com&#47;blog&#47;4841&#47;compatibility-update
    \ [&#8230;]"
- id: 40859
  author: Facebook Hack &amp; HHVM - Zend Framework Forum - ZF1 &#47; ZF2
  author_email: ''
  author_url: http://www.zfforum.de/php-x-talk/12902-facebook-hack-hhvm.html#post81738
  date: '2014-04-26 02:39:49 +0000'
  date_gmt: '2014-04-26 09:39:49 +0000'
  content: "[&#8230;] F&auml;llen PHP 5.x bereits abh&auml;ngt und Facebook alles
    daf&uuml;r tut die PHP-Welt an sich zu reissen (Compatibility Update &laquo; HHVM).
    Und das scheint nur der Anfang einer rasanten Entwicklung zu sein. Andererseits
    muss man sich [&#8230;]"
- id: 42557
  author: Tim Hawkins
  author_email: tim.thawkins@gmail.com
  author_url: http://airsoc.com
  date: '2014-04-27 01:43:54 +0000'
  date_gmt: '2014-04-27 08:43:54 +0000'
  content: "Just wanted to drop a note for folks who need mongodb integration. Mongofill-hhvm
    is a fully 10gen php driver complient extension for hhvm. The current version
    is essentialy beta, but I have been able to port several non-trivial php apps
    to the combination of hhvm 3.0.1 and mongofill-hhvm, with relativly little tweaking.
    In the cases  where tweaking was required, it was generaly a bug in the original
    code where hhvm's stricter parsing pulled it out. \r\n\r\nhttps:&#47;&#47;github.com&#47;mongofill&#47;mongofill-hhvm\r\n\r\nTo
    install mongofill-hhvm you will need to have a hhvn installation built from source,
    not a packaged version as it is currently only supplied in source form."
- id: 45209
  author: Xandi Ostermeyr
  author_email: ao@codesprint.de
  author_url: https://plus.google.com/+XandiOstermeyr
  date: '2014-04-28 03:42:52 +0000'
  date_gmt: '2014-04-28 10:42:52 +0000'
  content: "Are there any plans to test magento2? \r\nWould be very interesting, to
    increase the performance of magento..."
- id: 50717
  author: HHVM and Hack on Heroku
  author_email: ''
  author_url: http://www.sitepoint.com/hhvm-hack-heroku/
  date: '2014-04-29 16:35:59 +0000'
  date_gmt: '2014-04-29 23:35:59 +0000'
  content: "[&#8230;] has been making new forays in popular library and framework
    compatibility, with the latest update to 3.1 adding full support [&#8230;]"
- id: 59867
  author: Fedir RYKHTIK
  author_email: fedir.rykhtik@gmail.com
  author_url: http://fedir.github.io
  date: '2014-05-02 10:26:26 +0000'
  date_gmt: '2014-05-02 17:26:26 +0000'
  content: "95% tests are green for TYPO3 CMS on HHVM !\r\n\r\nhttp:&#47;&#47;blog.macopedia.co&#47;post&#47;running-typo3-cms-on-hhvm-part2&#47;\r\n\r\n1.1%
    failed,  0.7% finished with error, 0.26% were incomplete and 2.37% were skipped."
- id: 65483
  author: Utomo
  author_email: Utomo.prawiro@gmail.com
  author_url: ''
  date: '2014-05-04 16:47:58 +0000'
  date_gmt: '2014-05-04 23:47:58 +0000'
  content: "How about http:&#47;&#47;fatfreeframework.com\r\nDoes that hhvm support
    it? \r\n\r\nI hope hhvm make tools to migrate php code to hhvm. \r\nBy doing that
    hhvm can get more people using it. \r\nAlso consider helping famous opensource
    to use hhvm,  example opencart,  and others"
- id: 65531
  author: Utomo
  author_email: Utomo.prawiro@gmail.com
  author_url: ''
  date: '2014-05-04 17:15:28 +0000'
  date_gmt: '2014-05-05 00:15:28 +0000'
  content: "I hope hhvm can try to make popular opensource compatible with hhvm. \r\nWordPress
    3.9 already on the way. \r\n\r\nLet's continue with opencart 2.0, Magento,  Drupal,
    \ Joomla,  etc. \r\nBy doing that many people will love and use hhvm"
- id: 66857
  author: 'Debug Roome #7 - Bien d&eacute;buter avec AWS | Debug Room'
  author_email: ''
  author_url: http://www.debugroom.fr/debug-roome-7-bien-debuter-aws
  date: '2014-05-05 06:00:32 +0000'
  date_gmt: '2014-05-05 13:00:32 +0000'
  content: "[&#8230;] Un update sur HHVM [&#8230;]"
- id: 182927
  author: Marko Rumpli
  author_email: mr@kapesnisvet.cz
  author_url: http://kapesnisvet.cz/
  date: '2014-06-24 06:05:45 +0000'
  date_gmt: '2014-06-24 13:05:45 +0000'
  content: "Hello Fred,\r\n\r\ncan I ask you how it looks with Nette support?"
- id: 184727
  author: 9.9 million lines of code and still moving fast &#8211; Facebook open source
    in 2014
  author_email: ''
  author_url: http://cyberoot.org/2014/06/9-9-million-lines-of-code-and-still-moving-fast-facebook-open-source-in-2014/
  date: '2014-06-28 09:23:45 +0000'
  date_gmt: '2014-06-28 16:23:45 +0000'
  content: "[&#8230;] ever before. In January, we were passing just 6 major frameworks&#8217;
    PHPUnit test suites. but we passed our goal of 20 in April, and are pleased to
    currently support 26 major frameworks with 100% pass [&#8230;]"
- id: 217547
  author: PHP News You May Have Missed
  author_email: ''
  author_url: http://www.sitepoint.com/news-may-missed/
  date: '2014-08-19 22:40:14 +0000'
  date_gmt: '2014-08-20 05:40:14 +0000'
  content: "[&#8230;] Their website features a wide variety of examples, good docs,
    and an interactive tutorial you can use to get familiar with it. It&rsquo;s not
    that different from PHP, so it&rsquo;ll be an easy entry for most PHP devs. HHVM
    has also achieved full compatibility with 23 popular libraries&#47;frameworks.
    [&#8230;]"
- id: 472637
  author: gorka
  author_email: gorkamola@outlook.com
  author_url: http://gorkamu.com/2015/04/test-funcionales-con-phpunit/
  date: '2015-05-02 09:59:51 +0000'
  date_gmt: '2015-05-02 16:59:51 +0000'
  content: Great post. I really like unit testing frameworks like <a href="http:&#47;&#47;gorkamu.com&#47;2015&#47;04&#47;test-funcionales-con-phpunit&#47;"
    rel="nofollow">phpunit<&#47;a>
- id: 528689
  author: Jelen
  author_email: MoraviaD1@gmail.com
  author_url: ''
  date: '2015-06-18 23:30:57 +0000'
  date_gmt: '2015-06-19 06:30:57 +0000'
  content: Any news?
- id: 529859
  author: Fred Emmott
  author_email: fe@fb.com
  author_url: ''
  date: '2015-06-22 14:29:06 +0000'
  date_gmt: '2015-06-22 21:29:06 +0000'
  content: We're not actively targeting or investigating frameworks at the moment;
    given our level of compatibility is generally very good now, investigating specific
    reported issues is a better use of our time now.
---

[Earlier this year](http://hhvm.com/blog/3743/hhvm-the-next-six-months) we set an ambitious goal of passing the PHPUnit test suites of 20 popular frameworks by the end of June; at the time, we were passing on only 6! With a huge amount of help from the community (especially our [OpenAcademy](https://www.facebook.com/OpenAcademyProgram) students), we're proud to have hit this goal more than 2 months early, and we have more frameworks expected to reach 100% shortly.

<!--truncate-->

![lotsoflogos](/static/images/posts/lotsoflogos1.png)

The full list (currently 23) is shown on our [framework tests page](http://hhvm.com/frameworks/); we consider the following to be popular, and will be supported in HHVM 3.1, and our nightly builds:




  * assetic


  * codeigniter


  * composer


  * doctrine2


  * facebookphpsdk


  * guzzle3 (guzzle4 coming soon)


  * idorm + paris


  * laravel


  * lessphp - thanks to [Camillus Gerard Cai](https://github.com/cgcai)


  * mediawiki


  * mockery


  * monolog - thanks to [Rafe Kettler](https://github.com/rafekettler)


  * mustache - thanks to [Kevan Fisher](https://github.com/k-fish)


  * phpbb3 - thanks to Kevan Fisher


  * phpmyadmin - thanks to [Jeff Chan](https://github.com/jeffchan)


  * phpunit


  * ratchet - thanks to Kevan Fisher


  * reactphp - thanks to Camillus Gerard Cai


  * slim


  * twig


Special thanks to [Ioan Negulescu](https://github.com/idn2104) for improving our Symfony support, and to [Joel Low](https://github.com/lowjoel) for several fundamental improvements to HHVM helping all of us, and for bringing Drupal 8's PHPUnit tests to 100% -  Drupal 8 is not included in the list above as the PHPUnit tests are a small portion of their full test suite.

What's next? Compatibility is still a huge priority for us, though we feel that targeting framework test suites has run its course and gotten us most of the low hanging fruit. After we've finished support for a few more frameworks that are nearly complete, we're going to refocus on fixing [issues](https://github.com/facebook/hhvm/issues?state=open) reported on GitHub. HHVM now has a great overall level of support for PHP5, and we think the best way to continue to improve it is to work on the issues that you and the rest of our community are finding in the real world. If you find compatibility problems, please [open an issue](https://github.com/facebook/hhvm/issues/new) and we'll fix it as soon as we can. We are starting on anything tagged [hi-pri](https://github.com/facebook/hhvm/issues?labels=hi-pri&page=1&state=open) and working down from there. Ask for a priority bump if your issue is blocking your HHVM deployment.
