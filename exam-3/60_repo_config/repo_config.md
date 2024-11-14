### Repo Configuration

#### Question


On ServerB, set up a local Yum/DNF repository using the /RHEL-9.iso image mounted on the /repo directory. Ensure the repository is accessible for package installation and updates, and address any potential issues with Red Hat Subscription Management registration.


<details>


Overall explanation

#### 1. Create the mount point:
```bash
$ sudo mkdir /repo
```

#### 2. Mount the ISO image:

##### Option 1: Persistent mounting in fstab (recommended for frequent use):
```bash    
$ su -c 'echo "/RHEL-9.iso /repo iso9660 loop 0 0" >> /etc/fstab'
$ mount -a
```
##### Option 2: Manual mounting for one-time or infrequent use:
```bash
$ sudo mount -o loop /RHEL-9.iso /repo
```

Both approaches are valid, but the "iso9660 loop" option is often explicitly used when dealing with ISO files to make it clear that a loopback device is involved in the mounting process.

#### 3. Configure the repository:
```bash
    $ sudo cp -v /repo/media.repo /etc/yum.repos.d/rhel9.repo
    $ sudo chmod 644 /etc/yum.repos.d/rhel9.repo
    $ sudo vi /etc/yum.repos.d/rhel9.repo
```
Replace the content with:
```
    [InstallMedia-BaseOS]
    name=RHEL 9 - BaseOS
    metadata_expire=-1
    gpgcheck=0
    enabled=1
    baseurl=file:///repo/BaseOS/
     
    [InstallMedia-AppStream]
    name=RHEL 9 - AppStream
    metadata_expire=-1
    gpgcheck=0
    enabled=1
    baseurl=file:///repo/AppStream/
```

#### 4. Clean metadata and cache
```bash
$ sudo dnf clean all
```

#### 5. Address subscription-manager warnings (optional):
```bash
# Optional for cleaning local subscription data
$ sudo subscription-manager clean 
$ sudo vi /etc/yum/pluginconf.d/subscription-manager.conf
Set enabled=0 to suppress warnings if not registered.
```
#### 6. Verify the repository:
```bash
$ sudo dnf repolist 
```
</details>





