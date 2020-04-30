---
title: "Security Update"
layout: post
author: jjergus
category: blog
---

A security update has been released for all supported HHVM versions. Please
update to one of the following versions to make sure you're secure:

- 4.8.8
- 4.32.2
- 4.49.1
- 4.50.1
- 4.51.1
- 4.52.2
- 4.53.1
- 4.54.1
- 4.55.1

This security update addresses the following vulnerabilities:

- If the
  [GlobalDocument](https://github.com/facebook/hhvm/commit/c59a087967633a37c8cd2389d38a0fb7904428e1)
  request routing mode is used, it is possible to infer
  the existence of arbitrary source code directories.
  This issue doesn't affect HHVM 4.8, since it doesn't support GlobalDocument.

The following were originally reported as PHP vulnerabilities, but HHVM is also affected:

- [CVE-2019-9638](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9638)
- [CVE-2019-9639](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9639)
- [CVE-2019-9640](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9640)
- [CVE-2019-11034](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11034)
- [CVE-2019-11038](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11038)
- [CVE-2019-11041](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11041)
- possible buffer overrun in `exif_read_data()`
- possible buffer overrun in `socket_sendto()`
- `sodium_crypto_generichash_init()`
  [leaks data](https://bugs.php.net/bug.php?id=78510) from uninitialized memory
