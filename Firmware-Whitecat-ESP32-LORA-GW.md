![](http://git.whitecatboard.org/gw-1.png)

## Included features

<table><tbody>
<tr><td>File systems</td><td>LFS, RAMFS.</td></tr>
<tr><td>Lua modules</td><td>cjson, cpu, event, fs, lora, mqtt, net, nvs, pack, socket, spi, thread, tmr.</td></tr>
<tr><td>Networking</td><td>RMII Ethernet, WiFi.</td></tr>
<tr><td>Network services</td><td>Captive DNS, Dropbear SSH server, HTTP server, SNTP.</td></tr>
</tbody></table>

## Hardware mapping

| CAN | Signal | GPIO |
|--------|--------|------|
| 0 | RX<br/>TX | GPIO35<br/>GPIO25 |

| I2C | Signal | GPIO |
|--------|--------|------|
| 0 | SCL<br/>SDA | GPIO32<br/>GPIO33 |
| 1 | SCL<br/>SDA | GPIO2<br/>GPIO15 |

| SPI | Signal | GPIO |
|--------|--------|------|
| 2 | MISO<br/>MOSI<br/>CLK | GPIO12<br/>GPIO13<br/>GPIO14 |
| 3 | MISO<br/>MOSI<br/>CLK | GPIO19<br/>GPIO23<br/>GPIO18 |

| UART | Signal | GPIO |
|--------|--------|------|
| 0 | RX<br/>TX | GPIO3<br/>GPIO1 |
| 1 | RX<br/>TX | GPIO26<br/>GPIO25 |
| 2 | RX<br/>TX | GPIO2<br/>GPIO15 |

|  RMII  | Signal | GPIO |
|--------|--------|------|
| 0 | TXD0<br/>TXD1<br/>TX_EN<br/>RXD0<br/>RXD1<br/>CLK<br/>MDC<br/>MDIO<br/>POWER | GPIO19<br/>GPIO22<br/>GPIO21<br/>GPIO25<br/>GPIO26<br/>GPIO0<br/>GPIO23<br/>GPIO18<br/>GPIO2 |
