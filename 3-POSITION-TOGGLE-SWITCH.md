# Specification

| What         |                  | Comments                   |
|--------------|------------------|----------------------------|
| Identifier   | 3P_TOGGLE_SWITCH | ![](http://git.whitecatboard.org/3p_switch.png) |
| Interface    | 2 GPIO           |                            |
| Provides     | pos              | 1 = switch in pos 1 (up position)<br/>2 = switch in pos 2 (down position)<br/>0 = switch in pos 0 (mid position)|
| Properties   | none             |                            |
| Callbacks?   | yes              | |

# Notes

* With this sensor you can get the position of a DPDT (double-pole, double-throw) switch.
* A DPDT has 6 terminals, organised in 2 rows. This sensor only use one row of terminals. Connect the common terminal to GND and each of the other terminals to a GPIO.
* Hardware pull-ups are not required.
* Hardware debouncing are not required.
* When the GPIO level state changes the sensor reads the switch position and a callback is executed reporting the switch position.

# Code

```lua
-- Attach the switch to GPIO26 and GPIO14
s = sensor.attach("3P_TOGGLE_SWITCH", 26, 14)
s:callback(
   function(data)
      print(data.pos)
   end
)
```