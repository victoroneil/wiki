# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | AM412       |                            |
| Interface    | GPIO        |                            |
| Provides     | presence    | 1 = somebody in area       |
|              |             | 0 = nobody in area         |
| Properties   | none        |                            |
| [Datasheet](http://aitendo3.sakura.ne.jp/aitendo_data/product_img/sensor/AM412/Am412.pdf)    |             | ![](http://git.whitecatboard.org/AM412.png)                           |


# Code

In this example an AM412 is attached to GPIO26. Sensor changes are processed using a callback:
```lua
s = sensor.attach("AM412", pio.GPIO26)

s:callback(
   function(magnitude)
      if (magnitude["presence"] == 1) then
         print("somebody in area")
      else
         print("nobody in area")
      end
   end
)
```

In this example an AM412 is attached to GPIO26. Sensor changes are processed using an infinite loop:
```lua
s = sensor.attach("AM412", pio.GPIO26)

while true do
   if (s:read("presence") == 1) then
      print("somebody in area")
   else
      print("nobody in area")
   end
end
```