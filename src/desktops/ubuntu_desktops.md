# Ubuntu Desktop Variants

Headless/LightDM-Gnome-Flashback/GDM3-Gnome-Flashback/OpenBox/Ubuntu-Minimal-Desktop

## 1. Ubuntu Server Headless

```bash
atom@virtualbox:~$ cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.6 LTS"

atom@virtualbox:~$ uname -a
Linux virtualbox 5.4.0-216-generic #236-Ubuntu SMP Fri Apr 11 19:53:21 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux
```

### Disk Size

```bash
atom@virtualbox:~$ df -h /
Filesystem                         Size  Used Avail Use% Mounted on
/dev/mapper/ubuntu--vg-ubuntu--lv   15G  5.4G  8.5G  39% /
```

### PS-Tree

```bash
atom@virtualbox:~$ pstree
systemd─┬─ModemManager───2*[{ModemManager}]
        ├─accounts-daemon───2*[{accounts-daemon}]
        ├─agetty
        ├─atd
        ├─cron
        ├─dbus-daemon
        ├─irqbalance───{irqbalance}
        ├─login───bash───htop
        ├─multipathd───6*[{multipathd}]
        ├─networkd-dispat
        ├─polkitd───2*[{polkitd}]
        ├─rsyslogd───3*[{rsyslogd}]
        ├─snapd───8*[{snapd}]
        ├─sshd───sshd───sshd───bash───pstree
        ├─systemd───(sd-pam)
        ├─systemd-journal
        ├─systemd-logind
        ├─systemd-network
        ├─systemd-resolve
        ├─systemd-timesyn───{systemd-timesyn}
        ├─systemd-udevd───15*[systemd-udevd]
        ├─udisksd───4*[{udisksd}]
        └─unattended-upgr───{unattended-upgr}
```

### PS-ELF

```bash
atom@virtualbox:~$ ps -eo pid,ppid,args
    PID    PPID COMMAND
      1       0 /sbin/init maybe-ubiquity
      2       0 [kthreadd]
      3       2 [rcu_gp]
      4       2 [rcu_par_gp]
      5       2 [kworker/0:0-events]
      6       2 [kworker/0:0H-kblockd]
      7       2 [kworker/u4:0-events_unbound]
      8       2 [mm_percpu_wq]
      9       2 [ksoftirqd/0]
     10       2 [rcu_sched]
     11       2 [migration/0]
     12       2 [idle_inject/0]
     14       2 [cpuhp/0]
     15       2 [cpuhp/1]
     16       2 [idle_inject/1]
     17       2 [migration/1]
     18       2 [ksoftirqd/1]
     20       2 [kworker/1:0H-kblockd]
     21       2 [kdevtmpfs]
     22       2 [netns]
     23       2 [rcu_tasks_kthre]
     24       2 [kauditd]
     25       2 [khungtaskd]
     26       2 [oom_reaper]
     27       2 [writeback]
     28       2 [kcompactd0]
     29       2 [ksmd]
     30       2 [khugepaged]
     77       2 [kintegrityd]
     78       2 [kblockd]
     79       2 [blkcg_punt_bio]
     80       2 [tpm_dev_wq]
     81       2 [ata_sff]
     82       2 [md]
     83       2 [edac-poller]
     84       2 [devfreq_wq]
     85       2 [watchdogd]
     86       2 [kworker/u4:1-flush-253:0]
     88       2 [kswapd0]
     89       2 [ecryptfs-kthrea]
     91       2 [kthrotld]
     92       2 [acpi_thermal_pm]
     93       2 [scsi_eh_0]
     94       2 [scsi_tmf_0]
     95       2 [scsi_eh_1]
     96       2 [scsi_tmf_1]
     97       2 [kworker/u4:2-events_unbound]
     98       2 [vfio-irqfd-clea]
    100       2 [ipv6_addrconf]
    109       2 [kstrp]
    112       2 [kworker/u5:0]
    114       2 [kworker/1:1H-kblockd]
    126       2 [charger_manager]
    127       2 [kworker/0:2-events]
    167       2 [scsi_eh_2]
    169       2 [scsi_tmf_2]
    170       2 [irq/18-vmwgfx]
    171       2 [ttm_swap]
    172       2 [cryptd]
    192       2 [kworker/0:1H-kblockd]
    220       2 [kdmflush]
    246       2 [raid5wq]
    293       2 [jbd2/dm-0-8]
    294       2 [ext4-rsv-conver]
    364       1 /lib/systemd/systemd-journald
    396       2 [kworker/1:5-events]
    401       2 [kworker/1:6-mm_percpu_wq]
    402       1 /lib/systemd/systemd-udevd
    419       2 [iprt-VBoxWQueue]
    559       2 [kaluad]
    560       2 [kmpath_rdacd]
    561       2 [kmpathd]
    562       2 [kmpath_handlerd]
    563       1 /sbin/multipathd -d -s
    575       2 [loop0]
    579       2 [loop1]
    580       2 [loop2]
    583       2 [loop3]
    585       2 [loop4]
    586       2 [loop5]
    589       2 [jbd2/sda2-8]
    590       2 [ext4-rsv-conver]
    606       1 /lib/systemd/systemd-timesyncd
    655       1 /lib/systemd/systemd-networkd
    657       1 /lib/systemd/systemd-resolved
    669       1 /usr/lib/accountsservice/accounts-daemon
    672       1 /usr/sbin/cron -f
    673       1 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
    679       1 /usr/sbin/irqbalance --foreground
    680       1 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
    682       1 /usr/lib/policykit-1/polkitd --no-debug
    683       1 /usr/sbin/rsyslogd -n -iNONE
    688       1 /usr/lib/snapd/snapd
    690       1 /lib/systemd/systemd-logind
    692       1 /usr/lib/udisks2/udisksd
    696       1 /usr/sbin/atd -f
    736       1 /usr/sbin/ModemManager
    750       1 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
    762       1 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
    912       2 [kworker/0:4-events]
   1160       1 /lib/systemd/systemd --user
   1161    1160 (sd-pam)
   1187     750 sshd: atom [priv]
   1265    1187 sshd: atom@pts/0
   1266    1265 -bash
   1314       1 /sbin/agetty -o -p -- \u --noclear tty6 linux
   1447       1 /sbin/agetty -o -p -- \u --noclear tty1 linux
   1463       2 [kworker/1:0]
   1464       2 [kworker/0:1-events]
   1468    1266 ps -eo pid,ppid,args
```

### Free-H

```bash
atom@virtualbox:~$ free -h
              total        used        free      shared  buff/cache   available
Mem:          1.9Gi       163Mi       1.4Gi       1.0Mi       413Mi       1.6Gi
Swap:         2.0Gi          0B       2.0Gi
```

### Snaps

![image_1_1](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_1_1.png)

---

## 2. LightDM + GNOME Flashback

### Install X-Server, DM and WM

```bash
sudo apt install -y gnome-session-flashback metacity gnome-panel xorg lightdm

$ ls /usr/share/xsessions/
gnome-flashback-compiz.desktop  gnome-flashback-metacity.desktop
```

### Configure LightDM

Ensure a LightDM greeter is available; otherwise install LightDM GTK, Unity, or Slick Greeter.

```bash
# GTK (simple, lightweight)
sudo apt install -y lightdm-gtk-greeter

# Unity (Ubuntu-style)
sudo apt install -y unity-greeter
ls /usr/share/xsessions/

# Slick (modern, Mint-style)
sudo apt install -y slick-greeter
```

```bash
$ ls /usr/share/xgreeters/
unity-greeter.desktop
```

Add the following configuration to `/etc/lightdm/lightdm.conf` to enable the LightDM greeter and start a **GNOME Flashback** session by default.

```bash
sudo sh -c 'echo "[Seat:*]\ngreeter-session=unity-greeter\nuser-session=gnome-flashback-metacity" >> /etc/lightdm/lightdm.conf'
```

```bash
$ cat /etc/lightdm/lightdm.conf
[Seat:*]
greeter-session=unity-greeter # lightdm-gtk-greeter/slick-greeter
user-session=gnome-flashback-metacity
```

> **Set Run level to graphical:**
>
>```bash
> sudo systemctl set-default graphical.target
>```
>
> Logout GUI session:
> `gnome-session-quit --logout --no-prompt`

### Enable/Restart LightDM

```bash
sudo systemctl enable lightdm
```

(or)

```bash
atom@virtualbox:~$ sudo systemctl restart lightdm

atom@virtualbox:~$ sudo systemctl status lightdm
● lightdm.service - Light Display Manager
     Loaded: loaded (/lib/systemd/system/lightdm.service; indirect; vendor preset: enabled)
     Active: active (running) since Sat 2026-01-03 21:05:35 IST; 5s ago
       Docs: man:lightdm(1)
    Process: 3375 ExecStartPre=/bin/sh -c [ "$(basename $(cat /etc/X11/default-display-manager 2>/dev/null))" = "lightdm" ] (code=exi>
   Main PID: 3379 (lightdm)
      Tasks: 7 (limit: 2250)
     Memory: 18.7M
     CGroup: /system.slice/lightdm.service
             ├─3379 /usr/sbin/lightdm
             ├─3386 /usr/lib/xorg/Xorg -core :0 -seat seat0 -auth /var/run/lightdm/root/:0 -nolisten tcp vt7 -novtswitch
             └─3520 lightdm --session-child 12 19

Jan 03 21:05:35 virtualbox systemd[1]: Starting Light Display Manager...
Jan 03 21:05:35 virtualbox systemd[1]: Started Light Display Manager.
Jan 03 21:05:36 virtualbox lightdm[3400]: pam_unix(lightdm-greeter:session): session opened for user lightdm by (uid=0)
Jan 03 21:05:36 virtualbox lightdm[3400]: gkr-pam: gnome-keyring-daemon started properly
Jan 03 21:05:36 virtualbox lightdm[3520]: pam_succeed_if(lightdm:auth): requirement "user ingroup nopasswdlogin" not met by user "ato>
```

> **Ref:***
>
>```bash
> atom@virtualbox:~$ ls /etc/xdg/autostart/
>
> at-spi-dbus-bus.desktop                  org.gnome.Evolution-alarm-notify.desktop             org.gnome.SettingsDaemon.Smartcard.desktop
> geoclue-demo-agent.desktop               org.gnome.SettingsDaemon.A11ySettings.desktop        org.gnome.SettingsDaemon.Sound.desktop
> gnome-flashback-clipboard.desktop        org.gnome.SettingsDaemon.Color.desktop               org.gnome.SettingsDaemon.UsbProtection.desktop
> gnome-flashback-nm-applet.desktop        org.gnome.SettingsDaemon.Datetime.desktop            org.gnome.SettingsDaemon.Wacom.desktop
> gnome-keyring-pkcs11.desktop             org.gnome.SettingsDaemon.Housekeeping.desktop        org.gnome.SettingsDaemon.Wwan.desktop
> gnome-keyring-secrets.desktop            org.gnome.SettingsDaemon.Keyboard.desktop            org.gnome.SettingsDaemon.XSettings.desktop
> gnome-keyring-ssh.desktop                org.gnome.SettingsDaemon.MediaKeys.desktop           print-applet.desktop
> gnome-shell-overrides-migration.desktop  org.gnome.SettingsDaemon.Power.desktop               pulseaudio.desktop
> im-launch.desktop                        org.gnome.SettingsDaemon.PrintNotifications.desktop  snap-userd-autostart.desktop
> indicator-application.desktop            org.gnome.SettingsDaemon.Rfkill.desktop              xdg-user-dirs.desktop
> indicator-messages.desktop               org.gnome.SettingsDaemon.ScreensaverProxy.desktop
> nm-applet.desktop                        org.gnome.SettingsDaemon.Sharing.desktop
>```
>

### Disk Size

```bash
atom@virtualbox:~$ df -h /
Filesystem                         Size  Used Avail Use% Mounted on
/dev/mapper/ubuntu--vg-ubuntu--lv   15G  6.2G  7.8G  44% /
```

### PS-Tree

```bash
atom@virtualbox:~$ pstree
systemd─┬─ModemManager───2*[{ModemManager}]
        ├─NetworkManager───2*[{NetworkManager}]
        ├─accounts-daemon───2*[{accounts-daemon}]
        ├─agetty
        ├─atd
        ├─avahi-daemon───avahi-daemon
        ├─colord───2*[{colord}]
        ├─cron
        ├─cups-browsed───2*[{cups-browsed}]
        ├─cupsd
        ├─dbus-daemon
        ├─gnome-keyring-d───3*[{gnome-keyring-d}]
        ├─irqbalance───{irqbalance}
        ├─lightdm─┬─Xorg───{Xorg}
        │         ├─lightdm─┬─gnome-session-b─┬─ssh-agent
        │         │         │                 └─2*[{gnome-session-b}]
        │         │         └─2*[{lightdm}]
        │         └─2*[{lightdm}]
        ├─multipathd───6*[{multipathd}]
        ├─networkd-dispat
        ├─polkitd───2*[{polkitd}]
        ├─rsyslogd───3*[{rsyslogd}]
        ├─rtkit-daemon───2*[{rtkit-daemon}]
        ├─snapd───8*[{snapd}]
        ├─sshd───sshd───sshd───bash───pstree
        ├─systemd─┬─(sd-pam)
        │         ├─at-spi-bus-laun─┬─dbus-daemon
        │         │                 └─3*[{at-spi-bus-laun}]
        │         ├─at-spi2-registr───2*[{at-spi2-registr}]
        │         ├─dbus-daemon
        │         ├─dconf-service───2*[{dconf-service}]
        │         ├─evolution-addre───5*[{evolution-addre}]
        │         ├─evolution-calen───8*[{evolution-calen}]
        │         ├─evolution-sourc───3*[{evolution-sourc}]
        │         ├─gnome-flashback─┬─ibus-daemon─┬─ibus-engine-sim───2*[{ibus-engine-sim}]
        │         │                 │             ├─ibus-extension-───3*[{ibus-extension-}]
        │         │                 │             ├─ibus-memconf───2*[{ibus-memconf}]
        │         │                 │             └─2*[{ibus-daemon}]
        │         │                 └─3*[{gnome-flashback}]
        │         ├─gnome-session-b─┬─evolution-alarm───5*[{evolution-alarm}]
        │         │                 ├─gnome-flashback───2*[{gnome-flashback}]
        │         │                 ├─gnome-panel─┬─gnome-control-c───8*[{gnome-control-c}]
        │         │                 │             ├─gnome-system-mo───3*[{gnome-system-mo}]
        │         │                 │             └─3*[{gnome-panel}]
        │         │                 ├─metacity───3*[{metacity}]
        │         │                 ├─nm-applet───3*[{nm-applet}]
        │         │                 └─3*[{gnome-session-b}]
        │         ├─gnome-session-c───{gnome-session-c}
        │         ├─goa-daemon───3*[{goa-daemon}]
        │         ├─goa-identity-se───2*[{goa-identity-se}]
        │         ├─gsd-a11y-settin───3*[{gsd-a11y-settin}]
        │         ├─gsd-color───3*[{gsd-color}]
        │         ├─gsd-datetime───3*[{gsd-datetime}]
        │         ├─gsd-housekeepin───3*[{gsd-housekeepin}]
        │         ├─gsd-keyboard───3*[{gsd-keyboard}]
        │         ├─gsd-media-keys───3*[{gsd-media-keys}]
        │         ├─gsd-power───3*[{gsd-power}]
        │         ├─gsd-print-notif───2*[{gsd-print-notif}]
        │         ├─gsd-printer───2*[{gsd-printer}]
        │         ├─gsd-rfkill───2*[{gsd-rfkill}]
        │         ├─gsd-screensaver───2*[{gsd-screensaver}]
        │         ├─gsd-sharing───3*[{gsd-sharing}]
        │         ├─gsd-smartcard───4*[{gsd-smartcard}]
        │         ├─gsd-sound───3*[{gsd-sound}]
        │         ├─gsd-usb-protect───3*[{gsd-usb-protect}]
        │         ├─gsd-wacom───2*[{gsd-wacom}]
        │         ├─gsd-wwan───3*[{gsd-wwan}]
        │         ├─gsd-xsettings───3*[{gsd-xsettings}]
        │         ├─gvfs-afc-volume───3*[{gvfs-afc-volume}]
        │         ├─gvfs-goa-volume───2*[{gvfs-goa-volume}]
        │         ├─gvfs-gphoto2-vo───2*[{gvfs-gphoto2-vo}]
        │         ├─gvfs-mtp-volume───2*[{gvfs-mtp-volume}]
        │         ├─gvfs-udisks2-vo───3*[{gvfs-udisks2-vo}]
        │         ├─gvfsd─┬─gvfsd-trash───2*[{gvfsd-trash}]
        │         │       └─2*[{gvfsd}]
        │         ├─gvfsd-metadata───2*[{gvfsd-metadata}]
        │         ├─ibus-portal───2*[{ibus-portal}]
        │         ├─ibus-x11───2*[{ibus-x11}]
        │         ├─indicator-appli───2*[{indicator-appli}]
        │         ├─indicator-bluet───3*[{indicator-bluet}]
        │         ├─indicator-datet───5*[{indicator-datet}]
        │         ├─indicator-keybo───3*[{indicator-keybo}]
        │         ├─indicator-messa───3*[{indicator-messa}]
        │         ├─indicator-power───3*[{indicator-power}]
        │         ├─indicator-print───2*[{indicator-print}]
        │         ├─indicator-sessi───3*[{indicator-sessi}]
        │         ├─indicator-sound───3*[{indicator-sound}]
        │         └─pulseaudio───3*[{pulseaudio}]
        ├─systemd-journal
        ├─systemd-logind
        ├─systemd-network
        ├─systemd-resolve
        ├─systemd-timesyn───{systemd-timesyn}
        ├─systemd-udevd
        ├─udisksd───4*[{udisksd}]
        ├─unattended-upgr───{unattended-upgr}
        ├─upowerd───2*[{upowerd}]
        └─wpa_supplicant
```

### PS-ELF

```bash
atom@virtualbox:~$ ps -eo pid,ppid,args
    PID    PPID COMMAND
      1       0 /sbin/init maybe-ubiquity
      2       0 [kthreadd]
      3       2 [rcu_gp]
      4       2 [rcu_par_gp]
      5       2 [kworker/0:0-events]
      6       2 [kworker/0:0H-kblockd]
      7       2 [kworker/u4:0-events_unbound]
      8       2 [mm_percpu_wq]
      9       2 [ksoftirqd/0]
     10       2 [rcu_sched]
     11       2 [migration/0]
     12       2 [idle_inject/0]
     14       2 [cpuhp/0]
     15       2 [cpuhp/1]
     16       2 [idle_inject/1]
     17       2 [migration/1]
     18       2 [ksoftirqd/1]
     20       2 [kworker/1:0H-kblockd]
     21       2 [kdevtmpfs]
     22       2 [netns]
     23       2 [rcu_tasks_kthre]
     24       2 [kauditd]
     25       2 [khungtaskd]
     26       2 [oom_reaper]
     27       2 [writeback]
     28       2 [kcompactd0]
     29       2 [ksmd]
     30       2 [khugepaged]
     35       2 [kworker/1:1-cgroup_destroy]
     77       2 [kintegrityd]
     78       2 [kblockd]
     79       2 [blkcg_punt_bio]
     80       2 [tpm_dev_wq]
     81       2 [ata_sff]
     82       2 [md]
     83       2 [edac-poller]
     84       2 [devfreq_wq]
     85       2 [watchdogd]
     86       2 [kworker/u4:1-scsi_tmf_1]
     88       2 [kswapd0]
     89       2 [ecryptfs-kthrea]
     91       2 [kthrotld]
     92       2 [acpi_thermal_pm]
     93       2 [scsi_eh_0]
     94       2 [scsi_tmf_0]
     95       2 [scsi_eh_1]
     96       2 [scsi_tmf_1]
     97       2 [kworker/u4:2-events_unbound]
     98       2 [vfio-irqfd-clea]
    100       2 [ipv6_addrconf]
    109       2 [kstrp]
    112       2 [kworker/u5:0]
    117       2 [kworker/1:1H-kblockd]
    126       2 [charger_manager]
    127       2 [kworker/0:2-events]
    159       2 [kworker/1:2-events]
    167       2 [scsi_eh_2]
    168       2 [cryptd]
    169       2 [scsi_tmf_2]
    171       2 [irq/18-vmwgfx]
    174       2 [ttm_swap]
    191       2 [kworker/0:1H-kblockd]
    219       2 [kdmflush]
    245       2 [raid5wq]
    290       2 [jbd2/dm-0-8]
    291       2 [ext4-rsv-conver]
    363       1 /lib/systemd/systemd-journald
    393       2 [kworker/1:3-events]
    401       1 /lib/systemd/systemd-udevd
    402       2 [kworker/0:3-events]
    426       2 [iprt-VBoxWQueue]
    572       2 [kaluad]
    573       2 [kmpath_rdacd]
    574       2 [kmpathd]
    575       2 [kmpath_handlerd]
    576       1 /sbin/multipathd -d -s
    586       2 [loop0]
    593       2 [loop1]
    595       2 [loop2]
    596       2 [loop3]
    597       2 [loop4]
    598       2 [loop5]
    600       2 [jbd2/sda2-8]
    601       2 [ext4-rsv-conver]
    622       1 /lib/systemd/systemd-timesyncd
    668       1 /lib/systemd/systemd-networkd
    670       1 /lib/systemd/systemd-resolved
    681       1 /usr/lib/accountsservice/accounts-daemon
    682       1 avahi-daemon: running [virtualbox.local]
    683       1 /usr/sbin/cupsd -l
    684       1 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
    687       1 /usr/sbin/NetworkManager --no-daemon
    691       1 /usr/sbin/irqbalance --foreground
    692       1 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
    693       1 /usr/lib/policykit-1/polkitd --no-debug
    695       1 /usr/sbin/rsyslogd -n -iNONE
    700       1 /usr/lib/snapd/snapd
    701       1 /lib/systemd/systemd-logind
    702       1 /usr/lib/udisks2/udisksd
    703       1 /sbin/wpa_supplicant -u -s -O /run/wpa_supplicant
    710     682 avahi-daemon: chroot helper
    734       1 /usr/sbin/cups-browsed
    746       1 /usr/sbin/ModemManager
    762       1 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
    777       1 /usr/sbin/cron -f
    782       1 /usr/sbin/atd -f
    792       1 /sbin/agetty -o -p -- \u --noclear tty1 linux
    800       1 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
    860       1 /usr/libexec/rtkit-daemon
   1000       1 /usr/lib/upower/upowerd
   1070       1 /usr/libexec/colord
   1113     800 sshd: atom [priv]
   1116       1 /lib/systemd/systemd --user
   1117    1116 (sd-pam)
   1122    1116 /usr/bin/pulseaudio --daemonize=no --log-target=journal
   1143    1116 /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
   1243    1113 sshd: atom@pts/0
   1244    1243 -bash
   1321       1 /usr/sbin/lightdm
   1327    1321 /usr/lib/xorg/Xorg -core :0 -seat seat0 -auth /var/run/lightdm/root/:0 -nolisten tcp vt7 -novtswitch
   1369    1321 lightdm --session-child 12 19
   1398       1 /usr/bin/gnome-keyring-daemon --daemonize --login
   1401    1369 /usr/libexec/gnome-session-binary --systemd --systemd --session=gnome-flashback-metacity --disable-acceleration-check
   1465    1401 /usr/bin/ssh-agent /usr/bin/im-launch /usr/lib/gnome-flashback/gnome-flashback-metacity
   1485    1116 /usr/libexec/gnome-session-ctl --monitor
   1486    1116 /usr/lib/x86_64-linux-gnu/indicator-application/indicator-application-service
   1487    1116 /usr/lib/x86_64-linux-gnu/indicator-bluetooth/indicator-bluetooth-service
   1488    1116 /usr/lib/x86_64-linux-gnu/indicator-datetime/indicator-datetime-service
   1489    1116 /usr/lib/x86_64-linux-gnu/indicator-keyboard/indicator-keyboard-service --use-gtk
   1490    1116 /usr/lib/x86_64-linux-gnu/indicator-messages/indicator-messages-service
   1491    1116 /usr/lib/x86_64-linux-gnu/indicator-power/indicator-power-service
   1492    1116 /usr/lib/x86_64-linux-gnu/indicator-printers/indicator-printers-service
   1493    1116 /usr/lib/x86_64-linux-gnu/indicator-session/indicator-session-service
   1494    1116 /usr/lib/x86_64-linux-gnu/indicator-sound/indicator-sound-service
   1544    1116 /usr/libexec/at-spi-bus-launcher
   1549    1544 /usr/bin/dbus-daemon --config-file=/usr/share/defaults/at-spi2/accessibility.conf --nofork --print-address 3
   1555    1116 /usr/libexec/gvfsd
   1567    1116 /usr/libexec/evolution-source-registry
   1572    1116 /usr/libexec/dconf-service
   1576    1116 /usr/libexec/at-spi2-registryd --use-gnome-session
   1585    1116 /usr/libexec/goa-daemon
   1586    1116 /usr/libexec/gnome-session-binary --systemd-service --session=gnome-flashback-metacity
   1595    1116 /usr/libexec/evolution-calendar-factory
   1608    1116 /usr/libexec/goa-identity-service
   1619    1586 /usr/lib/gnome-flashback/gnome-flashback-clipboard
   1620    1116 /usr/bin/gnome-flashback
   1632    1116 /usr/libexec/evolution-addressbook-factory
   1647    1116 /usr/libexec/gvfsd-metadata
   1667    1116 /usr/libexec/gvfs-udisks2-volume-monitor
   1672    1116 /usr/libexec/gvfs-goa-volume-monitor
   1676    1116 /usr/libexec/gvfs-mtp-volume-monitor
   1680    1116 /usr/libexec/gvfs-gphoto2-volume-monitor
   1684    1116 /usr/libexec/gvfs-afc-volume-monitor
   1692    1620 ibus-daemon --xim --panel disable
   1696    1692 /usr/libexec/ibus-memconf
   1697    1692 /usr/libexec/ibus-extension-gtk3
   1701    1116 /usr/libexec/ibus-x11 --kill-daemon
   1707    1116 /usr/libexec/ibus-portal
   1713    1116 /usr/libexec/gsd-a11y-settings
   1715    1116 /usr/libexec/gsd-color
   1716    1116 /usr/libexec/gsd-datetime
   1717    1116 /usr/libexec/gsd-housekeeping
   1718    1116 /usr/libexec/gsd-keyboard
   1719    1116 /usr/libexec/gsd-media-keys
   1720    1116 /usr/libexec/gsd-power
   1721    1116 /usr/libexec/gsd-print-notifications
   1725    1116 /usr/libexec/gsd-rfkill
   1728    1692 /usr/libexec/ibus-engine-simple
   1731    1116 /usr/libexec/gsd-screensaver-proxy
   1733    1116 /usr/libexec/gsd-sharing
   1736    1116 /usr/libexec/gsd-smartcard
   1737    1116 /usr/libexec/gsd-sound
   1742    1586 metacity
   1743    1116 /usr/libexec/gsd-usb-protection
   1746    1116 /usr/libexec/gsd-wacom
   1755    1116 /usr/libexec/gsd-wwan
   1762    1116 /usr/libexec/gsd-xsettings
   1788    1116 /usr/libexec/gsd-printer
   1834    1586 gnome-panel
   1887    1586 nm-applet
   1896    1586 /usr/libexec/evolution-data-server/evolution-alarm-notify
   1906    1555 /usr/libexec/gvfsd-trash --spawner :1.22 /org/gtk/gvfs/exec_spaw/0
   1944    1834 gnome-system-monitor
   1976    1834 gnome-control-center
   2024       2 [kworker/0:1]
   2025    1244 ps -eo pid,ppid,args
```

### Free-H

```bash
atom@virtualbox:~$ free -h
              total        used        free      shared  buff/cache   available
Mem:          1.9Gi       545Mi       790Mi       1.0Mi       635Mi       1.2Gi
Swap:         2.0Gi          0B       2.0Gi
```

### Snaps

#### Login Screen

![image_2_1](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_2_1.png)

#### Desktop Overview

![image_2_2](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_2_2.png)

#### System Monitor

![image_2_3](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_2_3.png)

---

## 3. GDM3  + GNOME Flashback

### Install X-Server and WM

```bash
sudo apt install -y gnome-session-flashback metacity gnome-panel xorg
```

```bash
atom@virtualbox:~$ ls -l /usr/share/xsessions/
total 8
-rw-r--r-- 1 root root 270 Dec  8  2020 gnome-flashback-compiz.desktop
-rw-r--r-- 1 root root 278 Dec  8  2020 gnome-flashback-metacity.desktop
```

### Install DM

```bash
sudo apt install -y --no-install-recommends gdm3
```

> `--no-install-recommends` option prevents pulling Ubuntu desktop

```bash
atom@virtualbox:~$ ls -l /etc/gdm3/
total 44
-rw-r--r-- 1 root root  996 Jul 12  2021 config-error-dialog.sh
-rw-r--r-- 1 root root  554 Jul 12  2021 custom.conf
-rw-r--r-- 1 root root 1474 Nov 10  2020 greeter.dconf-defaults
drwxr-xr-x 2 root root 4096 Jan  4 06:15 Init
drwxr-xr-x 2 root root 4096 Jan  4 06:15 PostLogin
drwxr-xr-x 2 root root 4096 Jan  4 06:15 PostSession
drwxr-xr-x 2 root root 4096 Jan  4 06:15 PreSession
drwxr-xr-x 2 root root 4096 Jan  4 06:15 Prime
drwxr-xr-x 2 root root 4096 Jan  4 06:15 PrimeOff
-rwxr-xr-x 1 root root 6463 Jul 12  2021 Xsession
```

### Reboot VM

### Disk Size

```bash
atom@virtualbox:~$ df -h /
Filesystem                         Size  Used Avail Use% Mounted on
/dev/mapper/ubuntu--vg-ubuntu--lv   15G  6.2G  7.8G  45% /
```

### PS-Tree

```bash
atom@virtualbox:~$ pstree
systemd─┬─ModemManager───2*[{ModemManager}]
        ├─NetworkManager───2*[{NetworkManager}]
        ├─accounts-daemon───2*[{accounts-daemon}]
        ├─at-spi-bus-laun─┬─dbus-daemon
        │                 └─3*[{at-spi-bus-laun}]
        ├─at-spi2-registr───2*[{at-spi2-registr}]
        ├─atd
        ├─avahi-daemon───avahi-daemon
        ├─colord───2*[{colord}]
        ├─cron
        ├─cups-browsed───2*[{cups-browsed}]
        ├─cupsd
        ├─dbus-daemon
        ├─dconf-service───2*[{dconf-service}]
        ├─gdm3─┬─gdm-session-wor─┬─gdm-x-session─┬─Xorg───{Xorg}
        │      │                 │               ├─dbus-run-sessio─┬─dbus-daemon
        │      │                 │               │                 └─gnome-session-b─┬─gnome-shell─┬─ibus-daemon─┬─ibus-engine-sim───2*[{ibus-engine-sim}]
        │      │                 │               │                                   │             │             ├─ibus-memconf───2*[{ibus-memconf}]
        │      │                 │               │                                   │             │             └─2*[{ibus-daemon}]
        │      │                 │               │                                   │             └─10*[{gnome-shell}]
        │      │                 │               │                                   ├─gsd-a11y-settin───3*[{gsd-a11y-settin}]
        │      │                 │               │                                   ├─gsd-color───3*[{gsd-color}]
        │      │                 │               │                                   ├─gsd-datetime───3*[{gsd-datetime}]
        │      │                 │               │                                   ├─gsd-housekeepin───3*[{gsd-housekeepin}]
        │      │                 │               │                                   ├─gsd-keyboard───3*[{gsd-keyboard}]
        │      │                 │               │                                   ├─gsd-media-keys───3*[{gsd-media-keys}]
        │      │                 │               │                                   ├─gsd-power───3*[{gsd-power}]
        │      │                 │               │                                   ├─gsd-print-notif───2*[{gsd-print-notif}]
        │      │                 │               │                                   ├─gsd-rfkill───2*[{gsd-rfkill}]
        │      │                 │               │                                   ├─gsd-screensaver───2*[{gsd-screensaver}]
        │      │                 │               │                                   ├─gsd-sharing───3*[{gsd-sharing}]
        │      │                 │               │                                   ├─gsd-smartcard───4*[{gsd-smartcard}]
        │      │                 │               │                                   ├─gsd-sound───3*[{gsd-sound}]
        │      │                 │               │                                   ├─gsd-wacom───2*[{gsd-wacom}]
        │      │                 │               │                                   └─3*[{gnome-session-b}]
        │      │                 │               └─2*[{gdm-x-session}]
        │      │                 └─2*[{gdm-session-wor}]
        │      ├─gdm-session-wor─┬─gdm-x-session─┬─Xorg───{Xorg}
        │      │                 │               ├─gnome-session-b───2*[{gnome-session-b}]
        │      │                 │               └─2*[{gdm-x-session}]
        │      │                 └─2*[{gdm-session-wor}]
        │      └─2*[{gdm3}]
        ├─gjs───4*[{gjs}]
        ├─gnome-keyring-d───3*[{gnome-keyring-d}]
        ├─gsd-printer───2*[{gsd-printer}]
        ├─ibus-portal───2*[{ibus-portal}]
        ├─ibus-x11───2*[{ibus-x11}]
        ├─irqbalance───{irqbalance}
        ├─multipathd───6*[{multipathd}]
        ├─networkd-dispat
        ├─polkitd───2*[{polkitd}]
        ├─rsyslogd───3*[{rsyslogd}]
        ├─rtkit-daemon───2*[{rtkit-daemon}]
        ├─snapd───8*[{snapd}]
        ├─sshd───sshd───sshd───bash─┬─htop
        │                           └─pstree
        ├─systemd─┬─(sd-pam)
        │         ├─dbus-daemon
        │         └─pulseaudio───3*[{pulseaudio}]
        ├─systemd─┬─(sd-pam)
        │         ├─at-spi-bus-laun─┬─dbus-daemon
        │         │                 └─3*[{at-spi-bus-laun}]
        │         ├─at-spi2-registr───2*[{at-spi2-registr}]
        │         ├─dbus-daemon
        │         ├─dconf-service───2*[{dconf-service}]
        │         ├─evolution-addre───5*[{evolution-addre}]
        │         ├─evolution-calen───8*[{evolution-calen}]
        │         ├─evolution-sourc───3*[{evolution-sourc}]
        │         ├─gnome-flashback─┬─ibus-daemon─┬─ibus-engine-sim───2*[{ibus-engine-sim}]
        │         │                 │             ├─ibus-extension-───3*[{ibus-extension-}]
        │         │                 │             ├─ibus-memconf───2*[{ibus-memconf}]
        │         │                 │             └─2*[{ibus-daemon}]
        │         │                 └─3*[{gnome-flashback}]
        │         ├─gnome-session-b─┬─evolution-alarm───5*[{evolution-alarm}]
        │         │                 ├─gnome-flashback───2*[{gnome-flashback}]
        │         │                 ├─gnome-panel─┬─xterm───htop
        │         │                 │             └─3*[{gnome-panel}]
        │         │                 ├─metacity───3*[{metacity}]
        │         │                 ├─nm-applet───3*[{nm-applet}]
        │         │                 └─3*[{gnome-session-b}]
        │         ├─gnome-session-c───{gnome-session-c}
        │         ├─goa-daemon───3*[{goa-daemon}]
        │         ├─goa-identity-se───2*[{goa-identity-se}]
        │         ├─gsd-a11y-settin───3*[{gsd-a11y-settin}]
        │         ├─gsd-color───3*[{gsd-color}]
        │         ├─gsd-datetime───3*[{gsd-datetime}]
        │         ├─gsd-housekeepin───3*[{gsd-housekeepin}]
        │         ├─gsd-keyboard───3*[{gsd-keyboard}]
        │         ├─gsd-media-keys───3*[{gsd-media-keys}]
        │         ├─gsd-power───3*[{gsd-power}]
        │         ├─gsd-print-notif───2*[{gsd-print-notif}]
        │         ├─gsd-printer───2*[{gsd-printer}]
        │         ├─gsd-rfkill───2*[{gsd-rfkill}]
        │         ├─gsd-screensaver───2*[{gsd-screensaver}]
        │         ├─gsd-sharing───3*[{gsd-sharing}]
        │         ├─gsd-smartcard───4*[{gsd-smartcard}]
        │         ├─gsd-sound───3*[{gsd-sound}]
        │         ├─gsd-usb-protect───3*[{gsd-usb-protect}]
        │         ├─gsd-wacom───2*[{gsd-wacom}]
        │         ├─gsd-wwan───3*[{gsd-wwan}]
        │         ├─gsd-xsettings───3*[{gsd-xsettings}]
        │         ├─gvfs-afc-volume───3*[{gvfs-afc-volume}]
        │         ├─gvfs-goa-volume───2*[{gvfs-goa-volume}]
        │         ├─gvfs-gphoto2-vo───2*[{gvfs-gphoto2-vo}]
        │         ├─gvfs-mtp-volume───2*[{gvfs-mtp-volume}]
        │         ├─gvfs-udisks2-vo───3*[{gvfs-udisks2-vo}]
        │         ├─gvfsd─┬─gvfsd-trash───2*[{gvfsd-trash}]
        │         │       └─2*[{gvfsd}]
        │         ├─ibus-portal───2*[{ibus-portal}]
        │         ├─ibus-x11───2*[{ibus-x11}]
        │         ├─indicator-appli───2*[{indicator-appli}]
        │         ├─indicator-bluet───3*[{indicator-bluet}]
        │         ├─indicator-datet───5*[{indicator-datet}]
        │         ├─indicator-keybo───3*[{indicator-keybo}]
        │         ├─indicator-messa───3*[{indicator-messa}]
        │         ├─indicator-power───3*[{indicator-power}]
        │         ├─indicator-print───2*[{indicator-print}]
        │         ├─indicator-sessi───3*[{indicator-sessi}]
        │         ├─indicator-sound───3*[{indicator-sound}]
        │         └─pulseaudio───3*[{pulseaudio}]
        ├─systemd-journal
        ├─systemd-logind
        ├─systemd-network
        ├─systemd-resolve
        ├─systemd-timesyn───{systemd-timesyn}
        ├─systemd-udevd
        ├─udisksd───4*[{udisksd}]
        ├─unattended-upgr───{unattended-upgr}
        ├─upowerd───2*[{upowerd}]
        └─wpa_supplicant
```

### PS-ELF

```bash
atom@virtualbox:~$ ps -eo pid,ppid,args
    PID    PPID COMMAND
      1       0 /sbin/init maybe-ubiquity
      2       0 [kthreadd]
      3       2 [rcu_gp]
      4       2 [rcu_par_gp]
      6       2 [kworker/0:0H-kblockd]
      8       2 [mm_percpu_wq]
      9       2 [ksoftirqd/0]
     10       2 [rcu_sched]
     11       2 [migration/0]
     12       2 [idle_inject/0]
     14       2 [cpuhp/0]
     15       2 [cpuhp/1]
     16       2 [idle_inject/1]
     17       2 [migration/1]
     18       2 [ksoftirqd/1]
     20       2 [kworker/1:0H-kblockd]
     21       2 [kdevtmpfs]
     22       2 [netns]
     23       2 [rcu_tasks_kthre]
     24       2 [kauditd]
     25       2 [khungtaskd]
     26       2 [oom_reaper]
     27       2 [writeback]
     28       2 [kcompactd0]
     29       2 [ksmd]
     30       2 [khugepaged]
     35       2 [kworker/1:1-events]
     77       2 [kintegrityd]
     78       2 [kblockd]
     79       2 [blkcg_punt_bio]
     80       2 [tpm_dev_wq]
     81       2 [ata_sff]
     82       2 [md]
     83       2 [edac-poller]
     84       2 [devfreq_wq]
     85       2 [watchdogd]
     86       2 [kworker/u4:1-events_unbound]
     88       2 [kswapd0]
     89       2 [ecryptfs-kthrea]
     91       2 [kthrotld]
     92       2 [acpi_thermal_pm]
     93       2 [scsi_eh_0]
     94       2 [scsi_tmf_0]
     95       2 [scsi_eh_1]
     96       2 [scsi_tmf_1]
     98       2 [vfio-irqfd-clea]
     99       2 [kworker/u4:3-events_unbound]
    100       2 [kworker/1:1H-kblockd]
    101       2 [ipv6_addrconf]
    110       2 [kstrp]
    113       2 [kworker/u5:0]
    126       2 [charger_manager]
    166       2 [scsi_eh_2]
    167       2 [scsi_tmf_2]
    169       2 [cryptd]
    189       2 [kworker/0:1H-kblockd]
    211       2 [irq/18-vmwgfx]
    212       2 [ttm_swap]
    220       2 [kdmflush]
    246       2 [raid5wq]
    290       2 [jbd2/dm-0-8]
    291       2 [ext4-rsv-conver]
    364       1 /lib/systemd/systemd-journald
    403       2 [kworker/1:4-events]
    404       1 /lib/systemd/systemd-udevd
    425       2 [iprt-VBoxWQueue]
    571       2 [kaluad]
    572       2 [kmpath_rdacd]
    573       2 [kmpathd]
    574       2 [kmpath_handlerd]
    575       1 /sbin/multipathd -d -s
    585       2 [loop0]
    590       2 [loop1]
    594       2 [loop2]
    596       2 [loop3]
    597       2 [jbd2/sda2-8]
    598       2 [loop4]
    599       2 [ext4-rsv-conver]
    600       2 [kworker/0:3-events]
    601       2 [loop5]
    620       1 /lib/systemd/systemd-timesyncd
    669       1 /lib/systemd/systemd-networkd
    671       1 /lib/systemd/systemd-resolved
    682       1 /usr/lib/accountsservice/accounts-daemon
    683       1 avahi-daemon: running [virtualbox.local]
    684       1 /usr/sbin/cupsd -l
    685       1 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
    688       1 /usr/sbin/NetworkManager --no-daemon
    692       1 /usr/sbin/irqbalance --foreground
    693       1 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
    694       1 /usr/lib/policykit-1/polkitd --no-debug
    698       1 /usr/sbin/rsyslogd -n -iNONE
    700       1 /usr/lib/snapd/snapd
    701       1 /lib/systemd/systemd-logind
    706       1 /usr/lib/udisks2/udisksd
    707       1 /sbin/wpa_supplicant -u -s -O /run/wpa_supplicant
    716     683 avahi-daemon: chroot helper
    734       1 /usr/sbin/cups-browsed
    737       1 /usr/sbin/ModemManager
    764       1 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
    777       1 /usr/sbin/cron -f
    780       1 /usr/sbin/atd -f
    793       1 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
    797       1 /usr/sbin/gdm3
    806     797 gdm-session-worker [pam/gdm-launch-environment]
    819       1 /lib/systemd/systemd --user
    820     819 (sd-pam)
    828     819 /usr/bin/pulseaudio --daemonize=no --log-target=journal
    830     806 /usr/lib/gdm3/gdm-x-session --register-session dbus-run-session -- gnome-session --autostart /usr/share/gdm/greeter/autostart
    832     830 /usr/lib/xorg/Xorg vt1 -displayfd 3 -auth /run/user/122/gdm/Xauthority -background none -noreset -keeptty -verbose 3
    833       1 /usr/libexec/rtkit-daemon
    836     819 /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
    858     830 dbus-run-session -- gnome-session --autostart /usr/share/gdm/greeter/autostart
    859     858 dbus-daemon --nofork --print-address 4 --session
    860     858 /usr/libexec/gnome-session-binary --systemd --autostart /usr/share/gdm/greeter/autostart
    867       1 /usr/libexec/at-spi-bus-launcher
    872     867 /usr/bin/dbus-daemon --config-file=/usr/share/defaults/at-spi2/accessibility.conf --nofork --print-address 3
    914       1 /usr/libexec/dconf-service
    917     860 /usr/bin/gnome-shell
   1031     917 ibus-daemon --panel disable --xim
   1034    1031 /usr/libexec/ibus-memconf
   1038       1 /usr/libexec/ibus-x11 --kill-daemon
   1041       1 /usr/libexec/ibus-portal
   1048       1 /usr/libexec/at-spi2-registryd --use-gnome-session
   1078       1 /usr/lib/upower/upowerd
   1088       1 /usr/bin/gjs /usr/share/gnome-shell/org.gnome.Shell.Notifications
   1108     860 /usr/libexec/gsd-color
   1109     860 /usr/libexec/gsd-print-notifications
   1112     860 /usr/libexec/gsd-a11y-settings
   1114     860 /usr/libexec/gsd-power
   1115     860 /usr/libexec/gsd-media-keys
   1117     860 /usr/libexec/gsd-rfkill
   1118     860 /usr/libexec/gsd-keyboard
   1121     860 /usr/libexec/gsd-wacom
   1123     860 /usr/libexec/gsd-housekeeping
   1129     860 /usr/libexec/gsd-sound
   1133     860 /usr/libexec/gsd-datetime
   1134    1031 /usr/libexec/ibus-engine-simple
   1138     860 /usr/libexec/gsd-smartcard
   1147     860 /usr/libexec/gsd-screensaver-proxy
   1149     860 /usr/libexec/gsd-sharing
   1183       1 /usr/libexec/gsd-printer
   1184       1 /usr/libexec/colord
   1252       1 /lib/systemd/systemd --user
   1253    1252 (sd-pam)
   1916       2 [kworker/0:4-events]
   2452     793 sshd: atom [priv]
   2586    2452 sshd: atom@pts/0
   2587    2586 -bash
   3200    1252 /usr/bin/pulseaudio --daemonize=no --log-target=journal
   3211    1252 /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
   3285       2 [kworker/1:0-cgroup_destroy]
   3382     797 gdm-session-worker [pam/gdm-password]
   3402       1 /usr/bin/gnome-keyring-daemon --daemonize --login
   3406    3382 /usr/lib/gdm3/gdm-x-session --register-session --run-script /usr/lib/gnome-flashback/gnome-flashback-metacity
   3408    3406 /usr/lib/xorg/Xorg vt2 -displayfd 3 -auth /run/user/1001/gdm/Xauthority -background none -noreset -keeptty -verbose 3
   3416    3406 /usr/libexec/gnome-session-binary --systemd --systemd --session=gnome-flashback-metacity --disable-acceleration-check
   3479    1252 /usr/libexec/gnome-session-ctl --monitor
   3480    1252 /usr/lib/x86_64-linux-gnu/indicator-application/indicator-application-service
   3481    1252 /usr/lib/x86_64-linux-gnu/indicator-bluetooth/indicator-bluetooth-service
   3482    1252 /usr/lib/x86_64-linux-gnu/indicator-datetime/indicator-datetime-service
   3483    1252 /usr/lib/x86_64-linux-gnu/indicator-keyboard/indicator-keyboard-service --use-gtk
   3484    1252 /usr/lib/x86_64-linux-gnu/indicator-messages/indicator-messages-service
   3487    1252 /usr/lib/x86_64-linux-gnu/indicator-power/indicator-power-service
   3488    1252 /usr/lib/x86_64-linux-gnu/indicator-printers/indicator-printers-service
   3496    1252 /usr/lib/x86_64-linux-gnu/indicator-session/indicator-session-service
   3497    1252 /usr/lib/x86_64-linux-gnu/indicator-sound/indicator-sound-service
   3525    1252 /usr/libexec/gnome-session-binary --systemd-service --session=gnome-flashback-metacity
   3547    1252 /usr/libexec/evolution-source-registry
   3552    1252 /usr/libexec/gvfsd
   3561    1252 /usr/libexec/at-spi-bus-launcher
   3572    3561 /usr/bin/dbus-daemon --config-file=/usr/share/defaults/at-spi2/accessibility.conf --nofork --print-address 3
   3576    1252 /usr/libexec/goa-daemon
   3578    1252 /usr/bin/gnome-flashback
   3583    3525 /usr/lib/gnome-flashback/gnome-flashback-clipboard
   3591    1252 /usr/libexec/evolution-calendar-factory
   3602    1252 /usr/libexec/at-spi2-registryd --use-gnome-session
   3622    1252 /usr/libexec/goa-identity-service
   3623    1252 /usr/libexec/evolution-addressbook-factory
   3625    1252 /usr/libexec/dconf-service
   3650    1252 /usr/libexec/gvfs-udisks2-volume-monitor
   3658    1252 /usr/libexec/gvfs-goa-volume-monitor
   3662    1252 /usr/libexec/gvfs-mtp-volume-monitor
   3666    1252 /usr/libexec/gvfs-gphoto2-volume-monitor
   3670    1252 /usr/libexec/gvfs-afc-volume-monitor
   3676    3578 ibus-daemon --xim --panel disable
   3680    3676 /usr/libexec/ibus-memconf
   3681    3676 /usr/libexec/ibus-extension-gtk3
   3685    1252 /usr/libexec/ibus-x11 --kill-daemon
   3689    1252 /usr/libexec/ibus-portal
   3700    1252 /usr/libexec/gsd-a11y-settings
   3701    1252 /usr/libexec/gsd-color
   3702    1252 /usr/libexec/gsd-datetime
   3704    1252 /usr/libexec/gsd-housekeeping
   3705    1252 /usr/libexec/gsd-keyboard
   3706    1252 /usr/libexec/gsd-media-keys
   3707    1252 /usr/libexec/gsd-power
   3709    3525 metacity
   3710    1252 /usr/libexec/gsd-print-notifications
   3713    1252 /usr/libexec/gsd-rfkill
   3714    1252 /usr/libexec/gsd-screensaver-proxy
   3719    1252 /usr/libexec/gsd-sharing
   3720    1252 /usr/libexec/gsd-smartcard
   3725    1252 /usr/libexec/gsd-sound
   3726    1252 /usr/libexec/gsd-usb-protection
   3734       2 [kworker/0:0-events]
   3736    1252 /usr/libexec/gsd-wacom
   3742    1252 /usr/libexec/gsd-wwan
   3743    1252 /usr/libexec/gsd-xsettings
   3771    1252 /usr/libexec/gsd-printer
   3777    3676 /usr/libexec/ibus-engine-simple
   3831    3525 gnome-panel
   3837    3552 /usr/libexec/gvfsd-trash --spawner :1.28 /org/gtk/gvfs/exec_spaw/0
   3862    3525 nm-applet
   3869    3525 /usr/libexec/evolution-data-server/evolution-alarm-notify
   3899    3831 xterm -e htop
   3901    3899 htop
   3908       2 [kworker/u4:0-events_unbound]
   3923       2 [kworker/0:1-events]
   3926       2 [kworker/0:2-events]
   3927       2 [kworker/0:5-cgroup_destroy]
   3945    2587 htop
   3949    2587 ps -eo pid,ppid,args
```

### Free-H

```bash
atom@virtualbox:~$ free -h
              total        used        free      shared  buff/cache   available
Mem:          1.9Gi       689Mi       628Mi       5.0Mi       653Mi       1.1Gi
Swap:         2.0Gi          0B       2.0Gi
```

### Snaps

#### Login Screen

![image_3_1](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_3_1.png)

#### Desktop Overview

![image_3_2](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_3_2.png)

#### System Monitor

![image_3_3](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_3_3.png)

---

## 4. GDM3  + Ubuntu Session

### Install X-Server, DM and WM

```bash
  sudo apt install -y gnome-session-flashback metacity gnome-panel xorg gdm3
```

```bash
atom@virtualbox:~$ ls -l /usr/share/xsessions/
total 12
-rw-r--r-- 1 root root 270 Dec  8  2020 gnome-flashback-compiz.desktop
-rw-r--r-- 1 root root 278 Dec  8  2020 gnome-flashback-metacity.desktop
-rw-r--r-- 1 root root 303 Mar 26  2020 ubuntu.desktop
```

### Disk Size

```bash
atom@virtualbox:~$ df -h /
Filesystem                         Size  Used Avail Use% Mounted on
/dev/mapper/ubuntu--vg-ubuntu--lv   15G  6.2G  7.8G  45% /
```

### PS-Tree

```bash
atom@virtualbox:~$ pstree
systemd─┬─ModemManager───2*[{ModemManager}]
        ├─NetworkManager───2*[{NetworkManager}]
        ├─accounts-daemon───2*[{accounts-daemon}]
        ├─atd
        ├─atop
        ├─atopacctd
        ├─avahi-daemon───avahi-daemon
        ├─colord───2*[{colord}]
        ├─cron
        ├─cups-browsed───2*[{cups-browsed}]
        ├─cupsd
        ├─dbus-daemon
        ├─gdm3─┬─gdm-session-wor─┬─gdm-x-session─┬─Xorg───{Xorg}
        │      │                 │               ├─gnome-session-b─┬─ssh-agent
        │      │                 │               │                 └─2*[{gnome-session-b}]
        │      │                 │               └─2*[{gdm-x-session}]
        │      │                 └─2*[{gdm-session-wor}]
        │      └─2*[{gdm3}]
        ├─glances
        ├─gnome-keyring-d───3*[{gnome-keyring-d}]
        ├─irqbalance───{irqbalance}
        ├─multipathd───6*[{multipathd}]
        ├─networkd-dispat
        ├─packagekitd───2*[{packagekitd}]
        ├─polkitd───2*[{polkitd}]
        ├─rsyslogd───3*[{rsyslogd}]
        ├─rtkit-daemon───2*[{rtkit-daemon}]
        ├─snapd───8*[{snapd}]
        ├─sshd───sshd───sshd───bash─┬─htop
        │                           └─pstree
        ├─switcheroo-cont───2*[{switcheroo-cont}]
        ├─systemd─┬─(sd-pam)
        │         ├─at-spi-bus-laun─┬─dbus-daemon
        │         │                 └─3*[{at-spi-bus-laun}]
        │         ├─at-spi2-registr───2*[{at-spi2-registr}]
        │         ├─dbus-daemon
        │         ├─dconf-service───2*[{dconf-service}]
        │         ├─evolution-addre───5*[{evolution-addre}]
        │         ├─evolution-calen───8*[{evolution-calen}]
        │         ├─evolution-sourc───3*[{evolution-sourc}]
        │         ├─gjs───4*[{gjs}]
        │         ├─gnome-session-b─┬─evolution-alarm───5*[{evolution-alarm}]
        │         │                 ├─indicator-messa───3*[{indicator-messa}]
        │         │                 └─3*[{gnome-session-b}]
        │         ├─gnome-session-c───{gnome-session-c}
        │         ├─gnome-shell─┬─gnome-system-mo───3*[{gnome-system-mo}]
        │         │             ├─ibus-daemon─┬─ibus-engine-sim───2*[{ibus-engine-sim}]
        │         │             │             ├─ibus-extension-───3*[{ibus-extension-}]
        │         │             │             ├─ibus-memconf───2*[{ibus-memconf}]
        │         │             │             └─2*[{ibus-daemon}]
        │         │             └─13*[{gnome-shell}]
        │         ├─gnome-shell-cal───5*[{gnome-shell-cal}]
        │         ├─goa-daemon───3*[{goa-daemon}]
        │         ├─goa-identity-se───2*[{goa-identity-se}]
        │         ├─gsd-a11y-settin───3*[{gsd-a11y-settin}]
        │         ├─gsd-color───3*[{gsd-color}]
        │         ├─gsd-datetime───3*[{gsd-datetime}]
        │         ├─gsd-housekeepin───3*[{gsd-housekeepin}]
        │         ├─gsd-keyboard───3*[{gsd-keyboard}]
        │         ├─gsd-media-keys───5*[{gsd-media-keys}]
        │         ├─gsd-power───3*[{gsd-power}]
        │         ├─gsd-print-notif───2*[{gsd-print-notif}]
        │         ├─gsd-printer───2*[{gsd-printer}]
        │         ├─gsd-rfkill───2*[{gsd-rfkill}]
        │         ├─gsd-screensaver───2*[{gsd-screensaver}]
        │         ├─gsd-sharing───3*[{gsd-sharing}]
        │         ├─gsd-smartcard───4*[{gsd-smartcard}]
        │         ├─gsd-sound───3*[{gsd-sound}]
        │         ├─gsd-usb-protect───3*[{gsd-usb-protect}]
        │         ├─gsd-wacom───2*[{gsd-wacom}]
        │         ├─gsd-wwan───3*[{gsd-wwan}]
        │         ├─gsd-xsettings───3*[{gsd-xsettings}]
        │         ├─gvfs-afc-volume───3*[{gvfs-afc-volume}]
        │         ├─gvfs-goa-volume───2*[{gvfs-goa-volume}]
        │         ├─gvfs-gphoto2-vo───2*[{gvfs-gphoto2-vo}]
        │         ├─gvfs-mtp-volume───2*[{gvfs-mtp-volume}]
        │         ├─gvfs-udisks2-vo───3*[{gvfs-udisks2-vo}]
        │         ├─gvfsd───2*[{gvfsd}]
        │         ├─gvfsd-metadata───2*[{gvfsd-metadata}]
        │         ├─ibus-portal───2*[{ibus-portal}]
        │         ├─ibus-x11───2*[{ibus-x11}]
        │         └─pulseaudio───3*[{pulseaudio}]
        ├─systemd-journal
        ├─systemd-logind
        ├─systemd-network
        ├─systemd-resolve
        ├─systemd-timesyn───{systemd-timesyn}
        ├─systemd-udevd
        ├─udisksd───4*[{udisksd}]
        ├─unattended-upgr───{unattended-upgr}
        ├─upowerd───2*[{upowerd}]
        └─wpa_supplicant
```

### PS-ELF

```bash
atom@virtualbox:~$ ps -eo pid,ppid,args
    PID    PPID COMMAND
      1       0 /sbin/init maybe-ubiquity
      2       0 [kthreadd]
      3       2 [rcu_gp]
      4       2 [rcu_par_gp]
      5       2 [kworker/0:0-events]
      6       2 [kworker/0:0H-kblockd]
      7       2 [kworker/u4:0-events_unbound]
      8       2 [mm_percpu_wq]
      9       2 [ksoftirqd/0]
     10       2 [rcu_sched]
     11       2 [migration/0]
     12       2 [idle_inject/0]
     13       2 [kworker/0:1-events]
     14       2 [cpuhp/0]
     15       2 [cpuhp/1]
     16       2 [idle_inject/1]
     17       2 [migration/1]
     18       2 [ksoftirqd/1]
     19       2 [kworker/1:0-events]
     20       2 [kworker/1:0H-kblockd]
     21       2 [kdevtmpfs]
     22       2 [netns]
     23       2 [rcu_tasks_kthre]
     24       2 [kauditd]
     25       2 [khungtaskd]
     26       2 [oom_reaper]
     27       2 [writeback]
     28       2 [kcompactd0]
     29       2 [ksmd]
     30       2 [khugepaged]
     35       2 [kworker/1:1-cgroup_destroy]
     77       2 [kintegrityd]
     78       2 [kblockd]
     79       2 [blkcg_punt_bio]
     80       2 [tpm_dev_wq]
     81       2 [ata_sff]
     82       2 [md]
     83       2 [edac-poller]
     84       2 [devfreq_wq]
     85       2 [watchdogd]
     86       2 [kworker/u4:1-events_unbound]
     88       2 [kswapd0]
     89       2 [ecryptfs-kthrea]
     91       2 [kthrotld]
     92       2 [acpi_thermal_pm]
     93       2 [scsi_eh_0]
     94       2 [scsi_tmf_0]
     95       2 [scsi_eh_1]
     96       2 [scsi_tmf_1]
     97       2 [kworker/u4:2-events_power_efficient]
     98       2 [vfio-irqfd-clea]
     99       2 [kworker/u4:3]
    100       2 [ipv6_addrconf]
    109       2 [kstrp]
    112       2 [kworker/u5:0]
    125       2 [kworker/1:1H-kblockd]
    126       2 [charger_manager]
    127       2 [kworker/1:2-cgroup_destroy]
    166       2 [irq/18-vmwgfx]
    167       2 [ttm_swap]
    168       2 [scsi_eh_2]
    169       2 [kworker/1:3-cgroup_destroy]
    170       2 [scsi_tmf_2]
    171       2 [cryptd]
    191       2 [kworker/0:2-events]
    219       2 [kdmflush]
    245       2 [raid5wq]
    289       2 [jbd2/dm-0-8]
    290       2 [ext4-rsv-conver]
    327       2 [kworker/0:1H-kblockd]
    364       1 /lib/systemd/systemd-journald
    402       1 /lib/systemd/systemd-udevd
    423       2 [iprt-VBoxWQueue]
    569       2 [kaluad]
    570       2 [kmpath_rdacd]
    571       2 [kmpathd]
    572       2 [kmpath_handlerd]
    573       1 /sbin/multipathd -d -s
    580       2 [kworker/0:3-cgroup_destroy]
    585       2 [loop0]
    592       2 [loop1]
    593       2 [loop2]
    595       2 [jbd2/sda2-8]
    596       2 [ext4-rsv-conver]
    597       2 [loop3]
    598       2 [loop4]
    599       2 [loop5]
    614       1 /lib/systemd/systemd-timesyncd
    665       1 /lib/systemd/systemd-networkd
    667       1 /lib/systemd/systemd-resolved
    678       1 /usr/lib/accountsservice/accounts-daemon
    680       1 avahi-daemon: running [virtualbox.local]
    681       1 /usr/sbin/cupsd -l
    682       1 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
    685       2 [kworker/0:4-events]
    686       1 /usr/sbin/NetworkManager --no-daemon
    688       1 /usr/sbin/atopacctd
    694       1 /usr/sbin/irqbalance --foreground
    696       1 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
    697       1 /usr/lib/policykit-1/polkitd --no-debug
    699       1 /usr/sbin/rsyslogd -n -iNONE
    706       1 /usr/lib/snapd/snapd
    707       1 /usr/libexec/switcheroo-control
    708       1 /lib/systemd/systemd-logind
    712       1 /usr/lib/udisks2/udisksd
    713       1 /sbin/wpa_supplicant -u -s -O /run/wpa_supplicant
    719       1 /usr/bin/atop -R -w /var/log/atop/atop_20260104 600
    720       2 [kworker/0:5-events]
    723     680 avahi-daemon: chroot helper
    742       1 /usr/sbin/cups-browsed
    744       1 /usr/sbin/ModemManager
    765       1 /usr/bin/python3 /usr/bin/glances -s -B 127.0.0.1
    781       1 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
    803       1 /usr/sbin/cron -f
    808       1 /usr/sbin/atd -f
    817       2 [kworker/0:6-events]
    827       1 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
    829       1 /usr/sbin/gdm3
    857       1 /usr/libexec/rtkit-daemon
   1062       1 /usr/lib/upower/upowerd
   1066       1 /usr/lib/packagekit/packagekitd
   1246       1 /usr/libexec/colord
   1269     827 sshd: atom [priv]
   1287       1 /lib/systemd/systemd --user
   1288    1287 (sd-pam)
   1293    1287 /usr/bin/pulseaudio --daemonize=no --log-target=journal
   1314    1287 /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
   1414    1269 sshd: atom@pts/0
   1415    1414 -bash
   1462       2 [kworker/1:4-events]
   1518     829 gdm-session-worker [pam/gdm-password]
   1534       2 [kworker/1:5-events]
   1553       1 /usr/bin/gnome-keyring-daemon --daemonize --login
   1557    1518 /usr/lib/gdm3/gdm-x-session --run-script env GNOME_SHELL_SESSION_MODE=ubuntu /usr/bin/gnome-session --systemd --session=ubuntu
   1559    1557 /usr/lib/xorg/Xorg vt2 -displayfd 3 -auth /run/user/1001/gdm/Xauthority -background none -noreset -keeptty -verbose 3
   1567    1557 /usr/libexec/gnome-session-binary --systemd --systemd --session=ubuntu
   1632    1567 /usr/bin/ssh-agent /usr/bin/im-launch env GNOME_SHELL_SESSION_MODE=ubuntu /usr/bin/gnome-session --systemd --session=ubuntu
   1649    1287 /usr/libexec/at-spi-bus-launcher
   1654    1649 /usr/bin/dbus-daemon --config-file=/usr/share/defaults/at-spi2/accessibility.conf --nofork --print-address 3
   1671    1287 /usr/libexec/gnome-session-ctl --monitor
   1687    1287 /usr/libexec/dconf-service
   1691    1287 /usr/libexec/gnome-session-binary --systemd-service --session=ubuntu
   1707    1287 /usr/bin/gnome-shell
   1728    1287 /usr/libexec/gvfsd
   1736    1707 ibus-daemon --panel disable --xim
   1740    1736 /usr/libexec/ibus-memconf
   1741    1736 /usr/libexec/ibus-extension-gtk3
   1745    1287 /usr/libexec/ibus-x11 --kill-daemon
   1748    1287 /usr/libexec/ibus-portal
   1757    1287 /usr/libexec/at-spi2-registryd --use-gnome-session
   1762    1287 /usr/libexec/gnome-shell-calendar-server
   1770    1287 /usr/libexec/evolution-source-registry
   1776    1287 /usr/libexec/goa-daemon
   1779    1287 /usr/libexec/evolution-calendar-factory
   1786    1287 /usr/libexec/gvfs-udisks2-volume-monitor
   1796    1287 /usr/libexec/goa-identity-service
   1803    1287 /usr/libexec/gvfs-goa-volume-monitor
   1813    1287 /usr/libexec/evolution-addressbook-factory
   1814    1287 /usr/libexec/gvfs-mtp-volume-monitor
   1820    1287 /usr/libexec/gvfsd-metadata
   1825    1287 /usr/libexec/gvfs-gphoto2-volume-monitor
   1834    1287 /usr/libexec/gvfs-afc-volume-monitor
   1844    1287 /usr/bin/gjs /usr/share/gnome-shell/org.gnome.Shell.Notifications
   1847    1287 /usr/libexec/gsd-a11y-settings
   1848    1287 /usr/libexec/gsd-color
   1849    1287 /usr/libexec/gsd-datetime
   1850    1287 /usr/libexec/gsd-housekeeping
   1851    1287 /usr/libexec/gsd-keyboard
   1852    1287 /usr/libexec/gsd-media-keys
   1853    1287 /usr/libexec/gsd-power
   1854    1287 /usr/libexec/gsd-print-notifications
   1857    1287 /usr/libexec/gsd-rfkill
   1858    1287 /usr/libexec/gsd-screensaver-proxy
   1859    1287 /usr/libexec/gsd-sharing
   1863    1287 /usr/libexec/gsd-smartcard
   1864    1287 /usr/libexec/gsd-sound
   1872    1287 /usr/libexec/gsd-usb-protection
   1873    1287 /usr/libexec/gsd-wacom
   1874    1287 /usr/libexec/gsd-wwan
   1882    1287 /usr/libexec/gsd-xsettings
   1888    1691 /usr/libexec/evolution-data-server/evolution-alarm-notify
   1889    1736 /usr/libexec/ibus-engine-simple
   1899    1691 /usr/lib/x86_64-linux-gnu/indicator-messages/indicator-messages-service
   1955    1287 /usr/libexec/gsd-printer
   2124    1707 gnome-system-monitor
   2146    1415 htop
   2151    1415 ps -eo pid,ppid,args
```

### Free-H

```bash
atom@virtualbox:~$ free -h
              total        used        free      shared  buff/cache   available
Mem:          1.9Gi       600Mi       692Mi       5.0Mi       678Mi       1.2Gi
Swap:         2.0Gi          0B       2.0Gi

```

### Snaps

#### Login Screen

![image_4_1](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_4_1.png)

#### Desktop Overview

![image_4_2](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_4_2.png)

#### System Monitor

![image_4_3](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_4_3.png)

---

## 5. OpenBox

### Install X-Server, DM and WM

```bash
sudo apt install --no-install-recommends openbox lightdm slick-greeter xorg
```

Optionally install panel `tinit2`/`gnome-panel`.

### Configure LightDM

```bash
sudo sh -c 'echo "[Seat:*]\ngreeter-session=slick-greeter\nuser-session=openbox" > /etc/lightdm/lightdm.conf'
```

```bash
$ ls /usr/share/xsessions/
openbox.desktop

$ ls /usr/share/xgreeters/
slick-greeter.desktop

$ ls /etc/xdg/autostart/
	<not-taken>
```

### Reboot VM

### Disk Size

```bash
atom@virtualbox:~$ df -h /
Filesystem                         Size  Used Avail Use% Mounted on
/dev/mapper/ubuntu--vg-ubuntu--lv   15G  5.6G  8.4G  40% /
```

### PS-Tree

```bash
atom@virtualbox:~$ pstree
systemd─┬─ModemManager───2*[{ModemManager}]
        ├─accounts-daemon───2*[{accounts-daemon}]
        ├─agetty
        ├─atd
        ├─cron
        ├─dbus-daemon
        ├─irqbalance───{irqbalance}
        ├─lightdm─┬─Xorg───{Xorg}
        │         ├─lightdm─┬─openbox─┬─ssh-agent
        │         │         │         └─xterm───bash───htop
        │         │         └─2*[{lightdm}]
        │         └─2*[{lightdm}]
        ├─multipathd───6*[{multipathd}]
        ├─networkd-dispat
        ├─polkitd───2*[{polkitd}]
        ├─rsyslogd───3*[{rsyslogd}]
        ├─snapd───7*[{snapd}]
        ├─sshd───sshd───sshd───bash─┬─htop
        │                           └─pstree
        ├─systemd─┬─(sd-pam)
        │         └─dbus-daemon
        ├─systemd-journal
        ├─systemd-logind
        ├─systemd-network
        ├─systemd-resolve
        ├─systemd-timesyn───{systemd-timesyn}
        ├─systemd-udevd
        ├─udisksd───4*[{udisksd}]
        ├─unattended-upgr───{unattended-upgr}
        └─upowerd───2*[{upowerd}]
```

### PS-ELF

```bash
atom@virtualbox:~$ ps -eo pid,ppid,args
    PID    PPID COMMAND
      1       0 /sbin/init maybe-ubiquity
      2       0 [kthreadd]
      3       2 [rcu_gp]
      4       2 [rcu_par_gp]
      5       2 [kworker/0:0-events]
      6       2 [kworker/0:0H-kblockd]
      7       2 [kworker/u4:0-events_unbound]
      8       2 [mm_percpu_wq]
      9       2 [ksoftirqd/0]
     10       2 [rcu_sched]
     11       2 [migration/0]
     12       2 [idle_inject/0]
     13       2 [kworker/0:1-events]
     14       2 [cpuhp/0]
     15       2 [cpuhp/1]
     16       2 [idle_inject/1]
     17       2 [migration/1]
     18       2 [ksoftirqd/1]
     19       2 [kworker/1:0-events]
     20       2 [kworker/1:0H-kblockd]
     21       2 [kdevtmpfs]
     22       2 [netns]
     23       2 [rcu_tasks_kthre]
     24       2 [kauditd]
     25       2 [khungtaskd]
     26       2 [oom_reaper]
     27       2 [writeback]
     28       2 [kcompactd0]
     29       2 [ksmd]
     30       2 [khugepaged]
     35       2 [kworker/1:1-cgroup_destroy]
     77       2 [kintegrityd]
     78       2 [kblockd]
     79       2 [blkcg_punt_bio]
     80       2 [tpm_dev_wq]
     81       2 [ata_sff]
     82       2 [md]
     83       2 [edac-poller]
     84       2 [devfreq_wq]
     85       2 [watchdogd]
     86       2 [kworker/u4:1-events_power_efficient]
     88       2 [kswapd0]
     89       2 [ecryptfs-kthrea]
     91       2 [kthrotld]
     92       2 [acpi_thermal_pm]
     93       2 [scsi_eh_0]
     94       2 [scsi_tmf_0]
     95       2 [scsi_eh_1]
     96       2 [scsi_tmf_1]
     97       2 [kworker/u4:2-events_unbound]
     98       2 [vfio-irqfd-clea]
     99       2 [kworker/u4:3]
    100       2 [ipv6_addrconf]
    109       2 [kstrp]
    112       2 [kworker/u5:0]
    125       2 [charger_manager]
    126       2 [kworker/1:1H-kblockd]
    127       2 [kworker/1:2-events]
    166       2 [scsi_eh_2]
    167       2 [scsi_tmf_2]
    168       2 [kworker/0:2-events]
    169       2 [irq/18-vmwgfx]
    170       2 [ttm_swap]
    171       2 [cryptd]
    191       2 [kworker/0:1H-kblockd]
    219       2 [kdmflush]
    245       2 [raid5wq]
    290       2 [jbd2/dm-0-8]
    293       2 [ext4-rsv-conver]
    363       1 /lib/systemd/systemd-journald
    394       2 [kworker/0:3-cgroup_destroy]
    398       2 [kworker/1:3-cgroup_destroy]
    399       1 /lib/systemd/systemd-udevd
    423       2 [iprt-VBoxWQueue]
    564       2 [kaluad]
    565       2 [kmpath_rdacd]
    566       2 [kmpathd]
    567       2 [kmpath_handlerd]
    568       1 /sbin/multipathd -d -s
    580       2 [loop0]
    586       2 [loop1]
    587       2 [loop2]
    589       2 [jbd2/sda2-8]
    590       2 [ext4-rsv-conver]
    591       2 [loop3]
    592       2 [loop4]
    593       2 [loop5]
    612       1 /lib/systemd/systemd-timesyncd
    658       1 /lib/systemd/systemd-networkd
    660       1 /lib/systemd/systemd-resolved
    672       1 /usr/lib/accountsservice/accounts-daemon
    675       1 /usr/sbin/cron -f
    677       1 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
    684       1 /usr/sbin/irqbalance --foreground
    685       1 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
    686       1 /usr/lib/policykit-1/polkitd --no-debug
    687       1 /usr/sbin/rsyslogd -n -iNONE
    690       1 /usr/lib/snapd/snapd
    693       1 /lib/systemd/systemd-logind
    695       1 /usr/lib/udisks2/udisksd
    700       1 /usr/sbin/atd -f
    727       1 /usr/sbin/lightdm
    728       1 /sbin/agetty -o -p -- \u --noclear tty1 linux
    738       1 /usr/sbin/ModemManager
    751       1 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
    761       1 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
    765     727 /usr/lib/xorg/Xorg -core :0 -seat seat0 -auth /var/run/lightdm/root/:0 -nolisten tcp vt7 -novtswitch
    864       1 /usr/lib/upower/upowerd
    954     727 lightdm --session-child 12 19
    963       2 [kworker/1:4-events]
    989       1 /lib/systemd/systemd --user
    990     989 (sd-pam)
    995     954 /usr/bin/openbox --startup /usr/lib/x86_64-linux-gnu/openbox-autostart OPENBOX
   1011     989 /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
   1038     995 /usr/bin/ssh-agent /usr/bin/openbox-session
   1047     751 sshd: atom [priv]
   1181    1047 sshd: atom@pts/0
   1182    1181 -bash
   1227    1182 htop
   1234     995 xterm -class UXTerm -title uxterm -u8
   1240    1234 bash
   1246    1240 htop
   1249    1182 ps -eo pid,ppid,args
```

### Free-H

```bash
atom@virtualbox:~$ free -h
              total        used        free      shared  buff/cache   available
Mem:          1.9Gi       204Mi       1.3Gi       1.0Mi       456Mi       1.6Gi
Swap:         2.0Gi          0B       2.0Gi
```

### Snaps

#### Login Screen

![image_5_1](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_5_1.png)

#### Desktop Overview

![image_5_2](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_5_2.png)

---

## 6. OpenBox Gnome Session

### Install X-Server, DM and WM

```bash
sudo apt install openbox-gnome-session xorg gdm3
```

### Reboot VM

### Disk Size

```bash
atom@virtualbox:~$ df -h /
Filesystem Size Used Avail Use% Mounted on
/dev/mapper/ubuntu--vg-ubuntu--lv 15G 6.3G 7.7G 45% /
```

### PS-Tree

```bash
atom@virtualbox:~$ pstree
systemd─┬─ModemManager───2*[{ModemManager}]
        ├─NetworkManager───2*[{NetworkManager}]
        ├─accounts-daemon───2*[{accounts-daemon}]
        ├─agent───2*[{agent}]
        ├─applet.py
        ├─at-spi-bus-laun─┬─dbus-daemon
        │                 └─3*[{at-spi-bus-laun}]
        ├─at-spi2-registr───2*[{at-spi2-registr}]
        ├─atd
        ├─avahi-daemon───avahi-daemon
        ├─colord───2*[{colord}]
        ├─cron
        ├─cups-browsed───2*[{cups-browsed}]
        ├─cupsd
        ├─dbus-daemon
        ├─gdm3─┬─gdm-session-wor─┬─gdm-x-session─┬─Xorg───{Xorg}
        │      │                 │               ├─openbox─┬─ssh-agent
        │      │                 │               │         ├─xterm───bash───htop
        │      │                 │               │         └─2*[{openbox}]
        │      │                 │               └─2*[{gdm-x-session}]
        │      │                 └─2*[{gdm-session-wor}]
        │      └─2*[{gdm3}]
        ├─irqbalance───{irqbalance}
        ├─multipathd───6*[{multipathd}]
        ├─networkd-dispat
        ├─nm-applet───3*[{nm-applet}]
        ├─packagekitd───2*[{packagekitd}]
        ├─polkitd───2*[{polkitd}]
        ├─rsyslogd───3*[{rsyslogd}]
        ├─rtkit-daemon───2*[{rtkit-daemon}]
        ├─snapd───8*[{snapd}]
        ├─sshd───sshd───sshd───bash─┬─htop
        │                           └─pstree
        ├─switcheroo-cont───2*[{switcheroo-cont}]
        ├─systemd─┬─(sd-pam)
        │         ├─dbus-daemon
        │         ├─gvfsd───2*[{gvfsd}]
        │         └─pulseaudio───3*[{pulseaudio}]
        ├─systemd-journal
        ├─systemd-logind
        ├─systemd-network
        ├─systemd-resolve
        ├─systemd-timesyn───{systemd-timesyn}
        ├─systemd-udevd
        ├─udisksd───4*[{udisksd}]
        ├─unattended-upgr───{unattended-upgr}
        ├─upowerd───2*[{upowerd}]
        └─wpa_supplicant
```

### PS-ELF

```bash
atom@virtualbox:~$ ps -eo pid,ppid,args
    PID    PPID COMMAND
      1       0 /sbin/init maybe-ubiquity
      2       0 [kthreadd]
      3       2 [rcu_gp]
      4       2 [rcu_par_gp]
      5       2 [kworker/0:0-events]
      6       2 [kworker/0:0H-kblockd]
      7       2 [kworker/u4:0-events_freezable_power_]
      8       2 [mm_percpu_wq]
      9       2 [ksoftirqd/0]
     10       2 [rcu_sched]
     11       2 [migration/0]
     12       2 [idle_inject/0]
     13       2 [kworker/0:1-memcg_kmem_cache]
     14       2 [cpuhp/0]
     15       2 [cpuhp/1]
     16       2 [idle_inject/1]
     17       2 [migration/1]
     18       2 [ksoftirqd/1]
     19       2 [kworker/1:0-events]
     20       2 [kworker/1:0H-kblockd]
     21       2 [kdevtmpfs]
     22       2 [netns]
     23       2 [rcu_tasks_kthre]
     24       2 [kauditd]
     25       2 [khungtaskd]
     26       2 [oom_reaper]
     27       2 [writeback]
     28       2 [kcompactd0]
     29       2 [ksmd]
     30       2 [khugepaged]
     35       2 [kworker/1:1-events]
     77       2 [kintegrityd]
     78       2 [kblockd]
     79       2 [blkcg_punt_bio]
     80       2 [tpm_dev_wq]
     81       2 [ata_sff]
     82       2 [md]
     83       2 [edac-poller]
     84       2 [devfreq_wq]
     85       2 [watchdogd]
     86       2 [kworker/u4:1-events_unbound]
     88       2 [kswapd0]
     89       2 [ecryptfs-kthrea]
     91       2 [kthrotld]
     92       2 [acpi_thermal_pm]
     93       2 [scsi_eh_0]
     94       2 [scsi_tmf_0]
     95       2 [scsi_eh_1]
     96       2 [scsi_tmf_1]
     97       2 [kworker/u4:2-events_unbound]
     98       2 [vfio-irqfd-clea]
     99       2 [kworker/u4:3]
    100       2 [ipv6_addrconf]
    109       2 [kstrp]
    112       2 [kworker/u5:0]
    125       2 [charger_manager]
    126       2 [kworker/1:1H-kblockd]
    127       2 [kworker/0:2-cgroup_destroy]
    166       2 [kworker/1:2-cgroup_destroy]
    167       2 [scsi_eh_2]
    168       2 [scsi_tmf_2]
    169       2 [irq/18-vmwgfx]
    170       2 [cryptd]
    171       2 [ttm_swap]
    191       2 [kworker/0:1H-kblockd]
    219       2 [kdmflush]
    245       2 [raid5wq]
    289       2 [jbd2/dm-0-8]
    290       2 [ext4-rsv-conver]
    363       1 /lib/systemd/systemd-journald
    394       2 [kworker/0:3-events]
    395       2 [kworker/0:4-events]
    401       2 [kworker/0:5-cgroup_destroy]
    403       1 /lib/systemd/systemd-udevd
    425       2 [iprt-VBoxWQueue]
    575       2 [kaluad]
    576       2 [kmpath_rdacd]
    577       2 [kmpathd]
    578       2 [kmpath_handlerd]
    579       1 /sbin/multipathd -d -s
    589       2 [loop0]
    597       2 [loop1]
    599       2 [jbd2/sda2-8]
    600       2 [ext4-rsv-conver]
    601       2 [loop2]
    602       2 [loop3]
    603       2 [loop4]
    605       2 [loop5]
    623       1 /lib/systemd/systemd-timesyncd
    672       1 /lib/systemd/systemd-networkd
    674       1 /lib/systemd/systemd-resolved
    685       1 /usr/lib/accountsservice/accounts-daemon
    686       1 avahi-daemon: running [virtualbox.local]
    687       1 /usr/sbin/cupsd -l
    688       1 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
    689       1 /usr/sbin/NetworkManager --no-daemon
    695       1 /usr/sbin/irqbalance --foreground
    697       1 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
    698       1 /usr/lib/policykit-1/polkitd --no-debug
    700       1 /usr/sbin/rsyslogd -n -iNONE
    703       1 /usr/lib/snapd/snapd
    704       1 /usr/libexec/switcheroo-control
    705       1 /lib/systemd/systemd-logind
    708       1 /usr/lib/udisks2/udisksd
    709       1 /sbin/wpa_supplicant -u -s -O /run/wpa_supplicant
    711     686 avahi-daemon: chroot helper
    740       1 /usr/sbin/cups-browsed
    748       1 /usr/sbin/ModemManager
    773       2 [kworker/1:3-events]
    778       1 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
    796       1 /usr/sbin/cron -f
    802       1 /usr/sbin/atd -f
    806       2 [kworker/0:6-ata_sff]
    807       2 [kworker/0:7-events]
    823       1 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
    824       1 /usr/sbin/gdm3
    849       1 /usr/libexec/rtkit-daemon
   1056       1 /usr/lib/upower/upowerd
   1059       1 /usr/lib/packagekit/packagekitd
   1189       1 /usr/libexec/colord
   1258     824 gdm-session-worker [pam/gdm-password]
   1278       1 /lib/systemd/systemd --user
   1279    1278 (sd-pam)
   1286    1278 /usr/bin/pulseaudio --daemonize=no --log-target=journal
   1294    1278 /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
   1296    1258 /usr/lib/gdm3/gdm-x-session --register-session --run-script /usr/bin/openbox-session
   1299    1296 /usr/lib/xorg/Xorg vt2 -displayfd 3 -auth /run/user/1001/gdm/Xauthority -background none -noreset -keeptty -verbose 3
   1306    1296 /usr/bin/openbox --startup /usr/lib/x86_64-linux-gnu/openbox-autostart OPENBOX
   1364    1306 /usr/bin/ssh-agent /usr/bin/im-launch /usr/bin/openbox-session
   1398       1 /usr/bin/python3 /usr/share/system-config-printer/applet.py
   1402       1 /usr/libexec/geoclue-2.0/demos/agent
   1406       1 /usr/libexec/at-spi-bus-launcher --launch-immediately
   1409       1 nm-applet
   1416    1406 /usr/bin/dbus-daemon --config-file=/usr/share/defaults/at-spi2/accessibility.conf --nofork --print-address 3
   1425    1278 /usr/libexec/gvfsd
   1437       1 /usr/libexec/at-spi2-registryd --use-gnome-session
   1473     823 sshd: atom [priv]
   1607    1473 sshd: atom@pts/0
   1608    1607 -bash
   1635    1306 xterm
   1637    1635 bash
   1659    1637 htop
   1660    1608 htop
   1662    1608 ps -eo pid,ppid,args
```

#### Desktop Overview

![image_6_1](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_6_1.png)

---

## 7. Ubuntu Desktop Minimal (Without Install Recommends)

### Install X-Server, DM and WM

```bash
sudo apt install -y --no-install-recommends ubuntu-desktop-minimal
```

```bash
atom@virtualbox:~$ ls /usr/share/xsessions/
ubuntu.desktop

atom@virtualbox:~$ ls /etc/xdg/autostart/
at-spi-dbus-bus.desktop                        org.gnome.SettingsDaemon.Keyboard.desktop            org.gnome.SettingsDaemon.XSettings.desktop
geoclue-demo-agent.desktop                     org.gnome.SettingsDaemon.MediaKeys.desktop           print-applet.desktop
gnome-keyring-pkcs11.desktop                   org.gnome.SettingsDaemon.Power.desktop               pulseaudio.desktop
gnome-keyring-secrets.desktop                  org.gnome.SettingsDaemon.PrintNotifications.desktop  snap-userd-autostart.desktop
gnome-keyring-ssh.desktop                      org.gnome.SettingsDaemon.Rfkill.desktop              spice-vdagent.desktop
gnome-shell-overrides-migration.desktop        org.gnome.SettingsDaemon.ScreensaverProxy.desktop    tracker-extract.desktop
im-launch.desktop                              org.gnome.SettingsDaemon.Sharing.desktop             tracker-miner-fs.desktop
org.gnome.Evolution-alarm-notify.desktop       org.gnome.SettingsDaemon.Smartcard.desktop           update-notifier.desktop
org.gnome.SettingsDaemon.A11ySettings.desktop  org.gnome.SettingsDaemon.Sound.desktop               user-dirs-update-gtk.desktop
org.gnome.SettingsDaemon.Color.desktop         org.gnome.SettingsDaemon.UsbProtection.desktop       xdg-user-dirs.desktop
org.gnome.SettingsDaemon.Datetime.desktop      org.gnome.SettingsDaemon.Wacom.desktop
org.gnome.SettingsDaemon.Housekeeping.desktop  org.gnome.SettingsDaemon.Wwan.desktop
```

### Reboot VM

### Disk Size

```bash
atom@virtualbox:~$ df -h /
Filesystem                         Size  Used Avail Use% Mounted on
/dev/mapper/ubuntu--vg-ubuntu--lv   15G  6.0G  8.0G  43% /
```

### PS-Tree

```bash
atom@virtualbox:~$ pstree
systemd─┬─ModemManager───2*[{ModemManager}]
        ├─accounts-daemon───2*[{accounts-daemon}]
        ├─anacron
        ├─atd
        ├─colord───2*[{colord}]
        ├─cron
        ├─dbus-daemon
        ├─gdm3─┬─gdm-session-wor─┬─gdm-x-session─┬─Xorg───{Xorg}
        │      │                 │               ├─gnome-session-b─┬─ssh-agent
        │      │                 │               │                 └─2*[{gnome-session-b}]
        │      │                 │               └─2*[{gdm-x-session}]
        │      │                 └─2*[{gdm-session-wor}]
        │      └─2*[{gdm3}]
        ├─irqbalance───{irqbalance}
        ├─multipathd───6*[{multipathd}]
        ├─networkd-dispat
        ├─packagekitd───2*[{packagekitd}]
        ├─polkitd───2*[{polkitd}]
        ├─rsyslogd───3*[{rsyslogd}]
        ├─snapd───8*[{snapd}]
        ├─sshd───sshd───sshd───bash─┬─htop
        │                           └─pstree
        ├─systemd─┬─(sd-pam)
        │         ├─at-spi-bus-laun─┬─dbus-daemon
        │         │                 └─3*[{at-spi-bus-laun}]
        │         ├─at-spi2-registr───2*[{at-spi2-registr}]
        │         ├─dbus-daemon
        │         ├─dconf-service───2*[{dconf-service}]
        │         ├─evolution-addre───5*[{evolution-addre}]
        │         ├─evolution-calen───8*[{evolution-calen}]
        │         ├─evolution-sourc───3*[{evolution-sourc}]
        │         ├─gjs───4*[{gjs}]
        │         ├─gnome-keyring-d───3*[{gnome-keyring-d}]
        │         ├─gnome-session-b─┬─evolution-alarm───5*[{evolution-alarm}]
        │         │                 ├─update-notifier───3*[{update-notifier}]
        │         │                 └─3*[{gnome-session-b}]
        │         ├─gnome-session-c───{gnome-session-c}
        │         ├─gnome-shell─┬─xterm───htop
        │         │             └─12*[{gnome-shell}]
        │         ├─gnome-shell-cal───5*[{gnome-shell-cal}]
        │         ├─gsd-a11y-settin───3*[{gsd-a11y-settin}]
        │         ├─gsd-color───3*[{gsd-color}]
        │         ├─gsd-datetime───3*[{gsd-datetime}]
        │         ├─gsd-housekeepin───3*[{gsd-housekeepin}]
        │         ├─gsd-keyboard───3*[{gsd-keyboard}]
        │         ├─gsd-media-keys───3*[{gsd-media-keys}]
        │         ├─gsd-power───3*[{gsd-power}]
        │         ├─gsd-print-notif───2*[{gsd-print-notif}]
        │         ├─gsd-printer───2*[{gsd-printer}]
        │         ├─gsd-rfkill───2*[{gsd-rfkill}]
        │         ├─gsd-screensaver───2*[{gsd-screensaver}]
        │         ├─gsd-sharing───3*[{gsd-sharing}]
        │         ├─gsd-smartcard───4*[{gsd-smartcard}]
        │         ├─gsd-sound───3*[{gsd-sound}]
        │         ├─gsd-usb-protect───3*[{gsd-usb-protect}]
        │         ├─gsd-wacom───2*[{gsd-wacom}]
        │         ├─gsd-wwan───3*[{gsd-wwan}]
        │         ├─gsd-xsettings───3*[{gsd-xsettings}]
        │         ├─gvfs-udisks2-vo───3*[{gvfs-udisks2-vo}]
        │         ├─gvfsd─┬─gvfsd-trash───2*[{gvfsd-trash}]
        │         │       └─2*[{gvfsd}]
        │         ├─gvfsd-metadata───2*[{gvfsd-metadata}]
        │         ├─nautilus───4*[{nautilus}]
        │         ├─pulseaudio───3*[{pulseaudio}]
        │         ├─tracker-miner-f───4*[{tracker-miner-f}]
        │         └─xdg-permission-───2*[{xdg-permission-}]
        ├─systemd-journal
        ├─systemd-logind
        ├─systemd-network
        ├─systemd-resolve
        ├─systemd-timesyn───{systemd-timesyn}
        ├─systemd-udevd
        ├─udisksd───4*[{udisksd}]
        ├─unattended-upgr───{unattended-upgr}
        ├─upowerd───2*[{upowerd}]
        └─wpa_supplicant
```

### PS-ELF

```bash
atom@virtualbox:~$ ps -eo pid,ppid,args
    PID    PPID COMMAND
      1       0 /sbin/init maybe-ubiquity
      2       0 [kthreadd]
      3       2 [rcu_gp]
      4       2 [rcu_par_gp]
      5       2 [kworker/0:0-events]
      6       2 [kworker/0:0H-kblockd]
      7       2 [kworker/u4:0-events_unbound]
      8       2 [mm_percpu_wq]
      9       2 [ksoftirqd/0]
     10       2 [rcu_sched]
     11       2 [migration/0]
     12       2 [idle_inject/0]
     13       2 [kworker/0:1-events]
     14       2 [cpuhp/0]
     15       2 [cpuhp/1]
     16       2 [idle_inject/1]
     17       2 [migration/1]
     18       2 [ksoftirqd/1]
     19       2 [kworker/1:0-events]
     20       2 [kworker/1:0H-kblockd]
     21       2 [kdevtmpfs]
     22       2 [netns]
     23       2 [rcu_tasks_kthre]
     24       2 [kauditd]
     25       2 [khungtaskd]
     26       2 [oom_reaper]
     27       2 [writeback]
     28       2 [kcompactd0]
     29       2 [ksmd]
     30       2 [khugepaged]
     35       2 [kworker/1:1-events]
     77       2 [kintegrityd]
     78       2 [kblockd]
     79       2 [blkcg_punt_bio]
     80       2 [tpm_dev_wq]
     81       2 [ata_sff]
     82       2 [md]
     83       2 [edac-poller]
     84       2 [devfreq_wq]
     85       2 [watchdogd]
     86       2 [kworker/u4:1-events_unbound]
     88       2 [kswapd0]
     89       2 [ecryptfs-kthrea]
     91       2 [kthrotld]
     92       2 [acpi_thermal_pm]
     93       2 [scsi_eh_0]
     94       2 [scsi_tmf_0]
     95       2 [scsi_eh_1]
     96       2 [scsi_tmf_1]
     97       2 [kworker/u4:2-events_unbound]
     98       2 [vfio-irqfd-clea]
     99       2 [kworker/u4:3]
    100       2 [ipv6_addrconf]
    109       2 [kstrp]
    112       2 [kworker/u5:0]
    119       2 [kworker/1:1H-kblockd]
    126       2 [charger_manager]
    127       2 [kworker/1:2-cgroup_destroy]
    165       2 [kworker/0:2-events]
    167       2 [scsi_eh_2]
    168       2 [scsi_tmf_2]
    169       2 [kworker/0:3-cgroup_destroy]
    170       2 [cryptd]
    190       2 [kworker/0:1H-kblockd]
    212       2 [irq/18-vmwgfx]
    213       2 [ttm_swap]
    219       2 [kdmflush]
    246       2 [raid5wq]
    290       2 [jbd2/dm-0-8]
    291       2 [ext4-rsv-conver]
    364       1 /lib/systemd/systemd-journald
    389       2 [kworker/1:3-cgroup_destroy]
    398       1 /lib/systemd/systemd-udevd
    417       2 [iprt-VBoxWQueue]
    590       2 [kaluad]
    591       2 [kmpath_rdacd]
    592       2 [kmpathd]
    593       2 [kmpath_handlerd]
    594       1 /sbin/multipathd -d -s
    604       2 [loop0]
    609       2 [loop1]
    613       2 [loop2]
    615       2 [jbd2/sda2-8]
    616       2 [ext4-rsv-conver]
    617       2 [loop3]
    618       2 [loop4]
    619       2 [loop5]
    636       1 /lib/systemd/systemd-timesyncd
    683       1 /lib/systemd/systemd-networkd
    685       1 /lib/systemd/systemd-resolved
    696       1 /usr/lib/accountsservice/accounts-daemon
    698       1 /usr/sbin/anacron -d -q -s
    699       1 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
    706       1 /usr/sbin/irqbalance --foreground
    707       1 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
    710       1 /usr/lib/policykit-1/polkitd --no-debug
    716       1 /usr/sbin/rsyslogd -n -iNONE
    719       1 /usr/lib/snapd/snapd
    726       1 /lib/systemd/systemd-logind
    727       1 /usr/lib/udisks2/udisksd
    728       1 /sbin/wpa_supplicant -u -s -O /run/wpa_supplicant
    759       1 /usr/sbin/cron -f
    766       1 /usr/sbin/atd -f
    775       1 /usr/sbin/ModemManager
    794       1 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
    798       1 /usr/sbin/gdm3
    812       1 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
   1032       1 /usr/lib/upower/upowerd
   1035       1 /usr/lib/packagekit/packagekitd
   1160       1 /usr/libexec/colord
   1202     798 gdm-session-worker [pam/gdm-password]
   1215       1 /lib/systemd/systemd --user
   1216    1215 (sd-pam)
   1221    1215 /usr/bin/pulseaudio --daemonize=no --log-target=journal
   1224    1215 /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
   1226    1202 /usr/lib/gdm3/gdm-x-session --run-script env GNOME_SHELL_SESSION_MODE=ubuntu /usr/bin/gnome-session --systemd --session=ubuntu
   1228    1226 /usr/lib/xorg/Xorg vt2 -displayfd 3 -auth /run/user/1001/gdm/Xauthority -background none -noreset -keeptty -verbose 3
   1241    1226 /usr/libexec/gnome-session-binary --systemd --systemd --session=ubuntu
   1368    1241 /usr/bin/ssh-agent /usr/bin/im-launch env GNOME_SHELL_SESSION_MODE=ubuntu /usr/bin/gnome-session --systemd --session=ubuntu
   1445    1215 /usr/libexec/at-spi-bus-launcher
   1450    1445 /usr/bin/dbus-daemon --config-file=/usr/share/defaults/at-spi2/accessibility.conf --nofork --print-address 3
   1467    1215 /usr/libexec/gnome-session-ctl --monitor
   1482    1215 /usr/libexec/gnome-session-binary --systemd-service --session=ubuntu
   1494    1215 /usr/bin/gnome-keyring-daemon --start --components=pkcs11
   1501    1215 /usr/bin/gnome-shell
   1522    1215 /usr/libexec/gvfsd
   1532    1215 /usr/libexec/gnome-shell-calendar-server
   1533    1215 /usr/libexec/xdg-permission-store
   1542    1215 /usr/libexec/evolution-source-registry
   1549    1215 /usr/libexec/dconf-service
   1556    1215 /usr/libexec/evolution-calendar-factory
   1557    1215 /usr/libexec/gvfs-udisks2-volume-monitor
   1570    1215 /usr/libexec/evolution-addressbook-factory
   1575    1215 /usr/libexec/gvfsd-metadata
   1580    1215 /usr/bin/nautilus --gapplication-service
   1590    1522 /usr/libexec/gvfsd-trash --spawner :1.24 /org/gtk/gvfs/exec_spaw/0
   1604    1215 /usr/bin/gjs /usr/share/gnome-shell/org.gnome.Shell.Notifications
   1607    1215 /usr/libexec/at-spi2-registryd --use-gnome-session
   1618    1215 /usr/libexec/gsd-a11y-settings
   1619    1215 /usr/libexec/gsd-color
   1620    1215 /usr/libexec/gsd-datetime
   1621    1215 /usr/libexec/gsd-housekeeping
   1622    1215 /usr/libexec/gsd-keyboard
   1623    1215 /usr/libexec/gsd-media-keys
   1624    1215 /usr/libexec/gsd-power
   1625    1215 /usr/libexec/gsd-print-notifications
   1626    1215 /usr/libexec/gsd-rfkill
   1627    1215 /usr/libexec/gsd-screensaver-proxy
   1628    1215 /usr/libexec/gsd-sharing
   1629    1215 /usr/libexec/gsd-smartcard
   1635    1215 /usr/libexec/gsd-sound
   1636    1215 /usr/libexec/gsd-usb-protection
   1644    1215 /usr/libexec/gsd-wacom
   1647    1215 /usr/libexec/gsd-wwan
   1649    1215 /usr/libexec/gsd-xsettings
   1690    1215 /usr/libexec/gsd-printer
   1707    1482 /usr/libexec/evolution-data-server/evolution-alarm-notify
   1797    1215 /usr/libexec/tracker-miner-fs
   1896    1501 xterm -e htop
   1898    1896 htop
   1971       2 [kworker/1:4-cgroup_destroy]
   1989       2 [kworker/0:4-events]
   2006     794 sshd: atom [priv]
   2140    2006 sshd: atom@pts/1
   2141    2140 -bash
   2151    1482 update-notifier
   2187    2141 htop
   2192    2141 ps -eo pid,ppid,args
```

### Free-H

```bash
atom@virtualbox:~$ free -h
              total        used        free      shared  buff/cache   available
Mem:          1.9Gi       570Mi       688Mi       6.0Mi       712Mi       1.2Gi
Swap:         2.0Gi          0B       2.0Gi
```

### Snaps

![image_7_1](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_7_1.png)

#### Login Screen

![image_7_2](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_7_2.png)

#### Desktop Overview

![image_7_3](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_7_3.png)

![image_7_4](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_7_4.png)

#### System Monitor

![image_7_5](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_7_5.png)

### Tune UI (Optional)

Install UI elements:

```bash
sudo apt install yaru-theme-gtk yaru-theme-icon yaru-theme-sound \
  humanity-icon-theme
```

Verify installation:

```bash
ls /usr/share/themes | grep Yaru
ls /usr/share/icons | grep Yaru
```

Apply:

```bash
gsettings set org.gnome.desktop.interface gtk-theme 'Yaru'
gsettings set org.gnome.desktop.interface icon-theme 'Yaru' # (Humanity|Yaru-dark)
gsettings set org.gnome.desktop.interface cursor-theme 'Yaru'
```

Verify:

```bash
gsettings get org.gnome.desktop.interface gtk-theme
gsettings get org.gnome.desktop.interface icon-theme
gsettings get org.gnome.desktop.interface cursor-theme
```

![image_7_6](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_7_6.png)

---

## 8. Ubuntu Desktop Minimal

### Install X-Server, DM and WM

```bash
sudo apt install -y ubuntu-desktop-minimal
```

```bash
atom@virtualbox:~$ ls /etc/xdg/autostart/
at-spi-dbus-bus.desktop                        org.gnome.SettingsDaemon.Color.desktop               org.gnome.SettingsDaemon.Wacom.desktop
geoclue-demo-agent.desktop                     org.gnome.SettingsDaemon.Datetime.desktop            org.gnome.SettingsDaemon.Wwan.desktop
gnome-initial-setup-copy-worker.desktop        org.gnome.SettingsDaemon.DiskUtilityNotify.desktop   org.gnome.SettingsDaemon.XSettings.desktop
gnome-initial-setup-first-login.desktop        org.gnome.SettingsDaemon.Housekeeping.desktop        print-applet.desktop
gnome-keyring-pkcs11.desktop                   org.gnome.SettingsDaemon.Keyboard.desktop            pulseaudio.desktop
gnome-keyring-secrets.desktop                  org.gnome.SettingsDaemon.MediaKeys.desktop           snap-userd-autostart.desktop
gnome-keyring-ssh.desktop                      org.gnome.SettingsDaemon.Power.desktop               spice-vdagent.desktop
gnome-shell-overrides-migration.desktop        org.gnome.SettingsDaemon.PrintNotifications.desktop  tracker-extract.desktop
gnome-welcome-tour.desktop                     org.gnome.SettingsDaemon.Rfkill.desktop              tracker-miner-fs.desktop
im-launch.desktop                              org.gnome.SettingsDaemon.ScreensaverProxy.desktop    ubuntu-report-on-upgrade.desktop
nm-applet.desktop                              org.gnome.SettingsDaemon.Sharing.desktop             update-notifier.desktop
orca-autostart.desktop                         org.gnome.SettingsDaemon.Smartcard.desktop           user-dirs-update-gtk.desktop
org.gnome.Evolution-alarm-notify.desktop       org.gnome.SettingsDaemon.Sound.desktop               xdg-user-dirs.desktop
org.gnome.SettingsDaemon.A11ySettings.desktop  org.gnome.SettingsDaemon.UsbProtection.desktop

atom@virtualbox:~$ ls /usr/share/xsessions/
ubuntu.desktop
```

### Disk Size

```bash
atom@virtualbox:~$ df -h /
Filesystem                         Size  Used Avail Use% Mounted on
/dev/mapper/ubuntu--vg-ubuntu--lv   15G  6.9G  7.1G  50% /
```

### PS-Tree

```bash
atom@virtualbox:~$ pstree
systemd─┬─ModemManager───2*[{ModemManager}]
        ├─NetworkManager───2*[{NetworkManager}]
        ├─accounts-daemon───2*[{accounts-daemon}]
        ├─acpid
        ├─anacron
        ├─atd
        ├─avahi-daemon───avahi-daemon
        ├─colord───2*[{colord}]
        ├─cron
        ├─cups-browsed───2*[{cups-browsed}]
        ├─cupsd
        ├─dbus-daemon
        ├─gdm3─┬─gdm-session-wor─┬─gdm-x-session─┬─Xorg───{Xorg}
        │      │                 │               ├─gnome-session-b─┬─ssh-agent
        │      │                 │               │                 └─2*[{gnome-session-b}]
        │      │                 │               └─2*[{gdm-x-session}]
        │      │                 └─2*[{gdm-session-wor}]
        │      └─2*[{gdm3}]
        ├─gnome-keyring-d───3*[{gnome-keyring-d}]
        ├─irqbalance───{irqbalance}
        ├─2*[kerneloops]
        ├─multipathd───6*[{multipathd}]
        ├─networkd-dispat
        ├─packagekitd───2*[{packagekitd}]
        ├─polkitd───2*[{polkitd}]
        ├─rsyslogd───3*[{rsyslogd}]
        ├─rtkit-daemon───2*[{rtkit-daemon}]
        ├─snapd───8*[{snapd}]
        ├─sshd───sshd───sshd───bash─┬─htop
        │                           └─pstree
        ├─switcheroo-cont───2*[{switcheroo-cont}]
        ├─systemd─┬─(sd-pam)
        │         ├─at-spi-bus-laun─┬─dbus-daemon
        │         │                 └─3*[{at-spi-bus-laun}]
        │         ├─at-spi2-registr───2*[{at-spi2-registr}]
        │         ├─dbus-daemon
        │         ├─dconf-service───2*[{dconf-service}]
        │         ├─evolution-addre───5*[{evolution-addre}]
        │         ├─evolution-calen───8*[{evolution-calen}]
        │         ├─evolution-sourc───3*[{evolution-sourc}]
        │         ├─gjs───4*[{gjs}]
        │         ├─gnome-session-b─┬─evolution-alarm───5*[{evolution-alarm}]
        │         │                 ├─gsd-disk-utilit───2*[{gsd-disk-utilit}]
        │         │                 ├─update-notifier───3*[{update-notifier}]
        │         │                 └─3*[{gnome-session-b}]
        │         ├─gnome-session-c───{gnome-session-c}
        │         ├─gnome-shell─┬─gnome-system-mo───4*[{gnome-system-mo}]
        │         │             ├─ibus-daemon─┬─ibus-engine-sim───2*[{ibus-engine-sim}]
        │         │             │             ├─ibus-extension-───3*[{ibus-extension-}]
        │         │             │             ├─ibus-memconf───2*[{ibus-memconf}]
        │         │             │             └─2*[{ibus-daemon}]
        │         │             └─12*[{gnome-shell}]
        │         ├─gnome-shell-cal───5*[{gnome-shell-cal}]
        │         ├─gnome-terminal-─┬─htop
        │         │                 └─4*[{gnome-terminal-}]
        │         ├─goa-daemon───3*[{goa-daemon}]
        │         ├─goa-identity-se───2*[{goa-identity-se}]
        │         ├─gsd-a11y-settin───3*[{gsd-a11y-settin}]
        │         ├─gsd-color───3*[{gsd-color}]
        │         ├─gsd-datetime───3*[{gsd-datetime}]
        │         ├─gsd-housekeepin───3*[{gsd-housekeepin}]
        │         ├─gsd-keyboard───3*[{gsd-keyboard}]
        │         ├─gsd-media-keys───3*[{gsd-media-keys}]
        │         ├─gsd-power───3*[{gsd-power}]
        │         ├─gsd-print-notif───2*[{gsd-print-notif}]
        │         ├─gsd-printer───2*[{gsd-printer}]
        │         ├─gsd-rfkill───2*[{gsd-rfkill}]
        │         ├─gsd-screensaver───2*[{gsd-screensaver}]
        │         ├─gsd-sharing───3*[{gsd-sharing}]
        │         ├─gsd-smartcard───4*[{gsd-smartcard}]
        │         ├─gsd-sound───3*[{gsd-sound}]
        │         ├─gsd-usb-protect───3*[{gsd-usb-protect}]
        │         ├─gsd-wacom───2*[{gsd-wacom}]
        │         ├─gsd-wwan───3*[{gsd-wwan}]
        │         ├─gsd-xsettings───3*[{gsd-xsettings}]
        │         ├─gvfs-afc-volume───3*[{gvfs-afc-volume}]
        │         ├─gvfs-goa-volume───2*[{gvfs-goa-volume}]
        │         ├─gvfs-gphoto2-vo───2*[{gvfs-gphoto2-vo}]
        │         ├─gvfs-mtp-volume───2*[{gvfs-mtp-volume}]
        │         ├─gvfs-udisks2-vo───3*[{gvfs-udisks2-vo}]
        │         ├─gvfsd─┬─gvfsd-trash───2*[{gvfsd-trash}]
        │         │       └─2*[{gvfsd}]
        │         ├─gvfsd-fuse───5*[{gvfsd-fuse}]
        │         ├─gvfsd-metadata───2*[{gvfsd-metadata}]
        │         ├─ibus-portal───2*[{ibus-portal}]
        │         ├─ibus-x11───2*[{ibus-x11}]
        │         ├─pulseaudio───3*[{pulseaudio}]
        │         ├─tracker-miner-f───4*[{tracker-miner-f}]
        │         └─xdg-permission-───2*[{xdg-permission-}]
        ├─systemd-journal
        ├─systemd-logind
        ├─systemd-network
        ├─systemd-resolve
        ├─systemd-timesyn───{systemd-timesyn}
        ├─systemd-udevd
        ├─udisksd───4*[{udisksd}]
        ├─unattended-upgr───{unattended-upgr}
        ├─upowerd───2*[{upowerd}]
        ├─whoopsie───2*[{whoopsie}]
        └─wpa_supplicant
```

### PS-ELF

```bash
atom@virtualbox:~$ ps -eo pid,ppid,args
    PID    PPID COMMAND
      1       0 /sbin/init maybe-ubiquity
      2       0 [kthreadd]
      3       2 [rcu_gp]
      4       2 [rcu_par_gp]
      5       2 [kworker/0:0-events]
      6       2 [kworker/0:0H-kblockd]
      7       2 [kworker/u4:0-events_unbound]
      8       2 [mm_percpu_wq]
      9       2 [ksoftirqd/0]
     10       2 [rcu_sched]
     11       2 [migration/0]
     12       2 [idle_inject/0]
     13       2 [kworker/0:1-cgroup_destroy]
     14       2 [cpuhp/0]
     15       2 [cpuhp/1]
     16       2 [idle_inject/1]
     17       2 [migration/1]
     18       2 [ksoftirqd/1]
     19       2 [kworker/1:0-events]
     20       2 [kworker/1:0H-kblockd]
     21       2 [kdevtmpfs]
     22       2 [netns]
     23       2 [rcu_tasks_kthre]
     24       2 [kauditd]
     25       2 [khungtaskd]
     26       2 [oom_reaper]
     27       2 [writeback]
     28       2 [kcompactd0]
     29       2 [ksmd]
     30       2 [khugepaged]
     35       2 [kworker/1:1-events]
     77       2 [kintegrityd]
     78       2 [kblockd]
     79       2 [blkcg_punt_bio]
     80       2 [tpm_dev_wq]
     81       2 [ata_sff]
     82       2 [md]
     83       2 [edac-poller]
     84       2 [devfreq_wq]
     85       2 [watchdogd]
     86       2 [kworker/u4:1-events_unbound]
     88       2 [kswapd0]
     89       2 [ecryptfs-kthrea]
     91       2 [kthrotld]
     92       2 [acpi_thermal_pm]
     93       2 [scsi_eh_0]
     94       2 [scsi_tmf_0]
     95       2 [scsi_eh_1]
     96       2 [scsi_tmf_1]
     97       2 [kworker/u4:2-scsi_tmf_1]
     98       2 [vfio-irqfd-clea]
     99       2 [kworker/u4:3]
    100       2 [kworker/1:1H-kblockd]
    101       2 [ipv6_addrconf]
    110       2 [kstrp]
    113       2 [kworker/u5:0]
    126       2 [charger_manager]
    148       2 [kworker/0:2-cgroup_destroy]
    165       2 [kworker/1:2-events]
    167       2 [scsi_eh_2]
    168       2 [scsi_tmf_2]
    175       2 [cryptd]
    189       2 [kworker/0:1H-kblockd]
    210       2 [irq/18-vmwgfx]
    211       2 [ttm_swap]
    219       2 [kdmflush]
    245       2 [raid5wq]
    290       2 [jbd2/dm-0-8]
    291       2 [ext4-rsv-conver]
    367       1 /lib/systemd/systemd-journald
    396       2 [kworker/0:3-memcg_kmem_cache]
    400       1 /lib/systemd/systemd-udevd
    401       2 [kworker/0:4-events]
    430       2 [iprt-VBoxWQueue]
    602       2 [kaluad]
    603       2 [kmpath_rdacd]
    604       2 [kmpathd]
    605       2 [kmpath_handlerd]
    606       1 /sbin/multipathd -d -s
    617       2 [loop0]
    623       2 [loop1]
    625       2 [loop2]
    627       2 [jbd2/sda2-8]
    628       2 [ext4-rsv-conver]
    629       2 [loop3]
    630       2 [loop4]
    631       2 [loop5]
    646       1 /lib/systemd/systemd-timesyncd
    696       2 [kworker/1:3-cgroup_destroy]
    701       1 /lib/systemd/systemd-networkd
    703       1 /lib/systemd/systemd-resolved
    714       1 /usr/lib/accountsservice/accounts-daemon
    715       1 /usr/sbin/acpid
    716       1 /usr/sbin/anacron -d -q -s
    717       1 avahi-daemon: running [virtualbox.local]
    720       1 /usr/sbin/cupsd -l
    721       1 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
    722       1 /usr/sbin/NetworkManager --no-daemon
    727       1 /usr/sbin/irqbalance --foreground
    728       1 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
    730       1 /usr/lib/policykit-1/polkitd --no-debug
    735       1 /usr/sbin/rsyslogd -n -iNONE
    738       1 /usr/lib/snapd/snapd
    739       1 /usr/libexec/switcheroo-control
    742       1 /lib/systemd/systemd-logind
    743       1 /usr/lib/udisks2/udisksd
    745       1 /sbin/wpa_supplicant -u -s -O /run/wpa_supplicant
    751     717 avahi-daemon: chroot helper
    778       1 /usr/sbin/cups-browsed
    789       1 /usr/sbin/ModemManager
    822       1 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
    834       1 /usr/sbin/cron -f
    838       1 /usr/bin/whoopsie -f
    840       1 /usr/sbin/atd -f
    847       1 /usr/sbin/kerneloops --test
    850       1 /usr/sbin/kerneloops
    859       1 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
    868       1 /usr/sbin/gdm3
    897       1 /usr/libexec/rtkit-daemon
   1106       1 /usr/lib/upower/upowerd
   1109       1 /usr/lib/packagekit/packagekitd
   1262       1 /usr/libexec/colord
   1301     859 sshd: atom [priv]
   1304       1 /lib/systemd/systemd --user
   1305    1304 (sd-pam)
   1310    1304 /usr/bin/pulseaudio --daemonize=no --log-target=journal
   1337    1304 /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
   1439    1301 sshd: atom@pts/0
   1440    1439 -bash
   1450     868 gdm-session-worker [pam/gdm-password]
   1475       1 /usr/bin/gnome-keyring-daemon --daemonize --login
   1479    1450 /usr/lib/gdm3/gdm-x-session --run-script env GNOME_SHELL_SESSION_MODE=ubuntu /usr/bin/gnome-session --systemd --session=ubuntu
   1481    1479 /usr/lib/xorg/Xorg vt2 -displayfd 3 -auth /run/user/1001/gdm/Xauthority -background none -noreset -keeptty -verbose 3
   1489    1479 /usr/libexec/gnome-session-binary --systemd --systemd --session=ubuntu
   1558    1489 /usr/bin/ssh-agent /usr/bin/im-launch env GNOME_SHELL_SESSION_MODE=ubuntu /usr/bin/gnome-session --systemd --session=ubuntu
   1575    1304 /usr/libexec/at-spi-bus-launcher
   1580    1575 /usr/bin/dbus-daemon --config-file=/usr/share/defaults/at-spi2/accessibility.conf --nofork --print-address 3
   1598    1304 /usr/libexec/gnome-session-ctl --monitor
   1606    1304 /usr/libexec/gvfsd
   1613    1304 /usr/libexec/gvfsd-fuse /run/user/1001/gvfs -f -o big_writes
   1631    1304 /usr/libexec/dconf-service
   1635    1304 /usr/libexec/gnome-session-binary --systemd-service --session=ubuntu
   1649    1304 /usr/bin/gnome-shell
   1672    1649 ibus-daemon --panel disable --xim
   1678    1672 /usr/libexec/ibus-memconf
   1679    1672 /usr/libexec/ibus-extension-gtk3
   1683    1304 /usr/libexec/ibus-x11 --kill-daemon
   1688    1304 /usr/libexec/ibus-portal
   1695    1304 /usr/libexec/at-spi2-registryd --use-gnome-session
   1696    1304 /usr/libexec/xdg-permission-store
   1700    1304 /usr/libexec/gnome-shell-calendar-server
   1711    1304 /usr/libexec/evolution-source-registry
   1718    1304 /usr/libexec/goa-daemon
   1721    1304 /usr/libexec/evolution-calendar-factory
   1729    1304 /usr/libexec/gvfs-udisks2-volume-monitor
   1731    1304 /usr/libexec/goa-identity-service
   1743    1304 /usr/libexec/gvfs-goa-volume-monitor
   1750    1304 /usr/libexec/evolution-addressbook-factory
   1752    1304 /usr/libexec/gvfs-mtp-volume-monitor
   1756    1304 /usr/libexec/gvfsd-metadata
   1761    1304 /usr/libexec/gvfs-gphoto2-volume-monitor
   1771    1304 /usr/libexec/gvfs-afc-volume-monitor
   1785    1606 /usr/libexec/gvfsd-trash --spawner :1.14 /org/gtk/gvfs/exec_spaw/0
   1789    1304 /usr/bin/gjs /usr/share/gnome-shell/org.gnome.Shell.Notifications
   1806    1304 /usr/libexec/gsd-a11y-settings
   1807    1304 /usr/libexec/gsd-color
   1808    1304 /usr/libexec/gsd-datetime
   1809    1304 /usr/libexec/gsd-housekeeping
   1810    1304 /usr/libexec/gsd-keyboard
   1811    1304 /usr/libexec/gsd-media-keys
   1813    1304 /usr/libexec/gsd-power
   1821    1304 /usr/libexec/gsd-print-notifications
   1823    1304 /usr/libexec/gsd-rfkill
   1825    1304 /usr/libexec/gsd-screensaver-proxy
   1826    1304 /usr/libexec/gsd-sharing
   1828    1304 /usr/libexec/gsd-smartcard
   1830    1304 /usr/libexec/gsd-sound
   1833    1304 /usr/libexec/gsd-usb-protection
   1838    1304 /usr/libexec/gsd-wacom
   1842    1304 /usr/libexec/gsd-wwan
   1845    1304 /usr/libexec/gsd-xsettings
   1862    1304 /usr/libexec/gsd-printer
   1871    1672 /usr/libexec/ibus-engine-simple
   1899    1635 /usr/libexec/gsd-disk-utility-notify
   1907    1635 /usr/libexec/evolution-data-server/evolution-alarm-notify
   2001    1304 /usr/libexec/tracker-miner-fs
   2161    1635 update-notifier
   2238    1304 /usr/libexec/gnome-terminal-server
   2246    2238 htop
   2247    1649 gnome-system-monitor
   2254    1440 htop
   2258    1440 ps -eo pid,ppid,args
```

### Free-H

```bash
atom@virtualbox:~$ free -h
              total        used        free      shared  buff/cache   available
Mem:          1.9Gi       683Mi       491Mi       7.0Mi       796Mi       1.1Gi
Swap:         2.0Gi          0B       2.0Gi
```

### Snaps

#### Login Screen

![image_8_1](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_8_1.png)

#### Desktop Overview

![image_8_2](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_8_2.png)

![image_8_3](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_8_3.png)

![image_8_4](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_8_4.png)

#### System Monitor

![image_8_5](https://raw.githubusercontent.com/kribakarans/howto/master/src/desktops/res/image_8_5.png)

---
