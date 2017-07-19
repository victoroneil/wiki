# About this

This module contains functions for accessing graphic displays, and gives the programmer an api to work with graphic displays in a unified form, regardless of the used display.

Supported chipset displays:

* ST7735: 1.8", 1.44", 0.96"
* ILI9341
* PCD8544 (NOKIA 5110)

# General purpose functions

## gdisplay.attach(chipset, [orientation, framed, antialiasing])

Initialize the display and clear the screen.

Arguments:

* chipset: chipset used by the display.
* orientation (optional): display orientation, can be either gdisplay.LANDSCAPE, gdisplay.LANDSCAPE_FLIP, gdisplay.PORTRAIT, or gdisplay.PORTRAIT_FLIP. Default orientation is gdisplay.LANDSCAPE.
* framed (optional): if true frame buffer is used. Default is false.
* antialiasing (optional): if true antialiasing is applied when rendering. Default is false.

Returns: nothing, or an exception.

## gdisplay.clear([color])

Clear the display to specified color.

Arguments:

* color (optional): the color used to fill de display. The default color depends on the display chipset, for example in TFT displays it is black, and in monochrome LCD displays it is white. In general, the default color is one that keeps all of the screen pixels off.

Returns: noting, or an exception.

```lua
-- Clear the display to RED
gdisplay.clear(gdisplay.RED)

-- Clear the display to RED
gdisplay.clear({255, 0, 0})

-- Clear the display to default colot
gdisplay.clear()
```

## gdisplay.off()

Turns the display off and preserve power. Back light has to be turned off separately.

Arguments: nothing
Returns: nothing or an exception

## gdisplay.on()

Turns the display on.

Arguments: nothing
Returns: nothing or an exception

## gdisplay.invert(invert)

Arguments:

* invert: if true, show inverted colors, and if false, show normal colors.
Returns: nothing or an exception

## gdisplay.setorient(orientation)

Set the display orientation, and clear the screen to the default color. The default color depends on the display chipset, for example in TFT displays it is black, and in monochrome LCD displays it is white. In general, the default color is one that keeps all of the screen pixels off.

Arguments:

* orientaion: display orientation, can be either gdisplay.LANDSCAPE, gdisplay.LANDSCAPE_FLIP, gdisplay.PORTRAIT, or gdisplay.PORTRAIT_FLIP.

Returns: nothing, or an exception.

```lua
-- Set the display orientation to LANDSCAPE_FLIP
gdisplay.setorient(gdisplay.LANDSCAPE_FLIP)
```

# Clipping functions

## gdisplay.setclipwin(point0, point1)

Sets the clipping area coordinates. All writing to the display is clipped to that area.

Arguments:

* point0: top left point of the clipping area.
* point1: bottom right point of the clipping area.

Returns: nothing, or an exception.

```lua
-- Set the clipping area to (10,10) - (50, 50)
gdisplay.setclipwin({10,10}, {50, 50})

-- Draw a pixel outside the clipping area. Pixel is not show
-- on the display.
gdisplay.pixel({1,1})

-- Draw a pixel inside the clipping area. Pixel is show
-- on the display.
gdisplay.pixel({1,1})
```

## gdisplay.resetclipwin()

Reset the clipping area to full screen.

Arguments: nothing
Returns: nothing, or an exception.

# Text functions

Text functions are used for write text.

## gdisplay.setrot(angle)

Set text rotation when writing text.

Arguments:

* angle: rotation angle, in degrees (from 0 to 360)

Returns: nothing, or an exception.

## gdisplay.settransp(transparency)

Set transparency when writing the text.

Arguments:

* transparency: if true only text foreground color is shown, if false all the text background is filled with the background color.

Returns: nothing, or an exception.

## gdisplay.setwrap(wrap)

Set line wrapping when writing the text. If wrap is true, text will be wrap to new line, otherwise it will be clipped.

Arguments:

* wrap: if true wrapping is on.

Returns: nothing, or an exception.