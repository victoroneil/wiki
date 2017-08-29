# Specification

| What         |                 | Comments                   |
|--------------|-----------------|----------------------------|
| Identifier   | REL_ROT_ENCODER | ![](http://git.whitecatboard.org/encoder.png)|
| Interface    | 3 GPIO          | GPIO 1: A signal<br/>GPIO 2: B signal<br/>GPIO 3: SW signal (switch)|
| Provides     | dir             | -1: counter clockwise<br/>0: no movement<br/>1: clockwise|
|              | val             | encoder value              |
|              | sw              | 0: switch released<br/>1: switch pressed|
| Properties   | none            |                            |
| Callbacks?   | yes             | |

**Notes:**

  * This sensor requires debouncing by hardware

# Code

In this example an encoder is attached at GPIO26 (A), GPIO14 (B) and GPIO21 (SW)
```lua
-- Attach encoder. Signal assignments are:
-- A: GPIO26
-- B: GPIO14
-- SW: GPIO21
s = sensor.attach("REL_ROT_ENCODER", pio.GPIO26, pio.GPIO14, pio.GPIO21)
s:callback(
   function(magnitude)
      if (magnitude.dir == -1) then
         print("ccw, value "..magnitude.val)
      elseif (magnitude.dir == 1) then
         print("cw, value "..magnitude.val)
      end
      
      if (magnitude.sw == 1) then
         print("sw on")
      elseif (magnitude.sw == 0) then
         print("sw off")
      end
   end
)
```