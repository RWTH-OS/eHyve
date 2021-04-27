# ehyve - A minimal hypervisor for eduOS-rs

![Actions Status](https://github.com/RWTH-OS/ehyve/workflows/Build/badge.svg)

## Introduction

ehyve is small hypervisor to boot the operating systems [eduOS-rs](https://github.com/RWTH-OS/eduOS-rs), which is a Unix-like operating system based on a monolithic architecture for educational purposes. ehyve is tested under Linux, macOS, and Windows.

## Installation

ehyve can easily be installed via [cargo](https://doc.rust-lang.org/cargo/), which is shipped with Rust by default.
The **nightly** compiler must be activated for building ehyve.

```sh
$ cargo +nightly install --git https://github.com/RWTH-OS/ehyve.git --locked
$ ehyve --version
eHyve 0.0.10
```

## Requirements

ehyve requires a CPU with Virtualization features (Intel Hyper-V or AMD-V). **Ensure that these are enabled in the BIOS/EFI!**

### OS-Specific:

#### Linux
Linux users should install common developer tools.
For instance, on Ubuntu 18.04 the following command installs the required tools:

```sh
$ apt-get install -y curl wget make autotools-dev gcc g++ build-essential git
```

#### macOS
Apple's *Command Line Tools* must be installed.
The Command Line Tool package gives macOS terminal users many commonly used tools and compilers, that are usually found in default Linux installations.
Following terminal command installs these tools without Apple's IDE Xcode:

```sh
$ xcode-select --install
```

Additionally, the included hypervisor bases on the [Hypervisor Framework](https://developer.apple.com/documentation/hypervisor) depending on OS X Yosemite (10.10) or newer.
To verify if your processor is able to support this framework, run and expect the following in your Terminal:

```sh
$ sysctl kern.hv_support
kern.hv_support: 1
```

#### Windows

To build eduOS-rs you have to install a linker, [make](http://gnuwin32.sourceforge.net/packages/make.htm) and a [git client](https://git-scm.com/downloads).
We tested the eduOS-rs with the linker from Visual Studio.
Consequently, we suggest installing Visual Studio in addition to [make](http://gnuwin32.sourceforge.net/packages/make.htm) and [git](https://git-scm.com/downloads).

Furthermore, the included hypervisor bases on the [Windows Hypervisor Platform](https://docs.microsoft.com/en-us/virtualization/api/) depending on Windows 10 (build 17134 or above) or Windows Server (1803 or above).
Please activate this feature as *Administrator* by using the following command on your system:

```sh
Dism /Online /Enable-Feature /FeatureName:HypervisorPlatform
```

### Rust installation

It is required to install the Rust toolchain.
Please visit the [Rust website](https://www.rust-lang.org/) and follow the installation instructions for your operating system.
It is important that the *nightly channel* is used to install the toolchain.
This is queried during installation and should be answered as appropriate.

Afterwards the installation of the Rust runtimes source code is required to build the kernel:

```sh
$ rustup component add rust-src
```

## Building from source
ehyve can be build from source with `cargo`. You only need a copy of the repository with the submodules:

```sh
$ git clone git@github.com:RWTH-OS/ehyve.git
$ cd ehyve
$ git submodule update --init
$ cargo build --release
```
The ehyve binary can then be found at `target/release/ehyve`:

```sh> 
$ target/release/ehyve --version
eHyve 0.0.10
```


## Licensing
Licensed under either of

 * Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.
