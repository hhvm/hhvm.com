---
author: fred
layout: post
title: Using XHP with Bootstrap
category: blog
permalink: /blog/6515/using-xhp-with-bootstrap
comments:
- id: 286319
  author: Irfan Raza
  date: '2014-10-23 20:20:19 +0000'
  date_gmt: '2014-10-24 03:20:19 +0000'
  content: Great work guys.
- id: 286919
  author: Josan
  date: '2014-10-24 13:32:07 +0000'
  date_gmt: '2014-10-24 20:32:07 +0000'
  content: This is cool. I'm wondering what project I can use this with.
- id: 287615
  author: chahid khamis
  date: '2014-10-25 11:52:45 +0000'
  date_gmt: '2014-10-25 18:52:45 +0000'
  content: I need ur help. How.may i contact you?
- id: 288743
  author: Fred Emmott
  date: '2014-10-27 09:21:19 +0000'
  date_gmt: '2014-10-27 16:21:19 +0000'
  content: 'Could you file an issue at https:&#47;&#47;github.com&#47;hhvm&#47;xhp-bootstrap
    ? I''m also usually on freenode (nick: ''fred'') during Pacific hours'
- id: 480791
  author: Facebooks XHP in inniger Einigkeit mit Bootstrap - entwickler.de
  date: '2015-05-08 02:38:57 +0000'
  date_gmt: '2015-05-08 09:38:57 +0000'
  content: "[&#8230;] Vorteile findet man in der Vorstellung Using XHP with Bootstrap.
    Das Projekt selbst findet man auf GitHub. Alles, was man dann noch ben&ouml;tigt,
    ist die HHVM und [&#8230;]"
- id: 517067
  author: Cobis
  date: '2015-06-08 05:23:05 +0000'
  date_gmt: '2015-06-08 12:23:05 +0000'
  content: "Excellent. But may be you want to try this other tool:\r\n\r\nhttp:&#47;&#47;codecanyon.net&#47;item&#47;boothelp&#47;11636009"
---

![xhpbootstrap_logo_blacktext](/static/images/posts/xhpbootstrap_logo_blacktext.png)

[XHP](https://github.com/facebook/xhp) is a great way to safely create HTML user interfaces from PHP or Hack. We love how extensible it is, allowing you to create your own pseudo-elements that are composed of more basic building blocks - ultimately a series of HTML tags. This solves a similar problem to partial templates in other systems. At its most basic level, XHP provides an XML-like syntax for creating stringable objects representing markup:

<!--truncate-->

```php
<?php
function render_without_xhp($css_class, $content) {
  // Use htmlspecialchars() in case $content contains
  // '<script>do_malicious_stuff();</script>' or similar
  print '<span class="'.htmlspecialchars($css_class).'">'.
    htmlspecialchars($content).'</span>';
}

function render_with_xhp($css_class, $content) {
  print <span class={$css_class}>{$content}</span>;
}
```


Today, we're releasing [XHP-Bootstrap](http://bootstrap.hhvm.com) (source is [on GitHub](https://github.com/hhvm/xhp-bootstrap)), combining the safety of XHP with the power of the popular [Bootstrap framework](http://getbootstrap.com/); for example, you can create a dropdown menu like this:

```
print
  <bootstrap:dropdown>
    <bootstrap:button>
      Dropdown
      <bootstrap:caret />
    </bootstrap:button>
    <bootstrap:dropdown:menu>
      <bootstrap:dropdown:item href="#">
        Foo
      </bootstrap:dropdown:item>
      <bootstrap:dropdown:item href="#">
        Bar
      </bootstrap:dropdown:item>
      <bootstrap:dropdown:item disabled="true" href="#">
        Disabled
      </bootstrap:dropdown:item>
    </bootstrap:dropdown:menu>
  </bootstrap:dropdown>;
```

This produces the following:

![Screen Shot 2014-10-21 at 12.30.35 PM](/static/images/posts/Screen-Shot-2014-10-21-at-12.30.35-PM.png)

[The documentation](http://bootstrap.hhvm.com) includes live examples for all supported elements, [including dropdowns](http://bootstrap.hhvm.com/example.php?classname=xhp_bootstrap__dropdown).

One common question is why you'd want to do this instead of just using the CSS classes that bootstrap recognizes directly - there's a few major advantages which can dramatically reduce debugging/development time:


  * Validation - typo'ing a class name in CSS just results in it being ignored - you'll have a mis-rendered page, but not much debugging information.  HHVM will tell you if you use an invalid element name, and XHP will tell you about mistakes with the attributes


  * Semantic markup (server-side) - the element name describes exactly what it is, instead of everything being a <div> or <span> with the meaning being hidden in a class.


  * Encapsulation/implementation hiding - creating complex CSS components often requires a markup tree that doesn't actually make sense for the content (e.g. deeply nested <div>'s), but is needed to apply the required formatting. Doing this every time you want to use the components leads to duplicated code, and it's very easy to make mistakes.


  * Easier upgrade path - if Bootstrap makes incompatible changes or current behavior becomes deprecated, XHP-Bootstrap could automatically start using the new behavior with no changes to your code, or raise clear and easy-to-debug exceptions. This depends on how Bootstrap itself evolves in the future, and we hope to work with the community to decide on the best way for XHP-Bootstrap to handle any issues.


XHP is well-loved by our frontend engineers, and we wanted to make it more useful to the community - at one of Facebook's hackathons (where we're encouraged to work on anything that we wouldn't usually) we decided that this would be a good first step. We've included all the basic components, and we're looking forward to hearing your feedback.
