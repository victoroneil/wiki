Lua RTOS has support for the following network services:

* [sntp](#sntp)
* [http](#http)
* [Captive DNS](#captive-dns)
* [MDNS](#mdns)

## sntp

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

## http

## Captive DNS

## MDNS