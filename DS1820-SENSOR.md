# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | DS1820      |                            |
| Interface    | 1-WIRE      |                            |
| Provides     | temperature | celsius degrees            |
| Properties   | resolution  | bits of resolution         |
| Properties   | rom         | address in the bus         |
| Properties   | type        | model                      |
| Properties   | numdev      | number of DS180 sensor in the bus |
| [Datasheet] (https://datasheets.maximintegrated.com/en/ds/DS18S20.pdf)          |             | ![](http://whitecatboard.org/git/ds1820.png)                                 |


# Code

```lua
s1 = sensor.attach("TMP36", adc.ADC1, adc.ADC_CH6, 12)

s1:read("temperature")
```