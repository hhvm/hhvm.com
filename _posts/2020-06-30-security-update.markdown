---
title: "Security Update"
layout: post
author: jjergus
category: blog
---

A security update has been released for all supported HHVM versions. Please
update to one of the following versions to make sure you're secure:

- 4.32.3
- 4.56.1
- 4.57.1
- 4.58.2
- 4.59.1
- 4.60.1
- 4.61.1
- 4.62.1
- 4.64.0 (new version released today)

This security update addresses the following vulnerabilities:

- value of `hhvm.admin_server.password` could be revealed by functions like
  `ini_get()`, `ini_get_all()`, `phpinfo()`
- [CVE-2020-1898](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1898):
  possible crash (stack overflow) because of a missing nesting limit in `fb_unserialize()`, `fb_compact_unserialize()`
- [CVE-2020-1899](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1899):
  arbitrary memory access in `unserialize()` if type code 'S' is used
  maliciously
- [CVE-2020-1900](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1900):
  possible use-after-free in `unserialize()` when unserializing an object with
  dynamic properties
