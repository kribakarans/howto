# Recover Ubuntu boot loader with Boot repair tool

Execute below command to recover ubuntu boot partition:
```
curl -s https://raw.githubusercontent.com/kribakarans/bootrepair/master/bootrepair.sh | bash
```

### Install Grub to install Grub
```
sudo grub-install
```

### Re-order boot menu entry
```
efibootmgr # For Linux
    Example: sudo efibootmgr -o 0,1,2,3

bcdedit    # For Windows
```
### Weblinks:
<https://github.com/kribakarans/bootrepair.git><br>
<https://www.youtube.com/watch?v=WVqnfNheRj8><br>
<https://askubuntu.com/questions/485261/change-boot-order-using-efibootmgr>
