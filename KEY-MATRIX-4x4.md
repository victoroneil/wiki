# Specification

| What         |                | Comments                   |
|--------------|----------------|----------------------------|
| Identifier   | KEY_MATRIX_4_4 | ![](http://git.whitecatboard.org/push_button.png) |
| Interface    | GPIO           |                            |
| Provides     | on             | 1 = switch active<br/>0 = switch inactive|
| Properties   | none           |                            |
| Callbacks?   | yes            | |


# Code

```lua
-- Attach switch to GPIO26
s = sensor.attach("PUSH_SWITCH", pio.GPIO26)

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