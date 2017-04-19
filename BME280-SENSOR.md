# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | BME280      |                            |
| Interface    | I2C         |                            |
| Provides     | temperature | celsius degrees            |
|              | humidity    | % relative humidity        |
|              | pressure    | hPa                        |
| Properties   | address     | sensor address (r/w)       |
|              | mode        | sensor mode (r/w)          |
|              | standbytime |                            |
| [Datasheet](https://ae-bst.resource.bosch.com/media/_tech/media/datasheets/BST-BME280_DS001-11.pdf)    |             | ![](https://whitecatboard.org/git/bme280.jpg)                           |

# Code

```lua
-- Setup BME280, attached at I2C0, speed=400Khz
-- sda=GPIO14, scl=GPIO26, adress is 0x76
s1 = sensor.setup("BME280", i2c.I2C0, 400, pio.GPIO14, pio.GPIO26, 0x76)

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