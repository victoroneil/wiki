# About this

![](http://git.whitecatboard.org/keyes-encoder.jpg)

This module contains functions for work with digital relative rotary encoders. The functions of this module are organized in the following categories:

* [Setup functions](#setup-functions)
* [Operation functions](#operation-functions)

# Key concepts

A digital relative rotary encoder, is an electro-mechanical device that converts the angular position or motion of a shaft or axle to a digital signal. The output provides information about the motion of the shaft, which is typically further processed elsewhere into information such as speed, distance and position.

Encoders are used in many applications that require precise shaft unlimited rotation, including industrial controls, robotics, special purpose photographic lenses,computer input devices (such as optomechanical mice and trackballs), controlled stress rheometers, and rotating radar platforms.

Digital relative rotary encoders employ two outputs called A & B, which are called quadrature outputs, as they are 90 degrees out of phase. Signal A is known as clock, and B as data.

![](http://git.whitecatboard.org/encoder-quadrature.png)

The two output wave forms are 90 degrees out of phase, which is what quadrature means. These signals are decoded to produce a count up pulse or a count down pulse. For decoding Lua RTOS use interrupts and a machine state that filters invalid combinations.

Please, take note that encoders have built-in switches which generate the quadrature waveform during rotation. Those switches generate noise during the closing and the opening moments of their contacts that can cause erroneous direction and rotation detection if is not filtered.

![](http://git.whitecatboard.org/encoder-noise.png)

Filtering the noise out by using extra hardware is easier and it stops the noise at its source.

![](http://git.whitecatboard.org/encoder-filter.png)

The proposed values are R pull-up = 10 K, R = 0, C = 100nF.

# Setup functions

## instance = encoder.attach(A, B, SW, [callback])

Attach an encoder.

Arguments:

* A: the GPIO which encoder A signal is attached. Use pio.GPIOx defined for this purpose.
* B: the GPIO which encoder B signal is attached. Use pio.GPIOx defined for this purpose.
* SW: the GPIO which encoder SW (switch) signal is attached. Use pio.GPIOx defined for this purpose. Use nil for this argument if you don't want to use the switch.
* callback (optional): a callback function for get information about the encoder changes. This function takes 2 arguments: value (encoder value), and button (an integer that tell us if the switch is pressed, 1 = pressed, 0 = not pressed).

Returns: an encoder instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
function callback(value, button)
   print("position: "..value..", button: "..button)
end

-- Attach an encoder with A=pio.GPIO26, B=pio.GPIO14, SW=pio.GPIO21.
-- Using a calback for get the encoder changes.
enc = encoder.attach(pio.GPIO26, pio.GPIO14, pio.GPIO21, callback)
```

## instance:detach()

Detach an encoder, and free all resources used by the encoder.

Arguments: nothing. Returns: nothing, or an exception.

```lua
enc:detach()
```

# Operation functions

## instance:read()

Read the encoder position and the switch status. When encoder is attached the position is 0. If encoder rotates clockwise the position is incremented by 1. If encoder rotates counter-clockwise, the position is incremented by -1. If the switch status is 1 it is pressed, and if is 0 it is not pressed.

Arguments: nothing
Returns: the current encoder position and the switch status, or nothing.

```lua
-- Read the position
enc:read()
```

## instance:write(position)
 
Set the encoder position to a specified position.

Arguments: nothing
Returns: nothing

```lua
-- Set the position
enc:write(10)
```
