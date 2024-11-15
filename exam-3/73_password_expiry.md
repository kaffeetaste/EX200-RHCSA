### Password expiry

#### Tasks

On ServerB, all user passwords should expire after 100 days and be at least 9 characters in length.


<details><summary>Solution</summary>

(RHEL 9)

1. To edit the system-wide configuration file for login-related settings, edit /etc/login.defs: 
   Change PASS_MAX_DAYS to 100

2. To edit the password quality configuration file, edit /etc/security/pwquality.conf:
    Set minlen to 9

</details>