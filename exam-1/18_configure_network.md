### Configure network

Question 3

Incorrect?

Configure a NetworkManager connection profile named "myprofile1" on ServerA for the active interface with the following static settings:

    Static IPv4 Address: 192.168.1.2/24
    Static IPv6 Address: fd01::101/64
    IPv4 Default Gateway: 192.168.1.1
    IPv6 Default Gateway: fd01::100
    IPv4 DNS Servers: 8.8.8.8, 8.8.4.4
    IPv6 DNS Server: fd01::111
    DNS Search Domain: example.com

<details><summary>Solution</summary>



1. Create the connection:
```
# nmcli con add con-name myprofile1 ifname ens18 type ethernet
```
2. Set IPv4 and IPv6 settings:
```
# nmcli con mod myprofile1 ipv4.addresses 192.168.1.2/24 
# nmcli con mod myprofile1 ipv4.method manual
# nmcli con mod myprofile1 ipv4.gateway 192.168.1.1
# nmcli con mod myprofile1 ipv4.dns "8.8.8.8 8.8.4.4" 
# nmcli con mod myprofile1 ipv4.dns-search example.com

# nmcli con mod myprofile1 ipv6.addr fd01::101/64
# nmcli con mod myprofile1 ipv6.method manual
# nmcli con mod myprofile1 ipv6.gateway fd01::100
# nmcli con mod myprofile1 ipv6.dns "fd01::111"
# nmcli con mod myprofile1 ipv6.dns-search example.com
```
7. Activate the profile:
```
# nmcli connection up myprofile1
```

Verification:

1. Device and connection status:
```
# nmcli device status
```
2. Profile parameters:
```
# nmcli -p con show myprofile1
```
3. Interface address:
```
# ip address show enp0s3
```
4. Default gateway:
```
# ip route
```
5. DNS settings:
```
# cat /etc/resolv.conf
```
6. Ping test:
```
# ping 192.168.1.3
```

</details>