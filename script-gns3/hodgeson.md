# Hodgeson

Host di subnet `A21`, gateway `192.242.2.129`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.2.131/26 dev eth0
ip route replace default via 192.242.2.129 dev eth0
```
