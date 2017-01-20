# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | TMPO36      |                            |
| Interface    | ADC         |                            |
| Provides     | temperature | celsius degrees            |
| [Datasheet] (http://www.micropik.com/PDF/tmp36.pdf)    |             | ![](http://whitecatboard.org/git/tmp36.jpg)                           |


# Code

```lua
s1 = sensor.setup("TMP36", adc.ADC1, adc.ADC_CH6, 12)

s1:acquire()

s1:read("temperature")
```