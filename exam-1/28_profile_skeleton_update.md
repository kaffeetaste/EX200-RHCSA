### Profile skeleton update

#### Question 13

Ensure that a file named "Congrats" is automatically added to the home folders of all new users created on ServerA.

<details><summary>Solution</summary>

1. To achieve this, create a new empty file called "Congrats" in the "/etc/skel" directory using the following command:
```
$ sudo touch /etc/skel/Congrats
```
This creates an empty file named "Congrats" in the "/etc/skel" directory, which serves as a template for new user home directories.


2. Verify file permissions (optional):
```
$ sudo chmod 644 /etc/skel/Congrats
```

This ensures that the file has appropriate read permissions for new users.