# Specification

| What         |             | Comments                                    |
|--------------|-------------|---------------------------------------------|
| Identifier   | PING28015   |                                             |
| Interface    | GPIO        | 1 pin                                       |
| Provides     | distance    | meters                                      |
| Properties   | temperature | sound speed depends on ambient temperature  |
| [Datasheet](https://www.parallax.com/sites/default/files/downloads/28015-PING-Sensor-Product-Guide-v2.0.pdf)    |             | ![](http://git.whitecatboard.org/ping-sensor.png)                            |

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