# About this

This module contains functions for accessing the sensors supported by Lua RTOS. Although Lua RTOS allows you to access sensor data using the provided hardware access modules, mostly used sensors in education and industry are supported directly by the operating system. Please feel free to send us any suggestion for include new sensors in Lua RTOS.

Sensor module allows the programmer to access sensors in an unified way from a common interface. Programs are written faster and source code is more clearly.

```lua
s1 = sensor.setup("DHT11", pio.GPIO4)
s1:acquire()
s1:read("temperature")
s1:read("humidity")
````

# Supported sensors

  * Temperature
    - DHT11
    - TMP36

  * Humidity
    - DHT11

  * Distance
    - PING))) 28015