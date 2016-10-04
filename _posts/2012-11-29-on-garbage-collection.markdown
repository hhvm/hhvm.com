---
author: oyamauchi
layout: post
title: On Garbage Collection
category: blog
permalink: /blog/431/on-garbage-collection
---

In this post, I'll expand on a topic that I briefly mentioned in the footnote to my [previous post](/wp/?p=311): memory management.

Most modern programming languages, including PHP, have automatic memory management. Programmers don't explicitly free the memory they allocate, and the language runtime does that for them. There are a variety of approaches that language runtimes can take to implement this, and they lie on a spectrum.

<!--truncate-->

At one end of the spectrum is _eager reference counting_: every time a reference to a chunk of allocated memory is created or destroyed, the allocation's reference count is immediately updated and it is freed if its refcount drops to zero. At the other end is _tracing_: periodically during the program's execution, the runtime computes, by following objects' references to each other, which allocations are no longer reachable and frees them. Nothing special happens immediately when references are created and destroyed. In the middle of the spectrum are a variety of hybrid approaches, such as deferred refcounting, generational collectors that trace young values and refcount old values, etc. We won't go into those here; the academic literature on this topic is extensive.

For those unfamiliar with tracing GC, it works by starting from a _root set_ and then _tracing_ references from it recursively. A root set is a set of values that are assumed to be visible and reachable from PHP code: the eval stack, local variables, and global variables. Tracing references means to enumerate other values that are reachable through a given value: all keys and values of an array, and all properties of an object. We build a _reachable set_ that starts as just the root set, and then iterate through the current reachable set, tracing each value's references and adding those to the reachable set. When this is done, any values on the heap that aren't in the reachable set are assumed to be garbage and are freed.

PHP's language semantics require eager refcounting of arrays and objects — I explain why below. But the idea of moving HHVM towards the use of tracing in some contexts has been around since the project's early days. The increased flexibility of implementation offered by tracing can translate into increased performance, so it's an attractive idea. We've done some experiments to see if it's worthwhile; read on for details.


## Why does PHP require eager refcounting?


There are two ways by which PHP code can observe the runtime's memory management scheme.




  * **Object destructors**; that is, `__destruct()` methods. These methods have to be called immediately when the object's refcount goes to zero. A tracing GC wouldn't detect that an object was garbage until some time after the last reference to it had disappeared, so it wouldn't be able to call the destructor at the right time.


  * **Copy-on-write arrays**. PHP's arrays have value semantics. Here's an example:


    $a = array(20);
    $b = $a;
    $b[0] = 4500;
    echo $a[0];  // prints "20"


In principle, the assignment `$b = $a` makes a copy of the array. PHP runtimes don't actually copy the array at that point. Instead, they wait until the program tries to modify one of the "copies". To be able to do this, the array needs an accurate refcount.

You may think that copy-on-write arrays are just an optimization — that a PHP runtime could eagerly copy arrays and still have correct behavior. In fact, PHP code can tell that copy-on-write is happening under the hood, by taking a reference to an array element:


    $arr = array(10);
    $ref =& $arr[0];
    $copy = $arr;   // the array is "copied" at this point
    $arr[0] = 'whoops';
    echo $copy[0];  // prints "whoops"





This means that we have to keep eagerly refcounting arrays and objects to preserve correct behavior. However, there are a couple of options for limited usage of tracing GC: strings, and cycle collection. We've made attempts at both of these. Here are the details.


## Collecting strings


It's impossible for PHP code to observe how the runtime is implementing memory management of strings. They're immutable, so no copy-on-write logic is observable, and there's no PHP code that gets run when they're destroyed. This means we have some room to experiment.

The first problem we run into is that HHVM does copy-on-write of strings. As I said before, PHP strings are immutable as far as the language is concerned, but HHVM mutates strings in-place as long as there's no way for PHP code to tell. We determine that there's no way for PHP code to tell by checking the refcount: if it's exactly 1, we can mutate. To start using tracing GC on strings, we had to stop keeping accurate refcounts for them; that would defeat the purpose. So we had to start eagerly copying strings. This is obviously a performance hit, but we were hoping that not having to refcount would make up the difference.

Unfortunately, we were never really able to isolate the effect of eager-copying strings from the rest of the effects that this change caused. Memory allocation and deallocation patterns were changed, affecting data locality and potentially allocator performance. Less refcounting code was emitted, affecting code locality and memory access patterns. We couldn't easily measure these effects separately. Worse, the overall effect on performance was negative.

The second, more serious problem that we run into here is root-finding. In my description above, I made HHVM's root set sound simple (stack, locals, globals) but the reality is quite a bit more complicated than that.




  * **Enregistered roots in JIT-compiled code**. The JIT compiler loads eval stack slots and local variables — which contain references to heap-allocated data — into hardware registers. This means that, if a tracing cycle is invoked from C++ code that's been called from JIT-compiled code, the in-memory eval stack and local variables may be stale. To get the real root set, we would have to (a) remember/compute which machine registers each stack slot/local variable was mapped to in each JIT-code frame above us; and (b) walk the C++ stack to find the values of the JIT's registers, which were saved according to the usual x86-64 ABI as control passed from JIT-compiled code into C++. None of this is impossible; it would just be very messy in the current system.


  * **Untracked C++ references**. We hold pointers to heap-allocated data in member variables of C++ objects in many places. These are all roots or references that should be traced, even though they may not correspond directly to anything in PHP source.Most of these references are held within our smart-pointer classes `Variant`, `Array`, `Object` and `String`, so we tried a technique where the smart-pointer classes' constructors added their inner raw pointers to a temporary root set for use by the GC, and their destructors removed them. In addition to causing an unacceptable performance hit, this still wasn't enough. There are C++ roots in the form of raw pointers too, and there is no elegant solution for tracking them; we'd be slowly working our way down a long tail.


Having an approximate root set isn't good enough. The failure mode of having a non-comprehensive root set is that we mistakenly decide some objects are unreachable, so we mistakenly free a reachable object and leave a dangling reference somewhere. That would be unacceptable.


## Cycle collection


As I mentioned before, naïve eager refcounting can't detect and free cyclical garbage (unreachable objects that hold references to each other). Here's an example:


    $a = new stdClass;
    $b = new stdClass;
    $a->prop = $b;
    $b->prop = $a;
    unset($a);
    unset($b);


The two objects are unreachable — there's no way to refer to them from PHP — but they will never be freed. They each have a refcount of 1, and the only way it could go to 0 is for the other object to be freed.

If we can detect such cycles, we can free them without introducing incorrect behavior. Going back to the two ways that PHP code can observe the runtime's memory management:




  * "Correct" behavior (not freeing cycles) is that object destructors don't run on cyclical garbage, so we can simply skip destructors while freeing cycles.


  * It's impossible to observe array copy-on-write effects as shown above, because cyclical garbage is unreachable by definition.


With the cycle collector, we avoided the root-finding problem that we had with the string collector, because everything still had accurate refcounts. We could just look at references among heap allocations — not considering any references into the heap from outside it — and infer which ones were reachable and which weren't. Here's a sketch of the algorithm:


  1. Iterate over every array and object in the heap. For each one, trace its internal references (all values in an array, all properties in an object) and decrement the refcount of each of them.


  2. At this point, anything in the heap that still has a refcount greater than zero must have a reference to it from _outside_ the heap, because its refcount has been decremented by one for each reference to it from _within_ the heap. These allocations form an inferred root set.


  3. Put the inferred root set into a queue. Iterate over the queue; for each allocation in it, add each allocation it references to the queue and increment its refcount. This reconstructs their original refcounts, which we decremented in step 1.


  4. Free everything that still has zero refcount; it wasn't reachable from the inferred root set.


So really, the algorithm isn't specifically looking for cycles at all. All it's doing is calculating reachability and then freeing unreachable memory. It just so happens that the only way to produce unreachable, unfreed memory with PHP code is to create a cycle.

It turned out that Facebook's PHP codebase simply doesn't produce much cyclical garbage. The majority of it comes from a handful of places in the code, and from a small number of very large cyclical structures. When their memory usage gets to be problematic, it's easiest just to break the cycle by modifying the PHP code. That being the case, it's simply not cost-effective to have a cycle collector constantly operating on production web servers. The idea is to use it as an on-demand cycle detector (so PHP developers can find cycles to break), and as a collector in long-running scripts.

The cycle collector is checked in (`src/runtime/vm/backup_gc.cpp`), but currently disabled due to bugs. We are aiming to fix it in the near future.
