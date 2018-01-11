Lua RTOS has support for the following network services:

* [ping](#ping)
* [curl](#curl)
* [scp put](#netscpputhost-port-src-dst-user-password)
* [scp get](#netscpgethost-port-src-dst-user-password)
* [ssh exec](#netsshexechost-port-command-line-user-password)

## net.ping(host)

The net.ping utility is used to test the reachability of a host on an Internet Protocol (IP) network. The host argument is a string with the host name o the host ip address.

```lua
/ > net.ping("whitecatboard.org")
PING whitecatboard.org (5.196.211.36): 32 data bytes
60 bytes from 0.0.0.0: icmp_seq=1 time=37.567 ms
60 bytes from 0.0.0.0: icmp_seq=2 time=36.479 ms
60 bytes from 0.0.0.0: icmp_seq=3 time=36.865 ms
60 bytes from 0.0.0.0: icmp_seq=4 time=36.871 ms
60 bytes from 0.0.0.0: icmp_seq=5 time=36.861 ms
60 bytes from 0.0.0.0: icmp_seq=6 time=36.861 ms
60 bytes from 0.0.0.0: icmp_seq=7 time=36.880 ms
60 bytes from 0.0.0.0: icmp_seq=8 time=36.859 ms
60 bytes from 0.0.0.0: icmp_seq=9 time=36.873 ms
60 bytes from 0.0.0.0: icmp_seq=10 time=36.858 ms
10 packets transmitted, 10 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 36.479/36.897/37.567/0.251 ms
```

```lua
/ > net.ping("8.8.8.8")
PING 8.8.8.8 (8.8.8.8): 32 data bytes
60 bytes from 8.0.0.0: icmp_seq=1 time=27.440 ms
60 bytes from 8.0.0.0: icmp_seq=2 time=27.531 ms
60 bytes from 8.0.0.0: icmp_seq=3 time=27.811 ms
60 bytes from 8.0.0.0: icmp_seq=4 time=27.830 ms
60 bytes from 8.0.0.0: icmp_seq=5 time=27.819 ms
60 bytes from 8.0.0.0: icmp_seq=6 time=27.853 ms
60 bytes from 8.0.0.0: icmp_seq=7 time=27.826 ms
60 bytes from 8.0.0.0: icmp_seq=8 time=27.838 ms
60 bytes from 8.0.0.0: icmp_seq=9 time=27.827 ms
60 bytes from 8.0.0.0: icmp_seq=10 time=27.847 ms
10 packets transmitted, 10 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 27.440/27.762/27.853/0.140 ms
```

Pinging can be interrupted by pressing the Ctrl-c key.

## net.curl

The net.curl utility supports the following functions:

* res, header, body = net.curl.get(url [, filename])
* res, header, body = net.curl.post(url, tparams)
* res, header, resp = net.curl.ftp(upload, url, user, pass [, filename])
* ret, msg = net.s.curl.sendmail(options)
* servername, serverport = net.curl.mailserver([servername, serverport])
* net.curl.cleanup()
* version, versionnum = net.curl.info([showdetails])
* verbose = net.curl.verbose([verbose])
* progress_seconds = net.curl.progress([progress_seconds])
* timeout_seconds = net.curl.timeout([timeout_seconds])
* maxbytes = net.curl.reclimit([maxbytes])

## net.scp.get(host, port, src, dst, user, password)

Transfers the file src from the remote host to the Lua device's file system with the name dst.

```lua
-- Get the file named src-filename.lua
net.scp.get("remotehost",22,"~/lua/src-filename.lua","/examples/lua/dst-filename.lua","username","secretpass")
```

## net.scp.put(host, port, src, dst, user, password)

Transfers the file src from the Lua device's file system to the remote host to the file named dst.

```lua
-- Put the local file named logfile.txt to the remote host
net.scp.get("remotehost",22,"/examples/lua/logfile.txt","~/logs/logfile.txt","username","secretpass")
```

## net.ssh.exec(host, port, command line, user, password)

```lua
-- Execute a command on the remote host
net.ssh.exec("remotehost",22,"cat /foo/bar/secret.txt","username","secretpass")
```