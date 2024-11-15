#### Question

On ServerB, modify your active network interface configuration to follow the following specifications statically:

IPv4 address: 10.2.125.203/14  
IPv4 gateway: 10.0.0.1  
DNS: 10.2.107.201  
DNS search domain: phrygix.wz  

\# var1 steht für host  
var1 = \<host\>
neue Zeile\
noch eine
On ServerB, add the following secondary IPV4 address statically to your current running interface. Do this in a way that doesn’t compromise your existing settings: IPV4 additional address: 10.2.125.230/14\
neue Zeile!!!
<details>

```bash
ssh rhcsaB
sudo -i
```

1. Show activa connection:
```bash
$ nmcli con show
NAME   UUID                                  TYPE      DEVICE
ens18  659e5d2e-3c41-378f-b3f6-be4ee151ef04  ethernet  ens18
lo     944a156f-06bc-4942-867e-ea7fdb3a23c7  loopback  lo
```

2. Set ipv4 values as specified:
```bash
nmcli con mod ens18 ipv4.addr 10.2.125.203/14
nmcli con mod ens18 ipv4.gateway 10.0.0.1
nmcli con mod ipv4.dns 10.2.107.201
nmcli con mod ipv4.dns-search phrygix.wz
nmcli con mod ipv4.method manual
```
Alternatively, use nmtui



3. Bring down and up again interface ens18, i.e.

```bash
nmcli con down esn18
nmcli con up ens18
```

4. Verify ipv4 settings
```bash
nmcli con show ens18 | grep ipv4
ipv4.method:                            manual
ipv4.dns:                               10.0.0.1
ipv4.dns-search:                        phrygix.wz
ipv4.dns-options:                       --
ipv4.dns-priority:                      0
ipv4.addresses:                         10.2.125.203/14
ipv4.gateway:                           10.0.0.1
ipv4.routes:                            --
ipv4.route-metric:                      -1
ipv4.route-table:                       0 (unspec)
ipv4.routing-rules:                     --
ipv4.replace-local-rule:                -1 (default)
ipv4.ignore-auto-routes:                no
ipv4.ignore-auto-dns:                   no
ipv4.dhcp-client-id:                    --
ipv4.dhcp-iaid:                         --
ipv4.dhcp-dscp:                         --
ipv4.dhcp-timeout:                      0 (default)
ipv4.dhcp-send-hostname:                yes
ipv4.dhcp-hostname:                     --
ipv4.dhcp-fqdn:                         --
ipv4.dhcp-hostname-flags:               0x0 (none)
ipv4.never-default:                     no
ipv4.may-fail:                          yes
ipv4.required-timeout:                  -1 (default)
ipv4.dad-timeout:                       -1 (default)
ipv4.dhcp-vendor-class-identifier:      --
ipv4.link-local:                        0 (default)
ipv4.dhcp-reject-servers:               --
ipv4.auto-route-ext-gw:                 -1 (default)
```
</details>
