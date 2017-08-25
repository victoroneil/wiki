# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | DHT11       |                            |
| Interface    | GPIO        | 1 pin                      |
| Provides     | temperature | celsius degrees            |
|              | humidity    | % relative humidity        |
| Properties   | none        |                            |
| [Datasheet](http://www.micropik.com/PDF/dht11.pdf)    |             | ![](http://git.whitecatboard.org/dht11.jpg)                           |


# Code

```lua
-- Attach DHT11 to  GPIO26
s = sensor.attach("DHT11", pio.GPIO26)

while true do
  print("temp: "..s:read("temperature")..", hum: "..s:read("humidity"))
  tmr.delayms(500)
end
```