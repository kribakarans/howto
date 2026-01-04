
# Ubuntu Desktop Tweaks

## Install **Yaru**, **Ubuntu fonts**, and GNOME utilities

```bash
sudo apt install -y \
  yaru-theme-gtk \
  yaru-theme-icon \
  humanity-icon-theme \
  yaru-theme-sound \
  yaru-theme-unity \
  ubuntu-font-family \
  gnome-tweaks \
  gnome-shell-extensions
```

## Verify Installed Fonts

```bash
fc-list | grep "Ubuntu Mono"
```

## Apply Theme Using GNOME Tweaks (GUI Method)

```bash
gnome-tweaks
```

| Setting      | Value    |
| ------------ | -------- |
| Applications | **Yaru** |
| Cursor       | **Yaru** |
| Icons        | **Yaru** |
| Shell        | **Yaru** |

## Enable GNOME Shell Theme Support

```bash
sudo apt install -y gnome-shell-extension-user-theme
```

Restart GNOME Shell:

- Press **Alt + F2**
- Type `r`
- Press Enter

Now reopen **GNOME Tweaks** → Appearance → Shell → **Yaru**

## Apply Theme Using CLI (Headless / VNC Friendly)

```bash
gsettings set org.gnome.desktop.interface gtk-theme 'Yaru'
gsettings set org.gnome.desktop.interface icon-theme 'Yaru'
gsettings set org.gnome.desktop.interface cursor-theme 'Yaru'
gsettings set org.gnome.desktop.interface font-name 'Ubuntu 11'
gsettings set org.gnome.desktop.interface monospace-font-name 'Ubuntu Mono 13'
```

### Prefer Dark mode

```bash
gsettings set org.gnome.desktop.interface color-scheme 'prefer-dark' (GTK4)
gsettings set org.gnome.desktop.wm.preferences theme 'Yaru-dark'
```

### Usage

```bash
gsettings set org.gnome.desktop.interface gtk-theme 'Yaru'
gsettings set org.gnome.desktop.interface icon-theme 'Yaru' # (Humanity|Yaru-dark)
gsettings set org.gnome.desktop.interface cursor-theme 'Yaru'
```

### Apply system-wide (optional)

If you want all users to default to Yaru:

**Add:**

sudo vi /etc/dconf/db/local.d/00-yaru

```bash
[org/gnome/desktop/interface]
gtk-theme='Yaru'
icon-theme='Yaru'
cursor-theme='Yaru'

[org/gnome/metacity]
theme='Yaru'
```

**Apply:**

```bash
sudo dconf update
```

**Logout and Login:**

```bash
gnome-session-quit --logout --no-prompt
```

## Set Ubuntu Mono for Terminal

1. Open Terminal → Preferences
2. Select Profile → Text
3. Enable **Custom font**
4. Choose: Ubuntu Mono Regular Size: 12–14

## File Manager & System UI Polish

Ensure Nautilus follows Yaru:

```bash
gsettings set org.gnome.nautilus.preferences default-folder-viewer 'list-view'
gsettings set org.gnome.nautilus.preferences show-hidden-files true
```

## Managing GNOME Extensions

```bash
gnome-extensions list                           # List extensions
gnome-extensions info ubuntu-dock@ubuntu.com    # Check status
gnome-extensions enable ubuntu-dock@ubuntu.com  # Enable
gnome-extensions disable desktop-icons@csoriano # Disable
apt purge gnome-shell-extension-desktop-icons   # Remove
```

Manage via GUI (Optional)

```bash
sudo apt install -y gnome-shell-extension-manager
```

## Troubleshooting

### Fonts not updating?

```bash
fc-cache -rv
```

### Reset themes to defaults

```bash
gsettings reset-recursively org.gnome.desktop.interface
```

---
