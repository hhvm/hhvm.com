---
title: "Project Update and OSS Support Changes"
layout: post
author: paulbiss
category: blog
---

Hi everyone 👋

It’s been a while since our last update here, and a lot has changed in the last year. The Hack and HHVM teams have been busy working on a wide array of improvements to both the language and the runtime, this year we’ve already landed over 2.5k commits. A lot has changed for us in the last year - our teams have been asked to take on a lot of new scope and projects, and we continue to have a very small number of open source users picking up our HHVM+Hack builds. As a result, we feel we need to reevaluate some of our open source strategy. First let’s talk about some of the major changes to the project:

  * We’ve made the decision to drop support for GCC. Meta has begun using Clang for all internal builds, and with Meta’s reduced investment, we can’t afford to maintain a separate CI for GCC.
  * Additionally, we will no longer be creating official releases of HHVM and Hack. As we’ve increased the cadence and automation around our internal releases, maintaining old versions of HHVM has become a full-time job that we lack the bandwidth for.
  * Finally, while we plan to keep CI for our CMake build system on GitHub, we will no longer be supporting these builds ourselves. We’re asking that the community take a more active role in fixing and maintaining this system. For years, our CMake builds have required very little attention but the increasing coupling of Hack and HHVM and the introduction of more Rust code has made this far more time-consuming.

We remain committed to sharing the work we’re doing and engaging with the open-source community, but the reality is, we can’t afford to validate and release the variety of HHVM and Hack combinations like we used to. 

Our team has been working hard on a number of internal projects focused on improving the performance of our developer tools, enhancing the Hack language, improving the reliability of the runtime, and completing some major infrastructure changes, and we look forward to sharing those wins with this community.

This year has brought many new features to the Hack language, so far we’ve completed work on true types, equality refinement, with refinement, and type constant support for enum classes. Each of these features deserves its own more detailed breakdown, but we will summarize them here. With true types, Hack can now differentiate between three classes of type information: trusted, best effort, and dynamic. A type is said to be trusted when we’re sure that the static inference from the type checker is correct; best effort when that inference may be incorrect in the presence of dynamic code, and dynamic when a meaningful type cannot be inferred.  Equality refinements allow Hack to narrow inferred types using the result of === and !== comparisons, resulting in more fluent code with fewer duplicative checks to satisfy the type checker. The new with refinement feature behaves similarly to a where clause, but can correctly handle abstract type constants and require less boilerplate.

Improving the performance and usability of our developer tooling has been a major focus of our teams. This year we’ve made major improvements to the performance of HHVM’s autoloader resulting in 50-60% faster autoloading on sandboxes.  The REPL incorporated with HHVM’s debugger has been improved to support automatic lambda captures of variables defined in the REPL, and await syntax used in top-level expressions in the REPL. We also plan to complete the deprecation of the old HPHPD debugger in favor of our LSP bindings from the vsdebug extension.

On the HHVM team, we’ve completed work on a pair of major infrastructure changes, FactsDB and Declaration Directed Bytecode (DDB). FactsDB is a replacement for user-specified autoload maps created using autoload_set_paths. It computes an autoload map for a repository within HHVM, allowing us to reuse the map for various optimizations and new features, including DDB. It also provides an API for introspection over the codebase that can answer subtype queries not generally possible with reflection. With autoloading now occurring natively we also plan to begin removing support for explicit require and include statements. Building on Facts, DDB is a new feature that allows HHVM’s bytecode compiler to access information about top-level declarations stored in FactsDB while compiling source files. We plan to leverage this new functionality to enable new classes of language features that either have not previously been possible or have been prohibitively complicated to implement.

We have resumed our work to support the ARM architecture in our compiler backend and runtime. HHVM is once again being tested in an ARM environment and we have been actively making fixes and improvements to enhance the performance of workloads running on ARM.

Lastly, we have continued to invest in the tooling we use to further our work on the Hack and HHVM projects. We have been implementing debugging tools for use with lldb similar to those we have made available for gdb as part of our move to Clang. We have begun work to pair down the enormous number of configuration options currently available in HHVM, which we find are often under tested.

