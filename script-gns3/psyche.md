# Psyche

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.242.20.146 | /29 | shared Switch2 |
| eth1 | 192.242.8.1 | /22 | LAN Karl/Lin |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.20.146/29 dev eth0
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.8.1/22 dev eth1
ip route replace default via 192.242.20.145 dev eth0
```
