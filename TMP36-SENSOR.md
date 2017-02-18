# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | TMP36       |                            |
| Interface    | ADC         |                            |
| Provides     | temperature | celsius degrees            |
| Properties   | none        |                            |
| [Datasheet] (http://www.analog.com/media/en/technical-documentation/data-sheets/TMP35_36_37.pdf)    |             | ![](http://whitecatboard.org/git/tmp36.png)                           |


# Code

```lua
s1 = sensor.setup("TMP36", adc.ADC1, adc.ADC_CH6, 12)

s1:read("temperature")
```