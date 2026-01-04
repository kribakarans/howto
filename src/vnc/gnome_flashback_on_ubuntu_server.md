# Gnome Flashback VNC on Ubuntu Server

## Install required packages

```bash
sudo apt install --no-install-recommends \
    tigervnc-standalone-server tigervnc-common dbus-x11 \
    gnome-session-flashback gnome-panel metacity
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

## (Optional) Installation System Utilities

```bash
sudo apt install --no-install-recommends \
    gnome-terminal nautilus gnome-settings-daemon gnome-system-monitor \
    yaru-theme-gtk yaru-theme-icon yaru-theme-sound ubuntu-wallpapers gnome-tweaks
```

## Gnome Panel Indicator Support

### Install indicator packages

```bash
sudo apt install \
  gnome-settings-daemon \
  indicator-application \
  indicator-datetime \
  indicator-power \
  indicator-session \
  indicator-sound
```

### Update VNC startup script

```bash
#!/bin/bash

unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS

export XDG_SESSION_TYPE=x11
export XDG_CURRENT_DESKTOP=GNOME-Flashback:GNOME
export DESKTOP_SESSION=gnome-flashback-metacity
export XDG_RUNTIME_DIR=/run/user/$(id -u)

mkdir -p "$XDG_RUNTIME_DIR"
chmod 700 "$XDG_RUNTIME_DIR"

# Start DBus
eval "$(dbus-launch --sh-syntax)"

# Start PulseAudio (REQUIRED for sound indicator)
pulseaudio --start --exit-idle-time=-1

# Start GNOME settings daemon (REQUIRED for most indicators)
gnome-settings-daemon &

# Start panel + flashback
gnome-session --session=gnome-flashback-metacity &

sleep 3

# Start ALL indicator services
for svc in \
    /usr/lib/x86_64-linux-gnu/indicator-*/indicator-*-service \
    /usr/lib/x86_64-linux-gnu/indicator-*-service
do
    [ -x "$svc" ] && "$svc" &
done

wait
```

Alternate script (indicator-sound omitted):

```bash
#!/bin/bash

unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS

export XDG_SESSION_TYPE=x11
export XDG_CURRENT_DESKTOP=GNOME-Flashback:GNOME
export DESKTOP_SESSION=gnome-flashback-metacity
export XDG_RUNTIME_DIR=/run/user/$(id -u)

mkdir -p "$XDG_RUNTIME_DIR"
chmod 700 "$XDG_RUNTIME_DIR"

# DBus for the session
eval "$(dbus-launch --sh-syntax)"

# GNOME Flashback (panel + WM)
gnome-session --session=gnome-flashback-metacity &

sleep 2

# Minimal indicator set
/usr/lib/x86_64-linux-gnu/indicator-network/indicator-network-service &
/usr/lib/x86_64-linux-gnu/indicator-power/indicator-power-service &
/usr/lib/x86_64-linux-gnu/indicator-datetime/indicator-datetime-service &
/usr/lib/x86_64-linux-gnu/indicator-session/indicator-session-service &

wait
```

## Restart VNC server

```bash
vncserver -kill :1 && vncserver :1 -localhost no -geometry 1368x768
```

---
