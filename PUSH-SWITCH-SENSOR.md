# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | HALL_SWITCH | ![](http://git.whitecatboard.org/push_button.png) |
| Interface    | GPIO        |                            |
| Provides     | on          | 1 = switch active<br/>0 = switch inactive|
| Properties   | none        |                            |
| Callbacks?   | yes         | |


# Code

```lua
-- Attach switch to GPIO26
s = sensor.attach("PUSH_SWITCH", pio.GPIO26)

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