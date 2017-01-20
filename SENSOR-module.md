# About this

This module contains functions for accessing the sensors supported by Lua RTOS. Although Lua RTOS allows you to access sensor data using the provided hardware access modules, mostly used sensors in education and industry are supported directly by the operating system. Please feel free to send us any suggestion for include new sensors in Lua RTOS.

Sensor module allows the programmer to access sensors in an unified way from a common interface. Programs are written faster and source code is more clearly.

```lua
-- Instantiate a DHT11 sensor connected to GPIO4
s1 = sensor.setup("DHT11", pio.GPIO4)

-- Acquire data
s1:acquire()

-- Read temperature and humidity
s1:read("temperature")
s1:read("humidity")
````

# Supported sensors

Here is the list of sensors currently natively supported in Lua RTOS. Remember that through Kconfig options you can build your own firmware only with the sensors that you need for your project.

  * Temperature
    - [DHT11] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/DHT11-SENSOR)
    - [TMP36] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/TMP36-SENSOR)

  * Humidity
    - [DHT11] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/DHT11-SENSOR)

  * Distance
    - [PING))) 28015 ultrasonic sensor] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/PING)))-28015-ultrasonic-sensor)