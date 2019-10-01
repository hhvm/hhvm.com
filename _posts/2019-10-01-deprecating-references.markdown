---
title: "Deprecating &$references"
layout: post
author: dneiter
category: blog
---

PHP-style references (`&$variable`) have been a source of confusion and
unsoundness in the Hack type system (read on to learn why). After a long
effort, we are now finally ready to remove them from the Hack language.

**We expect to remove support for PHP-style references from HHVM in about
2&ndash;4 weeks.**


## Migrating your code

By far the most common use case for PHP references is passing function arguments
by reference.
[Inout parameters](https://docs.hhvm.com/hack/functions/inout-parameters) are
built to address this use case without relying on PHP references. See also
[Migrating to inout parameters](https://docs.hhvm.com/hack/functions/inout-parameters#references-deprecated__migrating-to-inout-parameters).

We have updated all built-in functions with reference parameters (such as
`sort()`, `array_pop()`, or `preg_match()` with a `&$matches` argument) to use
inout parameters instead. In some cases, the function that takes an inout
argument has a new name (e.g. `preg_match_with_matches()`). You can migrate your
calls automatically using HHAST v4.21.7 or newer:

```
hhast-migrate --ref-to-inout
```

For references other than function parameters, the
[`Ref`](https://docs.hhvm.com/hsl/reference/class/HH.Lib.Ref/) class can be used
to explicitly achieve reference semantics when necessary. A common example is
needing to share mutable state between a lambda and enclosing function:

```php
function sort_and_count_comparisons(inout vec<int> $a): int {
  $comparisons = Ref(0);
  \usort(
    inout $a,
    ($left, $right) ==> {
      $comparisons->value++;
      return $left - $right;
    }
  );
  return $comparisons->value;
}
```

## What are PHP references?

PHP references allow the same variable to be accessed using multiple different
names. Changes done via one reference are visible through all references to the
same variable. Let’s look at a simple example (all examples use PHP7 unless
noted otherwise, as Hack no longer supports most of reference behaviors):

```php
$var = 'abc';
$other_var = &$var;          // $other_var is now an alias to $var
$one_more_var = &$other_var; // $one_more_var is also an alias to $var
$arr['key'] = &$var;         // references can be stored inside arrays
$obj->prop = &$var;          // and in object properties

$other_var = 'def';          // $var, $other_var, $arr['key'] and $obj->prop now contain 'def'

foreach($arr as &$x) {       // iterate over array by reference
  ++$x;                      // modifying $x modifies $arr elements
}

function &returns_ref(&$arr) {
  return $arr['key'];        // references can be returned from functions
}
// functions can take parameters by reference
function increment(&$value) {
  $value += 1;
}
```

References are widely used in PHP standard library&mdash;`sort()`,
`array_pop()`, `preg_match()` to name a few most frequently used examples.


## References can be confusing

Let’s look at another example:

```php
$arr = array(0, 1, 2);
foreach ($arr as &$v) {
  $v += 1;
}
foreach ($arr as $v) {
  var_dump($v);
}
```

What is the produced output, and more importantly why does it work this way?
([Spoilers](https://3v4l.org/BeGi3)).

This is almost never intended behavior, and the resulting issue is very easy to
miss. As part of deprecating foreach-by-reference support at Facebook we have
discovered multiple bugs, following this pattern.


## References are unsound

PHP references are a major blocker for making the Hack type system sound (i.e.
reaching the point where Hack typechecker is correct about types 100% of time).
PHP references were designed for a dynamically typed language and they cannot
be modeled in Hack type system without significantly restricting their power.

The unsoundness problem is best illustrated by another example
([3v4l](https://3v4l.org/A2gKE)):

```php
class Foo {
  public $prop;
}

$foo = new Foo();

$str = 'abc';          // $str is a string
$foo->prop = &$str;
var_dump($foo->prop);  // "abc"

$arr = array();
$foo->prop = $arr;
var_dump($foo->prop);  // array()
var_dump($str);        // array() - surprise! $str is now an array
```


## HHVM wins

PHP references are a significant source of complexity and performance overhead
in HHVM. Moreover, references make it possible for Hack code to observe a number
of runtime implementation details (e.g. reference counting), blocking HHVM team
from exploring more efficient alternatives.

Multiple efforts in HHVM have already taken advantage of references removal. All
of these provided significant measurable CPU improvements when we deployed them
to Facebook servers:

* [Property type enforcement](https://hhvm.com/blog/2019/04/09/hhvm-4.1.0.html#property-type-enforcement)&mdash;binding
  references to typed properties is disallowed
* [Hack arrays](https://docs.hhvm.com/hack/built-in-types/arrays)&mdash;references
  to Hack array elements are disallowed
* improvements around handling function calls in HHVM internals&mdash;made
  possible by requiring reference (and inout) parameters to be annotated at call
  sites

With references removal now complete, we expect more wins down the line.
