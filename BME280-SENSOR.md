# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | BME280      |                            |
| Interface    | I2C         |                            |
| Provides     | temperature | celsius degrees            |
|              | humidity    | % relative humidity        |
|              | pressure    | hPa                        |
| Properties   | mode        | sensor mode (r/w)<br>0=sleep, 1=forced, 2=normal          |
|              | standbytime | standby time in msecs (r/w)|
| Notes        | BME280 adress is 0x76 or 0x77 |

| [Datasheet](https://ae-bst.resource.bosch.com/media/_tech/media/datasheets/BST-BME280_DS001-11.pdf)    |             | ![](http://git.whitecatboard.org/bme280.jpg)                           |

# Code

```lua
-- Attach BME280 to I2C0, speed=400Khz
-- sda=GPIO14, scl=GPIO26, adress is 0x76
s1 = sensor.attach("BME280", i2c.I2C0, 400, 0x76)

while true do
  -- Read temperature
  temperature = s1:read("temperature")

  -- Read humidity
  humidity = s1:read("humidity")

  -- Read preassure
  pressure = s1:read("pressure")

  -- Print results
  print("temp: "..temperature..", humidity: "..humidity..", pressure: "..pressure)

  tmr.delayms(500)
end
```