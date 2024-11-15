### GRUB2

#### Question
On ServerB, boot messages should be present (not silenced).

<details>

1. Edit the GRUB configuration file using vim.
```
vim /etc/default/grub

In the “GRUB_CMDLINE_LINUX” line, remove “rhgb quiet”
```


2. To generate the “grub.cfg” file, which is the main configuration file for the GRUB2 bootloader, run:
```
# grub2-mkconfig -o /boot/grub2/grub.cfg
```
3. Reboot to verify
```
reboot
```
</details>