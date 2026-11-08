# Taro

Host di subnet `A17`, gateway `192.242.6.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.6.2/26 dev eth0
ip route replace default via 192.242.6.1 dev eth0
```
