---
title: "Security Update"
layout: post
author: jjergus
category: blog
---

A security update has been released for all supported HHVM versions. Please
update to one of the following versions to get the update:

- 4.21.0 (new version being released today)
- 4.20.2
- 4.19.1
- 4.18.2
- 4.17.3
- 4.16.4
- 4.15.3
- 4.8.4
- 3.30.10

This security update addresses a possible memory overflow in the GD extension
when a carefully constructed invalid JPEG input is passed in.

More information can be found in the respective CVEs:

- [CVE-2019-11925](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11925)
- [CVE-2019-11926](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11926)
