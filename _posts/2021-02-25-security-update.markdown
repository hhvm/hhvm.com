---
title: "Security Update"
layout: post
author: jjergus
category: blog
---

A security update has been released for all supported HHVM versions. Please
update to one of the following versions to make sure you're secure:

- 4.56.3 (release 4.56.4 is identical but fixes Ubuntu 16.04 and Debian 8 support)
- 4.80.2 (release 4.80.3 is identical but fixes Ubuntu 20.10 support)
- 4.93.2
- 4.94.1
- 4.95.1
- 4.96.1
- 4.97.1
- 4.98.1

This security update addresses the following vulnerabilities:

- [CVE-2020-1917](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1917):
  out-of-bounds write (1 byte) in `exif_read_data()`
- [CVE-2020-1918](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1918):
  memory disclosure vulnerability using "data:" URLs
- [CVE-2020-1919](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1919):
  out-of-bounds heap read in `substr_compare()`
- [CVE-2020-1921](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1921):
  out-of-bounds write (1 byte) in `crypt()`
- [CVE-2021-24025](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-24025):
  integer overflow causing out-of-bounds heap write in `preg_quote()`
- out-of-bounds heap read (2 bytes) in `exif_read_data()`
