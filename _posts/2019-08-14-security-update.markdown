---
title: "Security Update"
layout: post
author: jjergus
category: blog
---

A security update has been released for all supported HHVM versions. Please
update to one of the following versions to get the update:

- 4.18.1
- 4.17.2
- 4.16.3
- 4.15.2
- 4.14.2
- 4.13.2
- 4.12.2
- 4.8.3
- 3.30.9

This security update addresses a HTTP/2 Deny-of-Service vulnerability in the
Proxygen library bundled with HHVM.

More information can be found in the respective CVEs:

- [CVE-2019-9512](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9512)
- [CVE-2019-9513](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9513)
- [CVE-2019-9514](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9514)
- [CVE-2019-9515](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9515)

Note that these vulnerabilities are not specific to HHVM or Proxygen, so keep an
eye out for updates to other HTTP/2 server and client packages.
