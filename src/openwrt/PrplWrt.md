# [PrplWrt](https://prplfoundation.org/project/prplwrt/)

PrplWrt/PrplOS is an open-source, enterprise-grade software framework designed to power the next generation of WiFi routers and gateways.

# [PrplOS Development Environment](https://gitlab.com/soft.at.home/docker/oss-dbg)

#### Create your debug and development container

```
docker pull registry.gitlab.com/soft.at.home/docker/oss-dbg:latest
docker run -ti -d --name oss-dbg --restart always --cap-add=SYS_PTRACE --sysctl net.ipv6.conf.all.disable_ipv6=1 -e "USER=$USER" -e "UID=$(id -u)" -e "GID=$(id -g)"  registry.gitlab.com/soft.at.home/docker/oss-dbg:latest
```
#### Open a terminal to your container

`docker exec -ti oss-dbg /bin/bash`

#### Configure your development container

This is the last step to make the container you have created usable.
##### Gitlab configuration

The container should have access to Gitlab. You could share the private/public keys from your host system, but this is not recommended. It is better to create a new pair of keys.

Make sure that you are not "root" in the container (use "su" to change to your user id)

```
ssh-keygen -N "" -t rsa -b 2048 -C "<YOUR EMAIL HERE>" -f ~/.ssh/id_rsa
```
##### Git configuration

In the container (terminal/console) configure some git global settings. Let git know who you are:
```
git config --global user.email "<YOUR EMAIL HERE>"
git config --global user.name "<YOUR FULL NAME HERE>"
```
### Ambiorix repository

Now that the docker container is created and running it is time to fetch some sources from Gitlab. This is an example for the ambiorix project.

As the Ambiorix project has many sub-projects (libraries, examples, applications, ...) a google repo config is available, which will make it easier to work with them.

#### Fetch the Gitlab repositories

Make sure that you have a terminal open to the "oss-dbg" container and that you switch the user to your user id.

```
mkdir ~/projectdir/ambiorix
cd ~/projectdir/ambiorix
repo init -u git@gitlab.com:prpl-foundation/components/ambiorix/ambiorix.git
repo sync
repo forall -c "git checkout master"
```
#### Building and installing

All components of the Ambiorix project compile out of source tree.

That is all intermediate files (`*.o`, `*.d`, `*.gcdna`, ....) are not put next to the source, but in a separate directory.

This directory is called "output". An extra sub-directory is created for each compile target (machine). This makes it possible to compile the sources with different toolchains.

By default there is only one toolchain installed "x86_64-linux-gnu". Unless you install a different toolchain and set the correct environment variables, all intermediate files and the compilation artifacts are put in the directory "./output/x86_64_linux-gnu".

To make development more comfortable, the `debug & development` container contains some [local commands](https://gitlab.com/soft.at.home/docker/oss-dbg/-/blob/main/resources/usr/local/bin/local_commands.sh).

You can simply build all ambiorix components by executing:
```
amx_rebuild_all
```
##### Ambiorix Libraries

The libraries must be compiled and installed in a specific order. Some of them depend on other libraries. You can find a dependency graph in the [`getting started`](https://gitlab.com/prpl-foundation/components/ambiorix/tutorials/getting-started/-/blob/main/README.md#manual) tutorial.

You can manually install a library by executing the following commands:
```
make
sudo -E make install
```
Or use the predefined command to install all of them at once:
```
amx_rebuild_libs
```
##### Bus back-ends

The order of building and installing the backends is not of importance.<br>
You can manually install a backend by executing:
```
make
sudo -E make install
```
Or use the predefined command to install all of them at once:
```
amx_rebuild_bus_backends
```
##### Applications

You can manually install an application by executing:
```
make
sudo -E make install
```
Or use the predefined command to install all of them at once:
```
amx_rebuild_apps
```
##### Examples

You can manually install an example by executing:
```
make
sudo -E make install
```
Or use the predefined command to install all of them at once:
```
amx_rebuild_examples
```
#### Testing

Most of the Ambiorix Gitlab repo's contain (unit) tests. Currently the applications do not have tests available.<br>
When changing code it is recommended that you:

1. run the existing tests
2. add tests to test your changes

Be aware that whenever you need to change existing tests, you probably broke backwards compatibility.
##### Run tests

To run a test for a specific Gitlab repo, all you need to do is cd in that repo and run the tests.

##### Example:
```
cd ~/projectdir/ambiorix/libraries/libamxc
make test
```
You could run all tests for all libraries at once - just be sure that you already compiled all libraries and installed them.
```
cd ~/projectdir/ambiorix
repo forall libraries/* -c "make test"
```
##### Open coverage reports

When tests have been run, test code coverage reports are generated. These reports are available in the output directory (default = ./output/x86_64_linux-gnu/coverage/report).

These reports are in HTML format. If the output directory is on the shared filesystem with the host system, you can directly open the reports on the host system:
```
cd ~/ambiorix/libraries/libamxc/output/x86_64-linux-gnu/coverage/report/
xdg-open index.html
```
If the output directory is not on the shared filesystem, you can run a HTTP server in the container:
```
cd ~/projectdir
python3 -m http.server 8080
```
You could open a separate terminal to the container and run the HTTP server in that terminal or run the HTTP server in background and redirect all output to "/dev/null".<br>
When the HTTP server is started you can access the coverage reports using your browser on the host system.<br>
The url is typically (unless you use different names):
```
http://172.17.0.2:8080/ambiorix/libraries/libamxc/output/x86_64-linux-gnu/coverage/report/
```
The IPv4 address is the IPv4 address of your container.

#### Debugging

Any application or test suite can be debugged using gdb or - if you prefer a graphical user interface frontend for gdb - gdbgui.

gdb documentation is available at: [https://www.gnu.org/software/gdb/documentation/](https://www.gnu.org/software/gdb/documentation/)

More information about gdbgui is available at: [https://www.gdbgui.com/](https://www.gdbgui.com/)

##### Example:

Debugging a test case using gdbgui.

All you need to do is build the test suite, for this example let's debug the test suite "amxo_include" from libamxo (the odl parser).

First make sure you can build and run the tests of libamxo:
```
cd ~/projectdir/ambiorix/libraries/libamxo
make test
```
Change the directory to the test directory and start the test using gdbgui:
```
cd tests/amxo_include/
gdbgui -r ./run_test
```
As a response you should see some output of gdbgui:
```
Opening gdbgui with default browser at http://127.0.0.1:5000
exit gdbgui by pressing CTRL+C
```
Now open a browser (or a new tab) and open the uri "[http://127.0.0.1:5000](http://127.0.0.1:5000)"<br>
Now you should see the gdbgui user interface in your browser, and you can start debugging.


# Build PrplOS Image

### [PrplOS source code](https://gitlab.com/prpl-foundation/prplos/prplos)

`git clone https://gitlab.com/prpl-foundation/prplos/prplos.git`

### Build system setup

Modernized set for Ubuntu 24.04 that has Python 3.12 without python3-distutils:
```
sudo apt update
sudo apt install build-essential clang flex bison g++ gawk \
gcc-multilib g++-multilib gettext git libelf-dev libncurses5-dev libssl-dev \
python3-setuptools rsync swig unzip zlib1g-dev file wget
```
### Add the Prpl Feed to OpenWrt

For more details, visit [here](https://gitlab.com/prpl-foundation/prplos/feeds/feed-prpl).
```
echo "src-git feed_prpl https://gitlab.com/prpl-foundation/prplOS/feed-prpl.git" >> feeds.conf.default
```
### Update the feeds
```
./scripts/feeds update  -a
./scripts/feeds install -a
```
### Configure the Target
```
make menuconfig
```
- To build X86_64 Image:

		Target System (x86)  --->  x86
		Subtarget (x86_64)  ---> x86_64
		Target Profile (Generic x86/64)  ---> Generic x86/64

- Enable Ambiorix Components

		Prpl Foundation  ---> Ambiorix/Libraries/Netmodel/...

### Build the Firmware

`FORCE_UNSAFE_CONFIGURE=1 make -j$(nproc) V=sc`

### Final Image for Virtualization

- Use `openwrt/bin/targets/x86/64/openwrt-x86-64-generic-image.iso` to create Virtualbox instance
- Use `openwrt/bin/targets/x86/64/openwrt-x86-64-generic-rootfs.tar.gz` to create Docker instance

# Run PrplOS in Docker Container

### 1. The PrplOS (prplwrt/openwrt) image has been built at the path

	openwrt/bin/targets/x86/64/openwrt-x86-64-generic-rootfs.tar.gz

### 2. Import Docker Image

	docker import openwrt-x86-64-generic-rootfs.tar.gz prplwrt

### 3. Run PrplOS Container
```
$ docker run -it prplwrt /sbin/init
$ docker run -it prplwrt /bin/ash
$
$ docker run -it prplwrt cat /etc/banner
                   _  ___  ____
  _ __  _ __ _ __ | |/ _ \/ ___|
 | '_ \| '__| '_ \| | | | \___ \
 | |_) | |  | |_) | | |_| |___) |
 | .__/|_|  | .__/|_|\___/|____/
 |_|        |_| based on OpenWrt
 --------------------------------
      OpenWrt 3.0.0-ec4a2136
 --------------------------------
```
