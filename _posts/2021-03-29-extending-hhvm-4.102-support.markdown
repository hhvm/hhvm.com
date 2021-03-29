---
title: "Extending HHVM 4.102 Support"
layout: post
author: jjergus
category: blog
---

HHVM 4.102 is the last release where `varray` and `darray` are treated as
distinct types from `vec` and `dict`. From HHVM 4.103 on, `varray` becomes an
alias for `vec`, and `darray` an alias for `dict` (in HHVM 4.101 and 4.102, the
INI option `hhvm.hack_arr_dv_arrs=1` can be used to enable the new behavior).

To give users more time to migrate, we are promoting HHVM 4.102 to a long-term
support (LTS) release. Similarly to other LTS releases, it will be supported for
approximately 48 weeks&mdash;until superseded by two regularly scheduled LTS
releases, expected to be HHVM 4.128 and 4.152.

This replaces the regularly scheduled LTS release, HHVM 4.104, which will likely
be a standard release (supported for 6 weeks). However, we might add one more
unscheduled LTS release between HHVM 4.102 and 4.128 if it makes the migration
from `varray`/`darray` to `vec`/`dict` easier.
