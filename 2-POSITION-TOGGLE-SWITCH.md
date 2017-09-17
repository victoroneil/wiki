# Specification

| What         |                  | Comments                   |
|--------------|------------------|----------------------------|
| Identifier   | 2P_TOGGLE_SWITCH | ![](http://git.whitecatboard.org/2p_switch.png) |
| Interface    | 1 GPIO           |                            |
| Provides     | pos              | 1 = switch in pos 1<br/>0 = switch in pos 0|
| Properties   | none             |                            |
| Callbacks?   | yes              | |

# Notes

* With this sensor you can get the position of a SPST (single-pole, single-throw) switch, or a SPDT (single-pole, double-throw) switch.
* A SPST has 2 terminals. Connect one terminal to a GPIO, and the other terminal to GND.
* A SPDT has 3 terminals. Connect one terminal to a GPIO, and one of the others to GND.
* Hardware pull-ups are not required.
* Hardware debouncing are not required.
* When the GPIO level state changes the sensor reads the switch position and a callback is executed reporting the switch position.

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