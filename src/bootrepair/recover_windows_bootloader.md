# Windows 10 bootloader recovery

Follow the below instructions to recover Windows bootloader:
1. Boot from the original installation DVD (or the recovery USB)
2. At the Welcome screen, click `Repair your computer`
3. Choose `Troubleshoot`
4. Choose `Command Prompt`
5. When the Command Prompt loads, type the following commands:
	```
	bootrec /fixmbr
	bootrec /fixboot
	bootrec /scanos
	bootrec /rebuildbcd
	```
6. Press `Enter` after each command and wait for each operation to finish
7. Remove the DVD from the disk tray
8. Type `exit` and Hit Enter
9. Restart your computer and check if Windows can now boot

# Weblinks
<https://neosmart.net/wiki/fix-mbr>
