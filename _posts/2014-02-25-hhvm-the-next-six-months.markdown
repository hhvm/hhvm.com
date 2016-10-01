---
author: joelp
comments: true
layout: post
title: 'HHVM: The Next Six Months'
category: blog
redirect_from:
  - /blog/3743/hhvm-the-next-six-months
---

The HHVM team has just wrapped up its planning for the first half of 2014. We’d like to share our plans, providing you a bit of context.

**2014 Themes:**

  * Open Source


  * Increase Web Efficiency


  * Make HHVM Hackable


<!--truncate-->

**Open Source goals:**

  * Increase community participation and adoption


    * [20+ top PHP frameworks have 100% unit tests passing](http://www.hhvm.com/blog/875/wow-hhvm-is-fast-too-bad-it-doesnt-run-my-code)


    * Support two major HHVM deployments


    * Encourage and accept 1+ significant new feature implementation (e.g., new and improved garbage collector).





  * Move to open development


    * Figure out a way to have all non-Facebook specific HHVM development done in the open.





[We’ve been making steady progress on HHVM’s compatibility](http://www.hhvm.com/blog/2813/we-are-the-98-5-and-the-16) with PHP in the wild, but we still have a lot of work ahead of us. We’re using unit test pass rates as a proxy for success measurement, but you can help by [adding HHVM to your Travis configuration](http://www.hhvm.com/blog/2393/hhvm-2-3-0-and-travis-ci), and reporting bugs and issues through [GitHub](https://github.com/facebook/hhvm). We are resourced to help support a couple of major HHVM deployments, which we hope has the side effect of exposing us to "non-Facebook" deployment and maintenance challenges.

We are also going to push for a more open development model, with the goal of increasing our community participation. We’ll have more to say on what this means later on. Stay tuned!

**Increase Web Efficiency:**




  * Further CPU time reduction


    * JIT improvements (including region compiler work)


    * HHBBC (HH bytecode-to-bytecode compiler)


    * Code and data layout optimizations


    * [Lockdown improvements](http://www.hhvm.com/blog/1499/locking-down-for-performance-and-parity)





  * Reduce Memory


    * Memory bandwidth reductions


    * Working set reductions


    * Ship a memory profiler





  * ARM64


    * 25% bytecode coverage on simulator





  * Prototype LLVM integration


We’ve set very aggressive efficiency goals for the half that we hope to achieve through a range of [JIT compiler](http://www.hhvm.com/blog/2027/faster-and-cheaper-the-evolution-of-the-hhvm-jit) projects. We hope these translate into wins for a variety of PHP workloads. We’re shooting for wins via the region compiler project, which is a compilation strategy that stitches together multiple basic blocks into larger chunks of code. This means that the current optimization passes we have in place can do a better job at identifying and exploiting optimization opportunities.

HHBBC (HipHop Bytecode to Bytecode compiler) is essentially a redesign and reimplementation of something we already have: a type inference pass. Right now we do type inference during the AST (Abstract Syntax Tree) generation phase, but we think we can do a better job of this at the bytecode level while giving us option value to augment bytecode with richer type information through tooling and offline static analysis. Having more type information on hand means generating faster and more specific code -- it’s like "peering in to a dynamic program, and pulling out its static equivalent".

We’re also planning on really knuckling down on memory consumption: both total working set and memory bandwidth usage. Reducing both will inevitably give us CPU time wins (a lot of our CPU time is spent waiting for memory requests) and will allow us to deploy to servers with a smaller memory footprint. All requests start with a fresh heap, add and subtract to it over the lifetime of the request, and then throw it away. As we increase RPS (inevitable side-effect of better quality code generation) we also increase bandwidth pressure on the memory subsystem. We want to make sure that the memory bus does not become a bottleneck.

**Hackable HHVM:**




  * "Hackers guide to HHVM" 50% complete


  * Reduce complexity in `[hphp/compiler](https://github.com/facebook/hhvm/tree/master/hphp/compiler)`


  * [100% conversion to HNI extension interface](https://github.com/facebook/hhvm/issues/1480)


  * Remove legacy tracelet compiler features (analyzer/translator, HHBC guard relaxation, etc.)


Hackable HHVM really means "move faster". We want to ship better documentation to help you guys (and it really helps us too…) get hacking on HHVM. One significant part of the “Hackable HHVM” theme is moving all of our internal extensions over to the [HNI interface](https://github.com/facebook/hhvm/blob/master/hphp/runtime/vm/native.h) which is a super fast lightweight way of building extensions for HHVM.

**An Exciting Road:**



![The Road Ahead](/static/images/posts/curved-road1.png)



Clearly it's going to be a big half in terms of technical agenda, and probably our biggest in terms of open source engagement. We’ll be attending conferences, shipping code, getting faster and having fun this year.

Please continue your awesome effort of [using](https://github.com/facebook/hhvm/wiki#wiki-installing-pre-built-packages-for-hhvm) and [contributing](https://github.com/facebook/hhvm#contributing) to HHVM, and discussing all things HHVM on IRC at [#hhvm](http://webchat.freenode.net/?channels=hhvm). We looking forward to having you join us for the ride in 2014 and beyond.
