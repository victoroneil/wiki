# About this

This module contains functions to work with leds connected in a one-wired bus, such as the WS2812B led. Each led in the bus is known as pixel.

The primary limiting factor for the number of pixels you can drive with this module is the memory you have on your board. With 1 Kb of memory you can drive 128 pixels. In ESP32, when Lua RTOS is booted you have arround of 200 Kb of memory available for your applications, so you can drive a very high number of pixels.

# Setup funcions

## instance = neopixel.attach(type, gpio, pixels)

Attach the NEOPIXEL bus.

Arguments:

* type: the led type you have connected to the bus. For now only neopixel.WS2812B is supported.
* gpio: the GPIO to use for drive the bus. Use any of the pio.GPIOx values defined in the pio module for this.
* pixels: number of pixels (leds) connected to the bus.

Returns: a NEOPIXEL bus instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Attch a NEOPIXEL bus formed by 6 WS2812B leds, connected to GPIO14
neo = neopixel.attach(neopixel.WS2812B, pio.GPIO14, 6)
```

# Operation functions

## instance:setPixel(pixel, red, green, blue)

Set the pixel's color, expressed in it's r/g/b components. This function only updates the internal pixel buffer, but anything is transmitted over the bus. You must call to the update function for update the leds connected to the bus.

Arguments:

* pixel: pixel number.
* red: red component, from 0 to 255.
* green: green component, from 0 to 255.
* blue: blue component, from 0 to 255.

Returns: nothing, or an exception.

```lua
-- Setup a NEOPIXEL bus formed by 6 WS2812B leds, connected to GPIO14
neo = neopixel.attach(neopixel.WS2812B, pio.GPIO14, 6)

-- Set color for pixel 0 (pure red)
neo:setPixel(0, 255, 0, 0)

-- Set color for pixel 1 (pure green)
neo:setPixel(1, 0, 255, 0)

-- Set color for pixel 2 (pure white)
neo:setPixel(2, 255, 255, 255)
```

## instance:update()

Updates the leds connected to the bus.

Arguments: nothing.

Returns: nothing, or an exception.

```lua
-- Setup a NEOPIXEL bus formed by 6 WS2812B leds, connected to GPIO14
neo = neopixel.attach(neopixel.WS2812B, pio.GPIO14, 6)

-- Set color for pixel 0 (pure red)
neo:setPixel(0, 255, 0, 0)

-- Set color for pixel 1 (pure green)
neo:setPixel(1, 0, 255, 0)

-- Set color for pixel 2 (pure white)
neo:setPixel(2, 255, 255, 255)

-- Update the bus
neo:update()
```

# Full example

In this example a pixel is moved from right to left, and from left to right, in a 6 pixel bus.

```lua
thread.start(function()
  neo = neopixel.attach(neopixel.WS2812B, pio.GPIO14, 6)

  pixel = 0
  direction = 0

  while true do
    neo:setPixel(pixel, 0, 255, 0)
    neo:update()
    tmr.delayms(100)
    neo:setPixel(pixel, 0, 0, 0)

    if (direction == 0) then
      if (pixel == 5) then
        direction = 1
        pixel = 4
      else
        pixel = pixel + 1
      end
    else
      if (pixel == 0) then
        direction = 0
        pixel = 1
      else
        pixel = pixel - 1
      end
    end
  end
end)
```