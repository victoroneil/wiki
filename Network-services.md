Lua RTOS has support for the following network services:

* [SNTP](#sntp)
* [HTTP](#http)
* [Captive DNS](#captive-dns)
* [MDNS](#mdns)

## SNTP

This service can be used by the programmer for get the current time from a NTP server and update the internal Lua RTOS clock with this time.

**For start this service:**

```lua
-- Setup and start an ethernet connection
net.en.setup()
net.en.start()

-- Sync Lua RTOS clock with an NTP server
net.service.sntp.start()
```

The net.service.sntp.start accepts an optional argument to set the NTP server name to use. If this argument is not provided the NTP server name is set to "pool.ntp.org".

**For stop this service:**

   ```lua
   net.service.sntp.stop()
   ```

## HTTP

This service can be started to serve files via the http:// protocol.
For security reasons the document root is configured at compile time.
If a http request doesn't point to a file but a directory then that directory is searched for a file named index.lua or index.html If one of those is found the file is served, if none is found a directory listing is generated.
If a file is requested that ends on .lua then that file is being executed before it is served to the client.

**To start this service:**

```lua
-- Setup and start an ethernet connection
net.en.setup()
net.en.start()

-- Start HTTP server
net.service.http.start()

-- Start the HTTP server on a non-standard port
net.service.http.start(81)

-- Start the HTTP Server with HTTPS on port 443
net.service.http.start(80, 443, "/path/to/certificate.pem", "/path/to/privatekey.pem")

-- Start the HTTP Server with HTTPS on port 443 but do not serve HTTP
net.service.http.start(0, 443, "/path/to/certificate.pem", "/path/to/privatekey.pem")
```

**To stop this service:**

```lua
net.service.http.stop()
```

## Captive DNS

This service can be started to serve fake DNS answers to queries from other devices. That is useful if the Lua RTOS device creates a wifi AP and clients need to connect to the device e.g. to configure the actual wifi settings via a web browser. The Captive DNS service helps by automatically redirecting all name resolution to the Lua RTOS device's local ip in the same way as standard Captive Wifi logon portals do. Instead of providing a website with an "accept" button as usual captive portals (do for legal reasons) the Lua RTOS device can use the HTTP service with lua scripts to e.g. present a Lua RTOS device configuration form. For most operating systems the form will open automatically on the client device once it has connected to the AP.

**To start this service:**

```lua
-- Setup and start an ethernet connection
net.en.setup()
net.en.start()

-- Start HTTP server
net.service.http.start()

-- Start the Captive DNS service
net.service.captivedns.start()
```

**To stop this service:**

```lua
net.service.captivedns.stop()
```

## MDNS

This service adds support for Multicast DNS.

net.service.mdns.start([hostname [, instancename]])

**To start this service:**

```lua
net.service.mdns.start("ESP32")
```

**To stop this service:**

```lua
net.service.mdns.stop()
```

**To find a device by hostname:**

```lua
results = net.service.mdns.resolvehost(hostname [, timeout_seconds])
```

**To find a device by service type:**

```lua
service = "_http"
protocol = "_tcp"
results = net.service.mdns.findservice(service, protocol [, timeout_seconds])
```

**To make the Lua RTOS device itself advertise a service:**

```lua
service = "_http"
protocol = "_tcp"
port = 80
instancename = "ESP WebServer"
net.service.mdns.addservice(service, protocol, port [, instancename [, txt_table]])
```

**To make the Lua RTOS device itself no longer advertise a previously added service:**

```lua
service = "_http"
protocol = "_tcp"
net.service.mdns.removeservice(service, protocol)
```
