# Phantoma

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.242.3.54 | /30 | to Knights |
| eth1 | 192.242.3.57 | /30 | to Shibuya |
| eth2 | 192.242.3.1 | /27 | LAN Semi |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.3.54/30 dev eth0
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.3.57/30 dev eth1
ip link set eth2 up
ip addr flush dev eth2
ip addr add 192.242.3.1/27 dev eth2
ip route replace default via 192.242.3.53 dev eth0
ip route replace 192.242.2.192/26 via 192.242.3.58 dev eth1
```
