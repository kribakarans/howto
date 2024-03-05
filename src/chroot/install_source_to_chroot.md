# Install packages source to chroot environment

Install your package binaries to the chroot directory to test in isolated an environment. This guide has you install a minimal Ubuntu `focal` distribution in the chroot directory where you can install programs and run processes in an isolated space.

### Install dependencies
	sudo apt-get install debootstrap

### Create directory were to install chroot
	mkdir ./chroot

### Create chroot environment
	sudo debootstrap focal ./chroot/

### Mount required filesystems based on the requirements
	sudo mount --bind /sys  ./chroot/sys/
	sudo mount --bind /dev  ./chroot/dev/
	sudo mount --bind /proc ./chroot/proc/

### Do Make install the source to chroot
	make install DESTDIR=./chroot/

### Run your program in chroot environment
	sudo chroot ./chroot/ <user-program>

### Explore the chroot environment
	sudo chroot ./chroot/ bash

### Reference
<https://help.ubuntu.com/community/BasicChroot><br>
<https://www.linode.com/docs/guides/use-chroot-for-testing-on-ubuntu><br>
<https://askubuntu.com/questions/105840/install-program-from-source-to-chroot-env><br>
