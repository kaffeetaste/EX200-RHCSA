### Network IP update

#### Question 4

On ServerA, add the following secondary IPv4 address statically to the connection profile named "myprofile1".  
Do this in a way that doesn't compromise your existing settings:  

IPv4: 10.0.0.150/14

<details><summary>Solution</summary>


1. Check the active network connection profiles to ensure the current state:
```
# nmcli connection show --active
```
2. Verify the current configuration of the "myprofile1" profile:
```
# nmcli connection show myprofile1
```
3. Add a secondary IP address on "myprofile1":
```
# nmcli connection modify myprofile1 +ipv4.addresses 10.0.0.150/14
```
This command appends the new IPv4 address to the existing ipv4.addresses configuration of the "myprofile1" profile.

4. Bring up the "myprofile1" network connection:
```
# nmcli connection up myprofile1
```
This command reapplies the connection profile, activating the changes. Alternatively, you can reload NetworkManager configuration files without restarting the NetworkManager service:
```
# nmcli con reload
```
5. (Optional) If you encounter issues, consider restarting the NetworkManager service:
```
# systemctl restart NetworkManager
```
However, this is usually not necessary.

6. Verify the new configuration:
```
# nmcli connection show myprofile1
```
Check if the new IP address is listed in the ipv4.addresses section.


<details><summary>Note</summary>
To remove the added IP address, use the following command:
# nmcli connection modify myprofile1 -ipv4.addresses 10.0.0.5/24
Followed by nmcli connection up myprofile1 or nmcli con reload.
</details>
</details>