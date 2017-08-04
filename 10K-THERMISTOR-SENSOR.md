# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | THERMISTOR  |                            |
| Interface    | ADC         |                            |
| Provides     | temperature | celsius degrees            |
| Properties   | none        |                            |
| [Datasheet](https://cdn.sparkfun.com/datasheets/Sensors/Temp/ntcle100.pdf)    |             | ![](http://git.whitecatboard.org/thermistor.png)                           |


# Code

```lua
-- Attach 10K Thermistor sensor to GPIO35, 12 bits of resolution
s1 = sensor.attach("THERMISTOR", adc.ADC1, pio.GPIO35, 12)

-- Read temperature
s1:read("temperature")
```