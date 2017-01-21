# Specification

| What         |             | Comments                                   |
|--------------|-------------|--------------------------------------------|
| Identifier   | PING28015   |                                            |
| Interface    | GPIO        | 1 pin                                      |
| Provides     | distance    | meters                                     |
| Settings     | temperature | sound speed depends on ambient temperature |
| [Datasheet] (https://www.parallax.com/sites/default/files/downloads/28015-PING-Sensor-Product-Guide-v2.0.pdf)    |             | ![](http://whitecatboard.org/git/ping-sensor.png)                           |


# Code

```lua
s1 = sensor.setup("PING28015", pio.GPIO4)

s1:set("temperature", 25)

s1:acquire()

s1:read("distance")
```