### User add by id

#### Tasks

On ServerB, create a user sam whose UID is 1500, and he doesn't have access to any interactive shell on the system.

<details><summary>Solution</summary>



1. To create a new user account named "sam" with the specified user ID "1500" and shell "/sbin/nologin", run:
```
# useradd -u 1500 -s /sbin/nologin sam
```
2. To display the user and group ID of the user "sam", run:
```
# id sam
```
3. To verify, try switching to the user sam account by opening a new shell session with sam's environment settings:
```
# su - sam
```

Also, you can show the last line in the /etc/passwd file by running:
```
# tail -1 /etc/passwd 
```
</details>