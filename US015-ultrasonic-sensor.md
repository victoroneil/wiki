# About this

The US-015 sensor works by transmitting an ultrasonic burst and providing an output pulse that corresponds to the time required for the burst echo to return to the sensor. The distance is calculated by measuring the echo pulse width.

Please, take in mind, that sound speed depends on ambient temperature, about 0.6 m/secs per celsius degree, so combine this sensor with a temperature sensor if you want to get accurate measurements or if the sensor can be subjected to a wide temperature range.

**Power supply:**

* Supply voltage: +5 VDC

# Specification

| What         |             | Comments                                    |
|--------------|-------------|---------------------------------------------|
| Identifier   | US015       | ![](http://git.whitecatboard.org/us015.png)                                            |
| Interface    | 2 GPIO      | GPIO1: trigger signal<br/>GPIO2: echo signal. |
| Provides     | distance    | cm                                          |
|              | calibration | +/- cm. Default set to 0 cm.          |
| Properties   | temperature | current ambient temperature                 |
|     |             |                             |

# Code

```lua
-- Attach sensor to GPIO26 (TRIG) and GPIO14 (ECHO)
s = sensor.attach("US015", pio.GPIO26, pio.GPIO14)

-- We set the ambient temperature to 25º for adjust the sound speed,
-- used internally for calculate the distance from an
-- object
s:set("temperature", 25)

while true do
  print("distance: "..s:read("distance"))
  tmr.delayms(500)
end
```

# Code

In this example a BME280 sensor is used for set the ambient temperature at regular interval.

```lua
-- Create an event for syncronize the ping thread with
-- the temp thread. We don't want to take the first measure
-- until the thread temp sets the ping temp
tempSet = event.create()

-- Attach sensor to GPIO26 (TRIG) and GPIO14 (ECHO)
ping = sensor.attach("US015", pio.GPIO26, pio.GPIO14)

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
	  
      -- Read temperature again in 5 seconds
      tmr.sleep(5)
   end
end)

-- Ping thread
thread.start(function()
   tempSet:wait()
      
   while true do
      print("distance: "..ping:read("distance"))
	  
      tmr.sleepms(1000)
   end
end)
```

[Back to sensor list](./Sensor-module#supported-sensors)
