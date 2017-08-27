# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | GUVA-S12SD  |                            |
| Interface    | ADC         |                            |
| Provides     | UV Index    | celsius degrees            |
| Properties   | none        |                            |
| [Datasheet](https://cdn-shop.adafruit.com/datasheets/1918guva.pdf)    |             | ![](http://git.whitecatboard.org/guva-s12sd.png)                           |


# Code

```lua
-- Attach sensor using internal ADC at GPIO32
s1 = sensor.attach("GUVA-S12SD", adc.ADC1, pio.GPIO32)

s1:read("UV Index")
```