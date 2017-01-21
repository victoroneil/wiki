# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | DHT11       |                            |
| Interface    | GPIO        | 1 pin                      |
| Provides     | temperature | celsius degrees            |
|              | humidity    | % relative humidity        |
| Settings     | none        |                            |
| [Datasheet] (http://www.micropik.com/PDF/dht11.pdf)    |             | ![](http://whitecatboard.org/git/dht11.jpg)                           |


# Code

```lua
s1 = sensor.setup("DHT11", pio.GPIO4)

s1:acquire()

s1:read("temperature")
s1:read("humidity")
```