# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | DHT23       | (http://git.whitecatboard.org/dht23.png)                            |
| Interface    | GPIO        | 1 pin                      |
| Provides     | temperature | celsius degrees            |
|              | humidity    | % relative humidity        |
| Properties   | none        |                            |
| [Datasheet](https://kropochev.com/downloads/humidity/AM2301.pdf)    |             | ![]                           |


# Code

```lua
-- Attach DHT23 to GPIO26
s = sensor.attach("DHT23", pio.GPIO26)

while true do
  print("temp: "..s:read("temperature")..", hum: "..s:read("humidity"))
  tmr.delayms(500)
end
```