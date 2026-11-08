# Lin

Host di subnet `A13`, gateway `192.242.8.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.8.3/22 dev eth0
ip route replace default via 192.242.8.1 dev eth0
```
