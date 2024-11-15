### Webserver config

#### Question  
On ServerB, configure Apache to serve a basic website that shows the text "Hello World!"

<details><summary> Solution </summary>

1. To update the software packages installed on the system, run:

# dnf update -y

The “-y” flag in the command automatically confirms the installation without prompting for confirmation.

2. To install the Apache HTTP Server on the system, run:

# dnf install httpd -y

3. To enable and start the Apache web server, run:

# systemctl enable --now httpd

The “enable” option is used to enable the “httpd” service so that it starts automatically at system startup, while the “now” option starts the “httpd” service immediately.

4. To open the file “index.html” located in the “/var/www/html/” directory in the Vim text editor, run:

# vim /var/www/html/index.html

5. Add the following line:

Hello World!

6. To restart the Apache web server, run:

# systemctl restart httpd

This command will reload the configuration files for Apache and restart the server, which can be useful after making changes to the configuration files or website content.

7. To list all active firewall rules in the default zone, run:

# firewall-cmd --list-all

8. To add a permanent rule to the firewall configuration to allow incoming HTTP traffic on the public zone, run:

# firewall-cmd --zone=public --add-service=http --permanent

9. To add a permanent rule to the firewall configuration to allow incoming HTTPS traffic on the public zone, run:

# firewall-cmd --zone=public --add-service=https --permanent

Note that this command only modifies the firewall configuration file and does not immediately apply the changes. You need to run the “firewall-cmd --reload” command for the changes to take effect.

10. To reload the firewall configuration, run:

# firewall-cmd --reload

The “--reload” option tells the firewall daemon to read the updated configuration files and apply the changes.

11. To send an HTTP GET request to the local web server running on the system, run:

# curl http://localhost


</details>

Note:

    To serve over HTTPS, Apache needs to be configured with SSL/TLS. This involves generating or obtaining an SSL certificate and configuring Apache to use this certificate for HTTPS connections. If Apache isn’t configured to serve over HTTPS (port 443), you’ll get a “Connection refused” error when trying to access https://localhost/, even if the firewall is correctly configured.

    To resolve this issue, you would need to configure SSL for Apache. This typically involves steps like installing mod_ssl, generating or obtaining an SSL certificate, and configuring your Apache virtual host to use SSL.