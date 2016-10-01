---
author: kasper
comments: true
layout: post
title: Trait and interface requirements in Hack
category: blog
redirect_from:
  - /blog/9581/trait-and-interface-requirements-in-hack
---

In PHP, [traits](http://docs.hhvm.com/manual/en/hack.traits.php) are a mechanism of code reuse that, while very powerful, are also difficult to type check both efficiently and exhaustively. In this post we’ll dive more deeply into the reasons for that and see how Hack solves those problems, allowing you to use traits in a safe way without limiting their expressiveness.

To jog your memory: traits are bundles of code that can be dropped into any class to extends its functionality:


    trait T {
      public function f(string $s): string {
        ...
      }
    }

    class C {
      use T; // line that makes calls to $this->f(...) possible

      public function test(): string {
        return $this->f('foo');
      }
    }


At runtime, **using** the trait results in its body being basically copy-pasted into the using class. Trait code can then call class methods freely - to make it safe we need to ensure that those methods even exist, and that they accept and return expected types:


    // Note: this is a hypothetical example of kind of mistake that
    // we would like to catch. The type checker will actually prevent
    // it by rejecting the definition of T written here as not safe
    // - see discussion below.
    trait T {
      private function f(string $s): string {
        return $this->g();
      }
    }

    class C {
      use T;

      public function test(): void {
        $this->f("foo"); // ERROR: f will try calling g, which doesn't exist
      }                  // in this class

    }


So, how is this situation different from checking any other function and why can’t Hack _just work_ and do it? The key difference here is that the unsoundness might not be contained in the trait **definition** (its body) itself, nor in **using its declaration** at particular location, but depend on both of them. In the example above, it's not possible to look at the body of function `f` and say if it's correct or not (it depends on what `$this` is), nor is it possible to look at body of `C` and, knowing only signatures of functions in `T`, say whether using `T` there is safe -- it depends on what those functions do with `$this`.

Because of this, in PHP's unrestricted copy-paste model, in order to check trait usage we need the actual bodies, not just the definitions. This means that changing a single character in a trait function body would require going through all the classes using it and re-checking them. To understand why this is unacceptable, we need to look back at Hack original design goals.


## Hack type checker performance


One of the reasons why PHP was successful at Facebook is that it facilitates our _move fast_ philosophy: you can write your code, refresh the browser window or run your script, and immediately see the results, allowing you to iterate quickly. Jamming a “wait 20 seconds until we re-check your code” in between those two steps would either discourage people from using the type checker, or be a serious blow to developer productivity, so one of the Hack goals was high responsiveness and incremental mode. Most changes you do should be verified in less than 200 milliseconds, with only bigger ones (like a rebase that changes hundreds of files, or change to a function signature that is used in thousands of places) taking few seconds. This has to hold true for Facebook codebase, which contains millions of lines of code. This speed is also crucial for making a [Hack IDE](http://nuclide.io/) responsive and usable.

Hack achieves this performance by using function and class declarations as barriers that it never needs to cross when type checking. After gathering all the declarations, every file can be checked independently of others. In particular:




  * when function definition (body) has changed (the most common operation when writing code), we only need to re-check this one function - its declaration hasn’t changed, so there are definitely no new errors for its users


  * when changing function declaration (way less common), we only need to re-check the users of this function, which we know because Hack server keeps track of them




## Now, back to traits...


You can see how they are a big wrench thrown into this machinery. You cannot just look at the trait body and say “yeah, it will always work, regardless of where it will be used”, and you cannot look at the `use T;` statement and say “it will work”, without looking again at every single `$this` usage inside `T`. This may make even small changes prohibitively expensive to typecheck.

A partial solution here is to strengthen the contract provided in trait declaration by requiring it to list abstract declarations of all the functions used. This is similar to how a parent class can ensure that children classes will fulfill its expectations:


    trait T {
      private abstract function g(): string;

      public function f(string $s): string {
        return $this->g();
      }
    }


Now we know that any class using `T` will have a function `g` with the definition we expect. The drawback is that in more complicated cases this starts to be very verbose, because we are basically repeating the entire declaration of class using the trait. It also won't help with some other usages of `$this`:


    function takeC(C $c): void {
      ...
    }

    // Note: another hypothetical example, Hack would prevent this by
    // just disallowing such definition of T.
    trait T {
      private function g(): void {
        takeC($this);
      }
    }

    class C1 extends C {
      use T; // OK
      ...
    }

    class D {
      use T; // will pass an invalid argument to takeC when calling g();
      ...
    }


You can see that in both of those issues, a pattern starts to emerge: even though in principle a trait can be used by many classes which are completely unrelated to each other, in practice the majority of trait use cases involves tying them to some class hierarchy or interface. See the example below illustrating a very common use case of traits we observed in our codebase:


    abstract class C {
      // We want every subclass of C to implement one of the
      // few versions of function g()
      abstract public function g(): int;

      public function f(): int {
        ...
      }
    }

    // We can encapsulate those versions of g in traits and explain
    // their usage in comments, e.g:

    // "Use this trait in subclasses of C where you want g() to compute foo"
    trait FooTrait {
      public function g(): int {
        $x = $this->f();
        ... // compute foo
      }
    }

    // "Use this trait in subclasses of C where you want g() to compute bar"
    trait BarTrait {

      public function g(): int {
        $x = $this->f();
        ... // compute bar
      }
    }

    // Different subclasses of C now just need to use one of the provided
    // traits to satisfy the parent definition
    class C1 extends C {
      use FooTrait;
    }

    class C2 extends C {
      use FooTrait;
    }

    class C3 extends C {
      use BarTrait;
    }


Such implicit assumptions about intended trait usage, expressed by convention, or in a comment, are obviously not very type checker friendly. It turns out that formalizing them as language concept not only encourages a good programming practice of documenting assumptions, but also is exactly what we need to efficiently verify traits. We call them **trait requirements** and the their syntax is


    require extends C;


placed in trait definition. Type checker will now know and enforce that every class using this trait is also a subclass of `C`. Armed with that we can make the previous example type safe:


    trait FooTrait {
      require extends C; // This is the new language feature:
                         // a type checker friendly version of a
                         // comment saying "Use this trait in
                         // subclasses of C (and only in those
                         // subclasses)"

      public function g(): int {
        $x = $this->f(); // it is sure now that $this is a child of C
        ...              // and thus has a function f() that returns an int
      }
    }


We can similarly express the fact that the functionality required by a trait is shared by implementers of some interface. The syntax is analogous:


    require implements I;


placed in trait definition. Example of code that benefits from doing this:


    interface I {
      public function f(): int;
    }

    trait T {
      require implements I;

      public function g(): int {
        $x = $this->f(); // $this is known to implement I here
        ...
      }
    }


With a single require statement we can now:




  * say that `T` definitely doesn’t have any typing errors internally. We only need to look at body of `T` and know the declaration of class `C` required by it to check it.


  * say that using `T` in `C` won't cause any errors. We only need to know the declaration (which includes trait requirements) of `T` to check it.


To sum up: one of the main difficulties in finding errors with trait use boils down to not knowing enough about `$this` inside their bodies. It makes it impossible to verify them independently of their use sites, and vice-versa.

To make this verification tractable, traits in Hack and PHP, although they look a lot alike, are very subtly different. They're more than just a complier-assisted copy-paste. For Hack, traits really are little bundles of horizontally composable functionality. They not only define an external API that they provide, but also an API that they expect from the use callsite that is available to its internals. This API can be expressed using abstract functions or trait requirements, which are a new language feature allowing you to capture a very common assumption of trait being tied to some class hierarchy of interface. Being explicit about this makes them much more friendly to static analysis, at the cost of just adding a single line to their definition.


## Interface requirements


Consider the following code employing the [Marker Interface Pattern](http://en.wikipedia.org/wiki/Marker_interface_pattern):


    class C {
      public function f(): void {}
    }

    // "Use this to mark the subclasses of C that have foo"
    interface IHaveFoo {}

    class C1 extends C implements IHaveFoo {}
    class C2 extends C implements IHaveFoo {}
    class C3 extends C {}

    function takeFoo(IHaveFoo $x): void {
      $x->f(); // all implementers are also C, so this will work
               // ... but the type checker can't know that and so it
               // will complain
    }


This is a very similar problem to the one with traits described above — an assumption which the type checker doesn't know about — with an identical solution.
Hack allows you to express such assumption by allowing `require extends` in interfaces too:


    interface IHaveFoo {
      require extends C;
    }


With this definition, it is now known (and enforced by Hack) that every class implementing `IHaveFoo` will also be a subclass of `C`.


## Traits implementing interfaces


Traits are also sometimes described as _interfaces with implementation_ - when they fully define all the methods of some interface. By example:


    interface I {
      public function f(): int;
      public function g(): string;
    }

    trait T {
      public function f(): int {
        ...
      }
      public function g(): string {
        ...
      }
    }

    class C1 implements I {
      use T;
    }

    class C2 implements I {
      use T;
    }


There is redundancy here: every use `T` is accompanied by `implements I`, this is the only reason `T` exists. As some syntactic sugar, Hack allows you to express it by using


    implements I


syntax in trait declarations, identical to the one already used with classes and interfaces. It makes every class using this trait also implement I:


    trait T implements I {
      ...
    }

    class C { // implements I just by the virtue of using T, without
              // the need to redeclare it
      use T;
    }
