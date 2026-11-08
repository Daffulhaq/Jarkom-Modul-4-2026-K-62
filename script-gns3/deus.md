# Deus

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.242.3.42 | /30 | to Tachibana |
| eth1 | 192.242.3.45 | /30 | to Protocol7 |
| eth2 | 192.242.2.1 | /25 | LAN Lilith/Specter |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.3.42/30 dev eth0
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.3.45/30 dev eth1
ip link set eth2 up
ip addr flush dev eth2
ip addr add 192.242.2.1/25 dev eth2
ip route replace default via 192.242.3.41 dev eth0
ip route replace 192.242.2.0/23 via 192.242.3.46 dev eth1
```
