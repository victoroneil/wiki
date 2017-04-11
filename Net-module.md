# About this

This module contains functions for configure and access the network.

# Key concepts

Lua RTOS has support for the following network interfaces, each of one identified by it's name:

* en: ethernet interface
* wf: wifi interface

To use this module you must take into consideration the following:

1. Configure the interface, using the interface's setup function.

   ```lua
   -- Setup wifi
   net.wf.setup(...)
   ````

1. Start the interface, using the interface's start function.

   ```lua
   -- Start wifi
   net.wf.start()
   ````

1. Interact with the network, for example, creating and MQTT client instance and publish some messages.

1. Stop the interface, using the interface's stop function.

   ```lua
   -- Stop wifi
   net.wf.stop()
   ````

# Wi-Fi

## net.wf.scan([table])

Performs a wifi scan.

Arguments:

* table: if true, scan is return in a Lua table, if false scan is printed on the console.

Returns:

* if table is false: nothing or an exception.

* if table is true: a Lua table with the scan's result, or an exception. This table is an array of tables. Each entry corresponds to an station. Each station gives the following fields:

   * ssid: station ssid.
   * auth: authoritation type. Can be either net.wf.auth.OPEN, net.wf.auth.WEP, net.wf.auth.WPA_PSK, net.wf.auth.WPA2_PSK, or net.wf.auth.WPA_WPA2_PSK.
   * rssi: signal rssi.

```lua
-- Scan wifi, and print to the console
/ > net.wf.scan()

                           SSID  RSSI          AUTH
---------------------------------------------------
                  MOVISTAR_B450   -46      WPA2_PSK
           Xarxa Wi-Fi de JAUME   -71  WPA_WPA2_PSK
                  MASMOVIL_TVsm   -82  WPA_WPA2_PSK
                    Orange-3A24   -86  WPA_WPA2_PSK
                  MOVISTAR_8B90   -86      WPA2_PSK
                   vodafoneF6A7   -90       WPA_PSK
                  MOVISTAR_C461   -90      WPA2_PSK
                  MOVISTAR_91B0   -91      WPA2_PSK
                  MOVISTAR_C460   -91      WPA2_PSK
                   VodafoneG18F   -94       WPA_PSK
                    Josema_Casa   -94      WPA2_PSK
```

```lua
-- Scan wifi, and get result into a table
scan = net.wf.scan(true)
````

## net.wf.setup(mode, ssid, password)

Setup wifi interface.

Arguments:

* mode: wifi mode. In this version only net.wf.mode.STA (station) is supported.
* ssid: network's ssid to connect.
* password: network's password

Returns: nothing, or an exception.

## net.wf.start()

Start the wifi interface.

Arguments: nothing.
Returns: nothing, or an exception.

## net.wf.stop()

Stop the wifi interface.

Arguments: nothing.
Returns: nothing, or an exception.

# Common functions

## net.stat([table])

Get the network stats for all the available interfaces.

Arguments:

* table: if true, stats are return in a Lua table, if false stats are printed on the console.

Returns:

* if table is false: nothing or an exception.

* if table is true: a Lua table with the scan's result, or an exception. This table is an array of tables. Each entry corresponds to an interface. Each interface gives the following fields:

  * interface: the interface name. In this version only wf interface are returned.
  * ip: interface ip
  * gw: interface gateway ip
  * netmask: interface netmask

```lua
-- Get the network stats to the console
/ > net.stat()
wf: mac address 24:0a:c4:00:c9:5c
   ip address 192.168.1.41 netmask 255.255.255.0
   gw address 192.168.1.1
```

```lua
-- Get the network stats to a table
net.stat(true)
```
