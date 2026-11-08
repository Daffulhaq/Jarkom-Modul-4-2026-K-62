# Tachibana

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.242.20.138 | /30 | to Wired |
| eth1 | 192.242.3.41 | /30 | to Deus |
| eth2 | 192.242.0.1 | /23 | LAN Collective/Ghost |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.20.138/30 dev eth0
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.3.41/30 dev eth1
ip link set eth2 up
ip addr flush dev eth2
ip addr add 192.242.0.1/23 dev eth2
ip route replace default via 192.242.20.137 dev eth0
ip route replace 192.242.2.0/23 via 192.242.3.42 dev eth1
```
