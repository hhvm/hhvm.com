---
title: "Introducing `readonly`"
layout: post
author: jjwu
category: blog
---

As of HHVM version 4.139, we've released a new keyword called `readonly` in Hack. `readonly` is a new feature in Hack for restricting the mutability of object properties. It's designed for use cases that require performant, runtime-enforced mutability control. 

`readonly` has two main principles: **readonlyness** and **deepness**. 

- **Readonlyness**: Object properties of any readonly value cannot be modified (i.e. mutated).
- **Deepness**: All nested properties of a readonly value are readonly.

```
class Bar {
  public function __construct(
    public Foo $foo,
  ){}
}
class Foo {
  public function __construct(
    public int $prop,
  ) {}
}

function test(readonly Foo $foo, readonly Bar $bar) : void { 
  $foo->prop = 5; // error, $foo is readonly 

  // Deepness: $x is also readonly
  $x = $bar->foo;

  $x->prop = 3; // error, $x is readonly
}
```

The readonly keyword can be used in many places in Hack. 
- **Readonly expressions**: Any expression can be marked readonly with the `readonly` keyword. 
- **Readonly parameters**: A parameter marked readonly signal that a function or method can take in a readonly value, and does not modify it. 
- **Readonly return types**: A function can return readonly, which allows it to return a readonly reference. 
- **Readonly properties**: A property can be marked readonly, which allows you to assign a readonly value to it. Note that readonly properties *can* have their values replaced, as readonly is a modifier on the value of the property, not the property definition itself. 
- **Readonly methods**: An instance method can be marked readonly. Instance methods that are readonly treat `$this` as readonly. Readonly values can only call readonly methods. 
- **Readonly closures**: A readonly closure captures external variables as readonly. 

You can see some examples of the readonly keyword in this code snippet: 

```
class Bar {
  public int $prop = 0;
}
class Foo {
  public function __construct(public Bar $bar, public readonly Bar $ro_bar) {}

  // This method promises not to modify $this
  public readonly function getBar(): readonly Bar {
    // note that $this is readonly, so $this->prop is readonly, which is why
    // this method must return readonly
    return $this->bar;
  }

  public static function takesReadonlyExample(readonly Foo $x): void {
    $x->bar = new Bar(); // error, $x is readonly here!
  }

  public static function readonlyClosureExample(): void {
    $x = new Bar();
    $readonly_f = readonly (): void ==> {
      $x->prop = 5; // error, $x is captured as readonly since $readonly_f is a readonly function
    };
    $x->prop = 4; // $x is still mutable out here, so this is okay!
  }

  public function readonlyPropExample(Foo $foo): void {
    $x = readonly new Bar();
    $foo->bar = $x; // error, $x is readonly but bar is a regular property
    $foo->ro_bar = $x; // ok!
  }
}
```

Some function calls and property accesses require explicitly annotating the result of the call as readonly:

- If you call a function that returns a readonly value, you must annotate the call with the `readonly` keyword. 
- If you access a class's readonly property, you must annotate the access with the `readonly` keyword. 

```
function testExplicitReadonly(readonly Foo $foo): void {
    //     vvvvvvvv This keyword is required here since getBar returns readonly
    $bar = readonly $foo->getBar(); 
    //             vvvvvvvv This keyword is required here since $ro_bar is a readonly property
    $ro_bar_prop = readonly $foo->ro_bar;
}
```

For a full guide and specification to using readonly, you can check our full [documentation](https://docs.hhvm.com/hack/readonly/introduction) on the feature. 
