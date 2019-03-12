# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | LM35        | ![](http://git.whitecatboard.org/LM35.png)                           |
| Interface    | ADC         |                            |
| Provides     | temperature | celsius degrees            |
| Properties   | none        |                            |
| [Datasheet](http://www.ti.com/lit/ds/symlink/lm35.pdf)    |             |                            |


# Code

```lua
-- Attach sensor using internal ADC / channel 6
s1 = sensor.attach("LM35", adc.ADC1, 6)

s1:read("temperature")
```

[Back to sensor list](./Sensor-module#supported-sensors)
