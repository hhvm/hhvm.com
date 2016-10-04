---
author: oyamauchi
layout: post
title: HHVM Optimization Tips
category: blog
permalink: /blog/713/hhvm-optimization-tips
comments:
- id: 491
  author: Steve Clay
  author_email: steve@mrclay.org
  author_url: http://www.mrclay.org/
  date: '2013-05-30 13:02:11 +0000'
  date_gmt: '2013-05-30 20:02:11 +0000'
  content: |-
    Just curious re: unique classes, consider an app with a plugin system where each plugin has a PRS-0 classes directory. If multiple plugins ship with an identical class, vanilla PHP will just use whichever class file was found first by the autoloader.

    If HHVM analyzed both copies and found them identical (bytecode-wise), could it still not optimize this? Is the problem things like get_included_files(), __FILE__, etc?

    In practice, of course, a dev could just manually delete the class files that would never be called.
- id: 497
  author: B.Nicolotti
  author_email: bnicolotti@siapcn.it
  author_url: ''
  date: '2013-07-31 06:25:57 +0000'
  date_gmt: '2013-07-31 13:25:57 +0000'
  content: we're testing Hphpvm 2.1 to speed up a loop that runs 400-1000 times to
    read data from soap&#47;xml in memory and then insert 400-1000 times. We've moved
    the loop code to a function to avoid global scope. We've tested the new code on
    hphpvm and on regular php and. The (gib) problem is that on hphpvm it takes double
    time than on regular php :-(
- id: 503
  author: HHVM revisited - SitePoint
  author_email: ''
  author_url: http://www.sitepoint.com/hhvm-revisited/
  date: '2014-01-28 06:02:23 +0000'
  date_gmt: '2014-01-28 14:02:23 +0000'
  content: "[&#8230;] SSD for faster cache reads&#47;writes &#8211; pre-analyzing
    &#8211; authoritative cache &#8211; follow these [&#8230;]"
- id: 509
  author: J
  author_email: piranxa@gmail.com
  author_url: ''
  date: '2014-02-25 04:07:18 +0000'
  date_gmt: '2014-02-25 12:07:18 +0000'
  content: "Hello, excellent work on hhvm\n\nI tested it on a library&#47;framework
    i have written and i am seeing 5x the speed up compared to when it runs on php+apc\n\nMy
    question is related to the 'Declare Properties' section. My presentation&#47;control
    generation code is essentially a data driven engine where I supply a nested array
    \ of data into a bunch of control functions that further parse the array and generate
    the presentation and the control code for any site.\n\nas an example the data
    could look like:\n<code>$page = array('',array(4=>button_grp(array(array(...),...)),4=>well(nav($lav_list,'l'))),)<&#47;code>\n\nwhich
    would be parsed by a grid function to generate the overall grid and then each
    bit of it can follow different execution paths depending on the format. As a result
    there are calls such as is_array() and is_string() in order to determine the type
    of data and allocate the correct functions.\n\nnav() for example which essentially
    generates navigation elements using 's for various components does checks again
    of the data type\n\nie $nav_list can be:\n<code>\n$nav_list = array('#home'=>array(icon('home','Home','white'),'active'),'#book'=>icon('book','Library'),
    \n\t'#app'=>icon('pencil','Applications'),'#misc'=>icon('exclamation-sign','Misc'));\n<&#47;code>\nor
    \n<code>\n$nav_list2 = array('#home'=>array('Home','active'),'#help'=>'Help',array('Dropdown',
    array('#action'=>'Action',\n\t'#action2'=>'Another action','#something'=>'Something
    else here',array('','divider'),'#seper'=>'Separated link')),\n\tarray(array('Dropup','pull-right
    dropup'), array('#action'=>'Action', '#action2'=>'Another action','#something'=>'Something
    else here',<&#47;code>\n\nwould this be more optimal in hhvm by the use of an
    object with properties and possibly object nesting (or even an array of objects
    with different types) or does your code figure out the data types after a couple
    of runs (since they are constant per page) and optimise away. The speed up is
    very significant already for my test pages which I presume are mostly in this
    case related to function call overheads."
- id: 5681
  author: HHVM 是如何提升 PHP 性能的？ &#8211; 叶中奇
  author_email: ''
  author_url: http://www.yezhongqi.com/hhvm-is-how-to-improve-the-performance-of-php/
  date: '2014-03-26 07:44:37 +0000'
  date_gmt: '2014-03-26 14:44:37 +0000'
  content: "[&#8230;] HHVM Optimization Tips [&#8230;]"
- id: 5873
  author: HHVM 是如何提升 PHP 性能的？ | freemking的博客
  author_email: ''
  author_url: http://blog.256kan.com/?p=58
  date: '2014-03-27 00:11:24 +0000'
  date_gmt: '2014-03-27 07:11:24 +0000'
  content: "[&#8230;] HHVM Optimization Tips [&#8230;]"
- id: 6455
  author: Taking HHVM 3.0.0 for a spin | J&aacute;nos P&aacute;sztor
  author_email: ''
  author_url: http://www.janoszen.com/2014/03/29/taking-hhvm-3-0-0-for-a-spin/
  date: '2014-03-28 23:28:09 +0000'
  date_gmt: '2014-03-29 06:28:09 +0000'
  content: "[&#8230;] Not even a day has passed since Facebook released a new version
    of their PHP virtual machine called HHVM. If you don&#8217;t know HHVM and you&#8217;re
    coding PHP, you&#8217;ve probably living under a rock for the last few years,
    but the point is, it&#8217;s blazing fast. As a matter of fact it&#8217;s so fast
    that at the moment the network latency on my blog is more of an issue than page
    rendering speed, and I haven&#8217;t even started to do any optimization. [&#8230;]"
---

HHVM's JIT compiler allows it to execute PHP faster than Zend PHP in most cases, unmodified. However, we've gotten some interest from the community in HipHop-specific optimization tips, so I put together a few for this post.

The principle that underlies all of these tips is: write code that HHVM can _understand without running_. The more HHVM knows before the code runs, the more it can optimize.

<!--truncate-->


## Keep Hot Code Out of Global Scope



Code that runs in global scope is never passed to the JIT compiler. If, for example, you have a script that has a tight loop of computation, make sure that the loop isn't in global scope, by putting it inside a function.

The reason HHVM doesn't JIT-compile code in global scope is that any code, anywhere, can mutate the "local" variables of global scope. This severely hampers the JIT compiler's ability to track types of local variables. Here's a little quiz that demonstrates what I'm talking about:




    // This is in global scope. What code could we put here that
    // will result in $a being mutated by the statement "echo $b;"?

    $a = 20;
    echo $b;




Here are two possible answers.




    function handler() {
      $GLOBALS['a'] = 'hi';
    }
    set_error_handler('handler');




_Since `$b` will be undefined when echo'ed, a notice will be raised and the error handler will run._




    class C {
      public function __toString() {
        $GLOBALS['a'] = 'hi';
      }
    }
    $b = new C;




_Passing an object to `echo` will call its `__toString` method._

Granted, these are very contrived examples, but contrived or not, we have to run them correctly. In global scope, these issues are so widespread as to be inescapable, so we completely turn off the JIT.




## Make Class, Function, and Constant Names Unique



This only applies to [repo authoritative](/wp/?p=257) mode, where HHVM analyzes an entire codebase ahead of time. It's a fatal error to define a class or function with a name that's already been bound _at runtime_, but it's perfectly legal to have multiple functions or classes with the same name at analysis time. However, that will block some optimizations.

When a function has only one definition, that gives HHVM a lot of useful information at the function's callsites, all of which can be used to generate better code.





  * It knows if the callee returns by value or reference, so there's no need to insert a check after callsites. It may be able to infer the type that the callee returns (integer, string, etc.) and use that information below the callsite.


  * It knows if the callee takes its arguments by value or reference, so there's no need to insert runtime checks; we can emit unconditional boxing or unboxing[1] code as needed.


  * It may inline the function, if it's small enough and conforms to one of a few inlineable "shapes". For example, if the function just returns a constant, it will be inlined, and there will be no function call at runtime. (Additionally, the constant will be available for constant folding and propagation at the callsite.)



We can make similarly powerful assumptions about uniquely-named classes: we know their (and their ancestors') methods and declared properties, what interfaces they implement, etc. Their class constants are available for constant propagation. If we know that an object belongs to such a class, we know all of the above bits of information (arguments by reference, etc.) about the object's methods.




## Avoid Dynamic Variable Access



This means any code that reads or writes a local variable, but where it's impossible to tell _which_ local is being referred to until runtime. This includes:





  * `$$variable_name`.


  * `compact()`, `extract()`, and `get_defined_vars()`.



These constructs make for slower code because they require HHVM to do extra bookkeeping: every time we enter or exit a function containing these constructs, we have to set up and tear down a map of local variable names to memory locations.

In scopes where there are none of these constructs, we don't need to use local variable names. Every local variable read or write maps to a known constant offset from the VM's frame pointer, so that reading or writing a local can be done in a single machine instruction. We could also (though we don't currently) optimize away local variables entirely.

Consider this code:




    function f($vars) {
      $name = 'some_constant';
      // ...
      extract($vars);
      // ...
      other_function($name);
    }




If it weren't for the `extract()` call, we could constant-propagate `$name` to the places where it's used, and eliminate the local variable. But `extract()` might overwrite `$name`, so we can't. In practice, the surrounding application code might guarantee that `$vars` will never have a `'name'` key, but there's no way for HHVM to know that, so the optimization is blocked.





## Declare Properties



An expression like `$obj->prop` is faster to evaluate if `prop` is a declared property in `$obj`'s class. In HHVM, objects of a class with declared properties have memory allocated for each declared property, at a known constant offset from the start of the object. This makes accessing declared properties very fast: it can be done with a handful of machine instructions and memory operations. Accessing dynamic properties, by contrast, requires hashtable lookups.

Declared properties also allow us to inline getter methods in repo-authoritative mode. So the following code:




    class C {
      private $prop;
      public function getProp() {
        return $this->prop;
      }
    }

    $obj = new C;
    echo $obj->getProp();




is just as fast as this code:




    class C {
      public $prop;
    }

    $obj = new C;
    echo $obj->prop;




HHVM's ability to inline the getter lets you keep the property private (better encapsulation) without sacrificing speed.

This also means that when you want a struct-like container, you should use objects with declared properties, instead of arrays. (If you just need a dumb container, it's fine to declare public properties and forgo getters and setters -- this won't block any optimizations.) The trouble with arrays is that we can't allocate fixed slots for declared properties the way we do with objects, because there's no way to declare a set of fixed keys that will be in an array. Every read or write in an array is required to go through a hashtable lookup.

Caveat: declared-property optimizations are only available when we know the class of `$obj`. In practice, this is usually only the case when either (a) the expression on the left of the arrow is `$this`, or (b) `$obj` was constructed via `new` in the same scope. In Facebook's PHP codebase, this is overwhelmingly common; accessing properties of objects other than `$this` is very rare, so this optimization works well for us. Your mileage may vary.

Take note: declared properties seem to be slower than dynamic properties in Zend PHP versions older than 5.4.



## Don't Worry About This Too Much



HHVM's optimizer gets better and more sophisticated by the day. We're regularly finding new patterns to optimize by inspecting existing PHP codebases (primarily Facebook, but some third-party projects too). Spending time crafting micro-optimizations in your PHP code is unlikely to be worthwhile.

Still, if you're choosing between two ways to write a piece of code and you're wondering which one HHVM will do a better job with, put yourself in the mindset of a compiler writer and ask: which one gives the compiler more information? That one is likely to be the better choice. We may not optimize that specific pattern right now, but if the code conveys enough information, it'll be easier for us to optimize it in the future.


[1] Boxing and unboxing are HHVM-specific terms meaning, respectively, to convert a variable into a reference, and to read the value out of a reference.
