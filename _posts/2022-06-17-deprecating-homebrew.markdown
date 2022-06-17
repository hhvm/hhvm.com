---
title: "Stopping MacOS Homebrew Support"
layout: post
author: alexeyt
category: blog
---

#### HHVM will no longer support homebrew on MacOS going forward.

We are continuing support for it on LTS releases (4.128 and 4.153) until 
they reach EOL, but we are stopping nightly builds of HHVM on MacOS 
homebrew, will no longer be publishing MacOS homebrew packages for new 
releases, and will not be testing new versions of HHVM on MacOS going forward.

#### Why are we doing this?

We are dropping support for two reasons.  First, Homebrew has proven 
difficult to support.  Dependency versions change out from under us which 
require retroactive fixes and back-porting retroactive fixes to LTS 
releases.  Second, due to the current state of HHVM ARM support we are not 
able to provide a good experience on M1 Macs.

#### I use HHVM on MacOS homebrew, what should I do?

We recommend users on Intel macs switch to using one of our docker images. 
We are unable to support M1 users due to the different architecture and 
limitations of Rosetta. Therefore, we must recommend use of an Intel linux 
host instead.
