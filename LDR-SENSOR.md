# Specification

| What         |                 | Comments                    |
|--------------|-----------------|-----------------------------|
| Identifier   | LDR             |                             |
| Interface    | ADC             |                             |
| Provides     | illuminance     | lux (\*)                         |
| Properties   | R1<br/>R2              | R1 resistance in ohms (\*\*)<br/>R2 resistance in ohms (\*\*)   | 
|              |                 | ![](http://git.whitecatboard.org/ldr.png)                           |

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

**_(\*\*)_**

LDR component must be part of a voltage divider circuit:

![](http://git.whitecatboard.org/divider.png)

LDR can be placed in the R1 location and R2 is a fixed-value register, or in the R2 location and R1 is a fixed-value register.

Typically the fixed-value register is 10K = 10.000 ohms.

# Code

```lua
```