### Crontab

#### Question 16

On ServerA, configure a cron job that writes the message "Get Ready!" to the system log file /var/log/messages at noon (12 PM) on weekdays only. Ensure the job is executed with appropriate permissions and logging for troubleshooting.

<details><summary>Solution</summary>
```
ssh rhcsaA
```


1. Access the crontab with root privileges:
```
$ sudo crontab -e
```

2. Append the following cron job entry:

```
00 12 * * 1-5 logger "Get Ready!"
```

OR

```
00 12 * * 1-5 /usr/bin/logger -t "GetReadyCron" "Get Ready!"
```

OR

```
00 12 * * 1-5 /usr/bin/logger -t "GetReadyCron" "Get Ready!" 2>&1 | tee -a /var/log/cron_jobs.log
```


Explanation of the cron job entry:
    00 12: Runs at noon.
    * *: Runs every day of the month and every month.
    1-5: Runs only on weekdays (Monday to Friday).
    /usr/bin/logger: The command to log messages to the system log.
    -t "GetReadyCron": Specifies a tag for the log message, aiding in identification.
    "Get Ready!": The message to be logged.
    2>&1: Redirects both standard output and standard error to standard output.
    tee -a /var/log/cron_jobs.log: Appends the output to a log file for troubleshooting.


3. Verification:
```
$ sudo crontab -l
$ sudo tail -f /var/log/messages
```

</details>