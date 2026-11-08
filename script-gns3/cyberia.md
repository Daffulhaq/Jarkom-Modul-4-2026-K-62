# Cyberia

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.168.122.250 (statis) | /24 | to NAT GNS3 (gateway 192.168.122.1) |
| eth1 | 192.242.20.129 | /30 | to Wired |
| eth2 | 192.242.20.1 | /25 | LAN JJ/MyuMyu |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.168.122.250/24 dev eth0
ip route replace default via 192.168.122.1 dev eth0
echo 'nameserver 8.8.8.8' > /etc/resolv.conf
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.20.129/30 dev eth1
ip link set eth2 up
ip addr flush dev eth2
ip addr add 192.242.20.1/25 dev eth2
ip route replace 192.242.0.0/19 via 192.242.20.130 dev eth1
if command -v iptables >/dev/null 2>&1; then
  iptables -t nat -C POSTROUTING -o eth0 -j MASQUERADE 2>/dev/null || \
  iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
fi
```
