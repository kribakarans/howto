# OpenWRT

## [OpenWrt source code](https://github.com/openwrt/openwrt)
	git clone https://git.openwrt.org/openwrt/openwrt.git

## General source structure
These are the folders you can find in the project’s git:

- **/config**  : configuration files for menuconfig
- **/include** : makefile configuration files
- **/package** : packages makefile and configuration
- **/scripts** : miscellaneous scripts used throughout the build process
- **/target**  : makefile and configuration for building image builder, kernel, sdk and the toolchain built by buildroot.
- **/toolchain** : makefile and configuration for building the toolchain
- **/tools** : miscellaneous tools used throughout the build process

## Build system Directory structure
There are four key directories in the build system:
- **tools** - contains various utilities required for building toolchain and packages (e.g. autoconf automake), or for image generation (e.g. mkimage, squashfs).
- **toolchain** - refers to the compiler, the c library, and common tools which will be used to build the firmware image. The result of this is two new directories, `toolchain_build_<arch>` which is a temporary directory used for building the toolchain for a specific architecture, and `staging_dir_<arch>` where the resulting toolchain is installed.
- **target** - refers to the embedded platform, this contains items which are specific to a specific embedded platform. Of particular interest here is the `target/linux` directory which is broken down by platform and contains the kernel config and patches to the kernel for a particular platform. There's also the `target/image` directory which describes how to package a firmware for a specific platform.
- **package** - is for exactly that - packages. In an OpenWrt firmware, almost everything is an ipk, a software package which can be added to the firmware to provide new features or removed to save space.
- **dl** - anything downloaded by the toolchain, target or package steps will be placed in this directory.

Both the `target` and `package` steps will use the directory `build_<arch>` as a temporary directory for compiling.

## Difference between build_dir and staging_dir
The directory `build_dir` is used to unpack all the source archives and to compile them in.

The directory `staging_dir` is used to “install” all the compiled programs into, ready either for use in building further packages, or for preparing the firmware image.

There are three areas under `build_dir`:
- `build_dir/host`, for compiling all the tools that run on the host computer (OpenWrt builds its own version of `sed` and many other tools from source). This area will be used for compiling programs that run only on your host.
- `build_dir/toolchain...` for compiling the cross-C compiler and C standard library components that will be used to build the packages. This area will be used for compiling programs that run only on your host (the cross C compiler, for example) and also, libraries designed to run on the target that are linked to - e.g. uClibc, libm, pthreads, etc.
- `build_dir/target...` for compiling the actual packages, and the Linux kernel, for the target system

Under staging, there are also three areas:
- `staging_dir/host` is a mini Linux root with its own `bin/`, `lib/`, etc. that the host tools are installed into; the rest of the build system then prefixes its PATH with directories in this area
- `staging_dir/toolchain...` is a mini Linux root with its own `bin/`, `lib/`, etc that contains the cross C compiler used to build the rest of the firmware. You can actually use that to compile simple C programs outside of OpenWrt that can be loaded onto the firmware. The C compiler might be something like: `staging_dir/toolchain-mips_34kc_gcc-4.8-linaro_uClibc-0.9.33.2/bin/mips-openwrt-linux-uclibc-gcc`. You can see the version of the CPU, the C library and gcc encoded into it; this allows multiple targets to be built in the same area concurrently.
- `staging_dir/target.../root-...` contains “installed” versions of each target package again arranged with `bin/`, `lib/`, this will become the actual root directory that with some tweaking will get zipped up into the firmware image, something like `root-ar71xx`. There are some other files in `staging_dir/target...` primarily used for generating the packages and development packages, etc.

## Make targets
- Offers a number of high level make targets for standard package workflows
- Targets always in the format `component/name/action`, e.g. `toolchain/gdb/compile` or `package/mtd/install`
- Prepare a package source tree: `package/foo/prepare`
- Compile a package: `package/foo/compile`
- Clean a package: `package/foo/clean`

## Build sequence
1. `tools` – automake, autoconf, sed, cmake
2. `toolchain/binutils` – as, ld, ...
3. `toolchain/gcc` – gcc, g++, cpp, ...
4. `target/linux` – kernel modules
5. `package` – core and feed packages
6. `target/linux` – kernel image
7. `target/linux/image` – firmware image file generation

## Patch management
- Many packages will not work as-is and need patches to work on the target or to even compile
- The build system integrates `quilt` for easy patch management
- Turn package patches into quilt series: `make package/foo/prepare QUILT=1`
- Update patches from modified series: `make package/foo/update`
- Automatically rebase patches after an update: `make package/foo/refresh`

## Build system setup
Modernized set for Ubuntu 24.04 that has Python 3.12 without python3-distutils:
```
sudo apt update
sudo apt install build-essential clang flex bison g++ gawk \
gcc-multilib g++-multilib gettext git libncurses5-dev libssl-dev \
python3-setuptools rsync swig unzip zlib1g-dev file wget
```

set for Ubuntu 22.04 (that has older Python 3.xx):
```
sudo apt update
sudo apt install build-essential clang flex bison g++ gawk \
gcc-multilib g++-multilib gettext git libncurses-dev libssl-dev \
python3-distutils rsync unzip zlib1g-dev file wget
```

## Build OpenWRT Image
### 1. Download and update the sources
```
git clone https://git.openwrt.org/openwrt/openwrt.git
cd openwrt
git pull
```
### 2. Select a specific code revision
```
git branch -a
git tag
git checkout v23.05.0
```
### 3. Update the feeds
```
./scripts/feeds update -a
./scripts/feeds install -a
```
### 4. Configure the firmware image
	make menuconfig
### 5. Optional: configure the kernel (usually not required)
	make -j$(nproc) kernel_menuconfig

### 6. Build the firmware image
	make -j$(nproc) defconfig download clean world
	(or)
	FORCE_UNSAFE_CONFIGURE=1 make -j$(nproc) V=sc defconfig download clean world

## Build X86_64 Image
#### 1. Configure X86-64 Build Environment
	$ make menuconfig
	Target System (x86)  --->  x86
	Subtarget (x86_64)  ---> x86_64
	Target Profile (Generic x86/64)  ---> Generic x86/64
#### 2. Enable ISO and VDI Targets
	Target Images  ---> Build LiveCD image (ISO)
	Target Images  ---> Build VirtualBox image files (VDI)
#### 3. Build Openwrt Image
	FORCE_UNSAFE_CONFIGURE=1 make -j$(nproc) V=sc defconfig download clean world
#### 4. Deploy Image for Virtualization
- Use `openwrt/bin/targets/x86/64/openwrt-x86-64-generic-image.iso` to create Virtualbox instance
- Use `openwrt/bin/targets/x86/64/openwrt-x86-64-generic-rootfs.tar.gz` to create Docker instance

## Run Openwrt in Docker Container
1. The Openwrt image has been built at the path<br>
	`openwrt/bin/targets/x86/64/openwrt-x86-64-generic-rootfs.tar.gz`
2. Import Docker Image<br>
	`$ docker import openwrt-x86-64-generic-rootfs.tar.gz openwrt`
3. Run Openwrt instance
```
$ docker run -it openwrt /sbin/init
$ docker run -it openwrt /bin/ash
$
$ docker run -i -t openwrt-x86-64 cat /etc/banner
  _______                     ________        __
 |       |.-----.-----.-----.|  |  |  |.----.|  |_
 |   -   ||  _  |  -__|     ||  |  |  ||   _||   _|
 |_______||   __|_____|__|__||________||__|  |____|
          |__| W I R E L E S S   F R E E D O M
 -----------------------------------------------------
 OpenWrt 23.05.0, r23497-6637af95aa
 -----------------------------------------------------
```
## Creating a local feed
1. Prepare your `<buildroot>` with git cloning openwrt sources from github (e.g. from your fork).
2. Create a dir: `mkdir -p <buildroot>/my_packages/<section>/<category>/<package_name>`.<br>
Replace the `<package_name>` with the name of your package.
e.g. `mkdir -p my_packages/net/network/rpcbind`.
The section and category can be found in the `Makefile`.
3. Write a Makefile or download one `Makefile` from another package, look at samples on github.<br>
Edit your Makefile and add necessary files, sources...<br>
More: [Creating packages](https://openwrt.org/docs/guide-developer/packages) & [Creating a package from your application](https://openwrt.org/docs/guide-developer/helloworld/chapter3)
4. Append a line with your custom feed to `feeds.conf.default`:<br>
`src-link my_packages <buildroot>/my_packages`<br>
Replace the `<buildroot>` with cloned openwrt sources directory e.g. `~/openwrt`<br>
Move the line with your custom feed above standard feeds to override them.
5. Now run: `./scripts/feeds update -a`; `./scripts/feeds install <package_name>`<br>
If you are doing this to resolve a dependency you can run `./scripts/feeds install <package_name>` one more time and you should notice the dependency has been resolved.
6. Build your package.<br>
Select it in the menu of `make menuconfig`<br>
Build it with `make package/my_package/{clean,compile}`
More: [Building a single package](https://openwrt.org/docs/guide-developer/toolchain/single.package)

### Weblinks
- [Home](https://openwrt.org/docs/guide-developer/start)
- [Helloworld for Openwrt](https://openwrt.org/docs/guide-developer/helloworld/start)
- [GNU Debugger](https://openwrt.org/docs/guide-developer/gdb)
