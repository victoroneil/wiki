# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | HALL_SWITCH |                            |
| Interface    | GPIO        |                            |
| Provides     | on          | 1 = switch active          |
|              |             | 0 = switch inactive        |
| Properties   | none        |                            |
| [Datasheet](http://www.hyzt.com/manager/upimg/2007328165759.pdf)    |             | ![](http://git.whitecatboard.org/hall_switch.png)                           |


# Code

```lua
s = sensor.attach("HALL_SWITCH", pio.GPIO26)

s:callback(
   function(properties)
      if (properties["on"] == 1) then
         print("on")
      else
         print("off")
      end
   end
)
```