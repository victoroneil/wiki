# Specification

Infrared sensor

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | 2Y0A21      | ![](http://git.whitecatboard.org/GP2Y0A21YK.jpg)            |
| Interface    | ADC         |                            |
| Provides     | distance    | centimeters                |
| Properties   | none        |                            |
| [Datasheet](http://www.socle-tech.com/doc/IC%20Channel%20Product/Sensors/Distance%20Measuring%20Sensor/Analog%20Output/gp2y0a21yk_e.pdf)    |             |                            |


# Code

```lua
-- Attach sensor using an external ADC (ADS1115) / channel 0
s = sensor.attach("2Y0A21", adc.ADS1115, 0)

while true do
  print("distance: "..s:read("distance").." cm")
  tmr.delayms(500)
end
```

[Back to sensor list](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Sensor-module#supported-sensors)