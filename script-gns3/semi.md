# Semi

Host di subnet `A22`, gateway `192.242.3.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.3.2/27 dev eth0
ip route replace default via 192.242.3.1 dev eth0
```
