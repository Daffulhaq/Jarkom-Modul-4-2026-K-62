# Protocol7

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.242.3.46 | /30 | to Deus |
| eth1 | 192.242.3.49 | /30 | to Knights |
| eth2 | 192.242.2.129 | /26 | LAN Chisa/Hodgeson |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.3.46/30 dev eth0
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.3.49/30 dev eth1
ip link set eth2 up
ip addr flush dev eth2
ip addr add 192.242.2.129/26 dev eth2
ip route replace default via 192.242.3.45 dev eth0
ip route replace 192.242.3.0/26 via 192.242.3.50 dev eth1
ip route replace 192.242.2.192/26 via 192.242.3.50 dev eth1
ip route replace 192.242.3.40/30 via 192.242.3.45 dev eth0
```
