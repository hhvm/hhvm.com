---
author: sgolemon
layout: post
title: The Journey of a Thousand Bytecodes
category: blog
permalink: /blog/6323/the-journey-of-a-thousand-bytecodes
comments:
- id: 268517
  author: "Sara Golemon explains HHVM and how it compiles PHP\uFEFF | Die wunderbare
    Welt von Isotopp"
  date: '2014-10-04 14:15:42 +0000'
  date_gmt: '2014-10-04 21:15:42 +0000'
  content: "[&#8230;] The Journey of a Thousand Bytecodes Compilers are fun. &nbsp;They
    take nice, human readable languages like PHP or Hack and turn them into lean,
    mean, CPU executin&#8217; turing machines. &nbsp;Some of these are simple enough
    a CS student can write one up in a weekend, some are the products of decades of
    fine tuning and careful architecting. &nbsp;Somewhere in that proud&hellip; [&#8230;]"
- id: 269045
  author: Abbas Naderi Afooshteh
  date: '2014-10-05 06:56:16 +0000'
  date_gmt: '2014-10-05 13:56:16 +0000'
  content: "Everything except for step 4 (translator) seems trivial as all interpreters
    have some sort of it. They even have a sort of step 4 (pyc for python) but that's
    the major component of HHVM afaik, and you haven't described how it gets the feel
    at all.\r\n\r\nOverall the post was fun."
- id: 269057
  author: Sara Golemon
  date: '2014-10-05 06:58:14 +0000'
  date_gmt: '2014-10-05 13:58:14 +0000'
  content: Yeah, this article was a high-level nosebleed sort of coverage.  Hope to
    do some followups at some point exploring each stage in a bit more detail.
- id: 269999
  author: Mitsu
  date: '2014-10-06 09:54:12 +0000'
  date_gmt: '2014-10-06 16:54:12 +0000'
  content: When HHVM will be ready for Windows platform? I'm waiting for this various
    months ago... :(
- id: 270227
  author: HHVM - ātrāks PHP un ne tikai - Kristaps Kaupe
  date: '2014-10-06 16:16:46 +0000'
  date_gmt: '2014-10-06 23:16:46 +0000'
  content: "[&#8230;] Kam interesē&nbsp;vēl tehniskākas detaļas par to, kā HHVM ir
    būvēts un darbojas, var palasīt Sāras Golemones rakstu &#8220;The Journey of a
    Thousand Bytecodes&#8220;. [&#8230;]"
- id: 271049
  author: Sara Golemon
  date: '2014-10-07 14:06:49 +0000'
  date_gmt: '2014-10-07 21:06:49 +0000'
  content: We have a semi-working win32 build (emphasis on "semi"), it's going to
    take some effort to get this solid enough for casual use, but we are working on
    it.
- id: 272777
  author: Sina Salet
  date: '2014-10-09 06:28:26 +0000'
  date_gmt: '2014-10-09 13:28:26 +0000'
  content: Brilliant
- id: 276389
  author: PHP Annotated Monthly &#8211; October 2014 | JetBrains PhpStorm Blog
  date: '2014-10-13 05:29:29 +0000'
  date_gmt: '2014-10-13 12:29:29 +0000'
  content: "[&#8230;] does HHVM convert PHP code into x86 machine code? Good question!&nbsp;Sara
    Goleman explains&nbsp;in an elaborate blog [&#8230;]"
- id: 480785
  author: '6 und ein paar halbe Schritte: So funktioniert die HHVM - entwickler.de'
  date: '2015-05-08 02:38:33 +0000'
  date_gmt: '2015-05-08 09:38:33 +0000'
  content: "[&#8230;] &ndash; bisher. Denn keine Geringere als Sara Golemon sorgt
    jetzt f&uuml;r Aufkl&auml;rung. In ihrem Blogpost The Journey of a Thousand Bytecodes
    erkl&auml;rt sie in sechs (und zwei halben) Schritten, vom Lexing &uuml;ber das
    Parsing und die Optimierung [&#8230;]"
---

Compilers are fun.  They take nice, human readable languages like PHP or Hack and turn them into lean, mean, CPU executin' turing machines.  Some of these are simple enough a CS student can write one up in a weekend, some are the products of decades of fine tuning and careful architecting.  Somewhere in that proud tradition stands HHVM; In fact it's several compilers stacked in an ever-growing chain of logic manipulation and abstractions.  This article will attempt to take the reader through the HHVM compilation process from PHP-script to x86 machine code, one step at a time.

<!--truncate-->

**Step One: Lexing**

The first step of our journey should be familiar to many PHP users since it's actually exposed to user space as the [token_get_all](http://php.net/token_get_all)() function.   In this phase, we reduce a human-readable PHP script to a series of tokens; Numeric identifiers which the compiler will be able to recognize as having some intrinsic meaning.  For this, HHVM uses a tool called Flex to generate a program from a meta definition at [hphp/parser/hphp.ll](https://github.com/facebook/hhvm/blob/master/hphp/parser/hphp.ll).

The several rules in this file describe the how to recognize token-words.  For example, encountering "echo" inside of a <?php tag, but not within a string, should yield a T_ECHO token, but encountering it elsewhere should yield common strings, html or other token types.  The following example shows the token breakdown of a simple PHP script:

```
<?php
echo $a + $b;
```

If we ran this through token_get_all(), we'd get the following sequence of tokens:


```
T_OPEN_TAG // This represents the "<?php" token
T_WHITESPACE("\n")
T_ECHO
T_WHITESPACE(" ")
T_VARIABLE("$a")
T_WHITESPACE(" ")
'+'
T_WHITESPACE(" ")
T_VARIABLE("$b")
';'
```

Notice that simple, single character tokens aren't given a name, they're simply passed through as the characters which they are.  Now that we have a set of machine-readable tokens, we can start to build expressions from them.

**Step Two: Parsing**

The rules found in [hphp/parser/hphp.y](https://github.com/facebook/hhvm/blob/master/hphp/parser/hphp.y) are used by Bison to create a parser engine.  This piece of the compiler reads in tokens, fed to it by the lexer, to build an Abstract Syntax Tree (AST); A representation of the expressions contained in your PHP script.

Considering a slightly more complex piece of script:

```
<?php
echo "Does 1+2 equal 3?";
if ((1+2) == 3) {
  echo "Yes it does!";
} else {
  echo "No it doesn't...";
}
```


We generate an AST which looks something like the following:

```
EchoStatement
  ConstantExpression("Does 1+2 equal 3?")
IfBranchStatement
  BinaryOpExpression(EQUAL)
    BinaryOpExpression(ADD)
      ConstantExpression(1)
      ConstantExpression(2)
    ConstantExpression(3)
  EchoStatement
    ConstantExpression("Yes it does!")
  EchoStatement
    ConstantExpression("No it doesn't...")
```

Here we can see that our disorganized tokens have been grouped together such that logical expressions are nested into groups the way we, as humans, would expect to make sense of them.  This is at the heart of the definition of the language and it's what determines everything from order of operations (precedence) to the association of one statement into another.

**Step Two and a Half: Optimization**

I call this two and a half, because we're not really changing the representation of the original script's code at this point. Rather, we're reducing expressions which can be simplified before the code is ever run (also, some of this happens in step 3).  For example, we can evaluate "1+2" to 3, and our AST becomes:

```
EchoStatement
  ConstantExpression("Does 1+2 equal 3?")
IfBranchStatement
  BinaryOpExpression(EQUAL)
    ConstantExpression(3)
    ConstantExpression(3)
  EchoStatement
    ConstantExpression("Yes it does!")
  EchoStatement
    ConstantExpression("No it doesn't...")
```


Then evaluate `3 == 3` to `true`:


```
EchoStatement
  ConstantExpression("Does 1+2 equal 3?")
IfBranchStatement
  ConstantExpression(true)
  EchoStatement
    ConstantExpression("Yes it does!")
  EchoStatement
    ConstantExpression("No it doesn't...")
```

Now we know that we'll always take the truth branch and never take the false branch, so:


```
EchoStatement
  ConstantExpression("Does 1+2 equal 3?")
EchoStatement
  ConstantExpression("Yes it does!")
```

Which of course can be reduced to a single EchoStatement.  This script was obviously a bit contrived to show off this optimizer stage, but it's worth seeing what's possible.

_Question_: What's the difference between a Statement and an Expression?
_Answer_: Statements are terminal, they have no output value to be consumed by later nodes in the AST, and must therefor appear only as top-level siblings in an HHVM AST.  Expressions produce a value as a result, and may, as such, be used as input to other expressions or statements.

**Step 3: Compilation to Bytecode**

The last stage of our compiler's "front end" brings us through [hphp/compiler/analysis/emitter.cpp](https://github.com/facebook/hhvm/blob/master/hphp/compiler/analysis/emitter.cpp) where we turn that AST into bytecodes which can be executed by HHVM's interpreter.  We do this by "visiting" each expression from the base of the tree upwards, with each expression describing itself as a series of bytecodes.

For example, an echo statement has one or more children which, by virtue of being expressions themselves, may in turn be made up of other expressions.  For each child expression of an EchoStatement we first visit the expression, which will produce a number of bytecodes resulting in a single value having been pushed onto the "stack". We then emit a "Print" bytecode which will pop that value, outputting its contents, then push it's own result value of int(1).  Because Echo is a Statement, however, and therefore must not have an output value, we immediately pop it back off using PopC.

_Question_: Why push a value to the stack if Echo is a Statement, and not an Expression?
_Answer_: Because Echo cheats by reusing the same bytecode meant for the [print](http://php.net/print)() expression, which if you'll recall, does have a return value.  The PopC instruction throws that away as unneeded.

_Question_: Isn't that inefficient?
_Answer_: Yes, but only in interp mode, this disappears by the time we reach the JIT.

Let's take a look at that in practice:

```
<?php
echo "Hello ", $name, "\n";
```

Produces an AST for an EchoStatement with three child expressions:


```
EchoStatement
  ConstantExpression("Hello ")
  VariableExpression($name)
  ConstantExpression("\n")
```


Which visits the EchoStatement, who in turns visits each child:


```
String "Hello " // Push "Hello " onto the stack
Print  // Consume "Hello " from the stack, and push int(1)
PopC  // Consume int(1) and throw it away
CGetL 0  // Fetch Local#0 ($name) from the symbol table and push it onto the stack
Print  // etc... etc... etc...
PopC
String "\n"
Print
PopC
```


**Generating Bytecode Dumps**

To see byte codes for a given script, similar to how PHP allows you to view Opcodes via VLD, you have two options. The first is to run it through HHVM as usual with the -vEval.DumpBytecode=1 option. This format is designed for human readability and is meant primarily for runtime development and debugging.  For example, a simple Hello World program:


```
<?php
echo "Hello World\n";
```

Becomes:

```
$ hhvm -vEval.DumpBytecode=1 /tmp/hello-world.php

Pseudo-main at 0
maxStackCells: 1
numLocals: 0
numIterators: 0

// line 2
0: String "Hello World\n"
5: Print
6: PopC
7: Int 1
16: RetC

Pseudo-main at 0
maxStackCells: 1
numLocals: 0
numIterators: 0
```

If you're wondering about the Int 1/RetC at the end, that's the implicit "return 1;" which comes at the end of every file (which doesn't explicitly return something) so that the include expression has a return value.  Remember, the "global scope" acts like a nameless function which is invoked implicitly on startup, and shares its variable scope with all other top-level psuedo-main functions.

The second option is nearly identical in invocation, but produces noticeably different output:

```
$ hhvm -vEval.DumpHhas=1 /tmp/hello.php

.filepath "/tmp/hello.php";

.main {
  String "Hello World\n"
  Print
  PopC
  Int 1
  RetC
}
```

This is actually HHVM’s third language (PHP and Hack being the first two), HipHop Assembly. This hidden language, which is normally only recognized in Systemlib files, allows developers to bypass the first two steps of compilation and create raw bytecodes. You can find an existing example of this ([hphp/system/php/array_map.hhas](https://github.com/facebook/hhvm/blob/master/hphp/system/php/array_map.hhas)) in the implementation of [array_map](http://php.net/array_map)() where HHVM uses a custom bytecode explicitly designed to make the function more efficient.

For more on the meaning and uses of all of HHVM bytecodes, see [hphp/doc/bytecode.specification](https://github.com/facebook/hhvm/blob/master/hphp/doc/bytecode.specification).

**_Note_: You should not develop applications or libraries in HHAS. The syntax of HHAS and the behavior of specific bytecodes are NOT GUARANTEED between releases of HHVM and there is almost never any benefit to be had over writing scripts in normal PHP. The coverage in this article is meant for informational purposes only.**

**Step 3.5: HHBBC Optimization**

The optimizations we performed in step 2.5 were nice quick, obvious things we could shake out during the normal course of on-the-fly code compilation, but they're not the only improvements we can make.  When building in RepoAuthoritative mode, it's possible to look at the program a bit deeper and cut out even more unnecessary work.  Consider this script:

```
<?php

define('FOO', "Hello World\n");
echo FOO;

$x = 1 + 2;
if ($x == 3) {
  echo "X is three\n";
} else {
  echo "X is not three\n";
}
```

Again, a human can look at this and know that a simplified version of this script could be heavily reduced, but keeping track of that state is too complex for the first-pass compiler to do.  So we see bytecode looking like this:


```
$ hhvm -vEval.DumpBytecode=1 /tmp/three.php

// line 3
  0: String "Hello World\n"
  5: DefCns "FOO"
 10: PopC
 // line 4
 11: Cns "FOO"
 16: Print
 17: PopC
// line 6
 18: Int 3
 27: SetL 0
 29: PopC
// line 7
 30: Int 3
 39: CGetL2 0
 41: Eq
 42: JmpZ 17 (59)
// line 8
 47: String "X is three\n"
 52: Print
 53: PopC
// line 11
 54: Jmp 12 (66)
// line 10
 59: String "X is not three\n"
 64: Print
 65: PopC
```

If we pre-compile this with RepoAuthoritative mode, however, the compiler spends a little more time on those bytecodes and notices the obvious patterns.  The "Cns" being looked up was just defined, so propagate that straight in.   Also, that local being fetched by CGetL was just set from a constant, bring that constant forward as well.

```
// line 3
  0: String "Hello World\n"
  5: DefCns "FOO"
 10: PopC
 // line 4
 11: String "Hello World\n"
 16: Print
 17: PopC
// line 6
 18: Int 3
 27: SetL 0
 29: PopC
// line 7
 30: Int 3
 39: Int 3
 41: Eq
 42: JmpZ 17 (59)
// line 8
 47: String "X is three\n"
 52: Print
 53: PopC
// line 11
 54: Jmp 12 (66)
// line 10
 59: String "X is not three\n"
 64: Print
 65: PopC
```

Which of course, now means that the "Eq"/"JmpZ" have known behavior and we can just fall-through to the truth block, making the false block unreachable, so we can take it out too.

```
$ hhvm --hphp -l0 -k1 -o /tmp/three.repo /tmp/three.php
$ hhvm --hhbbc --no-logging -o /tmp/three.repo.hhbbc /tmp/three.repo
$ hhvm -vRepo.Authoritative=true -vRepo.Commit.Path=/tmp/three.repo.hhbbc \
       --file=/tmp/three.php

// line 3
  0: String "Hello World\n"
  5: DefCns "FOO"
 10: PopC
 // line 4
 11: String "Hello World\n"
 16: Print
 17: PopC
// line 6
 18: Int 3
 27: SetL 0
 29: PopC
// line 8
 47: String "X is three\n"
 52: Print
 53: PopC
```


And we have a simpler, saner looking script.  HHBBC, which performs many other optimiztions than this, can be found under [hphp/hhbbc](https://github.com/facebook/hhvm/tree/master/hphp/hhbbc).

**Interp Mode Runtime**

Now that we have a stream of opcodes, we have enough information to actually execute the script! This execution happens primarily in [hphp/runtime/vm/bytecode.cpp](https://github.com/facebook/hhvm/blob/master/hphp/runtime/vm/bytecode.cpp) with each bytecode being executed by methods named iopWhatever(), where "Whatever" is the name of the bytecode being executed. This mode of script execution is known as "Interpreter Mode", or "Interp" for short. At this stage we’re roughly equivalent to how PHP5 compiles and executes Opcodes.  Note that this is also the point at which RepoAuthoritative mode stops, as this is the extent of static analysis. All further compilation steps happen at runtime and are unique to HHVM (relative to PHP).

**Step 4: Intermediate Representation**

As our code is run, the engine gets a "feel" for what sorts of types enter each execution unit (function/method), and is able to apply this to larger-scale program analysis. When we enter a function with new argument types, we begin emitting instructions from [hphp/runtime/vm/jit/hhbc-translator.cpp](https://github.com/facebook/hhvm/blob/master/hphp/runtime/vm/jit/hhbc-translator.cpp) in the form of HHIR (HipHop Intermediate Representation) which you can see by "tracing" program execution.


```
$ TRACE=printir:1 hhvm /tmp/hello.php

[...lots of output, run it yourself to see...]
B2 (Preds B0)
  --- bc 5, spOff 1 ()
    5: Print
    (07) PrintStr "Hello World\n"
[...more output, ->B# represents a jump to that block...]
```


Notice that the Print bytecode got reduced back to a single logical instruction along with its argument.  That's because at this point the runtime has already analyzed that the stack value which came from the String bytecode belongs with this instruction, and this one only, and that its type is known ahead of time.  I know this feel a little backwards since we knew this earlier on in the compilation as well, but stay with me for a bit...

For details on each IR instruction, check out [hphp/doc/ir.specification](https://github.com/facebook/hhvm/blob/master/hphp/doc/ir.specification).

**Step 5: Virtual Assembly**

We’ve nearly reached machine code! In [hphp/runtime/vm/jit/code-gen-x64.cpp](https://github.com/facebook/hhvm/blob/master/hphp/runtime/vm/jit/code-gen-x64.cpp) [1], the cgWhatever() helper methods take an IR instruction from the previous step and translate it into a series of architecture agnostic "machine code" instructions. While a lot of assemblers might be concerned about moving values into appropriate registers and issuing type/size-specific cpu instructions, this form stops slightly short and focuses on the job at hand with arguments and addresses being relegated to "virtual" registers and instructions. For example, Vasm code to test the result value of a previous expression, and jump on a non-zero value might look like the following:


```
v << cmp{ inst->src(0), 0 };
v << jcc{ CC_E, {inst->next()} };
```


We don’t need to care, at this point, what register inst->src(0) refers to (e.g. rax, ebx, ch, dl, rdi, esi, etc…), only that it is the same register which came from some prior instruction’s ->dest() (destination). Similarly, we’re not concerned with how equality is checked. On x86 this might be done by testing the Zero flag, on others it may be by checking the negation of a "Difference" flag.  Lastly, we don’t need to know where the next instruction’s entry point is at. It could be one byte ahead (meaning no jump need be performed at all), 64 bytes on (calling for a short jump), or at the other end of our memory model entirely (necessitating a long jump). The next, and final step of compilation will take care of all of these details for us.

[1] _This file is somewhat misnamed due to legacy reasons and Vasm having only recently been introduced. It is (almost) not x86_64 specific._

**Step 6: Emitting machine code**

Now that we’ve followed our code from PHP to AST, HHBC, HHIR, and Vasm, we’re finally ready to write it into a block of executable memory to be run by the CPU directly without further involvement from HHVM’s compiler.

This actually occurs somewhat in parallel with the Vasm stage as we’re shifting virtual instructions into the compiler (v, in the example above). To see what is produced, we can simply turn up the detail on our TRACE.

```
$ TRACE=printir:2 hhvm /tmp/comparison.php

[...lots and lots of output...]
  0x30c00030: cmp qword ptr [rbp+0x8], 0
  0x30c00036: jz 0x30c0003b
[...even more output...]
```

Here we see those same Vasm instructions expressed, in this case, as x86_64 assembly. The cmp instruction is selected because we are comparing all 64bit of a quad-word stack address to 0. Pulling its value from a stack offset like that is a pretty good indication it was a function argument, though it could have been something else. As this is x86_64, we evaluation a truth compare by examining the zero flag with jz (jump on zero) targeting a location slightly further down (the target of inst->next()).

And there you have it. How HHVM’s sausage is made in six easy steps. Now you’re ready to get hacking on the compiler and make PHP run even faster!
