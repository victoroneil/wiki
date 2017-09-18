# About this

This sensor provides precise, non-contact distance measurements from about 2 cm to 3 meters.

The PING))) sensor works by transmitting an ultrasonic (well above human hearing range) burst and providing an output pulse that corresponds to the time required for the burst echo to return to the sensor. By measuring the echo pulse width, the distance to target can easily be calculated.

**Power supply:**

* Supply voltage: +5 VDC
* Supply current: 30 mA typ; 35 mA max 

# Specification

| What         |             | Comments                                    |
|--------------|-------------|---------------------------------------------|
| Identifier   | PING28015   | ![](http://git.whitecatboard.org/ping-sensor.png)                                            |
| Interface    | GPIO        | 1 pin                                       |
| Provides     | distance    | cm                                          |
| Properties   | temperature | sound speed depends on ambient temperature  |
| [Datasheet](https://www.parallax.com/sites/default/files/downloads/28015-PING-Sensor-Product-Guide-v2.0.pdf)    |             |                             |

# Code

```lua
-- Attach sensor to GPIO26
s = sensor.attach("PING28015", pio.GPIO26)

-- We tell to PING28015 that ambient temperature are 25º for adjust
-- the sound speed, used internally for calculate the distance from an
-- object
s:set("temperature", 25)

while true do
  print("distance: "..s:read("distance"))
  tmr.delayms(500)
end
```

[Back to sensor list](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Sensor-module#supported-sensors)