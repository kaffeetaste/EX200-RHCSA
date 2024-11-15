### IPv6 assignment

#### Question 5

On ServerA, include the following secondary IPv6 address statically to the connection profile named "myprofile1". Do this in a way that doesn't compromise your existing settings:

IPv6: fd01::121/64


<details><summary>Solution</summary>


```
$ ssh rhcsaA
$ sudo -i
```


To add a secondary IPv6 address to an existing NetworkManager connection profile without affecting other settings, follow these steps:

1. Verify IPv6 is Enabled:
Check the system's IPv6 status:
```
$ ip a
```
Look for an IPv6 address assigned to your network interface.

- Verify IPv6 is not disabled in kernel parameters:
```
$ sudo sysctl -a | grep ipv6.*disable
```
A value of 0 indicates IPv6 is enabled.


<details><summary>Note </summary>
    The "sysctl" command manipulates kernel parameters at runtime, and the "-a" option displays all kernel parameters.
    The "grep" command filters the output for lines containing the words "ipv6" and "disable".
    IPv6 is enabled by default on RHEL 9.
</details>

2. Add Secondary IPv6 Address:
Modify the "myprofile1" connection profile:
```
$ nmcli connection modify myprofile1 +ipv6.addresses fd01::121/64
```

3. Apply Changes:
Reload NetworkManager configuration:
```
$ nmcli con reload
```
Alternatively, you can restart NetworkManager, but this is generally not necessary:
```
$ systemctl restart NetworkManager
```

4. Verify New Configuration:
Check the updated profile:
```
$ nmcli connection show myprofile1
```
Verify the new IPv6 address is listed in the ipv6.addresses section.
</details>