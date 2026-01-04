# Optimize GNOME services for Low Resource Usage

## List Running Services

```bash
systemctl list-units --type=service --state=running
systemctl --user list-units --type=service --state=running
```

## Disable / Stop / Verify a Service

```bash
systemctl disable --now SERVICE
systemctl stop SERVICE
systemctl is-enabled SERVICE

systemctl --user disable --now SERVICE
systemctl --user mask SERVICE`
```

| Action  | Stops Now | Blocks Autostart | Blocks Manual Start | Blocks Dependency Start |
| ------- | --------- | ---------------- | ------------------- | ----------------------- |
| stop    | ✅        | ❌               | ❌                  | ❌                      |
| disable | ❌        | ✅               | ❌                  | ❌                      |
| mask    | ❌        | ✅               | ✅                  | ✅                      |

## Core Services (DO NOT TOUCH)

```bash
dbus
systemd-logind
NetworkManager
udev
polkit
at-spi-dbus-bus.service
gnome-session*
gnome-session-manager*
gsd-xsettings.service
gsd-keyboard.service
gsd-power.service
gvfs-*
xdg-desktop-portal*
ssh-agent.service
gnome-keyring.service Xorg
```

## GNOME Mail (Evolution)

```bash
systemctl --user mask evolution-calendar-factory.service
systemctl --user mask evolution-addressbook-factory.service

sudo apt purge -y evolution evolution-data-server
sudo apt autoremove --purge
```

## GNOME Sharing / Peripherals

```bash
systemctl --user mask gsd-sharing.service
systemctl --user mask gsd-smartcard.service
systemctl --user mask gsd-wacom.service
systemctl --user mask gsd-wwan.service
systemctl --user mask gsd-media-keys.service
```

## Remote Desktop (Disable GNOME Built-in)

```bash
gsettings set org.gnome.desktop.remote-desktop.rdp enable false
gsettings set org.gnome.desktop.remote-desktop.vnc enable false
```

## Disable GNOME Animations

```bash
gsettings set org.gnome.desktop.interface enable-animations false
```

## File / Network Discovery (Avahi)

```bash
sudo systemctl disable --now avahi-daemon.service
sudo systemctl mask avahi-daemon.service
systemctl --user mask unicast-local-avahi.service
systemctl --user mask unicast-local-avahi.path

sudo apt purge -y avahi-daemon avahi-utils
```

## Accessibility (Optional on Servers)

```bash
systemctl --user mask gsd-a11y-settings.service
```

## GNOME Online Accounts

```bash
systemctl --user mask goa-daemon.service

sudo apt purge -y gnome-online-accounts libgoa-1.0-0b
```

## Tracker (Search / Indexing) – **Critical**

```bash
tracker reset --hard

systemctl --user stop tracker-miner-fs.service
systemctl --user stop tracker-miner-rss.service
systemctl --user stop tracker-store.service
systemctl --user mask tracker-miner-fs.service
systemctl --user mask tracker-miner-rss.service
systemctl --user mask tracker-store.service
```

### GNOME Settings

```bash
gsettings set org.freedesktop.Tracker.Miner.Files enable-monitors false
gsettings set org.freedesktop.Tracker.Miner.Files crawling-interval -2
```

Optional Purge:

```bash
sudo apt purge -y tracker tracker-miner-fs tracker-extract
```

## Printing (CUPS)

```bash
sudo systemctl disable --now cups.service cups-browsed.service
systemctl --user mask gsd-print-notifications.service

sudo apt purge -y cups*
```

## Bluetooth

```bash
sudo systemctl disable --now bluetooth.service
sudo systemctl mask bluetooth.service

sudo apt purge -y bluez
```

## Camera / Media Sharing

```bash
sudo apt purge -y cheese cheese-common
```

## Location Services

```bash
gsettings set org.gnome.system.location enabled false

sudo systemctl disable --now geoclue.service
```

## Sound Servers (Headless Only)

```bash
systemctl --user mask pulseaudio.socket
systemctl --user mask pulseaudio.service
```

## Snapd (Optional but Saves RAM)

```bash
sudo systemctl disable --now snapd.service

sudo apt purge -y snapd
```

## Update Notifiers

```bash
systemctl --user mask update-notifier-crash.service
systemctl --user mask update-notifier-release.service
systemctl --user mask update-notifier-livepatch.service
```

## Validation

```bash
systemctl --failed systemctl --user --failed

free -h

ps -ef | wc -l
```

## One-Shot Script (Non-Destructive)

```bash
vi trim-gnome-services.sh

#!/usr/bin/env bash
#
# gnome-headless-harden.sh
#
# One-shot GNOME hardening for headless / VNC servers
# - Disables unnecessary GNOME + system services
# - Reduces memory usage
# - No apt purge / remove
# - Safe to re-run
#

set -e

log() { echo "INFO | $*"; }

log "Disabling GNOME animations"
gsettings set org.gnome.desktop.interface enable-animations false || true

log "Disabling GNOME remote desktop"
gsettings set org.gnome.desktop.remote-desktop.rdp enable false || true
gsettings set org.gnome.desktop.remote-desktop.vnc enable false || true

log "Disabling GNOME location services"
gsettings set org.gnome.system.location enabled false || true

log "Disabling Tracker indexing"
gsettings set org.freedesktop.Tracker.Miner.Files enable-monitors false || true
gsettings set org.freedesktop.Tracker.Miner.Files crawling-interval -2 || true

log "Stopping Tracker services"
systemctl --user stop tracker-miner-fs.service tracker-miner-rss.service tracker-store.service || true
systemctl --user mask tracker-miner-fs.service tracker-miner-rss.service tracker-store.service || true

log "Disabling GNOME sharing & peripherals"
systemctl --user mask \
  gsd-sharing.service \
  gsd-smartcard.service \
  gsd-wacom.service \
  gsd-wwan.service \
  gsd-media-keys.service || true

log "Disabling accessibility services"
systemctl --user mask gsd-a11y-settings.service || true

log "Disabling GNOME Online Accounts"
systemctl --user mask goa-daemon.service || true

log "Disabling print notifications"
systemctl --user mask gsd-print-notifications.service || true

log "Disabling user sound server (PulseAudio)"
systemctl --user mask pulseaudio.socket pulseaudio.service || true

log "Disabling system-wide services not needed on headless servers"

for svc in \
  bluetooth.service \
  cups.service \
  cups-browsed.service \
  avahi-daemon.service \
  geoclue.service \
  snapd.service
do
  systemctl disable --now "$svc" 2>/dev/null || true
done

log "Masking Avahi to prevent respawn"
systemctl mask avahi-daemon.service 2>/dev/null || true

#log "Disabling GNOME extensions (safe defaults)"
#for ext in \
#  ubuntu-dock@ubuntu.com \
#  ubuntu-appindicators@ubuntu.com \
#  desktop-icons@csoriano
#do
#  gnome-extensions disable "$ext" 2>/dev/null || true
#done

log "Hardening complete"
log "Re-login or restart VNC session for full effect"
```

---
