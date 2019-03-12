# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | VH400       | ![](http://git.whitecatboard.org/vh400.png)                           |
| Interface    | ADC         |                            |
| Provides     | vwc         | volumetric water content   |
| Properties   | none        |                            |
| [Datasheet](https://www.vegetronix.com/Products/VH400)    |             |                            |


# Code

```lua
-- Attach sensor using internal ADC / channel 6
s1 = sensor.attach("VH400", adc.ADC1, 6)

s1:read("vwc")
```

[Back to sensor list](./Sensor-module#supported-sensors)
