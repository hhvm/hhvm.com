---
title: "Introducing HackTest"
layout: post
author: fe
category: blog
---

As HHVM [moves away from PHP](https://hhvm.com/blog/2018/09/12/end-of-php-support-future-of-hack.html), Hack projects need to be able to move away from PHP dependencies; the most common dependency is PHPUnit, by a large margin. As such, we are releasing [HackTest](https://github.com/hhvm/hacktest/) (a framework for declaring and running unit tests) and retargetting [fbexpect](https://github.com/hhvm/fbexpect/) (an expressive assertion library) to be a supported library for non-Facebook users.

These libraries provide a slightly different API to PHPUnit:

```
<?hh // strict

use type Facebook\HackTest\HackTest;
use function Facebook\FBExpect\expect;

final class MyTest extends HackTest {
  <<__Override>>
  public static async function beforeFirstTestAsync(): Awaitable<void> {
    // this can be used to emulate setUpBeforeClass()
  }
  
  <<__Override>>
  public async function beforeEachTestAsync(): Awaitable<void> {
    // this can be used to emulate setUp()
  }
  
  <<__Override>>
  public async function afterEachTestAsync(): Awaitable<void> {
    // this can be used to emulate tearDown()
  }
  
  <<__Override>>
  public static async function afterLastTestAsync(): Awaitable<void> {
    // this can be used to emulate tearDownAfterClass()
  }
  
  public function testFoo(): void {
    // replaces $this->assertSame('bar', foo());
    expect(foo())->toBeSame('bar');
  }

  public function provideBars(): vec<(string, int)> {
    return vec[
      tuple('foo', 123),
      tuple('bar', 456),
    ];
  }
  
  <<DataProvider('provideBars')>> // replaces @dataProvider doccomment
  // tests can be async
  public async function testBar(string $a, int $_b): Awaitable<void> {
    $s = await get_message_async();
    // replaces @expectException and setExpectedException()
    expect(() ==> {
      throw new \Exception($s);
    )->toThrow(\Exception::class);
  }
}
```

To make moving from PHPUnit to HackTest practical, we have extended [HHAST](https://github.com/hhvm/hhast) to automate the required code changes - though the composer changes must be made separately.

We start with a Hack project that uses PHPUnit:

```
myproject$ hhvm vendor/bin/phpunit tests/
PHPUnit 5.7.27 by Sebastian Bergmann and contributors.

.............................................................   61 / 1309 (  4%)
.............................................................  122 / 1309 (  9%)
.............................................................  183 / 1309 ( 13%)
.............................................................  244 / 1309 ( 18%)
.............................................................  305 / 1309 ( 23%)
.............................................................  366 / 1309 ( 27%)
.............................................................  427 / 1309 ( 32%)
.............................................................  488 / 1309 ( 37%)
.............................................................  549 / 1309 ( 41%)
.............................................................  610 / 1309 ( 46%)
.............................................................  671 / 1309 ( 51%)
.............................................................  732 / 1309 ( 55%)
.............................................................  793 / 1309 ( 60%)
.............................................................  854 / 1309 ( 65%)
.............................................................  915 / 1309 ( 69%)
.............................................................  976 / 1309 ( 74%)
............................................................. 1037 / 1309 ( 79%)
............................................................. 1098 / 1309 ( 83%)
............................................................. 1159 / 1309 ( 88%)
............................................................. 1220 / 1309 ( 93%)
............................................................. 1281 / 1309 ( 97%)
............................                                  1309 / 1309 (100%)

Time: 13.95 seconds, Memory: 41.69MB

OK (1309 tests, 1310 assertions)
```

Then, we need to swap out the composer dependencies from PHPUnit to HackTest and FBExpect

```
myproject$ hhvm ~/composer.phar remove --dev phpunit/phpunit 91carriage/phpunit-hhi
...
myproject$ hhvm ~/composer.phar require --dev hhvm/hacktest facebook/fbexpect
...
```

Then we migrate the tests with HHAST, and run them with HackTest instead of PHPUnit:

```
myproject$ hhvm ~/code/hhast/bin/hhast-migrate --phpunit-to-hacktest tests/
myproject$ hhvm vendor/bin/hacktest tests/
...............................................................................
...............................................................................
...............................................................................
...............................................................................
...............................................................................
...............................................................................
...............................................................................
...............................................................................
...............................................................................
...............................................................................
...............................................................................
...............................................................................
...............................................................................
...............................................................................
...............................................................................
...............................................................................
.............................................

Summary: 1309 test(s), 1309 passed, 0 failed, 0 skipped, 0 error(s).
```

Finally, you might need to update your CI systems (such as TravisCI or CircleCI) to use HackTest instead of PHPUnit.

If you find cases that HHAST does not migrate correctly, we welcome GitHub issues and pull requests against [the HHAST project](https://github.com/hhvm/hhast/).
