# Denpa

Host di subnet `A15`, gateway `192.242.16.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.16.3/22 dev eth0
ip route replace default via 192.242.16.1 dev eth0
```
