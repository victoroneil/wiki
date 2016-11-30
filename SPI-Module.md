# About this

This module contains functions for accessing the CPU's SPI module.

SPI units are encoded into a byte and are platform-dependent. For this reason the SPI module define a numeric constant for each available SPI unit. For example in ESP32 SPI1 is defined by the constant spi.SPI1. Please refer to your platform or board documentation to know which SPI units are available. If you refer to an inexistent SPI, a nil value is returned.

SPI module can work in master or slave mode, each of then identified by spi.MASTER and spi.SLAVE constants.


# Functions

## spi = spi.setup(id, mode, cs, speed, polarity, phase, data bits)

Setup the SPI module.

Arguments:

* id: SPI unit identifier. Use spi.SPIx defined for this purpose.
* mode: SPI mode, can be either spi.MASTER or spi.SLAVE.
* cs: chip select pin, for example gpio.GPIO5. If cs is 0 the default cs pin for this SPI unit is used.
* speed: speed of the spi module, expressed in kilohertz.
* polarity: clock polarity (0 or 1)
* phase: clock phase (0 or 1)
* data bits: can be either, 8, 16 or 32 bits.

Returns: an spi instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Setup SPI2 as master, 1 Mhz speed, 8 bits
instance = spi.setup(spi.SPI2, spi.MASTER, 0, 1000, 1, 1, 8)
```


## instance:select()

Select the SPI hardware attached to the SPI instance.

Arguments: nothing
Returns: nothing


```lua
-- Setup SPI2 as master, 1 Mhz speed, 8 bits
instance = spi.setup(spi.SPI2, spi.MASTER, 0, 1000, 1, 1, 8)

-- Select
instance:select()

-- Do something
...
...
```


## instance:deselect()

Deselect the SPI hardware attached to the SPI instance.

Arguments: nothing
Returns: nothing


```lua
-- Setup SPI2 as master, 1 Mhz speed, 8 bits
instance = spi.setup(spi.SPI2, spi.MASTER, 0, 1000, 1, 1, 8)

-- Select
instance:select()

-- Do something
...
...

-- Deselect
instance:deselect()
```


## instance:write(data1, [data2], ... [datan])

Write data to the spi instance.

Arguments:
* data1 to datan: data to write, can be either a byte or a string.

Returns: nothing, or an exception.

```lua
-- Setup SPI2 as master, 1 Mhz speed, 8 bits
instance = spi.setup(spi.SPI2, spi.MASTER, 0, 1000, 1, 1, 8)

-- Select
instance:select()

-- Do something
instance:write("Hello, Lua RTOS!")

-- Deselect
instance:deselect()
```


## readed data = instance:readwrite(data1, [data2], ... [datan])

Write and read data to the SPI instance.

Arguments:
* data1 to datan: data to write, can be either a byte or a string.

Returns: readed data, or an exception.

```lua
-- Setup SPI2 as master, 1 Mhz speed, 8 bits
instance = spi.setup(spi.SPI2, spi.MASTER, 0, 1000, 1, 1, 8)

-- Select
instance:select()

-- Write and read
print(instance:write("Hello, whitecat!"))

-- Deselect
instance:deselect()
```