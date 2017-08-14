# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | DHT22       |                            |
| Interface    | GPIO        | 1 pin                      |
| Provides     | temperature | celsius degrees            |
|              | humidity    | % relative humidity        |
| Properties   | none        |                            |
| [Datasheet](https://cdn-shop.adafruit.com/datasheets/Digital+humidity+and+temperature+sensor+AM2302.pdf)    |             | ![](http://git.whitecatboard.org/dht22.jpg)                           |


# Code

```lua
s1 = sensor.attach("DHT22", pio.GPIO4)

s1:read("temperature")
s1:read("humidity")
```