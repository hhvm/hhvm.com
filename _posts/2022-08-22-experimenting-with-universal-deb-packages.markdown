
``` bash
apt-get update &&
apt-get install --yes software-properties-common apt-transport-https &&
apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xB4112585D386EB94 &&
add-apt-repository --yes --sourceslist deb https://dl.hhvm.com/universal nightly main &&
apt-get update &&
apt-get install --yes hhvm &&
hhvm --version
```
