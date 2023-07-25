---
title: "Integer Overflow leading to OOB write in HHVM"
layout: post
author: wilfred
category: blog
---


We've identified an issue where large multibyte uploads can overflow a
32-bit integer and cause out-of-bounds array access.

This is similar to a PHP had security issue in the past:
https://github.com/php/php-src/commit/3c8582ca4b8e84e5647220b647914876d2c3b124

Patches have been applied on the `HHVM-4.153`, `HHVM-4.168` and
`HHVM-172` branches (releases 4.172.2, 4.168.3 and 4.153.5
respectively), as well as the `master` branch. Packages are not
currently available, so users will need to build their own packages.
