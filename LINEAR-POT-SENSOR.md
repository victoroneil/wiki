# Specification

| What         |                 | Comments                    |
|--------------|-----------------|-----------------------------|
| Identifier   | LINEAR_POT      |                             |
| Interface    | ADC             |                             |
| Provides     | val             | Potentiometer % value, from 0 to 1. 0 is 0%,<br/>1 is 100%, 0.5 is 50%.|
| Properties   | none            |                             | 
|              |                 | ![](http://git.whitecatboard.org/pot.png)                           |

# Code

In this example an encoder is attached at GPIO26 (A), GPIO14 (B) and GPIO21 (SW)
```lua
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