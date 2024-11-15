### Password expiration

#### Question 14

Enforce password expiration after 90 days and a minimum length of 8 characters for all user passwords on ServerA.

<details><summary>Solution</summary>

(RHEL 9)

1. Edit the system-wide configuration file /etc/login.defs for login-related settings and change the line
Change the seetings for PASS_MAX_DAYS to 90:
```
PASS_MAX_DAYS 90 
```

2. Edit the file /etc/security/pwquality.conf and set minlen to 8:
```
minlen = 8
```


Note:
- In RHEL 9, the parameters [PASS_MIN_LEN, PASS_MAX_LEN, PASS_CHANGE_TRIES, PASS_ALWAYS_WARN] in "/etc/login.defs" are not supported.
- Instead, in RHEL 9, use "/etc/security/pwquality.conf" to set the password minimum length using the `minlen` variable.
- "pwquality.conf" allows configuring default password quality requirements for system passwords. It is utilized by the "libpwquality" library and associated utilities for password checks and generation.

- Refer to the manual page for comprehensive details on the "pwquality.conf" file.

- These changes will only affect newly created or changed passwords. To force immediate expiration of existing passwords, use the chage command: 

```
$ sudo chage -M 0 <username>
```
</details>