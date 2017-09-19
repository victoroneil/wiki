# Specification

| What         |                 | Comments                    |
|--------------|-----------------|-----------------------------|
| Identifier   | BH1620FVC       | ![](http://git.whitecatboard.org/ldr.png)                            |
| Interface    | ADC             |                             |
| Provides     | illuminance     | lux (\*)                         |
| Properties   | mode            | 0 = H-Gain mode<br/>1 = M-Gain mode<br/>2 = L-Gain mode| 
|              | r1              | Iout R1 resistance value, in ohms.<br/>Default value is set to 5600 ohms.<br/>Please, refer to the datasheet page 4 for more information about R1.                           |
| [Datasheet](http://rohmfs.rohm.com/en/products/databook/datasheet/ic/sensor/light/bh1620fvc-e.pdf) | | |

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
```