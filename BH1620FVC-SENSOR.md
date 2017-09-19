# About this

BH1620FVC is an analog current output ambient light sensor.

**Features:**

  * Spectral sensitivity close to human eyes sensitivity.
  * Output current in proportion to brightness.
  * Supply voltage operates from 2.4V to 5.5V
  * Built-in shutdown function
  * 3 steps controllable output current gain.
  * 1.8V logic input interface
  * Low sensitivity variation (+/-15%) 

# Specification

| What         |                 | Comments                    |
|--------------|-----------------|-----------------------------|
| Identifier   | BH1620FVC       | ![](http://git.whitecatboard.org/bh1620fvc.png)                            |
| Interface    | ADC             |                             |
| Provides     | illuminance     | lux (\*)                         |
| Properties   | gain            | 0 = H-Gain mode<br/>1 = M-Gain mode<br/>2 = L-Gain mode| 
|              | r1              | Iout R1 resistance value, in ohms.<br/>Default value is set to 5600 ohms.<br/>Please, refer to the datasheet page 4 for more information about R1.                           |
| [Datasheet](http://rohmfs.rohm.com/en/products/databook/datasheet/ic/sensor/light/bh1721fvc-e.pdf) | | |

# Notes

* The gain must be set according to the illuminance range to be measured (datasheet page 5) through pins 3 and 4.
* Once the gain is set, the programmer must set the gain property. By default the sensor expects an H-Gain setting.
* Adjust r1 value to your needs.
* Once the r1 is set, the programmer must set the r1 property. By default the sensor expects a r1 value of 5600 ohms.
* The programmer can use the calibration property to correct sensor readings that may be influenced by the location of the sensor, such as when the sensor is mounted behind a protective glass.

# Comments

**_(\*)_**

| lux            | Surfaces illuminated by                         |
|----------------|-------------------------------------------------|
| 0.0001         | Moonless, overcast night sky (starlight)        |
| 0.002          | Moonless clear night sky with airglow           |
| 0.05–0.36      | Full moon on a clear night                      |
| 3.4            | Dark limit of civil twilight under a clear sky  |
| 20–50          | Public areas with dark surroundings             |
| 50             | Family living room lights                       |
| 80             | Office building hallway/toilet lighting         |
| 100            | Very dark overcast day                          |
| 320–500        | Office lighting                                 |
| 400            | Sunrise or sunset on a clear day                |
| 1000           | Overcast day: typical TV studio lighting        |
| 10,000–25,000	 | Full daylight (not direct sun)                  |
| 32,000–100,000 | Direct sunlight

# Code

```lua
-- Attach BH1620FVC sensor to an external ADC (ADS1115) / channel 0
s = sensor.attach("BH1620FVC", adc.ADS1115, 0)

-- If your gain / r1 values differ from de default values uncomment the
-- following lines and set your values
-- s:set("gain", 0)
-- s:set("r1", 5600)
-- s:set("calibration", 0)

while true do
  print(s:read("illuminance"))
  tmr.delayms(500)
end
```

[Back to sensor list](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Sensor-module#supported-sensors)