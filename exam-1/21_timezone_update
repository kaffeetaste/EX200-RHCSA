### Time zone update

#### Question 6
On ServerA, configure the system time to the "America/New_York" timezone.

<details><summary>Solution</summary>



1. View the current system clock and timezone settings:
```
$ timedatectl
```
2. List available timezones:
```
$ timedatectl list-timezones
```
3. Show timezones starting with "America/Ne":
```
$ timedatectl list-timezones | grep -o "America/Ne.*"
```
4. Set the timezone to "America/New_York":
```
$ timedatectl set-timezone "America/New_York"
```
5. Verify the changes:
```
$ timedatectl
```
</details>