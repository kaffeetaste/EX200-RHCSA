### Configure their permissions for specific directories

#### Question 15

Create the following users and groups on ServerA, configure their permissions for specific directories, 
and ensure appropriate file ownership for newly created files.


Users:
  - amr and biko (members of the "admins" group)
  - carlos and david (members of the "developers" group)

Directories:
    /admins (accessible only to owner and admins group members, owned by biko)
    /developers (accessible only to developers group members, owned by carlos)

File Ownership:
    New files in /developers or /admins should be owned by the respective group owner.
    Only file creators should be allowed to delete their files.


<details><summary>Solution</summary>

1. Create users and groups:
```
$ sudo groupadd admins
$ sudo groupadd developers
```


2. Create users and add them to groups
```
$ sudo useradd amr
$ sudo usermod -aG admins amr
$ sudo useradd biko 
$ usermod -aG admins biko
$ sudo useradd carlos
$ usermod -aG developers carlos
$ sudo useradd david
$ usermod -aG developers david
```

2. Create and configure directories:
```
$ sudo mkdir /admins
$ sudo mkdir /developers
```

3. Set ownership and permissions for /admins
```
$ sudo chown biko:admins /admins
$ sudo chmod 770 /admins  
$ sudo chmod +t /admins
$ sudo chmod g+s /admins
```

4. Set ownership and permissions for /developers
```
$ sudo chown carlos:developers /developers
$ sudo chmod 770 /developers 
$ sudo chmod +t,g+s /developers 
```

Explanation:
    chmod 770 sets read, write, and execute permissions for the owner and group, while removing all access for others.
    chmod +t sets the sticky bit, ensuring only file owners or root can delete files.
    chmod g+s sets the setgid bit, making newly created files inherit the group ownership of the directory.


To verify:
    Use id <username> to verify user and group memberships.
    Use ls -ld <directory> to view directory permissions.

</details>
