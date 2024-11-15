### Webserver config

#### Question  
On ServerB, configure Apache to serve a basic website that shows the text "Hello World!"

<details><summary> Solution </summary>

1. To update the software packages installed on the system, run:
```
# dnf update -y
```

2. To install the Apache HTTP Server on the system, run:
```
# dnf install httpd -y
```

3. To enable and start the Apache web server, run:
```
# systemctl enable --now httpd
```

4. Edit the file index.html located in the “/var/www/html/”:
Add the following line:
Hello World!

5. To restart the Apache web server, run:
```
# systemctl restart httpd
```

6. To list all active firewall rules in the default zone, run:
```
# firewall-cmd --list-all
```

7. To add permanent rules to the firewall configuration to allow incoming HTTP and HTTPS traffic on the public zone and to reload the fierwall configuration, run:
```
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --zone=public --add-service=https --permanent
firewall-cmd --reload
```

8. Verify by running:
```
curl http://localhost
```

</details>

<details><summary> Note: </summary>
Note:
    To serve over HTTPS, Apache needs to be configured with SSL/TLS. This involves generating or obtaining an SSL certificate and configuring..
    Apache to use this certificate for HTTPS connections. If Apache isn’t configured to serve over HTTPS (port 443), you’ll get a “Connection refused”..
     error when trying to access https://localhost/, even if the firewall is correctly configured.

    To resolve this issue, you would need to configure SSL for Apache. This typically involves steps like installing mod_ssl, generating or obtaining an SSL certificate, and configuring your Apache virtual host to use SSL.
</details>
