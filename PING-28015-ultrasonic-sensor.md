# About this

This sensor provides precise, non-contact distance measurements from about 2 cm to 3 meters.

The PING))) sensor works by transmitting an ultrasonic (well above human hearing range) burst and providing an output pulse that corresponds to the time required for the burst echo to return to the sensor. By measuring the echo pulse width, the distance to target can easily be calculated.

Please, take in mind, that sound speed depends on ambient temperature, about 0.6 m/secs per celsius degree, so combine this sensor with a temperature sensor if you want to get accurate measurements or if the sensor can be subjected to a wide temperature range.

**Power supply:**

* Supply voltage: +5 VDC
* Supply current: 30 mA typ; 35 mA max 

# Specification

| What         |             | Comments                                    |
|--------------|-------------|---------------------------------------------|
| Identifier   | PING28015   | ![](http://git.whitecatboard.org/ping-sensor.png)                                            |
| Interface    | GPIO        | 1 pin                                       |
| Provides     | distance    | cm                                          |
|              | calibration | +/- cm. Default set to -0.6049 cm.          |
| Properties   | temperature | current ambient temperature                 |
| [Datasheet](https://www.parallax.com/sites/default/files/downloads/28015-PING-Sensor-Product-Guide-v2.0.pdf)    |             |                             |

# Code

```lua
-- Attach sensor to GPIO26
s = sensor.attach("PING28015", pio.GPIO26)

-- We tell to PING28015 that ambient temperature are 25º for adjust
-- the sound speed, used internally for calculate the distance from an
-- object
s:set("temperature", 25)

while true do
  print("distance: "..s:read("distance"))
  tmr.delayms(500)
end
```

# Code

In this example a BME280 sensor is used for set the ambient temperature at regular interval.

-- Create an event for syncronize the ping thread with
-- the temp thread. We don't want to take the first measure
-- until the thread temp sets the ping temp
tempSet = event.create()

-- Attach sensor to GPIO26
ping = sensor.attach("PING28015", pio.GPIO26)

-- Attach BME280 to I2C0, with default values
bme = sensor.attach("BME280", i2c.I2C0, 0)

-- Temperature thread
thread.start(function()
   local temp

   -- Read current ambient temperature
   temp = bme:read("temperature")

   -- Set current temperature to ping sensor
   ping:set("temperature", temp)

   tempSet:broadcast()

   while true do
      -- Read current ambient temperature
      temp = bme:read("temperature")

      -- Set current temperature to ping sensor
      ping:set("temperature", temp)
	  
      -- Read temperature again in 10 seconds
      tmr.sleep(5)
   end
end)

-- Ping thread
thread.start(function()
   tempSet:wait()
      
   while true do
      print("distance: "..ping:read("distance"))
	  
	  tmr.sleepms(500)
   end
end)

[Back to sensor list](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Sensor-module#supported-sensors)