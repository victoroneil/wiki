# About this

This module contains functions for accessing the CPU's I2C module.

I2C units are encoded into a byte and are platform-dependent. For this reason the I2C module define a numeric constant for each available I2C unit. For example in ESP32 I2C0 is defined by the constant i2c.I2C0. Please refer to your platform or board documentation to know which I2C units are available. If you refer to an inexistent I2C, a nil value is returned.

I2C module can work in master or slave mode, each of then identified by i2c.MASTER and i2C.SLAVE constants. For now only i2c.MASTER is allowed.

The functions of this module are organized in the following categories:

* [Configuration functions](#configuration-functions)
* [Operation functions](#operation-functions)
* [Example](#example)

# Key concepts

I²C (Inter-Integrated Circuit), is a multi-master, multi-slave, packet switched, single-ended, serial computer bus invented by Philips Semiconductor (now NXP Semiconductors). It is typically used for attaching lower-speed peripheral ICs to processors and microcontrollers in short-distance, intra-board communication.

I²C uses only two bidirectional open-drain lines, Serial Data Line (SDA) and Serial Clock Line (SCL), pulled up with resistors.

The I²C reference design has a 7-bit or a 10-bit (depending on the device used) address space. Common I²C bus speeds are the 100 kbit/s standard mode and the 10 kbit/s low-speed mode, but arbitrarily low clock frequencies are also allowed. Recent revisions of I²C can host more nodes and run at faster speeds (400 kbit/s Fast mode, 1 Mbit/s Fast mode plus or Fm+, and 3.4 Mbit/s High Speed mode). 

Note the bit rates are quoted for the transactions between master and slave without clock stretching or other hardware overhead. Protocol overheads include a slave address and perhaps a register address within the slave device, as well as per-byte ACK/NACK bits. Thus the actual transfer rate of user data is lower than those peak bit rates alone would imply. For example, if each interaction with a slave inefficiently allows only 1 byte of data to be transferred, the data rate will be less than half the peak bit rate.

The maximal number of nodes is limited by the address space and also by the total bus capacitance of 400 pF, which restricts practical communication distances to a few meters.

# Configuration functions

## instance = i2c.attach(id, mode, [speed])

Attach an I2C unit.

Arguments:

* id: I2C unit identifier. Use i2c.I2Cx defined for this purpose.
* mode: can be either i2c.MASTER or i2c.SLAVE. For now only i2c.MASTER is supported.
* speed (optional): I2C bus speed, expressed in hertz. This argument is optional, and if not provided default speed for 40000 (400 Khertz) is applied.

Returns: i2c device instance, or an exception. You must store this instance into a variable for further operations with it.

## instance:detach()

Detach an i2c device instance from the I2C bus, and release all the used resources.

Arguments: none.

Returns: nothing, or an exception.

## instance:setspeed(speed)

Set the I2C bus speed for a particular I2C instance.

Arguments:

* speed: I2C bus speed, expressed in hertz. 

Returns: nothing, or an exception.

# Operation functions

## instance:start()

Start an I2C transaction.

Arguments: none

Returns: nothing, or an exception.

## instance:address(address, read)

Send an address to the I2C bus for read or write, if the I2C instance is configured in master mode.

Arguments:

* address: an integer value, with the I2C address to send.
* read: a boolean value, that indicates if the address is used for read or write to / from the I2C bus. If it's true the address is used for read, and if it's false the address is used for write.

Returns: nothing, or an exception.

##  readed data = instance:read()

Read one byte from the I2C bus. Prior to use this function, you must send the I2C address for read.

Arguments: none

Returns:  readed data, or an exception.

## instance:write(byte0, [byte1, ..., byten])

Write one or more bytes to the I2C bus. Prior to use this function, you must send the I2C address for write.

Arguments:

* byte0, ...., byten: the bytes to write.

Returns: nothing, or an exception

## instance:write(string)

Write a string to the I2C bus. Prior to use this function, you must send the I2C address for write.

Arguments:

* string: the string to write.

Returns: nothing, or an exception

## instance:stop()

Stop an I2C transaction.

Arguments: none

Returns: nothing, or an exception.

# Example

This sample demonstrates how to communicate with i2c devices. The sample writes values into an EEPROM (4c256d) and then read from the EEPROM and test that values are equal.

```lua
-- Attach the eeprom to the i2c bus
function eeprom_attach()
  eeprom = i2c.attach(i2c.I2C0, i2c.MASTER, 400000)
end

-- Once the internally-timed write cycle has started and the EEPROM
-- inputs are disabled, acknowledge polling can be initiated.
-- This involves sending a start condition followed by the device address word.
-- If this fails (timeout, or ack not received) we can't write.
function eeprom_poll(devAddress) 
  local done = false
  
  while not done do
    try(
      function() 
        eeprom:start()
      eeprom:address(devAddress, false)
        eeprom:stop()
      done = true
      end
    )
  end
end

-- Write to eeprom (byte)
function eeprom_write(devAddress, address, value)
  eeprom:start()
  eeprom:address(devAddress, false)
  eeprom:write(0x00, address, value)
  eeprom:stop()

  eeprom_poll(devAddress)
end

-- Read from eeprom (byte)
function eeprom_read(devAddress, address)
  local read

  eeprom:start()
  eeprom:address(devAddress, false)
  eeprom:write(0x00, address)
  eeprom:start()
  eeprom:address(devAddress, true)

  read = eeprom:read()
  
  eeprom:stop()

  return read
end

-- Attach eeprom
eeprom_attach()

-- Write test bytes
for i=0,100 do
  eeprom_write(0x51, i, i)
end

-- Check bytes
for i=0,100 do
  if (eeprom_read(0x51, i) ~= i) then
    error("Readed "..read..", expected "..i)
  end
end
```
