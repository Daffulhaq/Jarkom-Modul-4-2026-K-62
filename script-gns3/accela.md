# Accela

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.242.20.170 | /30 | to Schumann |
| eth1 | 192.242.16.1 | /22 | LAN Omnipresence/Denpa |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.20.170/30 dev eth0
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.16.1/22 dev eth1
ip route replace default via 192.242.20.169 dev eth0
```
