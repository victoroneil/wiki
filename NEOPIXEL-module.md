# About this

This module contains functions for work with WS2812B leds connected in a one-wired bus. Each led in the bus is known as pixel. The primary limiting factor to the number of pixels you can drive with this module is the memory you have on your board, with 1 Kb of memory you can drive 128 pixels.

# Setup funcions

## instance = neopixel.setup(type, gpio, pixels)

Setup the NEOPIXEL bus.

Arguments:

* type: the led type you have connected to the bus. For now only neopixel.WS2812B is supported.
* gpio: the GPIO to use for drive the bus. Use any of the pio.GPIOx values defined in the pio module for this.
* pixels: number of pixels (leds) connected to the bus.

Returns: a NEOPIXEL bus instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Setup a NEOPIXEL bus formed by 6 WS2812B leds, connected to GPIO14
neo = neopixel.setup(neopixel.WS2812B, pio.GPIO14, 6)
```

# Operation functions

## instance:setPixel(pixel, red, green, blue)

Set the color, expressed in it's r/g/b components, for a pixel.

Arguments:

* pixel: pixel number.
* red: red component, from 0 to 255.
* green: green component, from 0 to 255.
* blue: blue component, from 0 to 255.

Returns: nothing, or an exception.

```lua
-- Setup a NEOPIXEL bus formed by 6 WS2812B leds, connected to GPIO14
neo = neopixel.setup(neopixel.WS2812B, pio.GPIO14, 6)

-- Set color for pixel 0 (pure red)
neo:setPixel(0, 255, 0, 0)

-- Set color for pixel 1 (pure green)
neo:setPixel(0, 255, 0, 0)

-- Set color for pixel 2 (pure white)
neo:setPixel(0, 255, 255, 255)
```