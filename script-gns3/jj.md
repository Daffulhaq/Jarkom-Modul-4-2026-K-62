# JJ

Host di subnet `A12`, gateway `192.242.20.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.20.2/25 dev eth0
ip route replace default via 192.242.20.1 dev eth0
```
