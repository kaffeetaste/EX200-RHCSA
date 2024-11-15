### LVM

#### Question

On ServerB, use /dev/sdb to do the following:

a) create a 4GiB volume group named “vgmyvg”.  
b) create a 1GiB logical volume named “lvmylv” inside the “vgmyvg” volume group.  
   The “lvmylv” logical volume should be formatted with the ext4 filesystem and mounted persistently on the /lvmylv directory.  
c) Extend the ext4 filesystem on “lvmylv” by 500M.  

<details><summary> Details a)</summary>


1. To list information about all available block devices on the system, run:
```
lsblk
```
2. To create a partition table on the block device "/dev/sdb" using the fdisk utility, run:
```
fdisk -c /dev/sdb
```
The "-c" option enables compatibility mode, which ensures that the partition table is compatible with older operating systems.


- n //new partition
- p //partition type: "p" for primary
- 1 //partition number
-  Press Enter to confirm the first default sector
- +4GiB // Last sector or required size
- l //List known partition types
- t // Change a partition type
- 8e // partition type code
- p //print the partition table
- w //To write the table to disk and exit

- To list all the available disk partitions and their related information, run:
```
fdisk -l
```

3. to display a summary of the physical volumes (PVs) on the system, run:
```
pvs
```
4. To initialize the physical volume “/dev/sdb1” for use by LVM to be allowed for use in a volume group (VG), run:
```
pvcreate /dev/sdb1
```
5. To verify, run:
```
pvs
```
6. To display the attributes of logical volumes and their associated volume groups, run:
```
vgs
```
7. To create a new volume group named "vgmyvg" and to add the physical volume /dev/sdb1 to it, run:
```
vgcreate vgmyvg /dev/sdb1
```
8. To verify, run:
```
vgs
```
9. To display the attributes of logical volumes and their associated volume groups, run:
```
vgs
```

<details><summary> Note: -c Option and DOS-compatibility mode </summary>
I used the “-c” option to turn off the DOS-compatible mode, which I recommended while creating partitions. Because DOS does not allow a partition to start (or end) the middle of a cylinder, it assumes the partition table is corrupt when it sees this and won't boot from any partition on the disk.

Note that
    The “-c” option is used to specify the compatibility mode 'dos' or 'nondos'. The default is the nondos mode.
    For backward compatibility, it is possible to use the option without the mode argument; in that case, the default is used.
</details>
</details>


<details><summary> Details b) </summary>

1. To create a new logical volume named "lvmylv" with a size of 1GiB within the volume group "vgmyvg", run:
```
lvcreate -n lvmylv -L 1GiB vgmyvg
```
2. To list all the logical volumes that are currently available on the system, along with their size, status, and the volume group they belong to, run:
```
lvs
```
3. To create an ext4 filesystem on the logical volume named "lvmylv" that belongs to the volume group named "vgmyvg", run:
```
mkfs.ext4 /dev/mapper/vgmyvg-lvmylv
```
4. To create a new directory “lvmylv”, run:
```
mkdir /lvmylv
```
5. Edit the file system table via /etc/fstab:
Add the following line:
/dev/mapper/vgmyvg-lvmylv /lvmylv ext4 defaults 0 0

6. To mount all the file systems listed in the “/etc/fstab” file that are not mounted yet, run:
```
mount -a
```
7. To list information about all available block devices on the system, run:
```
lsblk
```

8.  To display the attributes of logical volumes and their associated volume groups, run:
```
# vgs
```
</details>

<details><summary> Details c) </summary>

1. To extend the size of the logical volume “/dev/mapper/vgmyvg-lvmylv” by 500 MB and resize the file system to match the new size, run:
```
lvextend -r -L +500M /dev/mapper/vgmyvg-lvmylv
```
The “-r” option is used to automatically resize the file system to match the new size of the logical volume, and the “-L” option is used to specify the new size of the logical volume.

2. To list all the logical volumes that are currently available on the system, along with their size, status, and the volume group they belong to, run:
```
lvs
```

</details>

<details> <summary> Note </summary> 
The “-r” or “--resizefs” option is particularly useful as it saves the extra step of running the “resize2fs” command manually to resize the file system.
To shrink the “mylv” logical volume in “myvg” volume group to 500 megabytes, use the following command:

lvreduce --resizefs -L 500M myvg/mylv

Shrinking is not supported on a GFS2 or XFS file system.

Important
If the logical volume you are reducing contains a file system, I recommend using the “--resizefs” option of the “lvreduce” command to prevent data loss. When using this option, the “lvreduce” command tries to reduce the file system before shrinking the logical volume. If it fails, as it can if the file system is full or does not support shrink, the “lvreduce” command will fail and not attempt to shrink the logical volume.

</details>
