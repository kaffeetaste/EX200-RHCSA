Repo config

Question





<details>

```bash
podman network create my-net

podman volume create my-db-vol
podman volume create my-app-vol

podman run -d \
--name wordpress-db \
--network my-net \
-v my-db-vol:/var/lib/mysql:Z \
-e MYSQL_ROOT_PASSWORD=mypass \
-e MYSQL_PASSWORD=mypass \
-e MYSQL_DATABASE=wordpress_db \
-e MYSQL_USER=dbuser \
docker.io/mariadb:latest

podman run -d \
--name wordpress-app \
--network my-net \
-v my-app-vol:/var/www/html:Z \
-p 8004:80 \
-e WORDPRESS_DB_HOST=wordpress-db:3306 \
-e WORDPRESS_DB_NAME=wordpress_db \
-e WORDPRESS_DB_USER=dbuser \
-e WORDPRESS_DB_PASSWORD=mypass \
docker.io/wordpress:latest
```

</details>


On ServerB, set up a local Yum/DNF repository using the /RHEL-9.iso image mounted on the /repo directory. Ensure the repository is accessible for package installation and updates, and address any potential issues with Red Hat Subscription Management registration.


Overall explanation

1. Create the mount point:

$ sudo mkdir /repo


2. Mount the ISO image:


Option 1: Persistent mounting in fstab (recommended for frequent use):

    $ su -c 'echo "/RHEL-9.iso /repo iso9660 loop 0 0" >> /etc/fstab'
    $ mount -a


Option 2: Manual mounting for one-time or infrequent use:

$ sudo mount -o loop /RHEL-9.iso /repo


Note that

    The entry specifies the mount point (/repo), the file system type (iso9660), the mount options (defaults), and the dump and file system check options (0 0).

    This enables the system to automatically mount the ISO file to the specified mount point (/repo) during system boot.

    If you use "iso9660 defaults," the system will apply its default options for mounting ISO9660.

    If you use "iso9660 loop," it explicitly specifies the use of the loopback device for mounting the ISO image.

    Both approaches are valid, but the "iso9660 loop" option is often explicitly used when dealing with ISO files to make it clear that a loopback device is involved in the mounting process.


3. Configure the repository:

    $ sudo cp -v /repo/media.repo /etc/yum.repos.d/rhel9.repo
    $ sudo chmod 644 /etc/yum.repos.d/rhel9.repo
    $ sudo vi /etc/yum.repos.d/rhel9.repo


Replace the content with:

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


4. Clean metadata and cache:

$ sudo dnf clean all


5. Address subscription-manager warnings (optional):

$ sudo subscription-manager clean # Optional for cleaning local subscription data


$ sudo vi /etc/yum/pluginconf.d/subscription-manager.conf

Set enabled=0 to suppress warnings if not registered.


6. Verify the repository:

$ sudo dnf repolist 
