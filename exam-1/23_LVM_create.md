*** LVM create

**** Question 8

On ServerA, use /dev/sdb to do the following:

1. Create a 2GiB volume group named “myvg”.
2. Create a 500MiB logical volume named “mylv” inside the “myvg” volume group.
3. The “mylv” logical volume should be formatted with the ext4 filesystem and mounted persistently on the "/mylv" directory.
4. Extend the ext4 filesystem on “mylv” by 500M.


<details><summary>Solution</summary>


1. To list information about all available block devices on the system, run:
```
# lsblk
```
2. To create a partition table on the block device "/dev/sdb" using the fdisk utility, run:
```
# fdisk -c /dev/sdb
```
The "-c" option enables compatibility mode, ensuring the partition table is compatible with older operating systems.

- m //For help
- p //print the partition table
- n //new partition
- p //partition type "p" for primary
- 1 //partition number

Press Enter to confirm the default first sector

- +2GiB //Last sector - Type the required value then press Enter
- p //print the partition table
- l //List known partition types
- t // Change a partition type
- 8e //Linux LVM
- p //print the partition table
- w //Write table to disk and exit

3. To list the partition tables for all disk devices attached to the system, run:
```
# fdisk -l
```
4. To initialize the physical volume “/dev/sdb1” for use by LVM to be allowed for use in a volume group (VG), run:
```
$ sudo pvcreate /dev/sdb1
```
5. To display information about the physical volumes that have been configured in the LVM system, run:
```
$ sudo pvs
```
6. To create a new volume group in the LVM (Logical Volume Manager) system, run:
```
$ sudo vgcreate myvg /dev/sdb1
```
7. To display information about the volume groups in the LVM (Logical Volume Manager) system, run:
# vgs


Note: Gb vs GB vs GiB

G or Gb (Gigabit):
Since one byte equals eight bits, a gigabyte equals eight times a gigabit.

GB (Gigabyte):
One GB is 1000³ bytes.

GiB (Gibibyte):
One GiB is 1024³ bytes.


Note: The main difference between G/GB and GiB is the base for calculating the storage capacity. G/GB uses base 10 (decimal) whereas GiB uses base 2 (binary). This means that a storage device advertised as having a capacity of 1 GB can actually have a total of 0.93 GiB due to the difference in the calculation method.

8. To display information about the volume groups in the LVM (Logical Volume Manager) system, run:
```
# vgs
``` 
9. To create a new logical volume within an existing volume group, run:
```
#lvcreate -n mylv -L 500MiB myvg
```
The "-n" option specifies the name of the new logical volume, and the "-L" option specifies the size of the logical volume.

10. To verify, run:
```
# lvs
# vgs
```

Note: Methods to avoid the rounding error:
Method 1: As the physical extents default value is 4MB, and LVM allocates storage in multiples of the physical extent size, you must specify the requested size as an exact multiple of the physical extent size.

Method 2: Find the number of free physical extents in the volume group:
```
# vgdisplay myvg
```
Create the logical volume by entering the volume size in extents rather than bytes:
```
# lvcreate --extents 125 --name mylv myvg
```

Alternatively, you can extend the logical volume to use a percentage of the remaining free space in the volume group. For example:
```
# lvcreate --extents 25%FREE --name mylv myvg
```

11. To display information about the logical volumes that have been created in the LVM system, run:
```
# lvs
```
12. To create a new ext4 file system on “/dev/mapper/myvg-mylv”, run:
```
# mkfs.ext4 /dev/mapper/myvg-mylv
```

13. To create a new directory “/mylv”, run:
# mkdir /mylv

14. To permanently mount the new file sstem, add the following line to /Etc/fstab:
```
/dev/mapper/myvg-mylv /mylv ext4 defaults 0 0
```

15. To mount all file systems specified in the "/etc/fstab" file, run:
```
# mount -a
```

16. To list the available block devices, run:
```
# lsblk
```



17. To display information about the volume groups in the LVM (Logical Volume Manager) system, run:
```
# vgs
```
18. To extend the size of a logical volume “myvg-mylv”, run:
```
# lvextend -r -L +500M /dev/mapper/myvg-mylv
```
The "-r" option is used to resize the file system on the logical volume to match the new size, while the "-L" option specifies the new size of the logical volume.

19. To verify, run:
```
# lvs
```


Note: 
    You can use the “-r” or “--resizefs" option with the “lvextend” command to resize the file system instead of using the “resize2fs” command.
    To shrink the “mylv” logical volume in “myvg” volume group to 500 megabytes, use the following command: 
    ```
    $ sudo lvreduce --resizefs -L 500M myvg/mylv
    ```
    Both lvreduce -r -L 500M vo/myvol and lvresize -r -L -500M vo/myvol is the same.

    Shrinking is not supported on a GFS2 or XFS file system

Note:
    If the logical volume you are reducing contains a file system, I recommend using the “--resizefs” option of the “lvreduce” command to prevent data loss. When using this option, the “lvreduce” command tries to reduce the file system before shrinking the logical volume. If it fails, as it can if the file system is full or does not support shrink, the “lvreduce” command will fail and not attempt to shrink the logical volume.

  </details>