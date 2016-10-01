---
author: fred
comments: true
layout: post
title: Compatibility Update
category: blog
redirect_from:
  - /blog/4841/compatibility-update
---

[Earlier this year](http://hhvm.com/blog/3743/hhvm-the-next-six-months) we set an ambitious goal of passing the PHPUnit test suites of 20 popular frameworks by the end of June; at the time, we were passing on only 6! With a huge amount of help from the community (especially our [OpenAcademy](https://www.facebook.com/OpenAcademyProgram) students), we're proud to have hit this goal more than 2 months early, and we have more frameworks expected to reach 100% shortly.

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
