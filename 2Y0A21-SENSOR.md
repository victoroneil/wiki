# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | 2Y0A21      |                            |
| Interface    | ADC         |                            |
| Provides     | distance    | centimeters                |
| Properties   | none        |                            |
| [Datasheet](http://www.socle-tech.com/doc/IC%20Channel%20Product/Sensors/Distance%20Measuring%20Sensor/Analog%20Output/gp2y0a21yk_e.pdf)    |             | ![](http://git.whitecatboard.org/GP2Y0A21YK.jpg)                           |


# Code

```lua
s1 = sensor.attach("2Y0A21", adc.MCP3208, 0, 12)

s1:read("distance")
```