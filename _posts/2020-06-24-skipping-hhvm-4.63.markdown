---
title: "Skipping HHVM 4.63"
layout: post
author: jjergus
category: blog
---

We have decided to skip this week's regular release, HHVM 4.63.

There have been some bugs that prevented us from publishing the release earlier
this week. Instead of shipping the release only a few days before the next one,
we decided to skip it.

Support for HHVM 4.57 will be extended until the release of HHVM 4.64, scheduled
for next week.

# Breaking Changes

We expect next week's HHVM 4.64 to contain some significant changes affecting
legacy (PHP-style) arrays.

- We expect `array(...)` literals to be completely removed in the next release.
  All code will need to be migrated to `varray[...]` and `darray[...]`, or
  preferably `vec[...]` and `dict[...]` (if it can be done safely).
  - Automated migration is available in [HHAST](https://github.com/hhvm/hhast)
    v4.33.6 or newer: `hhast-migrate --php-arrays`
- The INI flag `hhvm.hack_arr_compat_specialization` will be removed and its
  behavior will be enabled by default. We highly recommend enabling this flag in
  your current HHVM release before upgrading to HHVM 4.64.
  This change disables the implicit inter-operability between `varray`s and
  `darray`s. Instead, `varray` and `darray` will be treated
  as types in their own right. Specifically:
  * Using a `varray` where a `darray` is expected (at parameter and return value
    typehints) will throw, and vice versa. The same goes for property typehints,
    if they are checked at runtime.
  * `varray`s will now maintain a “`vec`-like” layout, with integer keys from 0 to
    (size - 1). Attempting to set a string key in a `varray` will throw, as will
    attempting to unset any element other than the last one.
  * Tuples and shapes are internally represented as `varray`s and `darray`s,
    respectively. As a
    result, `darray is tuple(...)` will return `false` and `darray as tuple(...)`
    will throw. The same goes for `varray is shape(...)` and
    `varray as shape(...)`.
  * Comparing a `varray` and a `darray` using `==` or `===` will always return
    `false`.
  * Attempting to compare `varray`s to `darray`s relationally with `<`, `<=`,
    `>`, or `>=` will result in an exception.


