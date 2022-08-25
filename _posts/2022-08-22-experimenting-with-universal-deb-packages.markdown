---
title: "Experimenting with universal deb packages"
layout: post
author: atry
category: blog
---


We’re happy to announce that the availibility of universal deb packages, which do not depend on system libraries and should be able to be run on any Debian or Ubuntu distributions.

Note that the universal deb packages are built with Nix dependencies and then get repacked into deb format. As a result, they will conflict with packages directly installed with the Nix package manager. If you are a Nix package manager user, don't use the universal deb packages, and you should directly use the Nix packages.


``` bash
apt-get update &&
apt-get install --yes software-properties-common apt-transport-https &&
apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xB4112585D386EB94 &&
add-apt-repository --yes --sourceslist deb https://dl.hhvm.com/universal nightly main &&
apt-get update &&
apt-get install --yes hhvm &&
hhvm --version
```

``` bash
apt-get update &&
apt-get install --yes software-properties-common apt-transport-https &&
apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xB4112585D386EB94 &&
add-apt-repository --yes --sourceslist deb https://dl.hhvm.com/universal release main &&
apt-get update &&
apt-get install --yes hhvm &&
hhvm --version
```


``` bash
apt-get update &&
apt-get install --yes software-properties-common apt-transport-https &&
apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xB4112585D386EB94 &&
add-apt-repository --yes --sourceslist deb https://dl.hhvm.com/universal release-4.167 main &&
apt-get update &&
apt-get install --yes hhvm &&
hhvm --version
```
