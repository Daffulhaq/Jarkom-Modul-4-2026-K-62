# Shibuya

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.242.3.58 | /30 | to Phantoma |
| eth1 | 192.242.2.193 | /26 | LAN Lain/Mika |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.3.58/30 dev eth0
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.2.193/26 dev eth1
ip route replace default via 192.242.3.57 dev eth0
```
