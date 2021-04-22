---
title: "Removing Implicit Coercions"
layout: post
author: dizzy
category: blog
---

tl/dr: we’re doubling down on removing surprising implicit (and some explicit) coercions from the language. So far we

* are very close to having object → num conversion trigger exceptions
* have pieces in flight for the removal of coercions due to string interpolation/concatenation, mathematical operations (including bitwise), and pre/post increment/decrement
* have concrete plans for comparison operators, the (in)equality operators, and switch statements.

## Context

Implicit coercions can be unintuitive in edge cases, and these edge cases can be surprisingly common - making them the second most confusing language feature, behind arrays. Even those working on the language often make mistakes, and they are frequently a source of subtle bugs.

For those who don’t know, an implicit coercion is when a value of type A gets converted to type B as part of computing the result of an operation. Probably the most common example is how `0 == false` results in `true` courtesy of `0` being converted to `false` prior to the comparison, but things go straight downhill from there (hint: try comparing `'0'` with `false` and then `'0'` with `null`). We’ve determined that the time has finally come to tackle this once and for all. 

## So what are we going to do about it?

Well, we’ve actually already started doing something about it! Very shortly, attempting to convert an object into a number will universally throw an exception. On top of this almost finished step, we have a few portions in flight, as well as a few more not started but still very much planned.

For the following, the possible stages are

1. No Progress - Allowed by both the Type Checker and runtime. Lints may exist.
2. Enforced By Type Checker - the Type checker will report errors
3. Soft Runtime Enforcement - Violations may trigger logs via the runtime, configurable via flag.
4. Hard Runtime Enforcement - Violations will produce a runtime exception
5. New Behaviour - Following stage 4, we may decide to re-allow the operation but with a different result.

These stages are ordered such that by a certain stage, all previous stages are implied.

### String Concatenation (`.` , `.=`) interpolation

**Current Behaviour:**
int, null, bool, float, and resource will implicitly coerce to string

```
'' . true; // '1'
```

**Future Behaviour:**
*only* int will implicitly coerce. The rest will trigger exceptions
Example:

```
'' . true; // `InvalidOperationException` 
'one: ' . 1; // 'one: 1'
```

**Status of rollout:** 
Soft Runtime Enforcement

### Bitwise operations (`&`, `|`, `^`, `~`, `<<`, `>>`) and assignment equivalents

**Current Behaviour:**

`&`, `|`, `^`: null, bool, float, vec, dict, keyset, and resource will implicitly coerce to int. strings will implicitly coerce as well *unless* both operands are strings.

```
null & vec[]; // 0
keyset[1] & true; // 1
'abcd' & 'efgh'; // 'abc`'
```

`~`: floats will implicitly coerce to int

```
~1.2; // -2
```

`<<`, `>>`: null, bool, float, string, vec, dict, keyset, and resource will implicitly coerce to int

```
keyset[1] << true; // 2
```

**Future Behaviour:**
`&`, `|`, `^`: no operations will coerce. Attempting to operate on a non-int (unless both operands are strings) will trigger an exception.

```
null & vec[]; // InvalidOperationException
keyset[1] & true; // InvalidOperationException
'abcd' & 'efgh'; // 'abc`' - https://3v4l.org/CTH2o
```

`~`: no operations will coerce. Attempting to operate on a non-int or string will trigger an exception.

```
~1.2; // InvalidOperationException
```

`<<`, `>>`: no operations will coerce. Attempting to operate on a non-int will trigger an exception.

```
keyset[1] << true; // InvalidOperationException
```

**Status of rollout:** 
Soft Runtime Enforcement

### Pre/post increment/decrement

**Current Behaviour:**
Incrementing null, decrementing an empty string, and inc/dec a “numeric” string will implicitly coerce to int.

```
$x = null; ++$x; // 1
$x = ''; --$x; // -1
$x = ''; ++$x; // '1'
$x = '1.123'; ++$x; // 2.123
$x = '1bananas'; ++$x; // '1bananat'
$x = 'abcd'; ++$x; // 'abce'
```

**Future Behaviour:**
No operations will coerce. Additionally banning incrementing an empty string for consistency. The only valid values for inc/dec are ints, floats, and non-numeric strings. Note that while inc/dec a non-numeric string is still “legal,” it’s not necessarily a great idea.

```
$x = null; ++$x; // InvalidOperationException
$x = ''; --$x; // InvalidOperationException
$x = ''; ++$x; // InvalidOperationException
$x = '1.123'; ++$x; // InvalidOperationException
$x = '1bananas'; ++$x; // '1bananat'
$x = 'abcd'; ++$x; // 'abce'
```

**Status of rollout:** 
Soft Runtime Enforcement

### Mathematical operations (`+`, `-`, `*`, `/`, `%`, `**`) and assignment equivalents

**Current Behaviour:**
null, bool, string, and resource will coerce to int / float depending on the other operand (defaulting to int for two non-num operands)

```
null + true; // 1
```

**Future Behaviour:**
Operating on anything other than ints and floats will trigger an exception, with floats additionally being banned for use with `%`. It’s worth noting that we specifically decided to allow implicit coercions between ints and floats in this context.

```
null + true; // InvalidOperationException
```

**Status of rollout:** 
Soft Runtime Enforcement

### Comparison operations (`<` ,`<=`, `>` , `>=`, `<=>`)

**Current Behaviour:**
Attempting to list all the situations in which coercions happen and between which types would result in this post being twice as long. That should give you an idea of how much work this step will be.

```
null >= false; // true
false < new Foo(); // true
false < Foo::class; // true
true < Foo::class; // false
true > Foo::class; // false
```

**Future Behaviour:**
Comparing values of two different types will throw an exception. A notable exception to this will be comparing ints and floats. In that case, comparison works as you’d expect, with the usual caveats about comparisons involving two approximately equal floats (including an approximately equal int and float).

```
null >= false; // InvalidOperationException
false < new Foo(); // InvalidOperationException
false < Foo::class; // InvalidOperationException
true < Foo::class; // InvalidOperationException
true > Foo::class; // InvalidOperationException
```

**Status of rollout:** 
Enforced By Type Checker

### Equality operations (`==`, `!=`)

**Current Behaviour:**
All the same combinations of types trigger coercions as with the comparison operators, but with *even more* situations resulting in coercions.

```
null == false; // true
false == new Foo(); // false
false == Foo::class; // false
true == Foo::class; // true
```

**Future Behaviour:**
There will be two steps to this, going through both Hard Runtime Enforcement and then New Behaviour. First, comparing values of two different types will throw an exception. Then, comparing values of two different types will simply be false.

```
null == false; // InvalidOperationException then false
false == new Foo(); // InvalidOperationException then false
false == Foo::class; // InvalidOperationException then false
true == Foo::class; // InvalidOperationException then false
```

**Status of rollout:** 
No Progress

### Switch statements

This is may be a surprise to you, but switch statements utilize `==` under the hood and so result in all the same coercions. As such, refer to that section for current and future behaviour.

### **Long Tail**

In addition to the above major operational line items, we continue to discover a long tail of more minor coercions that will necessarily be tackled by this work, including things such as indexing into strings with other strings. 

## Next Steps

After this change, `==` and `===` will be very similar semantically, with the only major remaining differences appearing when operating on arrays and objects. This could make it confusing which one should be used. As a follow up, we will evaluate potentially removing one of the operators.

Additionally, there are a handful of above operations that don’t trigger coercions but we consider dubious nonetheless. Examples of this include bitwise operations and inc/dec on strings. As a followup, we will consider what to do about these operations.
