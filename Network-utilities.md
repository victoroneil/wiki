Lua RTOS has support for the following network services:

* [ping](#ping)
* [scp](#scp)
* [ssh](#ssh)

# net.ping(host)

The net.ping utility is used to test the reachability of a host on an Internet Protocol (IP) network. The host argument is a string with the host name o the host ip address.

```lua
/ > net.ping("whitecatboard.org")
PING whitecatboard.org (5.196.211.36): 32 data bytes
60 bytes from 8.0.0.0: icmp_seq=1 time=37.531 ms
60 bytes from 8.0.0.0: icmp_seq=2 time=37.398 ms
60 bytes from 8.0.0.0: icmp_seq=3 time=36.807 ms
60 bytes from 8.0.0.0: icmp_seq=4 time=36.844 ms
60 bytes from 8.0.0.0: icmp_seq=5 time=36.829 ms
60 bytes from 8.0.0.0: icmp_seq=6 time=36.830 ms
60 bytes from 8.0.0.0: icmp_seq=7 time=36.854 ms
60 bytes from 8.0.0.0: icmp_seq=8 time=36.816 ms
8 packets transmitted, 8 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 36.807/36.989/37.531/0.277 ms
```

```lua
/ > net.ping("8.8.8.8")
PING 8.8.8.8 (8.8.8.8): 32 data bytes
60 bytes from 8.0.0.0: icmp_seq=1 time=29.351 ms
60 bytes from 8.0.0.0: icmp_seq=2 time=27.406 ms
60 bytes from 8.0.0.0: icmp_seq=3 time=29.815 ms
3 packets transmitted, 3 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 27.406/28.857/29.815/1.044 ms
```

