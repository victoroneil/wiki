# Specification

| What         | Description | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | BME280      | ![](http://git.whitecatboard.org/bme280.jpg)                            |
| Interface    | I2C         |                            |
| Provides     | temperature | celsius degrees            |
|              | humidity    | % relative humidity        |
|              | pressure    | hPa                        |
| Properties   | mode        | sensor mode (r/w)<br>0=sleep, 1=forced, 2=normal          |
|              | standbytime | standby time in msecs (r/w)|
| Notes        | BME280 adress is 0x76 (default) or 0x77 |
| [Datasheet](https://ae-bst.resource.bosch.com/media/_tech/media/datasheets/BST-BME280_DS001-11.pdf)    |             |                           |

# Code

```lua
-- Attach BME280 to I2C0, with default values
s = sensor.attach("BME280", i2c.I2C0, 0)

while true do
  -- Read temperature
  temperature = s:read("temperature")

  -- Read humidity
  humidity = s:read("humidity")

  -- Read preassure
  pressure = s:read("pressure")

  -- Print results
  print("temp: "..temperature..", humidity: "..humidity..", pressure: "..pressure)

  tmr.delayms(500)
end
```