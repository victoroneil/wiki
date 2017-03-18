# About this

This module contains functions for accessing the CPU's SPI module.

SPI units are encoded into a byte and are platform-dependent. For this reason the SPI module define a numeric constant for each available SPI unit. For example in ESP32 SPI1 is defined by the constant spi.SPI1. Please refer to your platform or board documentation to know which SPI units are available. If you refer to an inexistent SPI, a nil value is returned.

SPI module can work in master or slave mode, each of then identified by spi.MASTER and spi.SLAVE constants. For now only spi.MASTER is allowed.


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

1. Create a SPI instance device, using the spi.setup function, and store the instance into a variable.

  ```lua
   device = spi.setup(.....)
   ```

2. Use the device instance for select the device. This selects the device trough the CS pin connected to the device and configures the bus (speed, polarity, etc ...):

   ```lua
   device:select()
   ```

3. Use the device instance for read from / write to the device:

   ```lua
   device:write(...)
   ```

4. Use the device instance for deselect the device. This deselects the device trough the CS pin connected to the device and disconnects the device from the bus:

   ```lua
   instance:deselect()
   ```

# Utility functions

# Setup functions

## spi = spi.setup(id, mode, cs, speed, data bits, mode number)

Setup a SPI device.

Arguments:

* id: SPI unit identifier. Use spi.SPIx defined for this purpose.
* mode: SPI mode, can be either spi.MASTER or spi.SLAVE.
* cs: device's chip select pin, for example gpio.GPIO5. If cs is 0 the default cs pin for this SPI unit is used.
* speed: speed of the spi module, expressed in kilohertz.
* mode number: an integer between 0 and 3, according the following table:

  |mode number|polarity|phase|
  |-----------|--------|-----|
  |     0     |   0    |  0  |
  |     1     |   0    |  1  |
  |     2     |   1    |  0  |
  |     3     |   1    |  1  |

* data bits: can be either, 8, 16 or 32 bits.

Returns: spi device instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Setup a SPI device using SPI2 as master, 1 Mhz speed, 8 bits, using GPIO5 as CS, number mode 0
device = spi.setup(spi.SPI2, spi.MASTER, pio.GPIO5, 1000, 8, 0)
```

# Operation functions

## instance:select()

Select the SPI device.

Arguments: nothing.
Returns: nothing, or an exception.


```lua
-- Setup a SPI device using SPI2 as master, 1 Mhz speed, 8 bits, using GPIO5 as CS, number mode 0
device = spi.setup(spi.SPI2, spi.MASTER, pio.GPIO5, 1000, 8, 0)

-- Select
device:select()

-- Do something
...
...
```


## instance:deselect()

Deselect the SPI device.

Arguments: nothing.
Returns: nothing, or an exception.


```lua
-- Setup a SPI device using SPI2 as master, 1 Mhz speed, 8 bits, using GPIO5 as CS, number mode 0
device = spi.setup(spi.SPI2, spi.MASTER, pio.GPIO5, 1000, 8, 0)

-- Select
device:select()

-- Do something
...
...

-- Deselect
device:deselect()
```


## instance:write(data1, [data2], ... [datan])

Write data to the spi device.

Arguments:
* data1 to datan: data to write, can be either a byte or a string.

Returns: nothing, or an exception.

```lua
-- Setup a SPI device using SPI2 as master, 1 Mhz speed, 8 bits, using GPIO5 as CS, number mode 0
device = spi.setup(spi.SPI2, spi.MASTER, pio.GPIO5, 1000, 8, 0)

-- Select
device:select()

-- Do something
device:write("Hello, Lua RTOS!")

-- Deselect
device:deselect()
```


## readed data = instance:readwrite(data1, [data2], ... [datan])

Write and read data to a SPI device.

Arguments:
* data1 to datan: data to write, can be either a byte or a string.

Returns: readed data, or an exception.

```lua
-- Setup a SPI device using SPI2 as master, 1 Mhz speed, 8 bits, using GPIO5 as CS, number mode 0
device = spi.setup(spi.SPI2, spi.MASTER, pio.GPIO5, 1000, 8, 0)

-- Select
device:select()

-- Write and read
print(device:write("Hello, Lua RTOS!"))

-- Deselect
device:deselect()
```