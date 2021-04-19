---
title: "Security Update"
layout: post
author: jjergus
category: blog
---

A security update has been released for all supported HHVM versions. Please
update to one of the following versions to make sure you're secure:

- 4.56.6
- 4.80.4
- 4.99.1
- 4.100.1
- 4.101.1
- 4.102.1
- 4.103.1
- 4.104.1
- 4.105.1

This security update addresses the following vulnerabilities:

- possible crash (null pointer dereference) in `mailparse_rfc822_parse_addresses()`
- "type confusion" bugs (possible memory corruption/out-of-bounds memory access) in:
  - `AsyncMysqlClient` methods: `connect()`, `connectAndQuery()`, `connectWithOpts()`
  - `AsyncMysqlConnectionPool::connectWithOpts()`
  - `mysql_connect_with_ssl()`
  - `IntlCalendar` methods: `after()`, `before()`, `equals()`, `isEquivalentTo()`
  - `IntlTimeZone::hasSameRules()`
  - `XMLReader::expand()`
  - various `DOMDocument`, `DOMNode`, `DOMImplementation`, `DOMXPath` methods
