### NTP Chrony

#### Question

On ServerB, ensure NTP sync is configured.

<details>
```
ssh rhcsaB
sudo -i
```


1. To view the system clock and time zone settings, run:
```
# timedatectl
```
2. To install the chrony package, run:
```
dnf install chrony -y
```
3. To enable and start the Chrony service immediately, run:
```
# systemctl enable chronyd --now
```
4. To display the contents of the chrony configuration file located at “/etc/chrony.conf”, run:
```
# cat /etc/chrony.conf
```
, to check the configuration file after installation (to check the pool).

5. To enable automatic time synchronization with NTP servers, run:
```
timedatectl set-ntp true
```
</details>