# About this

BH1721FVC is an digital Ambient Light Sensor IC for I2C bus interface. 

**Features:**

  * I2C bus Interface, Slave Address : "0100011"
  * Spectral responsibility is approximately human eye response
  * Illuminance to Digital Converter
  * Wide range and High resolution. (1 – 65528 lx )
  * Low Current by power down function
  * 50Hz / 60Hz Light noise reject-function
  * 1.8V Logic input interface
  * No need any external parts
  * Light source dependency is little. (ex. Incandescent Lamp. Fluorescent Lamp. Halogen Lamp. White LED. Sun Light)
  * Small measurement variation (+/- 15%)

# Specification

| What         |                 | Comments                    |
|--------------|-----------------|-----------------------------|
| Identifier   | BH1721FVC       | ![](http://git.whitecatboard.org/bh1620fvc.png)                            |
| Interface    | I2C             |                             |
| Provides     | illuminance     | lux (\*)                    |
| Properties   | resolution      | 0 = Auto-Resolution Mode<br/>1 = H-Resolution Mode<br/>2 = L-Resolution Mode<br/><br/>Default value is H-Resolution Mode | 
|              | calibration     | Calibration data +/- lux    |
| [Datasheet](http://rohmfs.rohm.com/en/products/databook/datasheet/ic/sensor/light/bh1721fvc-e.pdf) | | |

# Notes

* The resolution must be set according to the illuminance range to be measured (datasheet page 5).
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
-- Attach BH1721FVC sensor to I2C0
s = sensor.attach("BH1721FVC", i2c.I2C0, 0)

-- If your resolution / calibration values differ from de default values uncomment the
-- following lines and set your own values
-- s:set("resolution", 1)
-- s:set("calibration", 0)

while true do
  print(s:read("illuminance"))
  tmr.delayms(500)
end
```

[Back to sensor list](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Sensor-module#supported-sensors)