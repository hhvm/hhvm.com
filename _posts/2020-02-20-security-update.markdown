---
title: "Security Update"
layout: post
author: jjergus
category: blog
---

A security update has been released for all supported HHVM versions. Please
update to one of the following versions to make sure you're secure:

- 4.8.7
- 4.32.1
- 4.38.1
- 4.39.1
- 4.40.1
- 4.41.1
- 4.42.1
- 4.43.1
- 4.44.1
- 4.45.1

This security update addresses vulnerabilies in JSON decoding:

- [CVE-2020-1888](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1888):
  Insufficient boundary checks when decoding JSON in handleBackslash reads out
  of bounds memory, potentially leading to DOS.
- [CVE-2020-1892](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1892):
  Insufficient boundary checks when decoding JSON in JSON_parser allows read
  access to out of bounds memory, potentially leading to information leak and
  DOS.
- [CVE-2020-1893](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1893):
  Insufficient boundary checks when decoding JSON in TryParse reads out of
  bounds memory, potentially leading to DOS.

The new packages also include updates to some of the bundled dependencies:

- backported patch for
  [CVE-2017-14107](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-14107)
  in the bundled `libzip` library
- updated the bundled `libsqlite3` library from 3.23.1 to 3.30.1, as the older
  version might be affected by multiple published vulnerabilities

Note that the bundled dependencies are only used on systems that don't already
provide those libraries.
