# About this

BDE0600G is an analog current output temperature sensor.

# Specification

| What         |                 | Comments                    |
|--------------|-----------------|-----------------------------|
| Identifier   | BDE0600G        |                             |
| Interface    | ADC             |                             |
| Provides     | temperature     | celsius degrees             |
| Properties   | calibration     | Calibration data +/- ºC     |
| [Datasheet](http://www.farnell.com/datasheets/1448193.pdf) | | |

# Notes

* The programmer can use the calibration property to correct sensor readings that may be influenced by the location of the sensor, such as when the sensor is mounted into a box.

# Code

```lua
-- Attach BDE0600G sensor to an external ADC (ADS1115) / channel 0
s = sensor.attach("BDE0600G", adc.ADS1115, 0)

-- If your calibration differ from de default values uncomment the
-- following lines and set your values
-- s:set("calibration", 0)

while true do
  print(s:read("temperature"))
  tmr.delayms(500)
end
```

[Back to sensor list](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Sensor-module#supported-sensors)