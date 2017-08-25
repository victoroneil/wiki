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
s = sensor.attach("A49E", adc.ADS1115, 0)

while true do
  print("magnetic field: "..s:read("magnetic field").." gauss")
  tmr.delayms(500)
end
```