![](http://git.whitecatboard.org/whitecatn1.png)

## Included features

<table><tbody>
<tr><td>File systems</td><td>RAMFS, SPIFFS.</td></tr>
<tr><td>Lua modules</td><td>adc, bt, can, cjson, cpu, encoder, event, fs, gdisplay, i2c, lora, mqtt, neopixel, net, nvs, pack, pio, pwm, sdisplay, sensor, servo, socket, spi, stepper, thread, tmr, uart, ulp.</td></tr>
<tr><td>Networking</td><td>WiFi.</td></tr>
<tr><td>Network services</td><td>CAN gateway, Captive DNS, HTTP server, OTA updates, SNTP.</td></tr>
<tr><td>Sensors</td><td>10K Thermistor, 2P toggle switch, 2Y0A21, 3P toggle switch, 4x4 key matrix, A49E, Analog joystick, BDE0600G, BH1620FVC, BH1721FVC, BME280, DHT11, DHT22, DHT23, DS1820, GPS, GUVA S12SD, Hall flow sensor, Hall internal, Hall switch, LDR, LM35, Linear potentiometer, ML8511, PING28015, PIR AM412, Push switch, Relative rotary encoder, SDS011, TMP36, Tilt switch, US015.</td></tr>
</tbody></table>

## Hardware mapping

| CAN | Signal | GPIO |
|--------|--------|------|
| 0 | RX<br/>TX | GPIO14<br/>GPIO12 |

| I2C | Signal | GPIO |
|--------|--------|------|
| 0 | SCL<br/>SDA | GPIO21<br/>GPIO25 |
| 1 | SCL<br/>SDA | GPIO32<br/>GPIO33 |

| SPI | Signal | GPIO |
|--------|--------|------|
| 2 | MISO<br/>MOSI<br/>CLK | GPIO12<br/>GPIO13<br/>GPIO14 |
| 3 | MISO<br/>MOSI<br/>CLK | GPIO19<br/>GPIO23<br/>GPIO18 |

| UART | Signal | GPIO |
|--------|--------|------|
| 0 | RX<br/>TX | GPIO3<br/>GPIO1 |
| 1 | RX<br/>TX | GPIO26<br/>GPIO25 |
| 2 | RX<br/>TX | GPIO2<br/>GPIO15 |

## SPI displays on SPI3, touch panel on SPI3

| Display signal | GPIO |
|--------|------|
| MISO<br/>MOSI<br/>CLK<br/>CS<br/>RST<br/>CMD<br/>BCKL* | GPIO19<br/>GPIO23<br/>GPIO18<br/>GPIO15<br/>GPIO26<br/>GPIO2<br/>Not used |

_* back light_

| Touch panel signal | GPIO
|--------|------|
| MISO<br/>MOSI<br/>CLK<br/>CS | GPIO19<br/>GPIO23<br/>GPIO18<br/>GPIO21 |

## I2C displays on I2C0

| Signal | GPIO |
|--------|------|
| SCL<br/>SDA | GPIO21<br/>GPIO25 |
