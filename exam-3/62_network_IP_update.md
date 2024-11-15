### Network IP update

#### Question

On ServerB, add the following secondary IPV4 address statically to your current running interface. Do this in a way that doesn’t compromise your existing settings:
    IPV4 additional address: 10.2.125.230/14

<details>

```bash
ssh rhcsaB
sudo -i
```

~~durchgestrichener Text ~~

1. Display active connection
```bash
nmcli con show --active
```

2. Add ipv4 address
```
nmcli con mod ens18 +ipv4.addr 10.2.125.230/14
```

3. Reload the Network manager with new settings
```
nmcli con reload
nmcli con up ens18
```

4. Verify
```
nmcli con show ens18 | grep ipv4
```

</details>
