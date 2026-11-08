# Ghost

Host di subnet `A19`, gateway `192.242.0.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.0.3/23 dev eth0
ip route replace default via 192.242.0.1 dev eth0
```
