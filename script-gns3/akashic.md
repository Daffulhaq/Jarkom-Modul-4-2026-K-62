# Akashic

Host di subnet `A25`, gateway `192.242.20.161`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.20.162/29 dev eth0
ip route replace default via 192.242.20.161 dev eth0
```
