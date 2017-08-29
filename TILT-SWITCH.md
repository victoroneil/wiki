# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | TILT_SWITCH | ![](http://git.whitecatboard.org/sw520d.png) |
| Interface    | GPIO        |                            |
| Provides     | on          | 1 = switch active<br/>0 = switch inactive |
| Properties   | none        |                            |
| Callbacks?   | yes         |                            |
| [Datasheet](http://funduino.de/DL/SW-520D.pdf)    |             |                            |


# Code

```lua
-- Attach a tilt switch to GPIO26
s = sensor.attach("TILT_SWITCH", pio.GPIO26)

-- Register a callback. Callback is executed when some sensor property changes.
s:callback(
   function(data)
      if (data.on == 1) then
         print("on")
      elseif (data.on == 0) then
         print("off")
      end
   end
)
```