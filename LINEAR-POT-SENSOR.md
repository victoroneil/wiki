# Specification

| What         |                 | Comments                    |
|--------------|-----------------|-----------------------------|
| Identifier   | LINEAR_POT      | ![](http://git.whitecatboard.org/pot.png) |
| Interface    | ADC             |                             |
| Provides     | val             | Potentiometer % value, from 0.0 to 1. 0 is 0%,<br/>1.0 is 100%, 0.5 is 50%.|
| Properties   | none            |                             | 
| Callbacks?   | no              |                             |

# Code

In this example a potentiometer is used to control the brightness of a led (using PWM).

```lua
-- Attach a led at GPIO32
led = pwm.attach(pio.GPIO32, 1000, 0)
led:start()
      
-- Attach a potentiometer connected to an external ADC (ADS1115) / cannel 0
s = sensor.attach("LINEAR_POT", adc.ADS1115, 0)

-- Read potentiometer value every 10 msecs
thread.start(function()
  while true do
    tmr.delayms(10)
    led:setfreq(1000)
    led:setduty(s:read("val"))
  end
end)
```

[Back to sensor list](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Sensor-module#supported-sensors)