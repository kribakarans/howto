# Setup Ubuntu desktop environments

### [Ubuntu Minimal](https://askubuntu.com/questions/42964/installing-ubuntu-desktop-without-all-the-bloat)

	sudo apt-get install --no-install-recommends ubuntu-desktop-minimal

### Gnome Vannila Minimal

	sudo apt-get install --no-install-recommends xorg gdm3     # Gnome display manager
	sudo apt-get install --no-install-recommends xorg lightdm  # Light display manager

### [i3 desktop](https://medium.com/hacker-toolbelt/install-and-use-i3wm-da167b0348b4)

	sudo apt-get install --no-install-recommends xdm xorg i3      # X11 display manager
	sudo apt-get install --no-install-recommends ligntdm xorg i3  # Light display manager
	sudo systemctl enable lightdm

## Install Virtualbox Guest Additions

	sudo mkdir /media/cdrom             # Create mount point
	sudo mount /dev/cdrom /media/cdrom  # Mount CDrom
	cd /media/cdrom
	sudo ./VBoxLinuxAdditions.run       # Install Addon
	sudo reboot
	sudo usermod -aG vboxsf -- "$USER"  # Add user to vbosf group
	cat /etc/group | grep "$USER"       # Validate user group

More on [Window Managers for X](http://xwinman.org/blackbox.php)
