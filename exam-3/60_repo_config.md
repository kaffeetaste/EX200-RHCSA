### 60. Repo Configuration

#### Question

On ServerB, set up a local Yum/DNF repository using the /RHEL-9.iso image mounted on the /repo directory. Ensure the repository is accessible for package installation and updates, and address any potential issues with Red Hat Subscription Management registration.

<details>

```bash
ssh rhcsaB
sudo -i
```

1. Create the mount point and mount the iso image from /RHEL-9.iso
```
mkdir /repo
mount -o loop /RHEL-9.iso /repo

Alternatively, mount persistantly via /etc/fstab:
echo "/RHEL-9.iso /repo iso9660 loop 0 0" >> /etc/fstab
```


2. Configure the repository:

```bash
    cp -v /repo/media.repo /etc/yum.repos.d/rhel9.repo
    chmod 644 /etc/yum.repos.d/rhel9.repo
    vi /etc/yum.repos.d/rhel9.repo
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


3. Clean metadata and cache:
```bash
dnf clean all
```

4. Address subscription-manager warnings (optional):
```bash
# Optional for cleaning local subscription data
subscription-manager clean 
vi /etc/yum/pluginconf.d/subscription-manager.conf
(set enabled=0 to suppress warnings if not registered.)
```

5. Verify the repository:
```bash
dnf repolist 
```
</details>





