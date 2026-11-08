# Schumann

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.242.20.148 | /29 | shared Switch2 |
| eth1 | 192.242.20.169 | /30 | to Accela |
| eth2 | 192.242.20.161 | /29 | LAN Akashic (direct) |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.20.148/29 dev eth0
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.20.169/30 dev eth1
ip link set eth2 up
ip addr flush dev eth2
ip addr add 192.242.20.161/29 dev eth2
ip route replace default via 192.242.20.145 dev eth0
ip route replace 192.242.16.0/22 via 192.242.20.170 dev eth1
```
