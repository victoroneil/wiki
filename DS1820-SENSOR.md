# Specification

| What         |             | Comments                    |
|--------------|-------------|-----------------------------|
| Identifier   | DS1820      | ![](http://git.whitecatboard.org/ds1820.png)                            |
| Interface    | 1-WIRE      |                             |
| Provides     | temperature | celsius degrees             |
| Properties   | resolution  | bits of resolution          |
|              | rom         | address in the bus          |
|              | type        | model                       |
|              | numdev      | number of DS180 sensors in the bus |
| [Datasheet](https://datasheets.maximintegrated.com/en/ds/DS18S20.pdf)           |             |                                  |


# Code

```lua
-- Attach the second DS1820 sensor connected to GPIO26
s = sensor.attach("DS1820", pio.GPIO26, 2)

while true do
  print("temp: "..s:read("temperature"))
  tmr.delayms(500)
end
```

[Back to sensor list](./Sensor-module#supported-sensors)
