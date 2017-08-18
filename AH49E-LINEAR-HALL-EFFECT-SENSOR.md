# Specification

| What         |                | Comments                   |
|--------------|----------------|----------------------------|
| Identifier   | AH49E          |                            |
| Interface    | ADC            |                            |
| Provides     | magnetic field | gauss                      |
| Properties   | none           |                            |
| [Datasheet](https://www.diodes.com/assets/Datasheets/AH49E.pdf)    |             | ![](http://git.whitecatboard.org/ah49e.png)                           |


# Code

```lua
-- Attach an A49E sensor to an external ADC (ADS1115) on channel 0
s1 = sensor.attach("A49E", adc.ADS1115, 0)

s1:read("magnetic field")
```