---
title: "CVE-2023-0567: Invalid password hashes accepted by crypt()"
layout: post
author: wilfred
category: blog
---


We've just released patch releases for HHVM: 4.172.2, 4.168.3 and
4.153.5. These resolve the security issue CVE-2023-0567.

The function `crypt()` would accept invalid password hashes. This is
also an issue in PHP, which fixed this in 8.0.28.

https://bugs.php.net/bug.php?id=81744
https://github.com/php/php-src/security/advisories/GHSA-7fj2-8x79-rjf4
