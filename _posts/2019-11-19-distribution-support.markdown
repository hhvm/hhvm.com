---
title: "Support lifecycle for older distributions"
layout: post
author: fred
category: blog
---

We currently package for Debian 8 (Jessie) from 2015, and Ubuntu 16.04; this
constrains us in several ways, such as:

- supporting building with older system libraries, especially
  OpenSSL 1.0 (1.1+ includes many breaking changes)
- supporting older GCC versions, runtimes, and C++ ABIs
- maintaining internal test infrastructure for these old distributions

To allow more time to be spent on improving Hack itself, in the future, we will
be more aggressive about removing support for older distributions.

HHVM 4.32 - due to be announced later today - will be an LTS release; 4.56 will
be the next LTS release, and is due in 24 weeks (week of 2020-05-04). 4.56 will
be the last release that supports:
- MacOS Mojave
- Debian 8 Jessie
- Debian 9 Stretch
- Ubuntu 16.04

In HHVM 4.57 and above, we will aim to support:
- MacOS: the latest stable release (currently Catalina). If the release has been
  stable for less than 6 months, we will also aim to support the previous stable
  version (currently Mojave)
- Debian: `stable` (currently Buster). If the current `stable` was released in
  the last 6 months, we will also aim to support `oldstable` (currently
  Stretch). We are open to investigating support for Debian `testing` (currently
  Bullseye), but are not currently doing so.
- Ubuntu:
  - the current LTS release (18.04); if the LTS is less than 6 months old, the
    previous LTS will also be supported
  - non-LTS ('interim') releases will be supported for 9 months from their
    release; this matches the length of time that they are supported by
    Canonical

## What ending support means

In general, we do not intend to proactively stop testing/packaging for
distributions as soon as they become 'unsupported'; however:

- when we want to upgrade our internal test infrastructure or update the minimum
  versions of our dependencies, the versions provided by unsupported
  distributions will not be a factor in that decision
- if our packaging starts failing on supported distributions, we may stop
  building for them instead of fixing it

Given we want to remove support for OpenSSL 1.0 and for systems using the C++5
ABI, we expect to stop building packages for several distributions - especially
Debian 8 Jessie and Ubuntu 16.04 very shortly after the release of HHVM 4.56.

## Bugfix and security updates

If we build a package for a distribution for a x.y.0 release, we intend to build
packages for that distribution for any x.y.z releases - as long as the
distribution itself continues to receive security updates from the distribution
vendor.

In other words, dropping support for a distribution in a new release does not
affect support for that distribution in past verisons of HHVM.

For example:
- 4.56.0 will support Debian 8 Jessie and Ubuntu 16.04
- if a 4.56.1 release is made mid-June 2020, it would still support Debian 8 and
  Ubuntu 16.04 - even if 4.57 has been released without support for those
  distributions
- if a 4.56.2 release is made in July 2020, it would still support Ubuntu 16.04,
  but it would not support Debian 8, as Debian 8 reaches end of life on June
  30th, 2020

## Using unsupported distributions

We **strongly** recommend using a supported distribution instead. That said,
there are several options:

- run HHVM via Docker or other containerization techniques
- install/build updated versions of any required dependencies (likely to include
  GCC and OpenSSL), then build/package HHVM yourself
- send pull requests to fix builds on unsupported distributions - though we will
  not accept pull requests that increase the burden on developers; for example,
  once folly drops support for OpenSSL 1.0, we will not accept pull requests
  that re-add it

If you are using a current version of a distribution that we do not package for
at all (e.g. CentOS), we would appreciate pull requests to add support to
[our packaging infrastructure](https://github.com/hhvm/packaging); any new
packaging should be:
- reproducible. For example, fetching `master` of a dependency from github is
  not acceptable
- following the distribution's best practices for packaging as much as possible.
  For example, this could mean using `rpmbuild` or `debuild` or similiar instead
  of manually building a package from binaries created separately

The HHVM support lifecycle for any other distributions would likely be similar
to our support lifecycle for Debian and Ubuntu, aiming to provide some upgrade
window while allowing us to frequently update the minimum versions of
dependencies.
