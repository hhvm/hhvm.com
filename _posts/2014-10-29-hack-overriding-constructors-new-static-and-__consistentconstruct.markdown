---
author: jwatzman
layout: post
title: 'Hack: Overriding Constructors, "new static", and __ConsistentConstruct'
category: blog
permalink: /blog/6473/hack-overriding-constructors-new-static-and-__consistentconstruct
comments:
- id: 292469
  author: Jesse Schalken
  author_email: me@jesseschalken.com
  author_url: http://jesseschalken.com
  date: '2014-11-02 16:05:03 +0000'
  date_gmt: '2014-11-03 00:05:03 +0000'
  content: "Can a class be instantiated if the class name is a type parameter which
    has <>?\r\n\r\nExample:\r\n\r\n<>\r\nabstract class A {\r\n  function __construct(private
    int $x) {}\r\n}\r\n\r\nclass B {\r\n  function blah() {\r\n    $a = new T(6);
    &#47;&#47; <- should be okay since T must be an A which has a consistent constructor\r\n
    \ }\r\n}"
- id: 292871
  author: Josh Watzman
  author_email: jwatzman@fb.com
  author_url: https://www.facebook.com/jwatzman
  date: '2014-11-03 10:00:46 +0000'
  date_gmt: '2014-11-03 18:00:46 +0000'
  content: I don't follow your example -- what is `<>`? Your example isn't valid Hack
    code.
- id: 293507
  author: Jesse Schalken
  author_email: me@jesseschalken.com
  author_url: http://jesseschalken.com
  date: '2014-11-04 19:03:48 +0000'
  date_gmt: '2014-11-05 03:03:48 +0000'
  content: "Sorry, the reply form mangled my comment :( (maybe it's doing a strip_tags
    or something?)\r\n\r\nMy example is here: http:&#47;&#47;pastebin.com&#47;vQgRyjV7"
- id: 293771
  author: Josh Watzman
  author_email: jwatzman@fb.com
  author_url: https://www.facebook.com/jwatzman
  date: '2014-11-05 10:43:23 +0000'
  date_gmt: '2014-11-05 18:43:23 +0000'
  content: "You can't do `new T()` in Hack -- we have type erasure semantics for generics,
    so we don't actually know what `T` is at runtime.\r\n\r\nOr am I missing the point
    of the example for this? (Can you give a specific example that the typechecker
    gives the wrong result for now?)"
- id: 293879
  author: Jesse Schalken
  author_email: me@jesseschalken.com
  author_url: http://jesseschalken.com
  date: '2014-11-05 15:08:36 +0000'
  date_gmt: '2014-11-05 23:08:36 +0000'
  content: Ahh, so `static` can be resolved at runtime, but a type parameter can't.
    (so type parameters are more like Java than C#) That answers my question, thanks!
- id: 304589
  author: PHP News You May Have Missed - October &#47; November 2014
  author_email: ''
  author_url: http://www.sitepoint.com/php-news-may-missed-october-november-2014/
  date: '2014-11-26 10:03:19 +0000'
  date_gmt: '2014-11-26 18:03:19 +0000'
  content: "[&#8230;] explained in this blog post, hack has been upgraded with some
    new features. Due to Hack already supporting static typing, [&#8230;]"
- id: 386471
  author: john
  author_email: jonnmso@gmail.com
  author_url: ''
  date: '2015-02-21 04:03:16 +0000'
  date_gmt: '2015-02-21 12:03:16 +0000'
  content: "which editors can I use to program with HACK ?\r\nPlease help.."
---

A recent addition to Hack is the `__ConsistentConstruct` attribute, which allows `new static()` to be safely, properly typed. The need for this special attribute first requires some background in how method overriding and polymorphism normally work, and how constructors are special.

<!--truncate-->

When overriding a method, there are only specific ways that its type signature can be changed. For example, if a superclass has a method that promises to return an `int`, a subclass cannot override that method and change its signature to return a `?int`, since it might give a `null` to code polymorphically calling that method! For example:


```php
<?hh

class Superclass {
  public function f(): int {
    return 42;
  }
}

class Subclass extends Superclass {
  // ERROR: Illegal override, because...
  public function f(): ?int {
    return null;
  }
}

function g(Superclass $s) {
  // ... if $s is actually polymorphically a Subclass,
  // then $x will be null even though we promised it would
  // be an int!
  $x = $s->f();
}
```



`Superclass::f` promises callers that invoking that method on any instance of `Superclass` will return an `int`, but `Subclass::f` break that promise by sometimes returning `null`. The principles that govern how exactly overriding can be done safely are called the rules of [_covariance_ and _contravariance_](http://en.wikipedia.org/wiki/Covariance_and_contravariance_%28computer_science%29), which we'll come back to in detail in a later post.

Importantly, these rules only apply when a method might be polymorphically called. If you always know exactly which method is going to be called, then you can know its exact type, and none of these issues come into play. Constructors are one place where you always know exactly which method you are calling, with no chance for polymorphism, since you're always explicitly stating exactly which class you're instantiating! The Hack team found such overrides to be a fairly common pattern. Since it is useful and can be done safely, Hack relaxes these overriding rules for `__construct`, and will allow you to override a constructor with any other signature. For example:


```php
<?hh

class Widget {
  public function __construct(private string $color) {}

  public function getColor(): string {
    return $this->color;
  }
}

class SubWidget extends Widget {
  // Safe override!
  public function __construct(private int $size) {
    // SubWidget objects are always red.
    parent::construct('red');
  }

  public function getSize(): int {
    return $this->size;
  }
}
```



But it turns out that there's actually one place where you can call a constructor yet you don't know exactly which class you're instantiating, and so don't know exactly which signature to use: [`new static()`](http://php.net/manual/en/language.oop5.late-static-bindings.php). In the above example, if `Widget` had a call to `new static()`, since that could be constructing either a `Widget` or a `SubWidget`, depending on how exactly the method was called, the Hack typechecker wouldn't be able to know which set of constructor arguments to use. Until recently, the typechecker didn't have a good way to deal with `new static()`. (Technically, the same problem applies to `new $classname()`, but that highly dynamic code is impossible to check, and is disallowed in [strict mode](http://docs.hhvm.com/manual/en/hack.modes.php) altogether.)

Now, we have a new feature that allows you to properly typecheck `new static()`: the `__ConsistentConstruct` attribute. This attribute causes the typechecker to apply the usual rules of method overriding to constructors as well. This means that `new static()` can be called safely, since the type of the constructor is guaranteed -- and without the attribute, the typechecker will reject calls to `new static()`.

![640px-Malaysia_-_Malaka_-_22_-_identical_buildings_(6320845486)](/static/images/posts/640px-Malaysia_-_Malaka_-_22_-_identical_buildings_6320845486.jpg)

Here's an example.


```php
<?hh

<<__ConsistentConstruct>>
class C {
  protected function __construct() {
    // Secret things in a secret constructor!
  }

  final public static function make(): this {
    // Safe: since this class is __ConsistentConstruct, we know
    // that all our subclasses have constructors that take the
    // same arguments that we do, through the usual method
    // overriding rules. If we didn't have __ConsistentConstruct
    // then "new static" is an error, since it can't be used safely!
    return new static();
  }
}

class D extends C {
  // __ConsistentConstruct on our parent prevents us from changing
  // this constructor in incompatible ways.
  protected function __construct() {
    parent::__construct();
    // Other secret things!
  }
}
```



If you aren't familiar with the `<<Foo>>` syntax, it's a Hack feature called [user attributes](http://docs.hhvm.com/manual/en/hack.attributes.php). Since `__ConsistentConstruct` is an attribute that has special meaning to Hack, it's prefixed with two underscores, just like `__toString` and other similarly "magic" names.

So that's it for `ConsistentConstruct`. It's just a way to ensure type safety so that factory methods or other users of late static binding and `new static()`. A straightforward feature, but one that is surprisingly useful!

[Full information on  is available in the Hack documentation.](http://docs.hhvm.com/manual/en/hack.attributes.consistentconstruct.php)

That's all for now, but we've got plenty more features to talk about in later posts. If you have any questions, please leave them in the comments below!
