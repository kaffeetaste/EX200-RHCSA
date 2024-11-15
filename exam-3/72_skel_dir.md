### Skel dir

#### Task
On ServerB, all new users should have a file name “Note” in their home directory after account creation.

<details><summary>Solution</summary>

To create a new empty file called "Note" in the “/etc/skel” directory, run:
```
# touch /etc/skel/Note
```
The “/etc/skel” directory is used as a template directory for creating new user accounts on a Linux system. Any files placed in this directory will be copied to the home directory of new users when their accounts are created.

</details>