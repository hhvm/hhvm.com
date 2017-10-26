---
title: "The Hack Standard Library: v1.0"
layout: post
author: fred
category: blog
---

Today, [we're releasing](https://github.com/hhvm/hsl/releases/tag/v1.0.0) the first stable version of the Hack Standard Library. The Hack Standard Library addresses several issues:

* existing collection functionality (such as filtering and mapping) either returns PHP arrays, or [Hack Collection objects](https://docs.hhvm.com/hack/collections/introduction); we needed support for [the new `dict`, `keyset`, and `vec` types](https://docs.hhvm.com/hack/collections/hack-arrays) (Hack Arrays).
* we want Hack to have a standard library that is internally consistent.
* many PHP builtins can not be typed in Hack, due to intentional restrictions in the type system: parameters that accept multiple types (e.g. `string | object`) can only be typed as taking `mixed`, and while nullable types are supported (`?sometype`), falseable types aren't - so anything that returns `sometype | false` must be typed as returning `mixed` in Hack.
* we wanted users to be able to add functionality in a manner consistent with the standard library; this wasn't possible with Hack Collections where the functionality was defined as methods on builtin objects - any extensions needed to be committed to HHVM.

Since v0.1, our priority has been finding and addressing inconsistencies in our API; we're grateful to our community for helping us with this, and are proud to release v1.0 without any known issues.

<!--truncate-->

## Getting started

You'll need:

* [HHVM 3.21 or later](https://docs.hhvm.com/hhvm/installation/)
* [Composer](https://getcomposer.org/)
* [An autoloader that supports function autoloading](https://github.com/hhvm/hhvm-autoload)
* [The HSL itself](https://github.com/hhvm/hsl)

After installing HHVM and Composer, the next step is configuring hhvm-autoload via an `hh_autoload.json` file in your project root; full information on options is [in the readme](https://github.com/hhvm/hhvm-autoload#configuration-hh_autoloadjson), however this will be a good starting point for most projects:

```
{
  "roots": [
    "src/"
  ],
  "devRoots": [
    "tests/"
  ],
  "devFailureHandler": "Facebook\\AutoloadMap\\HHClientFallbackHandler"
}
```

With this configuration:

* the contents of `src/`, `tests/`, and `vendor/` will usually be autoloaded; vendor/ library autoloading is implicit, and handled according to each dependency's `hh_autoload.json` or `composer.json`.
* if `--no-dev` is passed to composer, `tests/` will not be autoloaded.
* if `--no-dev` is not passed, and autoloading fails, the autoloader will ask the Hack server where to find the required definition. This usually means that you can add, rename, modify, and delete any Hack autoloadable without having to rebuild the map. Some changes to PHP code will still require running `hhvm composer dump` or `vendor/bin/hh-autoload`

Once you've created the configuration file, you'll need to install hhvm-autoload and the HSL:

```
hhvm composer require hhvm/hhvm-autoload hhvm/hsl
```

Finally, you'll need to use the new autoloader - this is similar to using Composer's autoloader: include `vendor/hh_autoload.php` in your entrypoints, instead of `vendor/autoload.php`. If you are using PHPUnit, you will also need to include this from your bootstrap file; if you don't already have a bootstrap file, you can directly set `vendor/hh_autoload.php` as your bootstrap file.

### Container functions

There are four main groups of functions for interacting with containers:


* [`HH\Lib\Dict`](https://hhvm.github.io/hsl/api/Dict.html):  functions that return a `dict`.
* [`HH\Lib\Keyset`](https://hhvm.github.io/hsl/api/Keyset.html): functions that return a `keyset`.
* [`HH\Lib\Vec`](https://hhvm.github.io/hsl/api/Vec.html): functions that return a `vec`.
* [`HH\Lib\C`](https://hhvm.github.io/hsl/api/C.html): functions that operate on containers, but do not return a container.

For example, mapping and filtering functions exist in each of the `HH\Lib\{Dict, Keyset, Vec}` namespaces, however functions such as `contains()`, `contains_key()`, `count()`, and `reduce()` are in the `HH\Lib\C` namespace.

We recommend using Hack's `use namespace` feature for the HSL, as this allows aliasing the namespaces without affecting the types: while Hack considers names to be case sensitive (e.g. that `vec` and `Vec` do not conflict), the runtime is currently case-insensitive for PHP compatibility.

Operations are generally combined using the pipe operator:

```
<?hh

use namespace HH\Lib\{C, Vec};

function square_then_sum(vec<int> $in): int {
  return $in
    |> Vec\map($$, $x ==> $x * $x)
    |> C\reduce($$, ($acc, $x) ==> $acc + $x, 0);
}
```

The HSL also contains functions for common async operations on containers, such as:

* `HH\Lib\{Dict, Keyset, Vec}\from_async($in)`: create a `(dict|keyset|vec)<T>` from a `(Traversable|KeyedTraverable)<Awaitable<T>>`.
* `HH\Lib\{Dict, Keyset, Vec}\filter_async($in, (function(Tv):Awaitable<bool>) $async_predicate)`: returns a `dict|keyset|vec` containing the values from `$in` where awaiting the predicate returns true.
* `HH\Lib\{Dict, Keyset, Vec}\map_async($in, (function(Tv1):Awaitable<Tv2>) $mapper)`: returns a `dict|keyset|vec` from `$in`, where the values have been replaced with the result of awaiting the specified mapping function.

### Additional functions

The HSL also includes functions for common math and string operations, in the [`HH\Lib\Math`](https://hhvm.github.io/hsl/api/Math.html) and [`HH\Lib\Str`](https://hhvm.github.io/hsl/api/Str.html) namespaces. We expect to both increase the functionality in these namespaces, and start covering additional areas in the future, such as regular expressions.

## What's next?

In the short term, our priorities are to improve the documentation, and to use the HSL to make sure that [our other libraries](https://github.com/hhvm) have full support for the `dict`/`keyset`/`vec` types.

This is just the beginning: now that we have a solid starting point, we'll be adding functionality to the HSL, with the additional goal of eventually removing the need for Hack software to use PHP builtins directly - and once 'Pure Hack' projects are a practical reality, we can explore the possibility of removing the PHP builtins from HHVM itself.
