### Set up a basic web server

#### Question 9

Set up a basic web server on ServerA to display the message "Welcome to the webserver!" upon connection, while ensuring that the firewall allows http/https services.


<details><summary>Solution</summary>

```
$ssh rhcsaA
$sudo -i
```


To configure a basic web server on ServerA and allow http/https services through the firewall, follow these steps:

1. Install the Apache Server by running the following command:
```
# dnf install httpd -y
```
2. Enable Apache service to start automatically during system boot:
```
# systemctl enable httpd
```
3. Start Apache service:
```
# systemctl start httpd
```
4. Check Apache service status:
```
$ systemctl status httpd
```
5. Edit the "index.html" file located in the "/var/www/html/" directory and enter the line
```
"Welcome to the webserver!"
```

6. Restart the httpd service to apply the changes:
```
# systemctl restart httpd
```

7. Display a list of all active zones and their associated firewall rules in the firewalld service:
```
# firewall-cmd --list-all
```
8. List all available services in the firewall:
```
#firewall-cmd --get-services
```
9. Add a permanent firewall rule to allow incoming traffic to the HTTP service:
```
# firewall-cmd --zone=public --add-service=http --permanent
```
10. Add a permanent firewall rule to allow incoming traffic to the HTTPS service:
```
# firewall-cmd --zone=public --add-service=https --permanent
```
11. Reload the firewall configuration:
```
# firewall-cmd --reload
```

12. Display a list of all active zones and their associated firewall rules again:
```
# firewall-cmd --list-all
```
13. Perform a simple HTTP request to the web server running on the local machine using curl:
```
$ curl http://localhost
```
</details>