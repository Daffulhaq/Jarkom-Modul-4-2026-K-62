# Konfigurasi per Node - GNS3 CIDR

Prefix root: `192.242.0.0/19`

## Cyberia

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

## Wired

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

## Navi

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

## Tachibana

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

## Deus

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

## Protocol7

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

## Knights

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.242.3.50 | /30 | to Protocol7 |
| eth1 | 192.242.3.53 | /30 | to Phantoma |
| eth2 | 192.242.3.33 | /29 | LAN Eiri (direct) |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.3.50/30 dev eth0
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.3.53/30 dev eth1
ip link set eth2 up
ip addr flush dev eth2
ip addr add 192.242.3.33/29 dev eth2
ip route replace default via 192.242.3.49 dev eth0
ip route replace 192.242.3.0/26 via 192.242.3.54 dev eth1
ip route replace 192.242.2.192/26 via 192.242.3.54 dev eth1
ip route replace 192.242.3.40/30 via 192.242.3.49 dev eth0
ip route replace 192.242.3.44/30 via 192.242.3.49 dev eth0
```

## Phantoma

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

## Shibuya

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

## Psyche

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.242.20.146 | /29 | shared Switch2 |
| eth1 | 192.242.8.1 | /22 | LAN Karl/Lin |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.20.146/29 dev eth0
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.8.1/22 dev eth1
ip route replace default via 192.242.20.145 dev eth0
```

## Copland

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

## Schumann

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

## Accela

| Interface | IP | Prefix | Keterangan |
|---|---|---|---|
| eth0 | 192.242.20.170 | /30 | to Schumann |
| eth1 | 192.242.16.1 | /22 | LAN Omnipresence/Denpa |

```sh
sysctl -w net.ipv4.ip_forward=1
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.20.170/30 dev eth0
ip link set eth1 up
ip addr flush dev eth1
ip addr add 192.242.16.1/22 dev eth1
ip route replace default via 192.242.20.169 dev eth0
```

## JJ

Host di subnet `A12`, gateway `192.242.20.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.20.2/25 dev eth0
ip route replace default via 192.242.20.1 dev eth0
```

## MyuMyu

Host di subnet `A12`, gateway `192.242.20.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.20.3/25 dev eth0
ip route replace default via 192.242.20.1 dev eth0
```

## Alice

Host di subnet `A16`, gateway `192.242.4.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.4.2/24 dev eth0
ip route replace default via 192.242.4.1 dev eth0
```

## Reika

Host di subnet `A16`, gateway `192.242.4.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.4.3/24 dev eth0
ip route replace default via 192.242.4.1 dev eth0
```

## Taro

Host di subnet `A17`, gateway `192.242.6.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.6.2/26 dev eth0
ip route replace default via 192.242.6.1 dev eth0
```

## Yasuo

Host di subnet `A18`, gateway `192.242.5.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.5.2/24 dev eth0
ip route replace default via 192.242.5.1 dev eth0
```

## Miho

Host di subnet `A18`, gateway `192.242.5.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.5.3/24 dev eth0
ip route replace default via 192.242.5.1 dev eth0
```

## Kuma

Host di subnet `A18`, gateway `192.242.5.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.5.4/24 dev eth0
ip route replace default via 192.242.5.1 dev eth0
```

## Collective

Host di subnet `A19`, gateway `192.242.0.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.0.2/23 dev eth0
ip route replace default via 192.242.0.1 dev eth0
```

## Ghost

Host di subnet `A19`, gateway `192.242.0.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.0.3/23 dev eth0
ip route replace default via 192.242.0.1 dev eth0
```

## Lilith

Host di subnet `A20`, gateway `192.242.2.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.2.2/25 dev eth0
ip route replace default via 192.242.2.1 dev eth0
```

## Specter

Host di subnet `A20`, gateway `192.242.2.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.2.3/25 dev eth0
ip route replace default via 192.242.2.1 dev eth0
```

## Chisa

Host di subnet `A21`, gateway `192.242.2.129`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.2.130/26 dev eth0
ip route replace default via 192.242.2.129 dev eth0
```

## Hodgeson

Host di subnet `A21`, gateway `192.242.2.129`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.2.131/26 dev eth0
ip route replace default via 192.242.2.129 dev eth0
```

## Eiri

Host di subnet `A26`, gateway `192.242.3.33`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.3.34/29 dev eth0
ip route replace default via 192.242.3.33 dev eth0
```

## Semi

Host di subnet `A22`, gateway `192.242.3.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.3.2/27 dev eth0
ip route replace default via 192.242.3.1 dev eth0
```

## Lain

Host di subnet `A23`, gateway `192.242.2.193`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.2.194/26 dev eth0
ip route replace default via 192.242.2.193 dev eth0
```

## Mika

Host di subnet `A23`, gateway `192.242.2.193`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.2.195/26 dev eth0
ip route replace default via 192.242.2.193 dev eth0
```

## Karl

Host di subnet `A13`, gateway `192.242.8.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.8.2/22 dev eth0
ip route replace default via 192.242.8.1 dev eth0
```

## Lin

Host di subnet `A13`, gateway `192.242.8.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.8.3/22 dev eth0
ip route replace default via 192.242.8.1 dev eth0
```

## Masayuki

Host di subnet `A14`, gateway `192.242.12.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.12.2/23 dev eth0
ip route replace default via 192.242.12.1 dev eth0
```

## Juri

Host di subnet `A24`, gateway `192.242.14.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.14.2/26 dev eth0
ip route replace default via 192.242.14.1 dev eth0
```

## Omnipresence

Host di subnet `A15`, gateway `192.242.16.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.16.2/22 dev eth0
ip route replace default via 192.242.16.1 dev eth0
```

## Denpa

Host di subnet `A15`, gateway `192.242.16.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.16.3/22 dev eth0
ip route replace default via 192.242.16.1 dev eth0
```

## Akashic

Host di subnet `A25`, gateway `192.242.20.161`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.20.162/29 dev eth0
ip route replace default via 192.242.20.161 dev eth0
```
