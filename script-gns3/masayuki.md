# Masayuki

Host di subnet `A14`, gateway `192.242.12.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.12.2/23 dev eth0
ip route replace default via 192.242.12.1 dev eth0
```
