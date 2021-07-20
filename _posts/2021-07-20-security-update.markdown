---
title: "Security Update"
layout: post
author: fred
category: blgo
---

A security update has been released for all supported HHVM versions. Please
update to one of the following versions to get the update:

- 4.80.5
- 4.102.2
- 4.113.1
- 4.114.1
- 4.115.1
- 4.116.1
- 4.117.1
- 4.118.2

4.80.6 and 4.102.3 are also released for Debian 10 Buster and Ubuntu 18.04
Bionic, updating build system compatibility with those platforms.

This security update addresses:

- [CVE-2021-24036](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-24036),
  a remote code execution vulnerability in Folly's `IOBuf` class
- an issue in HHVM that could lead to specially crafted XBox request parameter
  data being interpreted as other RPCServer commands.
