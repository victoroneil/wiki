This sensor is intended for get the geographic coordinates received from UART NMEA 0183 compatible GPS sensors. A NMEA 0183 parser is included in the sensor driver that listens for GPGGA NMEA sentence.

# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | GPS         | NMEA 0183 UART             |
| Interface    | UAR         |                            |
| Provides     | lon         | longitude (degrees)        |
|              | lat         | latitude (degrees)         |
|              | sats        | number of satellites       |
| Properties   | none        |                            |


# Code

```lua
gps = sensor.attach("GPS", uart.UART1, 9600, 8, uart.PARNONE, uart.STOP1)
while true do
   lon = gps:read("lon")
   lat = gps:read("lat")
   sats = gps:read("sats")
   print("lon: "..lon..", lat: "..lat..", sats: "..sats)
   tmr.delayms(500)
end
```