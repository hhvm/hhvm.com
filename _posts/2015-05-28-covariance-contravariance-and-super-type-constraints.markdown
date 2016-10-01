---
author: jezng
comments: true
layout: post
title: Covariance, Contravariance, and super Type Constraints
category: blog
redirect_from:
  - /blog/9215/covariance-contravariance-and-super-type-constraints
---

Hack has recently enhanced its generics with two features: variance annotations and `super` type constraints. In this post, I'll explain how they work and why they were added.

<!--truncate-->

## Variance


Variance describes how the type parameters of a class affect subtyping. For example, consider `Vector<T>`. Should `Vector<int>` be a subtype of `Vector<mixed>`? That is, since `int` is a subtype of `mixed`, should `Vector<int>` and `Vector<mixed>` vary in the same way? Type parameters that behave this way are called covariant type parameters.

Many people would answer “yes” to the question above; indeed, it does seem intuitively right. However, treating `Vector` as covariant can actually break type safety, as the following code demonstrates:

```php
<?hh

class Vector<T> {
  // This is a subset of the actual Vector API.
  public function set(int $k, T $x): void {...}
  public function get(int $k): T {...}
}

function f(Vector<mixed> $x) {
  $x->set(0, 'a');
}

function g(Vector<int> $x) {
  f($x);
  // The typechecker only uses the information in the
  // signature of f to infer the type of $x, and the
  // type signature (function(Vector<mixed>)) doesn't
  // give any indication that the contents of $x could
  // be modified. Thus, the typechecker believes that
  // $x is still of type Vector<int> at this point.
  // However, this leads to a type error because we
  // end up adding 'a' to an integer below.
  return $x->get(0) + 1;
}
```

In function `f`, since `$x` is a `Vector<mixed>`, we allow elements of any type to be added to it. However, this means that after calling `f($x)`, `$x` is no longer a `Vector<int>` but a `Vector<mixed>`. The caller of `f` doesn't know anything about this, however, and continues to treat it like a `Vector<int>`, with confusing results.

Clearly, we should ban `Vector<T>::set`1 from being used if we want `Vector<T>` to be covariant, to prevent the type of `T` getting changed without the typechecker's knowledge. Indeed, the example above is rejected by the typechecker for this reason.

Roughly speaking, covariant type parameters can only be used to annotate read-only values. To be more precise, however, the issue is that `T` occurs as parameter type. We're telling `set` that it can expect to be passed values that are subtypes of `T`. But if we can treat a `Vector<int>` as a `Vector<mixed>`, then we can pass in types that are more general than `T`, thus breaking type safety.

The solution to this is to disallow covariance if `T` occurs as a parameter type or as the type of a mutable member. Moreover, for the sake of clarity, we require the user to declare explicitly whether a type should be covariant via the `+` annotation. If it is thus annotated, the typechecker will complain if it finds that type being used as the type of a method parameter, or the type of a member variable. As one might expect from the preceding discussion, the `ConstVector` interface in Hack satisfies these restrictions.2 (Indeed, covariance is the primary reason why we introduced `ConstVector` .) Here's a sampling of the `ConstVector` API:


```php
<?hh
interface ConstVector<+T> {
  /* This is illegal now since T is declared as covariant: */
  /* public function set(int $k, T $x): void; */
  public function get(int $k): T;
}

class Vector<T> implements ConstVector<T> {
  public function set(int $k, T $x): void {...}
  public function get(int $k): T {...}
}
```




## Contravariance


Contravariance is the opposite of covariance. We might have a contravariant class as follows:


```php
<?hh
class Handler<-T> {
  public function handle(T $x): void {...}
}
```

A contravariant type parameter has the opposite restriction of a covariant one: it can be used as a parameter type but not as a return type. As the name `Handler` suggests, contravariant type parameters are often useful for typing things that act like callbacks. Again, as a rough analogy, contravariant type parameters can only be used to annotate write-only values. I won't go into too much more detail here, but [Wikipedia](http://en.wikipedia.org/wiki/Covariance_and_contravariance_%28computer_science%29) has more information for the interested reader.


## Typing `ConstVector::concat`, or why we need `super` type constraints


We have established that `ConstVector<T>`'s immutability allows it to be covariant with respect to `T` — in contrast to `Vector<T>`, whose potential to be modified in-place means that it cannot be covariant. However, it seems eminently reasonable to allow methods on `ConstVector` that create new `ConstVector`s from the current one. `ConstVector::concat` is a case in point — it takes a second vector and returns a new vector that is the concatenation of the two, leaving the original vectors unmodified. Naively, we might write it like so:

```php
<?hh
interface ConstVector<+T> {
  public function concat(ConstVector<T> $x): ConstVector<T>;
}
```

But `T` is occurring as a parameter type, which we've demonstrated could be unsound! Even if we were to allow it, notice that this signature is overly restrictive: It allows you to concatenate a `Vector<int>` to a `Vector<num>`, since `int` is a subtype of `num`, but it doesn't allow you to concatenate a `Vector<int>` to a `Vector<float>`, even though one can reasonably type the return value as a `Vector<num>`.

One might notice that the implementation of `concat` really doesn't care what types the vector elements have — it just cares that it has two `Vector`s. So we could correctly type it as


    concat(ConstVector<mixed> $x): ConstVector<mixed>


But this loses type information; now the callers don't know anything about the elements of the returned `Vector`. On further reflection, one might realize that since we're putting elements of two different types into one vector, the type of the resulting vector must be a supertype of both of them. Hence we arrive at the following type signature:


    concat<Tu super T>(ConstVector<Tu> $x): ConstVector<Tu>


To see how this type signature gets interpreted, suppose we pass a `Vector<float>` as the argument to `Vector<int>::concat`. Since the argument must be a subtype of the parameter type `ConstVector<Tu>`, the typechecker knows that `float` is a subtype of `Tu`. Since we're calling the `concat` method on an object of type `Vector<int>`, the typechecker also knows that `Tu super int` is true, i.e. that `int` is a subtype of `Tu`. Thus it can conclude that `Tu` must either be a `num` or a `mixed` type.

Note that this type signature also avoids the problem of having `T` as a parameter type.


## How `super` relates to `as` constraints


As the reader may know, Hack has had support for `as` [type constraints](http://docs.hhvm.com/manual/en/hack.generics.constraints.php) for a while now. `T as Foo` asserts that `T` must be a subtype of `Foo`. `super` constraints complete the picture; now we can use `T super Foo` to assert that `T` must be a supertype of some class `Foo`. One might wonder why a new keyword was introduced for this; wouldn't `Foo as T` do the job in a more symmetric way? Perhaps so, but we felt it could lead to some confusion. Right now, `T as Foo` declares a new type `T` to be a subtype of the already-declared type `Foo`. If `Foo` is not declared yet it is an error. Likewise, in `T super Foo`, `Foo` must refer to an already-declared type. Allowing `Foo as T` would make it harder to discern which type is being declared.


## Historical Note


Before Hack supported variance annotations, all user-implemented generic type parameters could only be invariant. However, this was pretty untenable for container-style classes like `Vector`; as we've demonstrated, their natural use cases often rely on covariance. Thus we [hard-coded a list of class names](https://github.com/facebook/hhvm/blob/3b4b031d4aa1e8fbbd4d227d9684cf3833c0d954/hphp/hack/src/typing/typing_subtype.ml#L173) to be considered co- or contravariant by the typechecker. This was awkward to maintain and extend, and it had the unfortunate side-effect of exposing Facebook-internal class names in the typechecker. Additionally, without support for `super`, we were forced to type methods like `concat` using the more restrictive type signature above.


## Footnotes


1 Calling `$x->set(0, 'a')` is the same as doing `$x[0] = 'a'`. Likewise, `$x->get(0)` is the same as `$x[0]`. I've used `set` and `get` in these examples because they make it easier to talk about the relation between covariance and parameter types / return types.
2 `ConstVector` is actually more restrictive than required for covariance. That is, it is possible to have a covariant interface to `Vector` that isn't totally `Const` — we could expose `Vector::pop()`, for instance.
