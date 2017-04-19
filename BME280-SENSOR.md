# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | BME280      |                            |
| Interface    | I2C         |                            |
| Provides     | temperature | celsius degrees            |
|              | humidity    | % relative humidity        |
|              | pressure    | hPa                        |
| Properties   | none        |                            |
| [Datasheet](https://ae-bst.resource.bosch.com/media/_tech/media/datasheets/BST-BME280_DS001-11.pdf)    |             | ![](https://whitecatboard.org/git/bme280.jpg)                           |

# Code

```lua
-- Setup BME280, attached at I2C0, speed=400Khz
-- sda=GPIO14, SCL=GPIO26, adress is 0x76
s1 = sensor.setup("BME280", i2c.I2C0, 400, 14, 26, 0x76)

-- Read temperature
temperature = s1:read("temperature")

-- Read humidity
humidity = s1:read("humidity")

-- Read preassure
pressure = s1:read("pressure")
```