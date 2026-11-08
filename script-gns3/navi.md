# Navi

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.242.20.134 | /30 | to Wired |
| eth1 | 192.242.4.1 | /24 | LAN Alice/Reika |
| eth2 | 192.242.6.1 | /26 | LAN Taro |
| eth3 | 192.242.5.1 | /24 | LAN Yasuo/Miho/Kuma |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.20.134/30 dev eth0
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.4.1/24 dev eth1
ip link set eth2 up
ip addr flush dev eth2
ip addr add 192.242.6.1/26 dev eth2
ip link set eth3 up
ip addr flush dev eth3
ip addr add 192.242.5.1/24 dev eth3
ip route replace default via 192.242.20.133 dev eth0
```
