# Gnome Flashback VNC on Ubuntu Minimal Desktop

## Install required packages

```bash
sudo apt install --no-install-recommends \
    tigervnc-standalone-server tigervnc-common dbus-x11 \
    gnome-session-flashback gnome-panel metacity ubuntu-desktop-minimal
```

## Create or edit the VNC startup script

```bash
#!/bin/bash

unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS

export XDG_SESSION_TYPE=x11
export XDG_CURRENT_DESKTOP=GNOME-Flashback:GNOME # GNOME-Flashback:Unity

exec dbus-launch --exit-with-session \
    gnome-session --session=gnome-flashback-metacity

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
