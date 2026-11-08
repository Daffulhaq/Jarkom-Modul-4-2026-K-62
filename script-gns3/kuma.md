# Kuma

Host di subnet `A18`, gateway `192.242.5.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.5.4/24 dev eth0
ip route replace default via 192.242.5.1 dev eth0
```
