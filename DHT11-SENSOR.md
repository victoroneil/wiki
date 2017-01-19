![](http://whitecatboard.org/git/dht11.jpg)

|              |             | Comments                   |
|--------------|-------------|----------------------------|
| Interface    | GPIO        | 1 pin                      |
| Provides     | temperature | celsius degrees            |
|              | humidity    | % relative humidity        |

**Example code **

```lua
s1 = sensor.setup("DHT11", pio.GPIO4)

s1:acquire()

temperature = s1:read("temperature")
humidity = s1:read("humidity")
```

[Datasheet] (http://www.micropik.com/PDF/dht11.pdf)