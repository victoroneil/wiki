# About this

This module contains functions for accessing the CPU's SPI module.

SPI units are encoded into a byte and are platform-dependent. For this reason the SPI module define a numeric constant for each available SPI unit. For example in ESP32 SPI1 is defined by the constant spi.SPI1. Please refer to your platform or board documentation to know which SPI units are available. If you refer to an inexistent SPI, a nil value is returned.

SPI module can work in master or slave mode, each of then identified by spi.MASTER and spi.SLAVE constants.


# Key concepts

The Serial Peripheral Interface (SPI) bus is a synchronous serial communication interface specification used for short distance communication, primarily in embedded systems. The interface was developed by Motorola in the late eighties and has become a de facto standard.

SPI devices communicate in full duplex mode using a master-slave architecture with a single master. The master device originates the frame for reading and writing. 

SPI use 4 signals:

* SCLK / SCK: Serial Clock (output from master).
* MOSI / SDO: Master Output, Slave Input (output from master).
* MISO / SDI: Master Input, Slave Output (output from slave).
* SS   / CS : Slave Select (active low, output from master).

Multiple slave devices can share the same SPI bus (SCK, SDO and SDI lines), and each of them are selected through individual CS lines per device, when the master needs to communicate with one device; in addition each device can work at different speeds, clock polarity, etc ...

To use this module you must take into consideration the following:

1. Create an SPI instance per device, using the spi.setup function, and store the instance into a variable.

  ```lua
   instance = spi.setup(.....)
   ```

2. Use the variable instance for select the device. This selects the device trough the CS pin connected to the device and configures the bus (speed, polarity, etc ...):

   ```lua
   instance:select()
   ```

3. Use the variable instance for read from / write to the device:

   ```lua
   instance:write(...)
   ```

4. Use the variable instance for deselect the device. This deselects the device trough the CS pin connected to the device and disconnects the device from the bus:

   ```lua
   instance:deselect()
   ```

# Utility functions

## spi.pins()

Show available SPI units, an it's pins, provided but your platform.
   
```lua
/ > spi.pins()
spi1: sdi=07	(pin  7)	sdo=08	(pin  8)	sck=06	(pin  6)
spi2: sdi=012	(pin 12)	sdo=013	(pin 13)	sck=014	(pin 14)
spi3: sdi=019	(pin 19)	sdo=023	(pin 23)	sck=018	(pin 18)
/ >
```


# Setup functions

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

# Operation functions

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