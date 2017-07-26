**This page is under construction**

# About this

This module contains functions for work with digital relative rotary encoders.

# Key concepts

A digital relative rotary encoder, is an electro-mechanical device that converts the angular position or motion of a shaft or axle to a digital signal. The output provides information about the motion of the shaft, which is typically further processed elsewhere into information such as speed, distance and position.

Encoders are used in many applications that require precise shaft unlimited rotation, including industrial controls, robotics, special purpose photographic lenses,computer input devices (such as optomechanical mice and trackballs), controlled stress rheometers, and rotating radar platforms.

Digital relative rotary encoders employ two outputs called A & B, which are called quadrature outputs, as they are 90 degrees out of phase.

![](http://git.whitecatboard.org/encoder-quadrature.png)

The two output wave forms are 90 degrees out of phase, which is what quadrature means. These signals are decoded to produce a count up pulse or a count down pulse. For decoding Lua RTOS use interrupts and a machine state that filters invalid combinations.

Please, take note that encoders have built-in switches which generate the quadrature waveform during rotation.

![](http://git.whitecatboard.org/encoder-noise.png)
