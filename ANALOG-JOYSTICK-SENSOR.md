# Specification

| What         |                 | Comments                   |
|--------------|-----------------|----------------------------|
| Identifier   | ANALOG_JOYSTICK | ![](http://git.whitecatboard.org/joystick.png)|
| Interface    | 2 ADC<br/>1 GPIO           | ADC 1: X signal<br/>ADC 2: Y signal<br/>GPIO : SW signal (switch) |
| Provides     | x               | -1: left movement<br/>0: no movement<br/>1: right movement         |
|              | y               | -1: up movement<br/>0: no movement<br/>1: down movement         |
|              | sw              | 0: switch released<br/>1: switch pressed        |
| Properties   | none            |                            |
| Callbacks?   | yes             |    |

# Code

```lua
-- Attach a joystick connected as
-- x external ADC (ADC1115) / channel 0
-- y external ADC (ADC1115) / channel 1
-- sw (switch) GPIO26
s = sensor.attach("ANALOG_JOYSTICK", adc.ADS1115, 0, adc.ADS1115, 1, pio.GPIO26)

-- Register a callback. Callback is executed when some sensor property changes.
s:callback(function(data)
  if (data.x == -1) then
    print("left")
  elseif (data.x == 1) then
    print("right")
  end

  if (data.y == -1) then
    print("up")
  elseif (data.y == 1) then
    print("down")
  end
  
  if (data.sw == 1) then
    print("sw on")
  elseif (data.sw == 0) then
    print("sw off")
  end
end)
```