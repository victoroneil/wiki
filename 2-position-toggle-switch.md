# Specification

| What         |                  | Comments                   |
|--------------|------------------|----------------------------|
| Identifier   | 2P_TOGGLE_SWITCH | ![](http://git.whitecatboard.org/2p_switch.png) |
| Interface    | 1 GPIO           |                            |
| Provides     | pos              | 1 = switch in pos 1<br/>0 = switch in pos 0|
| Properties   | none             |                            |
| Callbacks?   | yes              | |

# Code

```lua
-- Attach switch to GPIO26
s = sensor.attach("2P_TOGGLE_SWITCH", 26)
s:callback(
   function(data)
   print(data.pos)
   end
)
```