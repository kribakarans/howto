# XFCE4 VNC on Ubuntu Server

## Install required packages

```bash
sudo apt install --no-install-recommends tigervnc-standalone-server tigervnc-common xfce4 xfce4-goodies
```

## Create VNC startup script

```bash
#!/bin/bash

# Set environment
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS

export XDG_SESSION_TYPE=x11
export XDG_CURRENT_DESKTOP=XFCE

# Start XFCE session
exec dbus-launch --exit-with-session startxfce4 &

# Keep script running
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

---
