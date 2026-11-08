# Copland

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.242.20.147 | /29 | shared Switch2 |
| eth1 | 192.242.12.1 | /23 | LAN Masayuki |
| eth2 | 192.242.14.1 | /26 | LAN Juri (direct) |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.20.147/29 dev eth0
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.12.1/23 dev eth1
ip link set eth2 up
ip addr flush dev eth2
ip addr add 192.242.14.1/26 dev eth2
ip route replace default via 192.242.20.145 dev eth0
```
