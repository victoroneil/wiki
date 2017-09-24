# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | TMP36       | ![](http://git.whitecatboard.org/tmp36.png)                           |
| Interface    | ADC         |                            |
| Provides     | temperature | celsius degrees            |
| Properties   | none        |                            |
| [Datasheet](http://www.analog.com/media/en/technical-documentation/data-sheets/TMP35_36_37.pdf)    |             |                            |


# Code

```lua
-- Attach sensor using internal ADC / channel 6
s1 = sensor.attach("TMP36", adc.ADC1, 6)

s1:read("temperature")
```

[Back to sensor list](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Sensor-module#supported-sensors)