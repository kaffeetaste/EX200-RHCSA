### Show boot messages

#### Question 11

On ServerA, ensure that boot messages are displayed, not silenced, for troubleshooting purposes.

<details><summary>Solution</summary>

```
ssh rhcsaA
```


Method 1: Modify GRUB Configuration File

1. Edit /etc/default/grub
Locate the "GRUB_CMDLINE_LINUX" line and remove "rhgb quiet".

2. Generate a new GRUB configuration file based on the current system configuration:
```
$ sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

3. Restart the system for the changes to take effect:
```
$ sudo reboot
```

Method 2: Update Kernel Command Line

1. Update the kernel command line for the currently running kernel, removing "rhgb" and "quiet":
```
$ sudo grubby --update-kernel=/boot/vmlinuz-$(uname -r) --remove-args="rhgb quiet"
```

This change takes effect upon the next system reboot, altering the boot process display and boot message verbosity.

2. Restart the system for the changes to take effect:
```
$ sudo reboot
```

Note:
- The "rhgb" and "quiet" options in the "GRUB_CMDLINE_LINUX" line control the graphical boot display and the verbosity of boot messages.
- rhgb (Red Hat Graphical Boot): Enables a graphical representation of the boot process, providing a visually appealing experience.
- quiet: Suppresses most kernel and initialization messages, creating a cleaner boot display. Removing it reveals more detailed boot messages, aiding troubleshooting.
- The "rhgb quiet" combination offers a user-friendly boot experience, but removing both options displays detailed messages in a text format. Choose based on the need for a smooth boot or detailed diagnostic information.

</details>