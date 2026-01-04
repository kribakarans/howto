# Openbox VNC on Ubuntu Server

## Install required packages

```bash
sudo apt install --no-install-recommends tigervnc-standalone-server openbox tint2 xterm dbus-x11
```

## Create VNC startup script

```bash
#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS

# Load X resources
[ -r "$HOME/.Xresources" ] && xrdb "$HOME/.Xresources"

# Panel
tint2 &

# Start Openbox session
exec openbox-session

wait
```

## Make the script executable

```bash
chmod +x ~/.vnc/xstartup
```

## (Re)Start VNC server

```bash
vncserver -kill :1 && vncserver :1 -localhost no -geometry 1368x768
```

## Install additional applications

```bash
sudo apt install --no-install-recommends midori nautilus gnome-panel
```

---
