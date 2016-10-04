---
layout: home
title: HHVM
id: home
---

## What is HHVM?

HHVM is an [open-source](http://github.com/facebook/hhvm) virtual machine designed for executing programs written in [Hack](http://hacklang.org/) and [PHP](http://php.net/). HHVM uses a just-in-time (JIT) compilation approach to achieve superior performance while maintaining the development flexibility that PHP provides.

HHVM supports [Hack](http://hacklang.org/), [PHP 5](http://php.net/) and the major features of [PHP 7](http://hhvm.com/blog/10859/php-7-support). We are aware of [minor incompatibilities](https://github.com/facebook/hhvm/issues?q=is%3Aopen+is%3Aissue+label%3A%22php5+incompatibility%22), so please [open issues](https://github.com/facebook/hhvm/issues/new) when you find them. HHVM also [supports many extensions](http://docs.hhvm.com/hhvm/extensions/introduction) as well.

<div class="gridBlock">
  <div class="blockElement twoByGridBlock alignLeft">
    <div class="blockContent">
      <h3>HHVM Features</h3>
      <ul>
        <li>The <a href="http://hacklang.org/">Hack Language</a></li>
        <li><a href="http://www.hhvm.com/blog/2027/faster-and-cheaper-the-evolution-of-the-hhvm-jit">JIT Compilation</a></li>
        <li><a href="https://github.com/facebook/hhvm/wiki/Extension-API">HNI</a></li>
        <li><a href="http://docs.hhvm.com/hhvm/basic-usage/proxygen">Proxygen</a> and <a href="http://docs.hhvm.com/hhvm/advanced-usage/fastCGI">FastCGI support</a></li>
        <li><code>hphpd</code> debugger</li>
        <li>... and <a href="http://docs.hhvm.com/hhvm/">more</a></li>
      </ul>
    </div>
  </div>

  <div class="blockElement twoByGridBlock alignLeft">
    <div class="blockContent">
      <h3>The JIT Compiler</h3>
      <p>
        Rather than directly interpret or <a href="https://en.wikipedia.org/wiki/HipHop_for_PHP#History_Before_HHVM">compile PHP code directly to C++</a>, HHVM compiles Hack and PHP into an intermediate bytecode. This bytecode is then translated into <a href="https://en.wikipedia.org/wiki/X64">x64</a> machine code dynamically at runtime by a just-in-time (<a href="https://en.wikipedia.org/wiki/Just-in-time_compilation">JIT</a>) compiler. This compilation process allows for all sorts of optimizations that cannot be made in a statically compiled binary, thus enabling higher performance of your Hack and PHP programs.
      </p>
    </div>
  </div>
</div>
