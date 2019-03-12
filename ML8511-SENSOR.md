# About this

The ML8511 is an UV sensor, which is suitable for acquiring UV intensity indoors or outdoors. The ML8511 is
equipped with an internal amplifier, which converts photo-current to voltage depending on the UV intensity.
This unique feature offers an easy interface to external circuits such as ADC. In the power down mode, typical
standby current is 0.1uA, thus enabling a longer battery life. 

**Features:**

* Photodiode sensitive to UV-A and UV-B
* Embedded operational amplifier
* Analog voltage output
* Low supply current (300uA typ.) and low standby current (0.1uA typ.)

# Specification

| What         |                 | Comments                    |
|--------------|-----------------|-----------------------------|
| Identifier   | ML8511       | ![](http://git.whitecatboard.org/ml8511.png)                            |
| Interface    | ADC             |                             |
| Provides     | intensity       | mW/cm2                      |
| Properties   | enable signal   | This sensor has an EN (enable) pin, active high. This property sets the GPIO number to use for enable the sensor.<br/><br/>Default value is -1 (sensor always enabled). | 
|              | calibration     | Calibration data +/- intensity  |
| [Datasheet](https://cdn.sparkfun.com/datasheets/Sensors/LightImaging/ML8511_3-8-13.pdf) | | |

# Notes

* The programmer can use the enable signal property to set the GPIO number to use for enable / disable the sensor. When not provided, or when it's value is -1, the sensor always it's enable).
* The programmer can use the calibration property to correct sensor readings that may be influenced by the location of the sensor, such as when the sensor is mounted behind a protective glass.

# Code

```lua
-- Attach ML8511 sensor to an external ADC (ADS1115) / channel 0
s = sensor.attach("ML8511", adc.ADS1115, 0)

-- If your enable signal / calibration values differ from de default values uncomment the
-- following lines and set your values
-- s:set("enable signal", -1)
-- s:set("calibration", 0)

while true do
  print(s:read("intensity"))
  tmr.delayms(500)
end
```

[Back to sensor list](./Sensor-module#supported-sensors)
