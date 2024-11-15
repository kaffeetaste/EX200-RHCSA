### Set root password

Question 1

You've forgotten the root password for ServerA. Securely reset the root password to regain access to the system. Remember, resetting a root password should only be done as a last resort and strong password practices should be followed after regaining access.

<details><summary>Solution</summary>


1. Reboot the system.

2. On the GRUB 2 boot screen, use the down arrow key to select "Advanced options for Red Hat Enterprise Linux."

3. Select the desired kernel version and press "e" to edit the boot options.

4. Go to the end of the line starting with linux by pressing Ctrl+E.

5. Add rd.break to the end of the linux line. (Optional: Remove any existing console= or vconsole.keymap= options to avoid conflicts)

6. Press Ctrl+X to start the system with the changed parameters.

7. You will be dropped into an emergency shell prompt.

8. Remount the root filesystem as writable with:
```
    mount -o remount,rw /sysroot
```
9. Enter the chroot environment:
```
    chroot /sysroot
```
10. Reset the root password:
```
    passwd root
```
(Set a strong password and avoid using the example password "word" in a real environment) 

11. Enable SELinux relabeling:
```
    touch /.autorelabel
```
    Exit the chroot environment and emergency shell with two Ctrl+D key presses.

    The system will automatically reboot with SELinux performing a relabeling process (this might take some time).
    Once the reboot is complete, you should be able to log in with the newly set root password.


</details>