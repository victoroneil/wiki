# About this

This module contains functions for access the sensors supported by Lua RTOS. Although with Lua RTOS you can access sensors using the provided hardware access modules, mostly used sensors in education and industry are supported directly by the operating system. Please feel free to send us any suggestion for include new sensors in Lua RTOS.

Sensor module allows the programmer to access sensors in an unified way from a common programming interface, programs are written faster, and source code is more clearly:

```lua
-- Instantiate a DHT11 sensor connected to GPIO4
s1 = sensor.attach("DHT11", pio.GPIO4)

-- Read temperature and humidity
s1:read("temperature")
s1:read("humidity")
````

# Key concepts

A sensor is a device that measures some type of magnitude from the physical environment, and generates an output signal  that can be process by other devices. The magnitude could be temperature, humidity, motion, sound, etc.

To use a sensor in your program you must do the following:

1. Attach the sensor to it's hardware interface, using the sensor.attach(..) function. This returns a sensor instance that you must store into a variable.

   ```lua
   -- Attach a DHT11 sensor connected to GPIO4
   s1 = sensor.attach("DHT11", pio.GPIO4)
   ````

2. Use the sensor instance for read data provided by the sensor:

   ```lua
   -- Read data provided by sensor
   s1:read("temperature")
   s1:read("humidity")
   ````

In some cases you must to configure your sensor, for example, set the measure resolution, set an alarm, etc. Sensor configuration are made using the set function:

```lua
-- Instantiate a DS1820 sensor connected to GPIO4
s1 = sensor.setup("DS1820", pio.GPIO4, 0x28ff900f, 0xb316041a)

-- Configure sensor resolution
s1:set("resolution", 10)

-- Read temperature
s1:read("temperature")
````

# Enumeration functions

Enumeration functions allows you to know which sensors are supported by your Lua RTOS firmware. Remember that through Kconfig options you can build your own firmware with the sensors that you need for your project.

These functions are usually used by the Whitecat IDE in order to know which sensors are supported by your board, but in some cases they will be useful for you.
 
## sensor.list([table])

List the sensors supported by your Lua RTOS firmware.

Arguments:

* table: if true, sensor's list is returned in a Lua table, if false sensor's list is printed on the console.

Returns:

* if table is false: nothing or an exception.

* if table is true: a Lua table with the sensor's list result, or an exception. This table is an array of tables. Each entry corresponds to a sensor. Each sensor gives the following fields:

  * id: the sensor's id.
  * interface: the sensor's interface name.

  * provides: an array with magnitudes provided by the sensor. Each magnitude have the following fields:
    * id: name of the magnitude.
    * type: data type of the magnitude. Can be either int, float or double.

  * settings: an array with setting parameters supported by the sensor. Each setting have the following fields:
    * id: name of the setting.
    * type: data type of the magnitude. Can be either int, float or double.

```lua
-- List the sensors supported by Lua RTOS firmware on the console
/ > sensor.list()
SENSOR      INTERFACE   PROVIDES                    SETTINGS                   
-------------------------------------------------------------------------------
DHT11       GPIO        temperature,humidity        
PING28015   GPIO        distance                    temperature
TMP36       ADC         temperature                 
```

```lua
-- List the sensors supported by Lua RTOS firmware to a table
sensors = sensor.list(true)
```

## sensor.enumerate(type, interface, [table])

In some cases, such as the 1-WIRE interface, sensors can be enumerated by the enumerate function. 

Arguments:

* type: enumeration type. For now only sensor.OWire are allowed.
* interface: the interface to enumerate. For now, a valid gpio.
* table: if true, enumeration list is returned in a Lua table, if falseenumeration list is printed on the console.

Returns:

* if table is false: nothing or an exception.

* if table is true: a Lua table with the enumeration list result, or an exception. This table is an array of tables. Each entry corresponds to a sensor. Each sensor gives the following fields for 1-WIRE:

  * id: the sensor's id.
  * device: device number in the bus.
  * addressh: the most significant word device address.
  * addressl: the less significant word device address.
  * model: a string containing the device's model name.

```lua
-- Enumerate the sensors connected to GPIO4 using 1-WIRE bus
/ > sensor.enumerate(sensor.OWire, pio.GPIO4)
SENSOR      DEVICE   ADDRESS             MODEL         
-------------------------------------------------------
DS1820      01       28ff900fb316041a    DS18B20
DS1820      02       28ffc1acb2160596    DS18B20
DS1820      03       28fff919b316034a    DS18B20
DS1820      04       28ffad17b31603d5    DS18B20
```

```lua
-- Enumerate the sensors connected to GPIO4 using 1-WIRE bus to a table
owire = sensor.enumerate(sensor.OWire, pio.GPIO4, true)
```

# Setup functions

## s = sensor.attach(id, ...)

Attach a sensor to it's hardware interface.

Arguments:

The arguments for this function varies according to the hardware interface type.

   For GPIO:
   ---------

      * id: a string containing the sensor id, for example DHT11.
      * gpio: the GPIO which sensor is attached. Use pio.GPIOx defined for this purpose.

   For ADC:
   --------

      * id: a string containing the sensor id, for example TMP36.
      * adc: ADC unit. Use adc.ADCx defined for this purpose.
      * channel: ADC channel. Use adc.ADC_CHx for this purpose.
      * resolution: resolution to use, can be either 12, 11, 10, 9, 8 or 6 bits.

   For 1-WIRE:
   -----------

      * id: a string containing the sensor id, for example DS1820.
      * gpio: the GPIO which sensor is attached. Use pio.GPIOx defined for this purpose.
      * adressh: sensor's address (most significant word) in the bus.
      * adressl: sensor's address (less significant word) in the bus.

Returns: a sensor instance or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Attach a DHT11 (gpio sensor) sensor to GPIO4
s = sensor.attach("DHT11", pio.GPIO4)
```

```lua
-- Attach a TMP36 (adc sensor) sensor using ADC1 module, ADC_CH6 channel
-- with a 12-bit resolution
s = sensor.attach("TMP36", adc.ADC1, adc.ADC_CH6, 12)
```

```lua
-- Attach a DS1820 (1-WIRE sensor) sensor to GPIO4 with 
-- address 0x28ff900fb316041a
s = sensor.attach("DS1820",pio.GPIO4, 0x28ff900f, 0xb316041a)
```

# Supported sensors

Here is the list of sensors currently natively supported in Lua RTOS.

  * Temperature
    - [DHT11] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/DHT11-SENSOR)
    - [TMP36] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/TMP36-SENSOR)

  * Humidity
    - [DHT11] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/DHT11-SENSOR)

  * Distance
    - [PING))) 28015 ultrasonic sensor] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/PING-28015-ultrasonic-sensor)