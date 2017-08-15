# About this

This module contains functions for accessing the CPU's SPI module.

SPI units are encoded into a byte and are platform-dependent. For this reason the SPI module define a numeric constant for each available SPI unit. For example in ESP32 SPI1 is defined by the constant spi.SPI1. Please refer to your platform or board documentation to know which SPI units are available. If you refer to an inexistent SPI, a nil value is returned.

SPI module can work in master or slave mode, each of then identified by spi.MASTER and spi.SLAVE constants. For now only spi.MASTER is allowed.

The functions of this module are organized in the following categories:

* [Information functions](#information-functions)
* [Configuration functions](#configuration-functions)
* [Operation functions](#operation-functions)

# Key concepts

The Serial Peripheral Interface (SPI) bus is a synchronous serial communication interface specification used for short distance communication, primarily in embedded systems. The interface was developed by Motorola in the late eighties and has become a de facto standard.

SPI devices communicate in full duplex mode using a master-slave architecture with a single master. The master device originates the frame for reading and writing. 

An SPI use 4 signals:

* CLK / SCK: Serial Clock (output from master).
* MOSI / SDO: Master Output, Slave Input (output from master).
* MISO / SDI: Master Input, Slave Output (output from slave).
* SS   / CS : Slave Select (active low, output from master).

Multiple slave devices can share the same SPI bus (SCK, SDO and SDI lines), and each of them are selected through individual CS lines per device, when the master needs to communicate with one device; in addition each device can work at different speeds, clock polarity, etc ...

To use this module you must take into consideration the following:

1. Attach an SPI device, using the spi.attach function. The attach function returns an instance of the SPI device. You must store this instance into a variable for further operation with it.

   ```lua
   device = spi.attach(.....)
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

# Information functions

## spi.pins([table])

List the pins assigned to the SPI ports. The initial assignments are defined in Kconfig under the Component config -> Lua RTOS -> Hardware -> SPI pin map. Prior to use any spi module function you can change the assigned pins through the spi.setpins function.


Arguments:

* table: if true, pin list is returned in a Lua table, if false pin list is printed on the console.

Returns:

* if table is false: nothing or an exception.

* if table is true: a Lua table with the pin list, or an exception. This table is an array of tables. Each entry corresponds to a SPI port. Each port gives the following fields:

  * id: the SPI port id.
  * miso: the GPIO number assigned to the miso signal.
  * mosi: the GPIO number assigned to the mosi signal.
  * clk: the GPIO number assigned to the clk signal.

```lua
/ > spi.pins()
SPI2: miso=GPIO12 mosi=GPIO13 clk=GPIO14 
SPI3: miso=GPIO19 mosi=GPIO23 clk=GPIO18 
```

# Contiguration functions

## spi.setpins(id, miso, mosi, clk)

Sets the pins assigned to an SPI port. Use this function if you need to change the initial assignments. The initial assignments are defined in Kconfig under the Component config -> Lua RTOS -> Hardware -> SPI pin map.

Arguments:

* id: SPI unit identifier. Use spi.SPIx defined for this purpose.
* miso: GPIO number assigned to the miso signal. Use any pio.GPIOxx constant for this.
* mosi: GPIO number assigned to the mosi signal. Use any pio.GPIOxx constant for this.
* clk: GPIO number assigned to the clk signal. Use any pio.GPIOxx constant for this.

## spi = spi.attach(id, mode, cs, speed, data bits, mode number, [flags])

Attach a SPI device.

Arguments:

* id: SPI unit identifier. Use spi.SPIx defined for this purpose.
* mode: SPI mode, can be either spi.MASTER or spi.SLAVE.
* cs: device's chip select pin, for example gpio.GPIO5. If cs is 0 the default cs pin for this SPI unit is used.
* speed: speed of the spi module, expressed in hertz.
* data bits: can be either, 8, 16 or 32 bits.
* mode number: an integer between 0 and 3, according the following table:

  |mode number|polarity|phase|
  |-----------|--------|-----|
  |     0     |   0    |  0  |
  |     1     |   0    |  1  |
  |     2     |   1    |  0  |
  |     3     |   1    |  1  |


* flags (optional): a bit mask formed by the following constants
   * spi.READ: attach the spi device as read only (only MISO is used)
   * spi.WRITE: attach the spi device as write only (only MOSI is used)
   * default value is spi.READ | spi.WRITE: attach the spi device as read / write (MISO and MOSI are used)


Returns: spi device instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Attach a SPI device using SPI2 as master, 1 Mhz speed, 8 bits, using GPIO5 as CS, number mode 0
device = spi.attach(spi.SPI2, spi.MASTER, pio.GPIO5, 1000000, 8, 0)
```

# Operation functions

## instance:select()

Select the SPI device.

Arguments: nothing.
Returns: nothing, or an exception.


```lua
-- Attach a SPI device using SPI2 as master, 1 Mhz speed, 8 bits, using GPIO5 as CS, number mode 0
device = spi.attach(spi.SPI2, spi.MASTER, pio.GPIO5, 1000000, 8, 0)

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
-- Attach a SPI device using SPI2 as master, 1 Mhz speed, 8 bits, using GPIO5 as CS, number mode 0
device = spi.attach(spi.SPI2, spi.MASTER, pio.GPIO5, 1000000, 8, 0)

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
-- Attach a SPI device using SPI2 as master, 1 Mhz speed, 8 bits, using GPIO5 as CS, number mode 0
device = spi.attach(spi.SPI2, spi.MASTER, pio.GPIO5, 1000000, 8, 0)

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
-- Attach a SPI device using SPI2 as master, 1 Mhz speed, 8 bits, using GPIO5 as CS, number mode 0
device = spi.attach(spi.SPI2, spi.MASTER, pio.GPIO5, 1000000, 8, 0)

-- Select
device:select()

-- Write and read
print(device:write("Hello, Lua RTOS!"))

-- Deselect
device:deselect()
```