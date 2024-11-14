### Network IP update

#### Question

On ServerB, add the following secondary IPV4 address statically to your current running interface. Do this in a way that doesn’t compromise your existing settings:
    IPV4 additional address: 10.0.0.130/14



Overall explanation

1. To display the currently active network connections, run:

# nmcli con sh --active

2. To modify an existing NetworkManager connection "myprofile2" and add an IPv4 address of "10.0.0.3/24" to it, run:

# nmcli con mod myprofile2 +ipv4.addresses 10.0.0.3/24

3. To reload NetworkManager configuration files without restarting the NetworkManager service, run:

# nmcli connection reload

OR

To bring up “myprofile2” network connection, run:

# nmcli con up myprofile2

4. To verify, use the following command to display the details of the network device "enp0s3":

# nmcli dev sh enp0s3

OR use the following command to display the details of the network connection profile named "myprofile2":

# nmcli con sh myprofile2 