# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | HALL_SWITCH | ![](http://git.whitecatboard.org/hall_switch.png) |
| Interface    | GPIO        |                            |
| Provides     | on          | 1 = switch active<br/>0 = switch inactive |
| Properties   | none        |                            |
| Callbacks?   | yes         |                            |
| [Datasheet](http://www.hyzt.com/manager/upimg/2007328165759.pdf)    |             |                            |


# Code

```lua
-- Attach a hall effect switch is attached to GPIO26
s = sensor.attach("HALL_SWITCH", pio.GPIO26)

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