# Specification

| What         |                 | Comments                   |
|--------------|-----------------|----------------------------|
| Identifier   | REL_ROT_ENCODER |                            |
| Interface    | 3 GPIO          | GPIO 1: A signal           |
|              |                 | GPIO 2: B signal           |
|              |                 | GPIO 3: SW signal (switch) |
| Provides     | dir             | -1: counter clockwise      |
|              |                 |  0: no movement            |
|              |                 |  1: clockwise              |
|              | val             | encoder value              |
|              | sw              | 0: switch released         |
|              |                 | 1: switch pushed           |
| Properties   | none            |                            |
|              |                 | ![](http://git.whitecatboard.org/encoder.png)                           |


# Code

In this example an encoder is attached at GPIO26 (A), GPIO14 (B) and GPIO21 (C)
```lua
s = sensor.attach("REL_ROT_ENCODER", pio.GPIO26, pio.GPIO14, pio.GPIO21)

s:callback(
   function(magnitude)
      if (magnitude["dir"] == -1) then
         print("ccw, value "..magnitude["val"])
      elseif (magnitude["dir"] == 1) then
         print("cw, value "..magnitude["val"])
      else
         printf("switch: "..magnitude["sw"])
      end
   end
)
```