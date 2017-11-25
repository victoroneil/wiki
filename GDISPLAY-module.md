**This page is under construction**

# About this

This module contains functions for accessing graphic SPI displays, and gives the programmer an api to work with SPI graphic displays in a unified form, regardless of the used display.

There are functions in this module that are not compatible with some displays. For example, it's not possible to show a JPG image (true color) in a monochrome display. Don't worry about this, the module raises an exception in this case.

# Supported chipsets

| Chipset      | Variants     | Comments                   | Identifier           |
|--------------|--------------|----------------------------|----------------------|
| ST7735       | ST7735_18    | Black tab, 1.8"            | gdisplay.ST7735_18   |
|              | ST7735B_18   | Blue tab, 1.8"             | gdisplay.ST7735B_18  |
|              | ST7735G_18   | Green tab, 1.8"            | gdisplay.ST7735G_18  |
|              | ST7735G_144  | Green tab, 1.44"           | gdisplay.ST7735G_144 |
|              | ST7735_096   | Green tab, 0.96"           | gdisplay.ST7735_096  |
| PCD8544      | ---          | Nokia 5110                 | gdisplay.PCD8544     |
| ILI9341      | ---          | ---                        | gdisplay.ILI9341     |

When using a display with this module you must attach the display, using the gdisplay.attach function, using the right display identifier.

# System fonts

| Font      | Identifier             | Comments |
| ----------|------------------------|----------|
| Default   | gdisplay.FONT_DEFAULT | |
| DejaVu 18 | gdisplay.FONT_DEJAVU18 | |
| DejaVu 24 | gdisplay.FONT_DEJAVU24 | |
| Ubuntu 16 | gdisplay.FONT_UBUNTU16 | |
| Comic 24  | gdisplay.FONT_COMIC24  | |
| Tooney 32 | gdisplay.FONT_TOONEY32 | |
| Minya 24  | gdisplay.FONT_MINYA24  | |
| 7segments | gdisplay.FONT_7SEG | |
| LCD       | gdisplay.FONT_LCD | Old style font, used in the past in smalls LCD, such as NOKIA 5110 |

# Points

Screen's coordinates are referenced as points. Many functions of this module expects one ore more points as an argument. For example, the gdisplay.putpixel has the following arguments:

* point: the point coordinates where draw the pixel.
* color (optional): the color to use for draw the pixel.

You can reference a point in two ways:

* table notation: in this case the point is referenced as a table in format {x, y}, where x and y are the point's coordinates.

   ```lua
   gdisplay.putpixel({10,10})
   ```

* legacy notation: in this case the point's coordinates are referenced as classical function arguments, using one argument for x and another argument for y.

   ```lua
   gdisplay.putpixel(10,10)
   ```

We recommend to use the table notation, because source code is more clear.


# Colors

Colors are referenced by it's R (red), G (green) and B (blue) components. Many functions of this module expects one ore more colors as an argument. For example, the gdisplay.clear has a color argument.

You can reference a color in two ways:

* table notation: in this case the color is referenced as a table in format {r, g, b}, where r, g and b are the color's components.

   ```lua
   gdisplay.clear({255,0,0})
   ```

* a system color: in this case the color is referenced using a predefined gdisplay constant.

   ```lua
   gdisplay.clear(gdisplay.RED)
   ```

   Available system colors:
   
   | Constant             | Constant           |
   |----------------------|--------------------|
   | gdisplay.BLACK       | gdisplay.BLUE      |
   | gdisplay.CYAN        | gdisplay.DARKCYAN  |
   | gdisplay.DARKGREEN   | gdisplay.GREEN     |
   | gdisplay.GREENYELLOW | gdisplay.LIGHTGREY |
   | gdisplay.MAGENTA     | gdisplay.MAROON    |
   | gdisplay.NAVY        | gdisplay.OLIVE     |
   | gdisplay.ORANGE      | gdisplay.PINK      |
   | gdisplay.PURPLE      | gdisplay.RED       |
   | gdisplay.WHITE       | gdisplay.YELLOW    |


# General purpose functions

## gdisplay.attach(chipset, [orientation, framed])

Initialize the display and clear the screen.

After the initialization the display has the following settings:

* All the pixels are turn off.
* Text foreground is set to white.
* Text background is set to black.
* Text rotation is set to 0 degrees.
* Text warp is set to false.
* Text transparency is set to true.

Arguments:

* chipset: chipset used by the display. Can be any identifier from the [supported chipsets](#supported-chipsets).
* orientation (optional): display orientation, can be either gdisplay.LANDSCAPE, gdisplay.LANDSCAPE_FLIP, gdisplay.PORTRAIT, or gdisplay.PORTRAIT_FLIP. Default orientation is gdisplay.LANDSCAPE.
* framed (optional): if true frame buffer is used. Default is false.

Returns: nothing, or an exception.

```lua
-- Attach an ILI9341 display with orientation LANDSCAPE_FLIP,
-- and without frame buffer
gdisplay.attach(gdisplay.ILI9341, gdisplay.LANDSCAPE_FLIP, false)
```

## gdisplay.getscreensize()

Get current screen size (width & height) in pixels. Remember that for the same display, the screen size may vary depending on the screen's orientation.

Arguments: nothing.

Returns: the screen size, or an exception

* xsize: width of the screen in pixels
* ysize: height of the screen in pixels

## gdisplay.clear([color])

Clear the display to the specified color. Any text property is change when the display is clear, such as text wrap, text orientation, etc ...

Arguments:

* color (optional): the color used to fill de display. The default color depends on the display chipset, for example in TFT displays it is black, and in monochrome LCD displays it is white. In general, the default color is one that keeps all of the screen pixels off.

Returns: noting, or an exception.

```lua
-- Clear the display to RED
gdisplay.clear(gdisplay.RED)

-- Clear the display to RED
gdisplay.clear({255, 0, 0})

-- Clear the display to default color
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
gdisplay.putpixel({1,1})

-- Draw a pixel inside the clipping area. Pixel is show
-- on the display.
gdisplay.putpixel({20,20})
```

## gdisplay.resetclipwin()

Reset the clipping area to full screen.

Arguments: nothing
Returns: nothing, or an exception.

```lua
-- Reset the clipping area to full screen
gdisplay.resetclipwin()

-- Pixel now is show on the display.
gdisplay.putpixel({1,1})
```

# Text functions

Text functions are used for write text.

## gdisplay.setforeground(color)

Set the foreground color. The foreground color is used to write text when the color is not specified.

Arguments:

* color: the foreground color

Returns: nothing, or an exception.

## gdisplay.setbackground(color)

Set the background color. The background color is used to write text when the color is not specified.

Arguments:

* color: the foreground color

Returns: nothing, or an exception.

## gdisplay.setfont(font identifier | font name)

Set the font used when writing the text to display.

Arguments:

* font identifier: the identifier of the system's font. Can be any identifier from the [system fonts](#system-fonts).
* font name: if the programmer wants to use a custom font, the file name with the font definition.

Returns: nothing, or an exception.

```lua
-- Set the font to UBUNTU16_FONT
gdisplay.setfont(gdisplay.UBUNTU16_FONT)
```

## gdisplay.getfontsize()

Get current font size in pixels. Useful if FONT_7SEG is used to get actual character width and height.

Arguments: nothing

Returns: the font size, or an exception

* xsize: width of the font character in pixels. For the proportional fonts, maximal char width will be returned.
* ysize: height of the font character in pixels.

## gdisplay.getfontheight()

Get current font height in pixels.

Arguments: nothing

Returns: height of the font character in pixels, or an exception.

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

## gdisplay.setfixed(force)

Forces fixed width print when using proportional fonts.

Arguments:

* force: if true force fixed.
Returns: nothing, or an exception.

# Drawing functions

## gdisplay.putpixel(point, [color])

Draws pixel on display at the point coordinates using the current foreground color, or a given color.

Arguments:

* point: the [point coordinates](#points) where draw the pixel.
* color (optional): the [color](#colors) to use for draw the pixel. If not specified, the foreground color is used.

Returns: nothing, or an exception.

```lua
-- Draw a pixel at point (50, 50), using current foreground
gdisplay.putpixel(50, 50)

-- Draw a pixel at point (50, 50), using current foreground
gdisplay.putpixel({50, 50})

-- Draw a pixel at point (50, 50), using RED color
gdisplay.putpixel({50, 50}, gdisplay.RED)

-- Draw a pixel at point (50, 50), using RED color
gdisplay.putpixel({50, 50}, {255, 0, 0})
```

## gdisplay.line(point 1, point 2,  [color])

Draws line from point 1 to point 2, using the current stroke color, or a given color.

Arguments:

* point 1: the start [point coordinates](#points).
* point 2: the end [point coordinates](#points).
* color (optional): the [color](#colors) to use for draw the line. If not specified, the stroke color is used.

Returns: nothing, or an exception.

```lua
-- Get the screen size
dw, dh = gdisplay.getscreensize()

-- Draw a diagonal line, from the first screen's point to
-- the last screen's point
gdisplay.line({0,0}, {dw - 1, dh - 1})
```

## gdisplay.rect(point, width, height, [color, fill color])

Draws a width * height rectangle starting at point, using the current stroke color, or a given color.  If the fill color is given, fills the rectangle.

Arguments:

* point: the start [point coordinates](#points).
* width: width of the rectangle in pixels.
* height: height of the rectangle in pixels.
* color (optional): the [color](#colors) to use for draw the rectangle. If not specified, the stroke color is used.
* fill color (optional): the [color](#colors) to use for fill the rectangle.

Returns: nothing, or an exception.

```lua
-- Get the screen size
dw, dh = gdisplay.getscreensize()

-- Draw a diagonal line, from the first screen's point to
-- the last screen's point
gdisplay.line({0,0}, {dw - 1, dh - 1})
```

Returns: nothing, or an exception.

```lua
-- Get the screen size
dw, dh = gdisplay.getscreensize()

-- Display 50 x 50 white rectangle, starting at screen's center, and blue filled
gdisplay.rect({dw / 2 - 1, dh / 2 - 1}, 50, 50, {255, 255, 255}, {0,0,255})
```

## gdisplay.circle(center point, radius, [color, fill color])

Draws a circle centered at center point with a given radius, using the current stroke color, or a given color.  If the fill color is given, fills the circle.

Arguments:

* center point: the center [point coordinates](#points).
* radius: circle's radius in pixels.
* color (optional): the [color](#colors) to use for draw the rectangle. If not specified, the stroke color is used.
* fill color (optional): the [color](#colors) to use for fill the rectangle.

Returns: nothing, or an exception.

```lua
-- Get the screen size
dw, dh = gdisplay.getscreensize()

-- Draw a 80-pixel radius white circle, centered at the screen, and blue filled
gdisplay.circle({dw /2 - 1, dh / 2 - 1}, 80, {255, 255, 255}, {0,0,255})
```

## Full examples

Display the "Senyera", the Catalonian's flag. This flag has been selected as a testimonial of where Lua RTOS has been developed.

```lua
function senyera()
	-- Attach
	gdisplay.attach(gdisplay.ILI9341, gdisplay.LANDSCAPE_FLIP, false)
	gdisplay.clear()

	-- Get the screen size
	local dw, dh = gdisplay.getscreensize()

	-- The Senyera has 9 bands
	local band = dh / 9

	-- The Senyera has 2 colors
	-- even bands are yellow, and odd bands are red
	color1 = gdisplay.YELLOW
	color2 = gdisplay.RED

	-- Draw bands
	i = 1
	y = 0
	for i = 1,9,1 do
	   if (i % 2 == 1) then
	      color = color1
	   else
	      color = color2
	   end 
   
	   gdisplay.rect({0, y}, dw - 1, band, color, color)
	   y = y + band - 1
	end
end

senyera()
```