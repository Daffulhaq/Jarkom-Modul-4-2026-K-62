# Wired

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.242.20.130 | /30 | to Cyberia |
| eth1 | 192.242.20.137 | /30 | to Tachibana |
| eth2 | 192.242.20.133 | /30 | to Navi |
| eth3 | 192.242.20.145 | /29 | shared Switch2 |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.20.130/30 dev eth0
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.20.137/30 dev eth1
ip link set eth2 up
ip addr flush dev eth2
ip addr add 192.242.20.133/30 dev eth2
ip link set eth3 up
ip addr flush dev eth3
ip addr add 192.242.20.145/29 dev eth3
ip route replace default via 192.242.20.129 dev eth0
ip route replace 192.242.0.0/22 via 192.242.20.138 dev eth1
ip route replace 192.242.4.0/22 via 192.242.20.134 dev eth2
ip route replace 192.242.8.0/22 via 192.242.20.146 dev eth3
ip route replace 192.242.12.0/22 via 192.242.20.147 dev eth3
ip route replace 192.242.16.0/22 via 192.242.20.148 dev eth3
ip route replace 192.242.20.160/28 via 192.242.20.148 dev eth3
```
