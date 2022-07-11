# Experimenting with Nix, GitHub Actions, and Visual Studio Code

We’re happy to announce that the [Nix](https://nixos.org/) packages of HHVM are
now available, as is the public CI status on GitHub Actions for it, and the
Visual Studio Code workspace with HHVM dependencies from Nix. The Nix packages
can be run on macOS and Linux of any distributions.

Currently, HHVM's Nix packages are not officially supported, yet. They are
provided as is and haven't been extensively battle-tested. Since we have
[dropped macOS Homebrew
support](https://hhvm.com/blog/2022/06/17/deprecating-homebrew.html), it is
likely that we will also stop building HHVM with Nix on macOS in the future,
too.

## How to Install Nix Built HHVM Packages


### For NixOS Users

For NixOS users, add the following settings to `/etc/nixos/configuration.nix` to
configure the binary cache for HHVM:


```
  nix.settings.substituters = [ "s3://hhvm-nix-cache?region=us-west-2&endpoint=hhvm-nix-cache.s3-accelerate.amazonaws.com" ];
  nix.settings.trusted-substituters = [ "s3://hhvm-nix-cache?region=us-west-2&endpoint=hhvm-nix-cache.s3-accelerate.amazonaws.com" ];
  nix.settings.trusted-public-keys = [ "hhvm-nix-cache-1:MvKxscw16fAq6835oG8sbRgTGITb+1xGfYNhs+ee4yo=" ];
  nix.settings.experimental-features = [ "nix-command" "flakes" ];
  environment.systemPackages = [
    pkgs.git # Required to support git+https protocol
  ];
```


In addition, if you want to build HHVM from source, add the following setting to
disable sandboxing because HHVM cannot be built in Nix's sandbox build
environment.


```
  nix.settings.sandbox = false;
```


Then execute the following shell command to apply the configuration to the
system:


```
nixos-rebuild switch
```


Then add HHVM to system packages, 


```
  environment.systemPackages = [
    (builtins.getFlake "git+https://github.com/facebook/hhvm.git?submodules=1&shallow=1&ref=refs/tags/nightly-2022.07.08").packages.x86_64-linux.default
    pkgs.git
  ];
```


and apply the configuration, again:


```
nixos-rebuild switch
```


Now hhvm is available.


```
hhvm --version
```



```
HipHop VM 4.164.0-dev (rel) (non-lowptr)
Compiler: 1657256394_118415120
Repo schema: 9845ff37f3bb751abbb48e4c823aa5641d5cb453
```


The above configuration has been tested on NixOS unstable and 22.11. The
configuration for older NixOS might be different.


### For Linux Users Other Than NixOS

For Linux users other than NixOS, the HHVM Nix package can be installed with the
following command if you have a [multi-user installation of
Nix](https://nixos.org/download.html#nix-install-linux):


```
(
sudo tee -a /etc/nix/nix.conf <<EOF
extra-experimental-features = nix-command flakes
extra-substituters = s3://hhvm-nix-cache?region=us-west-2&endpoint=hhvm-nix-cache.s3-accelerate.amazonaws.com
extra-trusted-substituters = s3://hhvm-nix-cache?region=us-west-2&endpoint=hhvm-nix-cache.s3-accelerate.amazonaws.com
extra-trusted-public-keys = hhvm-nix-cache-1:MvKxscw16fAq6835oG8sbRgTGITb+1xGfYNhs+ee4yo=
sandbox = false
EOF
) &&
sudo systemctl restart nix-daemon &&
nix profile install 'git+https://github.com/facebook/hhvm.git?submodules=1&shallow=1&ref=refs/tags/nightly-2022.07.08' &&
hhvm --version
```


Or if you have a [single-user installation of
Nix](https://nixos.org/download.html#nix-install-linux):


```
(
sudo tee -a ~/.config/nix/nix.conf <<EOF
extra-experimental-features = nix-command flakes
extra-substituters = s3://hhvm-nix-cache?region=us-west-2&endpoint=hhvm-nix-cache.s3-accelerate.amazonaws.com
extra-trusted-substituters = s3://hhvm-nix-cache?region=us-west-2&endpoint=hhvm-nix-cache.s3-accelerate.amazonaws.com
extra-trusted-public-keys = hhvm-nix-cache-1:MvKxscw16fAq6835oG8sbRgTGITb+1xGfYNhs+ee4yo=
sandbox = false
EOF
) &&
nix profile install 'git+https://github.com/facebook/hhvm.git?submodules=1&shallow=1&ref=refs/tags/nightly-2022.07.08' &&
hhvm --version
```


The above configuration is tested on Nix 2.9.1. The configuration for older Nix
might be different.


### For macOS Users

For macOS users, the HHVM Nix package can be installed with the following
command if you have a [multi-user installation of
Nix](https://nixos.org/download.html#nix-install-macos):


```
(
sudo tee -a /etc/nix/nix.conf <<EOF
extra-experimental-features = nix-command flakes
extra-substituters = s3://hhvm-nix-cache?region=us-west-2&endpoint=hhvm-nix-cache.s3-accelerate.amazonaws.com
extra-trusted-substituters = s3://hhvm-nix-cache?region=us-west-2&endpoint=hhvm-nix-cache.s3-accelerate.amazonaws.com
extra-trusted-public-keys = hhvm-nix-cache-1:MvKxscw16fAq6835oG8sbRgTGITb+1xGfYNhs+ee4yo=
sandbox = false
EOF
) &&
sudo launchctl remove org.nixos.nix-daemon && 
sudo launchctl load /Library/LaunchDaemons/org.nixos.nix-daemon.plist &&
sleep 3 &&
nix profile install 'git+https://github.com/facebook/hhvm.git?submodules=1&shallow=1&ref=refs/tags/nightly-2022.07.08' &&
hhvm --version
```


The above configuration is tested on Nix 2.9.1. The configuration for older Nix
might be different.


## How to Install a Different HHVM Version

The HHVM version to install is specified in the optional `ref` parameter in the
URL, which can be any git branch or tag. For example:



* To install the latest development version of HHVM
    * `nix profile install
      'git+https://github.com/facebook/hhvm.git?submodules=1&shallow=1'`
* To install HHVM nightly 2022.07.08
    * `nix profile install
      'git+https://github.com/facebook/hhvm.git?submodules=1&shallow=1&ref=refs/tags/nightly-2022.07.08'`
* To install HHVM 4.164.0
    * `nix profile install
      'git+https://github.com/facebook/hhvm.git?submodules=1&shallow=1&ref=refs/tags/HHVM-4.164.0'`
* To install the latest 4.164.* development version of HHVM
    * `nix profile install
      'git+https://github.com/facebook/hhvm.git?submodules=1&shallow=1&ref=refs/heads/HHVM-4.164'`

Since the Nix build is for new HHVM versions only, the `ref` parameter must
point to a child commit of
[21870f6097ac7dea56ea57cc9113bcfd0d1a03d0](https://github.com/facebook/hhvm/commit/21870f6097ac7dea56ea57cc9113bcfd0d1a03d0).

Also note that the binary cache for a git commit would take hours of time to be
available. If you are trying to install a recent commit, of which the binary
cache is not available yet, Nix will build it from source for you automatically,
otherwise Nix will just download the prebuilt binary.


## How to Hack on HHVM In A Nix Development Environment


### For Visual Studio Code Users

We provided a Visual Studio Code workspace to develop HHVM. To set up the VS
Code based HHVM development environment on any Linux or macOS machines:



1. Install Nix
2. Checkout HHVM with all submodules: `git clone
   https://github.com/facebook/hhvm.git --depth 1 --recurse-submodules `
3. Open `hhvm.code-workspace` from Visual Studio Code
4. Install extension recommendations
5. Reload Visual Studio Code
6. Wait for the extensions to be activated. Note that it would take minutes to
   download dependencies, depending on your network speed.
7. Click the Build button from the CMake panel in Visual Studio Code

See [this instructional video](/static/videos/posts/vscode.mp4) for more detail.


#### Using Development Containers Or GitHub Codespaces

Alternatively, we also provide a development container with Nix pre-installed,
which can be either used in a local Docker engine or in GitHub Codespaces. It is
easy to make trivial changes to the code base but it might not be suitable for
heavy development because the development container runs slower than the either
local VSCode or remote VSCode server via SSH.

See [this instructional video](/static/videos/posts/github-codespaces.mp4) for
more detail.


### Working From The Command Line

To start a clean build HHVM from source:



1. Install Nix.
2. Checkout HHVM with all submodules: `git clone
   https://github.com/facebook/hhvm.git --depth 1 --recurse-submodules`
3. Under the work tree, run `nix-build`

To incrementally edit the source and build HHVM:



1. Install Nix.
2. Checkout HHVM with all submodules: `git clone
   https://github.com/facebook/hhvm.git --depth 1 --recurse-submodules`
3. Under the work tree, run `nix develop .?submodules=1 --ignore-environment` to
   enter a development shell. All the HHVM dependencies and development tools
   will be available in **<code>$PATH</code></strong> and other environment
   variables.
4. In the development shell, run <code>configure -C "$CMAKE_INIT_CACHE"</code>
   to configure HHVM.
5. In the development shell, run <code>make</code> to build HHVM.
6. Make some changes to the source code.
7. In the development shell, run <code>make</code> to compile the affected files
   only.


### Making Ad-hoc Changes

Feel free to directly edit files in the [HHVM
repository](https://github.com/facebook/hhvm) on GitHub website and create a
pull request for ad-hoc changes. We have introduced GitHub Actions to build and
test your pull requests with Nix. Just take the advantage from the CI signal and
have fun!
