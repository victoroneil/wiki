# About this

This module contains functions for access the sensors supported by Lua RTOS. Although with Lua RTOS you can access sensors using the provided hardware access modules, mostly used sensors in education and industry are supported directly by the operating system. Please feel free to send us any suggestion for include new sensors in Lua RTOS.

Sensor module allows the programmer to access sensors in an unified way from a common programming interface, programs are written faster, and source code is more clearly:

```lua
-- Instantiate a DHT11 sensor connected to GPIO4
s1 = sensor.setup("DHT11", pio.GPIO4)

-- Read temperature and humidity
s1:read("temperature")
s1:read("humidity")
````

# Key concepts

A sensor is a device that measures some type of magnitude from the physical environment, and generates an output signal  that can be process by other devices. The magnitude could be temperature, humidity, motion, sound, etc.

To use a sensor in your program you must do the following:

1. Attach a sensor to it's hardware interface, using the sensor.attach function. This returns a sensor instance that you must store into a variable.

   ```lua
   -- Attach a DHT11 sensor connected to GPIO4
   s1 = sensor.setup("DHT11", pio.GPIO4)
   ````

2. Use the sensor instance for read data provided by the sensor:

   ```lua
   -- Read data provided by sensor
   s1:read("temperature")
   s1:read("humidity")
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

# Supported sensors

Here is the list of sensors currently natively supported in Lua RTOS.

  * Temperature
    - [DHT11] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/DHT11-SENSOR)
    - [TMP36] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/TMP36-SENSOR)

  * Humidity
    - [DHT11] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/DHT11-SENSOR)

  * Distance
    - [PING))) 28015 ultrasonic sensor] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/PING-28015-ultrasonic-sensor)