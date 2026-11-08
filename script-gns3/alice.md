# Alice

Host di subnet `A16`, gateway `192.242.4.1`.

```sh
ip link set eth0 up
ip addr flush dev eth0
ip addr add 192.242.4.2/24 dev eth0
ip route replace default via 192.242.4.1 dev eth0
```
