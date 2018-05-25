# About this

This module contains functions for configure and access the network. Lua RTOS has support for the following network interfaces, each of one identified by it's name:

* en: ethernet interface (SPI or RMII)
* wf: wifi interface

The functions of this module are organized in the following categories:

* [Common functions](#common-functions)
* [Wi-Fi functions](#wi-fi)
* [Ethernet functions](#ethernet)

# Comments about ethernet

Currently only SPI ethernet based on the ENC424J600 chip is supported in Lua RTOS. This is a design decision due to that SPI ethernet only requires 2 dedicated GPIO (chip select, and interrupt) and 3 shared GPIO that correspond to the SPI signals (clk, miso, mosi).

Please, keep in mind that SPI ethernet support is not enabled by default in KConfig. For enable it, follow the following steps:

* Run the config utility.

   ```lua
   make menuconfig
   ```

* Check the SPI pin map, and adapt the map to your needs. This is done under the "Component config -> Lua RTOS -> Hardware -> SPI pin map" category in Kconfig.

   ![](http://git.whitecatboard.org/spi_eth_1.png)

* Enable SPI ethernet support, and adapt de default configuration to your needs. This is done under "Component config -> Lua RTOS -> Hardware -> SPI ethernet" category in Kconfig.

   ![](http://git.whitecatboard.org/spi_eth_2.png)

* Save changes and build.

   ```lua
   make flash
   ```

   Read the following [instructions](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/How-to-build) if you need a complete guide about how to build Lua RTOS.

* Connect the hardware.

   In our tests we use the [Pmod NIC100 module](http://store.digilentinc.com/pmod-nic100-network-interface-controller).

   Proposed connections:

   | ESP32              | Pmid NIC100   |
   |--------------------|---------------|
   | GPIO19 - SPI3 MISO | PIN 3 - MOSI  |
   | GPIO23 - SPI3 MOSI | PIN 2 - MISO  |
   | GPIO18 - SPI3 CLK  | PIN 4 - SCLK  |
   | GPIO26             | PIN 1 - CS    |
   | GPIO21             | PIN 7 - NINT  |
   | VCC (3.3V)         | PIN 6 - VCC   |
   | GND                | PIN 5 - GND   |

# Key concepts

To use this module you must take into consideration the following:

1. Setup the interface.

   ```lua
   -- Setup wifi
   net.wf.setup(...)
   ````

1. Start the interface.

   ```lua
   -- Start wifi
   net.wf.start()
   ````

1. Interact with the network, for example, creating and MQTT client instance and publish some messages.

1. Stop the interface.

   ```lua
   -- Stop wifi
   net.wf.stop()
   ````

# Common functions

## net.connected()

Check if the network is available.

Arguments: nothing.
Returns: true if the network is available, false if is not available, or an exception.

## net.stat([table])

Get the network information for all the available interfaces.

Arguments:

* table: if true, the network information is placed into a Lua table, if false the information is printed on the console.

Returns:

* if table is false: nothing or an exception.

* if table is true: a Lua table with the network information, or an exception. This table is an array of tables. Each entry corresponds to an interface. Each interface gives the following fields:

  * interface: the interface name. In this version only wf interface are returned.
  * ip: interface ip
  * gw: interface gateway ip
  * netmask: interface netmask
  * mac: interface mac address

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

## ip = net.packip(ip1, ip2, ip3, ip4)

Returns packet representation of an IPv4 address that can be used with all 
net's module functions that require an IP address as argument. The IP address is
 provided from the 4 elements that make up an IPv4 address: ip1.ip2.ip3.ip4

Arguments:

* ip1: the first part of the ip address
* ip2: the second part of the ip address
* ip3: the third part of the ip address
* ip4: the fourth part of the ip address

Returns: an integer that encodes the IP address.

```lua
localhost = net.packip(127,0,0,1)
print(localhost)
16777343
```


## ip = net.packip("ip")

Returns a packet representation of an IPv4 address that can be used with all 
net's module functions that require an IP address as argument. The IP address is
 provided as the IPv4 canonical representation.

Arguments:

* ip: the IP addres string in  IPv4 canonical representation

Returns: an integer that encodes the IP address.

```lua
localhost = net.packip("127.0.0.1")
print(localhost)
16777343
```


## ip1, ip2, ip3, ip4 = net.unpackip(ip, '*n')

Returns an unpacked representation of an IPv4 address packed by net.packip 
function. The unpacket representation is provided by the 4 elements that make 
up an IPv4 address.

Arguments:

* ip: the packet IP address

Returns:

* ip1: the first part of the ip address
* ip2: the second part of the ip address
* ip3: the third part of the ip address
* ip4: the fourth part of the ip address

```lua
localhost = net.packip("127.0.0.1")
ip1, ip2, ip3, ip4 = net.unpackip(localhost, '*n')
print(ip1.." "..ip2.." "..ip3.." "..ip4)
127 0 0 1
```


## ip = net.unpackip(ip, '*s')

Returns an unpacked representation of an IPv4 address packed by net.packip 
function. The IP unpacket representation is provided as the IPv4 canonical 
representation.

Arguments:

* ip: the packet IP address

Returns: the IP addres string in  IPv4 canonical representation

```lua
localhost = net.packip("127.0.0.1")
ip = net.unpackip(localhost, '*s')
print(ip)
127.0.0.1
```

## ip = net.lookup(hostname)

Makes a DNS lookup.

Arguments:

* hostname: the hostname to make the lookup

Returns: the packet IP of the hostname.

```lua
ip = net.lookup("whitecatboard.org")
print(net.unpackip(ip, "*s"))
207.148.248.143
```

# Wi-Fi

## net.wf.scan([table])

Performs a wifi scan.

Arguments:

* table: if true, scan is return in a Lua table, if false scan is printed on the console.

Returns:

* if table is false: nothing or an exception.

* if table is true: a Lua table with the scan's result, or an exception. This table is an array of tables. Each entry corresponds to an station. Each station gives the following fields:

   * ssid: access point ssid.
   * rssi: signal rssi.
   * auth: authoritation type. Can be either net.wf.auth.OPEN, net.wf.auth.WEP, net.wf.auth.WPA_PSK, net.wf.auth.WPA2_PSK, or net.wf.auth.WPA_WPA2_PSK.
   * ch1: primary channel of access point
   * ch2: secondary channel of access point

```lua
-- Scan wifi, and print to the console
/ > net.wf.scan()


                           SSID  RSSI          AUTH  CH1  CH2
-------------------------------------------------------------
          Xarxa Wi-Fi de JAUME2   -43      WPA2_PSK    6    0
           Xarxa Wi-Fi de JAUME   -85  WPA_WPA2_PSK   11    0
```

```lua
-- Scan wifi, and get result into a table
scan = net.wf.scan(true)
````

## net.wf.setup(net.wf.mode.STA, ssid, password, [ip, mask, gw, dns1, dns2, powersave, channel, hidden])

Setup wifi interface in STA (station / client) mode.

Arguments:

* ssid: network's ssid to connect.
* password: network's password.
* ip: ip address, in packet representation. Use the net.packip for this.
* mask: network mask, in packet representation. Use the net.packip for this.
* gw: gateway ip, in packet representation. Use the net.packip for this.
* dns1 (optional): ip of the main dns server to use for resolve names, in packet representation. Use the net.packip for this. If this argument is not provided dns1 is set to 8.8.8.8.
* dns2 (optional): ip of the secondry dns server to use for resolve names, in packet representation. Use the net.packip for this. If this argument is not provided dns2 is set to 8.8.4.4.
* power save (optional): power save. Can be either net.wf.powersave.NONE (don't set power save) or net.wf.powersave.MODEM. Default value is net.wf.powersave.NONE.
* channel (optional): 
  - The starting channel number to use to connect to the AP. It's a natural number between 1 and 13. Set to 0 if the AP's channel is unknown.
  - Default value is 0.

Returns: nothing, or an exception.

```lua
-- Setup a wifi connection using a dynamic IP
net.wf.setup(net.wf.mode.STA, "ssid", "password")
```

```lua
-- Setup a wifi connection using a static IP
-- ip: 172.16.209.224
-- net mask: 255.255.0.0
-- gw: 172.16.0.1
-- dns1: 8.8.8.8
-- dns2: 8.8.4.4
net.wf.setup(
   net.wf.mode.STA,
   "ssid",
   "password",
   net.packip(172,16,209,224), net.packip(255,255,255,0),
   net.packip(172,16,0,1),
   net.packip(8,8,8,8), net.packip(8,8,4,4)
)
```

## net.wf.setup(net.wf.mode.AP, [powersave, channel, hidden])

Setup wifi interface in AP (access point) mode.

Arguments:

* ssid: network's ssid to connect.
* password: network's password.
* power save (optional): power save. Can be either net.wf.powersave.NONE (don't set power save) or net.wf.powersave.MODEM. Default value is net.wf.powersave.NONE.
* channel (optional): 
  - The channel number to use by the Soft-AP. It's a natural number between 1 and 13.
  - Default value is 0.
* hidden (optional): If true the SSID is hidden, if false it's visible.

Returns: nothing, or an exception.

## net.wf.start([async])

Start the wifi interface.

Arguments:

* async (optional): if true the interface is started asynchronously (don't wait for getting IP), and if false 
the interface is started synchronously. If not provided, the default value for this argument is true.

Returns: nothing, or an exception.

## net.wf.stop()

Stop the wifi interface.

Arguments: nothing.
Returns: nothing, or an exception.

# Ethernet

## net.en.setup(ip, mask, gw, [dns1, dns2])

Setup an ethernet connection with a fixed ip address.

Arguments:

* ip: ip address, in packet representation. Use the net.packip for this.
* mask: network mask, in packet representation. Use the net.packip for this.
* gw: gateway ip, in packet representation. Use the net.packip for this.
* dns1 (optional): ip of the main dns server to use for resolve names, in packet representation. Use the net.packip for this. If this argument is not provided dns1 is set to 8.8.8.8.
* dns2 (optional): ip of the secondry dns server to use for resolve names, in packet representation. Use the net.packip for this. If this argument is not provided dns2 is set to 8.8.4.4.

Returns: nothing or an exception.

```lua
-- Setup an ethernet connection using a dynamic IP
net.en.setup()
```

```lua
-- Setup an ethernet connection using a static IP
-- ip: 192.168.1.200
-- net mask: 255.255.255.0
-- gw: 192.168.1.1
-- dns1: 8.8.8.8
-- dns2: 8.8.4.4
net.en.setup(
   net.packip(192,168,1,200), net.packip(255,255,255,0),
   net.packip(192,168,1,1),
   net.packip(8,8,8,8), net.packip(8,8,4,4)
)
```

## net.en.setup()

Setup an ethernet connection with a dynamic ip. Connection settings are get from a DHCP server.

Arguments: nothing.

Returns: nothing or an exception.

```lua
-- Setup an ethernet connection
net.en.setup()
```

## net.en.start([async])

Start the ethernet interface.

Arguments:

* async (optional): if true the interface is started asynchronously (don't wait for getting IP), and if false 
the interface is started synchronously. If not provided, the default value for this argument is true.

Returns: nothing or an exception.

```lua
-- Setup an ethernet connection
net.en.setup()

-- Start
net.en.start()
```

## net.en.stop()

Stop the ethernet interface.

Arguments: nothing.

Returns: nothing or an exception.

```lua
-- Setup an ethernet connection
net.en.setup()

-- Start
net.en.start()

....

-- Stop
net.en.stop()
```