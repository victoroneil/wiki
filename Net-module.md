# About this

This module contains functions for configure and access the network.

# Network information

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
-- Scan wifi, and print to the console
scan = net.wf.scan(true)
````

# Network configuration

## net.wf.setup(mode, ssid, password)

Setup wifi interface.

Arguments:

* mode: wifi mode. In this version only net.wf.mode.STA (station) is supported.
* ssid: network's ssid to connect.
* password: network's password

Returns: nothing, or an exception.