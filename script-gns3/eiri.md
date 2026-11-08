# Eiri

Host di subnet `A26`, gateway `192.242.3.33`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.3.34/29 dev eth0
ip route replace default via 192.242.3.33 dev eth0
```
