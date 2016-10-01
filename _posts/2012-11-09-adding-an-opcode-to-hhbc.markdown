---
author: oyamauchi
comments: true
layout: post
title: Adding an opcode to HHBC
category: blog
redirect_from:
  - /blog/311/adding-an-opcode-to-hhbc
---

As part of our drive to improve HHVM's performance, I started looking into the general topic of builtin functions. Currently, HHVM is calling implementations of builtin functions that were originally written for HPHPc, the static compiler. We wrote compatibility wrappers around them for HHVM, to get it up and running as quickly as possible. We have evidence that this compatibility layer is hurting HHVM's performance, so we're looking at ways to reduce or eliminate its impact.

I loaded some Facebook pages in an instrumented build of HHVM, to find out which builtins we call most. Here are the top 10 most-called builtins.

<table >
	<tr >Percentage of callsCumulative pct.</tr>
<tr >
<td >9.68
</td>
<td > 9.68
</td>
<td >strlen
</td></tr>
<tr >
<td >7.36
</td>
<td >17.05
</td>
<td >count
</td></tr>
<tr >
<td >5.07
</td>
<td >22.12
</td>
<td >strncmp
</td></tr>
<tr >
<td >4.57
</td>
<td >26.69
</td>
<td >strpos
</td></tr>
<tr >
<td >4.09
</td>
<td >30.79
</td>
<td >substr
</td></tr>
<tr >
<td >4.06
</td>
<td >34.86
</td>
<td >apc_store
</td></tr>
<tr >
<td >2.98
</td>
<td >37.84
</td>
<td >key
</td></tr>
<tr >
<td >2.86
</td>
<td >40.70
</td>
<td >is_numeric
</td></tr>
<tr >
<td >2.50
</td>
<td >43.21
</td>
<td >reset
</td></tr>
<tr >
<td >2.44
</td>
<td >45.65
</td>
<td >error_reporting
</td></tr>
</table>

The top one, `strlen`, has very simple behavior for the common case where the argument is a string. The C++ class that we use to represent strings has a member variable that holds the string's length -- it takes a single machine instruction to retrieve it.

`strlen`'s simplicity makes it a very good candidate for turning into an HHBC opcode. That way, we'll be able to manually compile it to a handful of machine instructions. The verbal description of what the new opcode will do is simple: it pops a value off the evaluation stack, converts that value to a string if it's not already a string, and pushes the string's length onto the stack as an integer.

You can look at the final commit on [GitHub](https://github.com/facebook/hiphop-php/commit/3b96353ea0f494daa23b5db64cb2190429eb32b6). In the rest of this post, I'll explain the important parts of this commit: how to create the new opcode, implement its behavior, and make it fast by implementing it in the just-in-time compiler. By the end of it, you should be able to implement `count`, the next most-called builtin, as an opcode by following along with what I did for `strlen`. Their behavior is very similar.

<!-- more -->



## Add the opcode to the master enum



In `src/runtime/vm/hhbc.h`, there's a big table of preprocessor macros that lists every HHBC opcode, along with some information about them: whether they have any immediate arguments, what they push and pop on the evaluation stack, and whether they have any special behavior like affecting control flow. This table is used in many places to generate code that needs to enumerate all the opcodes. We add our new opcode, `OpStrlen`: no immediates, pops one cell, pushes one cell, no special behavior.




    O(Strlen, NA, ONE(CV), ONE(CV), NF)






## Emit the new opcode when we see a call to `strlen` in the source code



In `src/compiler/analysis/emitter.cpp` is the code that walks a parse tree and outputs the corresponding HHBC. We need to change the code that handles simple function calls, and have it emit our new `OpStrlen` opcode when it sees a call to `strlen`.




        ...
    } else if (call->isCallToFunction("strlen")) {
      if (params && params->getCount() == 1) {
        visit((*params)[0]);
        emitConvertToCell(e);
        e.Strlen();
        return true;
      }
    }
      ...




I want to note two points about this that limit the scope of the optimization:





  * This only covers direct calls to the builtin. There are other ways to call functions in PHP (e.g. `$f()`), and the new opcode won't be involved with those. We'll keep the C++ implementation of `strlen` in place for this reason. However, `strlen` is called directly in the vast majority of cases, so this restriction won't hurt the optimization much, if at all.


  * We only convert callsites that have one argument. (If you call `strlen` with any number of arguments other than one, a warning is raised and NULL is returned.) This is simply to keep the implementation of the opcode clean; we won't have to worry about checking the argument count, raising warnings, and adjusting the evaluation stack. Again, this restriction will have a negligible effect on performance.





## Implement it in the interpreter



In `src/runtime/vm/bytecode.cpp`, there are functions that implement the behavior of each opcode. (They're declared in `src/runtime/vm/bytecode.h`, using some of the aforementioned preprocessor macro tricks.)




    inline void OPTBLD_INLINE VMExecutionContext::iopStrlen(PC& pc) {
      NEXT();
      TypedValue* subj = m_stack.topTV();
      int64 ans = 0;
      if (LIKELY(IS_STRING_TYPE(subj->m_type))) {
        ans = subj->m_data.pstr->size();
      } else {
        ans = f_strlen(tvAsVariant(subj));
      }

      tvRefcountedDecRef(subj);
      subj->m_type = KindOfInt64;
      subj->m_data.num = ans;
    }




Note that we're only really going after the string-input case here. In all other cases, we fall back to the old behavior.

At this point, we've achieved correctness. Just-in-time-compiling opcodes is always optional. If the JIT encounters an opcode that it doesn't know how to translate, it simply falls back to the interpreter. This is slow, though, and the whole point of this new opcode was speed, so let's keep going.



## Describe the opcode's effects on types



In `src/runtime/vm/translator/translator.cpp`, there's another big table of preprocessor macros that has some more specific information about the inputs and outputs of each opcode. That is, which memory locations does it read from and write to, and what type does it output? `OpStrlen` is very simple: its only input is the top of the eval stack, and its only output is the same. Its output type is an integer. It does not cause the stack pointer to move.

This information drives the JIT compiler's logic for storing in-flight program values in machine registers. Before calling the function to emit machine code for the `OpStrlen` opcode itself, the JIT will ensure that the opcode's input is in registers already (possibly by emitting load instructions, if need be). It will also know which register the opcode's output is in, and what type it is. This allows it to synchronize enregistered program state back to memory, when the time comes.



## Emit native machine code



Now it's time to write out the machine instructions to implement this functionality. We'll call methods, representing x86 instructions, on an assembler object, which will write machine code to the HHVM process' translation cache.

First, we have to tell the JIT infrastructure how we intend to handle the instruction. This can range from entirely "native" -- using only generated machine code, with no calls to C++ helper functions -- to "interp", meaning fall back to the interpreter's implementation in `bytecode.cpp`. In this case, our answer depends on the type of the input, which the JIT knows, since it's compiling this chunk of bytecode on-demand.




    void TranslatorX64::analyzeStrlen(Tracelet& t,
                                      NormalizedInstruction& i) {
      switch (i.inputs[0]->rtt.valueType()) {
        NULLCASE() :
        case KindOfBoolean:
          i.m_txFlags = Native;
          break;
        STRINGCASE() :
          // May have to destroy a StringData, but can't reenter
          i.m_txFlags = Simple;
          break;
        case KindOfArray:
          i.m_txFlags = Supported;
          break;
        case KindOfInt64:
        case KindOfDouble:
        case KindOfObject:
          i.m_txFlags = Interp;
          break;
        default:
          not_reached();
      }
    }




As described in the previous step, the JIT infrastructure will ensure that the input to the opcode (the topmost value on the eval stack) is already in a register, and we can now get that register's name. Since the input and output are both the top of the eval stack, we write the output back to the input register. If the input were in `%r13`, say, we could do this:




        mov 0xc(%r13), %r13




Is that it? Are we done? Could it possibly be that easy? Are we now doing, with one instruction, what previously took many tens of instructions?

That's actually not quite correct, for a subtle reason, whose effects you won't directly see in PHP code. It's a memory leak: we're destroying a reference to a StringData object that we've allocated memory for, but we're not updating its reference count. We need to decrement its refcount, and free its memory if its refcount is now zero[1]. We play a little trick with the register allocator: we allocate a scratch register to hold the output, use the original input register to do the refcounting, and then tell the register to change which register it thinks the top stack slot is in.




    PhysReg rInput = getReg(i.inputs[0]->location);
        ...
    ScratchReg rScratch(m_regMap);
    a.  load_reg64_disp_reg32(rInput, StringData::sizeOffset(), *rScratch);
    emitDecRef(a, i, rInput, inType);
    m_regMap.bindScratch(rScratch, i.outStack->location, KindOfInt64,
                         RegInfo::DIRTY);




Note how closely this implementation mirrors `iopStrlen` in `bytecode.cpp`. We're essentially writing out machine instructions that do the same thing that that function does.



## The IR translator



There's another part of the commit that I haven't touched on at all: the implementation of `OpStrlen` in the IR translator. This is a new approach to the JIT compiler, more rooted in classical compiler theory. It transforms HHBC to a static single-assignment form IR, which allows us to cleanly optimize native code emission across several HHBC instructions. However, it's still new and rapidly evolving, so I'm not going to explain those parts in this post.



## Measuring performance



Any time you make a change in the name of performance, your demonstration of correctness has to include performance results. If there's no measurable speedup, there's no sense in committing this change: it doesn't fix a behavioral bug, it doesn't make the code any cleaner, and it doesn't open up any new opportunities.

As a sanity check, I wrote a microbenchmark that calls `strlen` in a loop 100,000 times. Here are the results, with times in milliseconds (smaller numbers are faster):

<table >
	<tr >Without JITWith JIT</tr>
	<tr >

<td >**Before**
</td>
<td >14.6
</td>
<td >1.83
</td>
	</tr>
	<tr >

<td >**After**
</td>
<td >5.3
</td>
<td >0.59
</td>
	</tr>
</table>

_Standard disclaimer: these numbers are specific to my environment, your mileage may vary, etc._

We have indeed sped up `strlen`, both with the JIT and without. However, this is not an answer to the question of whether we should actually proceed with this change. A 3x speedup on a microbenchmark may not translate into anything at production scale. We may not be calling `strlen` in production enough for this to make a noticeable difference.

Fortunately, though, this change does turn out to make a noticeable difference in production. According to our production performance measurement framework, this change reduces CPU time by just under 1%. This may seem like a small number, but given the volumes of CPU time that we burn on our production web servers, even tiny improvements matter.


[1] This is actually a gateway to an interesting realm of possibilities. Unlike arrays and objects, PHP's semantics don't require strict reference counting for strings -- there may be some potential for optimization here. This is a very large design space that we haven't even begun to explore, though. back
