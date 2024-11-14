### Repo Configuration

#### Question


On ServerB, set up a local Yum/DNF repository using the /RHEL-9.iso image mounted on the /repo directory. Ensure the repository is accessible for package installation and updates, and address any potential issues with Red Hat Subscription Management registration.


<details>


Overall explanation

#### 1. Create the mount point and mount the iso:
```bash
$ sudo mkdir /repo
$ sudo mount -o loop /RHEL-9.iso /repo
```

#### 2. Configure the repository:
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

#### 3. Clean metadata and cache
```bash
$ sudo dnf clean all
```

#### 4. Address subscription-manager warnings (optional):
```bash
# Optional for cleaning local subscription data
$ sudo subscription-manager clean 
$ sudo vi /etc/yum/pluginconf.d/subscription-manager.conf
Set enabled=0 to suppress warnings if not registered.
```
#### 5. Verify the repository:
```bash
$ sudo dnf repolist 
```
</details>





