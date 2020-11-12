---
title: "Security Update"
layout: post
author: jjergus
category: blog
---

A security update has been released for all supported HHVM versions. Please
update to one of the following versions to make sure you're secure:

- 4.56.2
- 4.78.1
- 4.79.1
- 4.80.1
- 4.81.1
- 4.82.1
- 4.83.1

This security update addresses the following vulnerabilities:

- `dump-static-strings`
  ([CVE-2019-3555](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-3555))
  and `dump-pcre-cache`
  ([CVE-2019-3556](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-3556))
  admin endpoints can write to any file the webserver has access to
- out of bounds read in `crypt()`
- `light-process.cpp` not dropping privileges correctly
- integer overflow in `gdImageCreate()`
- null pointer dereference in `XMLReader::expand()`
- buffer overflow in `ldap_escape()`
  ([CVE-2020-1916](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1916))
