---
author: dreeves
layout: post
title: Improving Arrays in Hack
category: blog
permalink: /blog/10649/improving-arrays-in-hack
comments:
- id: 671249
  author: Orvid
  date: '2015-10-30 20:25:33 +0000'
  date_gmt: '2015-10-31 03:25:33 +0000'
  content: There are other ways to solve the problems you've presented here, and one
    is to introduce the concepts of immutable and const. I won't go into detail here,
    but if I knew which issue number to reply to, I could go into a bit more detail
    there.
- id: 676865
  author: Josh Watzman
  date: '2015-11-05 03:52:21 +0000'
  date_gmt: '2015-11-05 11:52:21 +0000'
  content: "Immutability has its own issues. IIRC the crux of it is whether it's transitive
    or not (all a class's members must also be immutable). That can be painful to
    program with, but is useful for a ton of compiler optimizations and assumptions.\r\n\r\nFeel
    free to respond to one of the github issues above, or just grab us on IRC, since
    I know you're there anyways :)"
- id: 815669
  author: HHVM update for the week ending 2016-03-04 | Coding Aloud
  date: '2016-03-04 14:24:53 +0000'
  date_gmt: '2016-03-04 22:24:53 +0000'
  content: "[&#8230;] DictArray: initial, runtime support, serialisation, literal
    syntax, converting from an array, runtime [&#8230;]"
- id: 936023
  author: HHVM update for the two months ending 2016-05-20 | Coding Aloud
  date: '2016-05-20 05:09:01 +0000'
  date_gmt: '2016-05-20 12:09:01 +0000'
  content: "[&#8230;] continued work on the Hack array types (dict and vec so far,
    I&#8217;m guessing keyset will be along [&#8230;]"
- id: 949307
  author: Douglas
  date: '2016-05-28 18:56:23 +0000'
  date_gmt: '2016-05-29 01:56:23 +0000'
  content: Hack suffers from quickly adding a bunch of rushed alternatives to the
    same problems and keeping all the old ones.
---

>"*...use collections whenever and wherever possible. However, 100% usage of collections is obviously not realistic given how much arrays are used in various codebases ...there just may be legitimate use cases for an array*"


This is the guidance given to Hack developers on using arrays. While we still advise using collections whenever possible, in hindsight there are more “legitimate use cases” for arrays than we first believed. With that in mind, the team is planning on improving arrays so they are better supported in Hack. We've opened a number of issues on GitHub ([#6451](https://github.com/facebook/hhvm/issues/6451), [#6452](https://github.com/facebook/hhvm/issues/6452), [#6453](https://github.com/facebook/hhvm/issues/6453), [#6454](https://github.com/facebook/hhvm/issues/6454), [#6455](https://github.com/facebook/hhvm/issues/6455)) with our initial plans. Since this would be a significant change in the language we are looking for feedback from the community. Before diving into what we are thinking of building, let's take some time to examine the problem we want to solve.

<!--truncate-->

## The Problem with Arrays in Hack


Arrays are the ubiquitous data structure in PHP, used to represent everything from lists, associated lists, sets, tuples, or even a bag of data. This flexibility itself makes it challenging for Hack to understand how an array will be used. Consider the example below. Should `$arr` be treated as a map-like array that contains both `int` s and `string`s or a shape-like array whose `id` field is an `int`, but `name` is a `string`? Currently whenever the type checker encounters ambiguity like this it errs towards not reporting errors and trusts the programmer knows what he/she is doing.


```php     
$arr = [
  'id' => 4,
  'name' => 'mark',
];
$name = $arr['name'];
$arr[$name] = ucfirst($name);
```



If this was the only problem with PHP arrays, then the solution would be “simple”; make the type checker smarter (something we are working on). However there are a number of other semantic details around arrays that are nearly impossible to analyze statically.


### Indexing non-existent keys


In many languages, attempting to index a non-existent key throws an exception and execution is halted. Instead of halting execution, PHP will raise a `E_NOTICE` and return `null`. The type checker is faced with a difficult decision: should it treat any index operation as producing a potentially nullable value or ignore this possibility? Hack today chooses to ignore the fact that indexing an array may produce a null value, allowing potential bugs to go undetected.


### Key coercion


Arrays only support `string`s or `int`s as keys and coerces invalid types to one of these types. For instance, if a `float` is used as a key, it will be truncated to an `int`. Hack chooses not to support these key coercions and the type checker will report an error if you try to use a `float` as a key. But there is one coercion that the type checker cannot detect, which is the conversion of int-like strings to be `int`. This can lead to unexpected failures at runtime, as demonstrated in the code example below.


```php
function expects_string(string $s): void {}

function will_fail_at_runtime(): void {
 // Hack believes $arr is type array<string, int>
 $arr = array('123' => 123);

 foreach ($arr as $k => $_) {
   // The string '123' will be changed to int(123), triggering a
   // TypeHintException at runtime
   expects_string($k);
 }
}
```




### Arrays containing references


A more subtle semantic detail is how arrays behave when storing references. In particular, in some instances, a reference will be flattened to a value if the array contains the only reference to that value. This behavior is demonstrated below.

```php
$x = 0;
$arr1 = array(&$x);

$arr2 = $arr1;
$arr2[0]++;
var_dump($arr1, $arr2);
/* Changes in $arr2 reflected in $arr1
array(1) {
 [0]=>
 &int(1)
}
array(1) {
 [0]=>
 &int(1)
}
*/

unset($x);
$arr2 = $arr1;
$arr2[0]++;
var_dump($arr1, $arr2);
/* Changes in $arr2 no longer reflected in $arr1
array(1) {
 [0]=>
 int(1)
}
array(1) {
 [0]=>
 int(2)
}
*/
```


Here we begin by storing a reference to `$x` inside an array. We then assign the array to another variable `$arr2` and increment the value stored in the array. Since we stored a reference, the change will be reflected in both `$arr1` and `$arr2`. But if we run the same code after unsetting `$x` we get a different result. When we reassign `$arr1` to `$arr2`, the ref count of `$arr1[0]` drops to one and is flattened to a value. Now changes to `$arr2` are no longer reflected in `$arr1`. This is again behavior the type checker turns a blind eye to when dealing with arrays.


## Legitimate Use Cases


These quirks of arrays motivated the creation of collections in Hack. At the time we believed usage of arrays would dwindle over time and collections would be used everywhere. In retrospect we realized there are legitimate reasons why a programmer may want to choose an array over a collection, primarily due to the fact arrays are values while collections are mutable objects. Arrays being values have certain advantages over collections that cannot be closed without significantly changing how collections work.


### Values are eligible for more optimizations


To understand why this is the case, you have to be familiar with the execution model of HHVM, which was inherited from PHP. PHP has a shared-nothing model where data is not shared between requests. After each request all objects that were allocated are dumped and the next request starts with a clean slate. Consider the following code:

```php
<?hh
class MyConfig {
 private static Map<int, string> $collection = ImmMap {
   ... // statically map 100 ints to some string
 };

 private static array<int, string> $array = array(
   ... // same mapping as above
 );
}
```


In most languages, the static initializer of a variable is run once at the start of the program. However, since HHVM is required to clear the world for each request, static initializers are run for each request. HHVM constructs the `ImmMap` of `MyConfig::$collection` for every request, which can be a non-trivial amount of CPU. Since arrays are value-types, HHVM does not have to reconstruct `MyConfig::$array` for each request. Instead HHVM can initialize the array once at start up and reuse the same array for all requests (assuming the array only contains value types).

For similar reasons, storing and retrieving a collection from APC is more expensive than doing the same thing for an array. Given these performance ramifications, it is reasonable that someone would choose to use an array over a collection in these cases.


### Values are less prone to bugs


Collections are mutable by default. There are cases where this behavior is desirable, but in large part, mutability makes code more difficult to reason about. Consider the following code:

```php
<?hh
abstract final class FriendFetcher {

  /* Memoize the list of friends we fetch for the user */
  <<__Memoize>>
  public static async function forUser(int $id): Awaitable<Set<int>> {
    $ids = await fetch_friend_ids_from_backend($id);
    return new Set($ids);
  }

  public static async function mutualFriends(
    int $id1,
    int $id2,
  ): Awaitable<Set<int>> {
    // fetch both set of friends
    list($friends1, $friends2) = await genva(
      self::forUser($id1),
      self::forUser($id2),
    );

    // Union the two friend sets and retain only those
    // that appear in both sets
    return $friends1
      ->addAll($friends2)
      ->retain(
        $friend ==>
          $friends1->contains($friend) &&
          $friends2->contains($friend)
      );
  }
}
```


This code computes the set of mutual friends between users. This uses a simple algorithm of fetching both users’ set of friends and intersecting them. However there is a subtle bug in this code. `FriendFetcher::forUser` is annotated with `<<__Memoize>>` . This caches the result of the method for a given user ID, saving the cost of fetching from the backend multiple times for the same result. This returns the same `Set` object for a given user. `FriendFetcher::mutualFriends` uses `Set::addAll` to union two sets of friends together, modifying the `Set` instead of returning a new `Set` object. This is the same `Set` object that is cached using the `<<__Memoize>>` annotation. The next time we call `FriendFetcher::forUser` for `$id1`, the `Set` returned will also contain the friends of `$id2`.

There are mechanisms to work around this such as using `ConstSet` to hide the `Set::addAll` method, using `ImmSet` to make it an error to add anything to the set, or making the type checker aware of this potential bug and warning against it. While they would address this particular problem, this illustrates the dangers of defaulting to mutable collections. We considered changing `Set` to be `ImmSet` and introducing a `MutSet` type, but this comes with its own set of complications. When a programmer wants to modify a set, they would need to copy the immutable set to a mutable set, and then remember to make the set immutable again. The copy-on write behavior of arrays is desirable in these cases since it allows writing code as you are working with mutable data, but keeps it local to the function. When an array is passed to or returned from a function, the programmer has the guarantee that it will not be modified unless explicitly passed by reference.


### Values are easier to reason about


Another consequence of the mutable reference semantics of Collections is that their generics are [invariant](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science)). What does this mean? Consider the following code:

```php
function expects_vector_of_mixed(Vector<mixed> $vec): void {
...
}

function expects_vector_of_string(Vector<string> $vec): void {
 // Hack Error!!!
 expects_vector_of_mixed($vec);
}
```


Passing a `Vector<string>` to a function expecting a `Vector<mixed>` is not allowed by the type checker. This is because `expects_vector_of_mixed` could modify `$vec` by adding an `int` and now our `Vector<string>` no longer contains only `string`s. While we should prevent programmers from making this mistake, it is unintuitive to many programmers.

Because arrays are values we can avoid this issue. When an array is passed to another function we know that function cannot modify the array we gave it (assuming you do not use references). The variance of array type parameters are covariant, meaning it is safe to pass an `array<string>` to a function that expects an `array<mixed>`.


## Planned Improvements


Given the trade offs outlined with arrays and collections, we are exploring a third approach that combines the virtues of arrays and collections. It will be a value type like arrays, but have the clean semantics of collections. Details around these new kinds of arrays are being discussed and fleshed out in various issues on GitHub. Here is an outline of what we are thinking of building.




  * [#6451](https://github.com/facebook/hhvm/issues/6451) - Introduce `vec<T>` array type to mirror the `Vector<T>` collection class


  * [#6452](https://github.com/facebook/hhvm/issues/6452) - Introduce `dict<Tk, Tv>` array type to mirror the `Map<Tk, Tv>` collection class


  * [#6453](https://github.com/facebook/hhvm/issues/6453) - Introduce `keyset<T>` array type to mirror the `Set<T>` collection class


  * [#6454](https://github.com/facebook/hhvm/issues/6454) - Give stricter semantics for indexing these array types, while adding support for safely accessing potentially non-existent keys


  * [#6455](https://github.com/facebook/hhvm/issues/6455) - New sugar syntax for de-nesting function calls


If you have thoughts around these ideas, we invite you to join the discussion on GitHub.


## Looking Further Out


Having three different container types adds additional overhead to Hack, but we feel if implemented properly Hack arrays and collections will eliminate almost all legitimate use cases of PHP arrays. We are committed to continuing our support for PHP arrays and collections in the language, but may evolve their role in the future. Here are some really high level ideas we are thinking about.


### PHP arrays for PHP APIs


Hack arrays will replace PHP arrays as the suggested value-type container in Hack, but PHP arrays will still be useful when integrating with PHP code. For instance when creating an .hhi file for a PHP library that expects PHP arrays.

In typical Hack code, PHP arrays should be avoided because of the surprising semantics they have at runtime. To discourage their usage we could change the type checker to be more conservative and report more potential errors with arrays. Some ideas include




  * Make indexing a PHP array produce a nullable type


  * Make storing a `string` key change the key type of a PHP array to `arraykey`


  * Make PHP and Hack arrays incompatible with one another




### Move collections from the runtime to a library


Hack arrays will free up the Collections API from being an exact replacement for arrays. This would allow us to take greater advantage of the fact that these are objects instead of values. One idea is to move the implementation of Collections from a HHVM built-in to a library written in Hack. This would lower the barrier for adding new features/capabilities to Collections. For example supporting objects as keys for `Map` or `Set`, or creating specialized collections like `IntMap` that are optimized for storing integer keys.
