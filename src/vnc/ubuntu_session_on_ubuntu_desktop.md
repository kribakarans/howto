# Ubuntu VNC Session on Ubuntu Minimal Desktop

## Install required packages

```bash
sudo apt install --no-install-recommends \
    tigervnc-standalone-server tigervnc-common dbus-x11 \
    ubuntu-desktop-minimal
```

## Optionally install other packages

```bash
sudo apt install --no-install-recommends \
    yaru-theme-gtk yaru-theme-icon yaru-theme-sound gnome-tweaks
```

## Create or edit the VNC startup script

```bash
#!/bin/sh

unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS

export XDG_SESSION_TYPE=x11
export XDG_CURRENT_DESKTOP=ubuntu:GNOME

# Load X resources (optional but harmless)
[ -f "$HOME/.Xresources" ] && xrdb "$HOME/.Xresources"

exec dbus-launch --exit-with-session gnome-session --session=ubuntu

wait
```

Make the script executable:

```bash
chmod +x ~/.vnc/xstartup
```

## (Re)Start VNC server

```bash
vncserver -kill :1 && vncserver :1 -localhost no -geometry 1368x768
```

---
