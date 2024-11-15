### Configure repository

#### Question 2

Configure a Local Yum/DNF Repository on ServerA using the RHEL-9 ISO image mounted on the /mnt directory.

<details><summary>Solution</summary>


1. Mount the RHEL-9 ISO image:

Mount the RHEL-9.iso file to the /mnt directory as a loop device:
```
# mount -o loop RHEL-9.iso /mnt
```
Explanation:
    -o loop: specifies mounting the ISO as a loopback device.
    A loop device treats the ISO like a physical disk.
    Ensure you have the RHEL-9.iso file before proceeding.

2. Optionally make the mount persistent (skip if not needed):
Append the mount command to /etc/fstab to automatically mount the ISO at boot:
```
# echo "/path/to/RHEL-9.iso /mnt iso9660 loop 0 0" >> /etc/fstab
```

  Replace /path/to/RHEL-9.iso with the actual location of the ISO file.

  <details><summary>Notes</summary>
    If you use "iso9660 defaults," the system will apply its default options for mounting ISO9660.
    If you use "iso9660 loop," it explicitly specifies the use of the loopback device for mounting the ISO image.
    Both approaches are valid, but the "iso9660 loop" option is often explicitly used when dealing with ISO files to make it clear that a loopback device is involved in the mounting process.
  </details>

3. Create the local repository file:

Copy the '/mnt/media.repo' file to '/etc/yum.repos.d/rhel9.repo' or create a new '/etc/yum.repos.d/rhel9.repo' file:
```
# cp /mnt/media.repo /etc/yum.repos.d/rhel9.repo
```
This file defines the repository location and settings.

4. Set file permissions:

Set permissions for /etc/yum.repos.d/rhel9.repo to allow reading by all:
```
# chmod 644 /etc/yum.repos.d/rhel9.repo
```
5. Edit the repository file:

Open '/etc/yum.repos.d/rhel9.repo' in a text editor (e.g., vim).

Replace the existing content with the following:

    [InstallMedia-BaseOS]
    name=RHEL 9 - BaseOSmetadata_
    expire=-1
    gpgcheck=0
    enabled=1
    baseurl=file:///mnt/BaseOS/ 
     
    [InstallMedia-AppStream]
    name=RHEL 9 - AppStreammetadata_
    expire=-1
    gpgcheck=0
    enabled=1
    baseurl=file:///mnt/AppStream/

Explanation:
    The file defines two repositories: BaseOS and AppStream.
    metadata_expire=-1 disables metadata expiration checks.
    gpgcheck=0 skips GPG key verification (can be enabled later).
    enabled=1 activates the repository.
    baseurl points to the repository base directories within the mounted ISO.

6. Save and quit the editor.

7. Clean system caches (optional):
Clear the Yum/DNF and subscription-manager cache:
```
# dnf clean all
# subscription-manager clean
```

Note: You might see a "This system is not registered" message. To avoid it, edit /etc/yum/pluginconf.d/subscription-manager.conf and set enabled=0.

8. Verify the repository setup:

List available repositories:
```
# dnf repolist
```

<details>