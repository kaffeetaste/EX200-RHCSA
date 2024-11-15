### Persistent hostname

#### Question
On ServerB, change the hostname to rhel.server.test and make it persistent.

<details><summary>#### Solution</summary>

1. To set the hostname of the system to “rhel.server.com”, run:
```
# hostnamectl set-hostname rhel.server.test
```
This command will change the hostname in the “/etc/hostname” file and update the current hostname in the kernel as well. The change will take effect immediately and persist across reboots.

2. To display the current hostname information, run:
```bash
# hostnamectl
```
