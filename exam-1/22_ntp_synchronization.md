### NTP synchronization

#### Question 7

On ServerA, ensure NTP synchronization is configured for accurate timekeeping.


<details><summary>Solution</summary>

```
ssh rhcsaA
sudo -i
```

1. View the current system clock and timezone:
Run timedatectl to view the system clock and check if "NTP is set to: yes".
```
$ timedatectl
```
2. Install "chrony":
```
# dnf install chrony -y
```

3. Start and enable the "chronyd" service:
```
# systemctl enable chronyd --now
``` 
4. Display the contents of the "chrony.conf" configuration file:
```
$ cat /etc/chrony.conf
```
Note: This step is optional and is used to check the configuration file after installation (to check the pool).

5. Enable Network Time Protocol (NTP) synchronization:
```
$ timedatectl set-ntp true
```
Note: NTP is essential for accurate timekeeping on a Linux system and crucial for logging, debugging, and authentication tasks.

6. Verify the changes:
```
$ timedatectl
```

Procedure to Install and Configure the NTP Server and Client Using Chrony:

Test environment:

- NTP Server - ntp201 (10.2.123.201)
- NTP Server - ntp202 (10.2.123.202)
- NTP Server - ntp203 (10.2.123.203)
- NTP Server - ntp204 (10.2.123.204)


Install Chrony in RHEL:

1. Install the chrony suite:
```
$ sudo dnf install chrony
```
Note: The chrony suite includes chronyd and chronyc.

2. Start the chronyd service and enable it to auto-start at system boot:
```
$ sudo systemctl enable --now chronyd
```
3. Verify the running status of the chronyd service:
```
$ systemctl status chronyd
```

Configure the NTP Server Using Chrony (Off-topic)
Procedure to set up your RHEL NTP server as a master NTP time server.

1. Edit  /etc/chrony.conf configuration file
Look for the allow configuration directive uncomment it and set its value to the network or subnet address from which the clients are allowed to connect:
```
allow 10.0.0.0/14
```

2. Restart the chronyd service to apply the recent changes:
```
# systemctl restart chronyd
```
3. Open access to the NTP service in firewalld configuration to allow incoming NTP requests from clients:
```
# firewall-cmd --permanent --add-service=ntp
```
To reload the firewall rules that use the firewalld firewall management system, run:
```
# firewall-cmd --reload
```

Configure the NTP Client Using Chrony (On-topic):
1. Install the chrony package:
```
$ sudo dnf install chrony -y
```
2. Start and enable the chronyd service:
```
$ sudo systemctl enable --now chronyd
```
3. Verify the running status of the chronyd service:
```
$ systemctl status chronyd
```
4. Configure the system as a direct client of the NTP server. Edit the "/etc/chrony.conf" file:
Comment out the default NTP servers.
Specify the NTP servers your client-server should ask for the current time using the server directive:
server 10.2.123.201

Note: You can add the `iburst` option to allow chronyd to make the first update of the clock sooner. For example: `server 192.168.69.10 iburst`.

5. Restart the chronyd service:
```
$ sudo systemctl restart chronyd
```
9. Show the current time sources:
```
$ chronyc sources
```
10. Display information about NTP clients accessing the NTP server:
```
$ sudo chronyc clients
```
</details>