# Mika

Host di subnet `A23`, gateway `192.242.2.193`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.2.195/26 dev eth0
ip route replace default via 192.242.2.193 dev eth0
```
