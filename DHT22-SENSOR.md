# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | DHT22       | ![](http://git.whitecatboard.org/dht22.png)                           |
| Interface    | GPIO        | 1 pin                      |
| Provides     | temperature | celsius degrees            |
|              | humidity    | % relative humidity        |
| Properties   | none        |                            |
| [Datasheet](https://cdn-shop.adafruit.com/datasheets/Digital+humidity+and+temperature+sensor+AM2302.pdf)    |             |                            |


# Code

```lua
-- Attach DHT22 to GPIO26
s = sensor.attach("DHT22", pio.GPIO26)

while true do
  print("temp: "..s:read("temperature")..", hum: "..s:read("humidity"))
  tmr.delayms(500)
end
```

[Back to sensor list](./Sensor-module#supported-sensors)
