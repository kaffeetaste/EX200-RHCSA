### Kernel update

#### Question

On ServerB, install the appropriate kernel update. The following criteria must also be met:
a. The updated kernel is the default kernel when the system is rebooted.
b. The original kernel remains available and bootable on the system.

<details><summary>Solution</summary>

1. Update the installed pacakges on the system:
```
# dnf update -y
```
2. Update the kernel packages:
```
# dnf update kernel -y
```

Updating the kernel can improve system stability, security, and performance, as well as provide support for new hardware and software features.

3. After running this command, the system will typically need to be restarted to use the updated kernel:
```
# reboot
```
</details>