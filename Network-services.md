Lua RTOS has support for the following network services:

* [SNTP](#sntp)
* [HTTP](#http)
* [CAPTIVE DNS](#captive-dns])
* [MDNS](#mdns)

# SNTP

This service can be used by the programmer for get the current time from a NTP server and update the internal Lua RTOS clock with this time.

For start this service:

```lua
-- Setup and start an ethernet connection
net.en.setup()
net.en.start()

-- Sync Lua RTOS clock with an NTP server
net.service.sntp.start()
```

For stop this service:

```lua
net.service.sntp.stop()
```

# HTTP

# CAPTIVE DNS

# MDNS