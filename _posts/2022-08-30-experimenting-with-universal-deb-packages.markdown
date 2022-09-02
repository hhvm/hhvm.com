---
title: "Experimenting with universal deb packages"
layout: post
author: atry
category: blog
---

We’re happy to announce the availability of universal deb packages of HHVM,
which do not depend on system libraries and are expected to run on any version of
Debian, Ubuntu or any other Linux distributions with apt package manager.

The universal deb packages is still considered experimental like nix packages.
We encourage you to try it out and report any issues you encountered. We will
appreciate your feedback because it will help us decide if we will entirely
switch from distribution-specific packaging to universal packaging.

## Installation

These instructions require root; use `su -` or `sudo -i` to get a root shell
first.

### Obtaining The Latest Stable Version

``` bash
apt-get update &&
apt-get install --yes software-properties-common apt-transport-https &&
apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xB4112585D386EB94 &&
add-apt-repository 'deb https://dl.hhvm.com/universal release main' &&
apt-get update &&
apt-get install --yes hhvm &&
hhvm --version
```

### Obtaining A Specific Release Branch

``` bash
apt-get update &&
apt-get install --yes software-properties-common apt-transport-https &&
apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xB4112585D386EB94 &&
add-apt-repository 'deb https://dl.hhvm.com/universal release-4.167 main' &&
apt-get update &&
apt-get install --yes hhvm &&
hhvm --version
```

Currently 4.167 is the only release version including universal deb packages.
For future releases, you will be able to specify the apt suite name as
`release-x.yyy`, where x is the major version and yyy is the minor version.

### Obtaining The Nightly Version

``` bash
apt-get update &&
apt-get install --yes software-properties-common apt-transport-https &&
apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xB4112585D386EB94 &&
add-apt-repository 'deb https://dl.hhvm.com/universal nightly main' &&
apt-get update &&
apt-get install --yes hhvm &&
hhvm --version
```

## Known Issue

Note that the universal deb packages are built with nix package manager and then
get repacked into deb format. As a result, the universal deb packages will
conflict with packages directly installed from the nix package manager. If you
are a nix package manager user, you should directly use the nix packages
announced in [this
post](https://hhvm.com/blog/2022/07/12/experimenting-with-nix-github-actions-and-visual-studio-code.html),
instead of the universal deb packages in case of path conflicts.
