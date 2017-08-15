# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | TILT_SWITCH |                            |
| Interface    | GPIO        |                            |
| Provides     | on          | 1 = switch active          |
|              |             | 0 = switch inactive        |
| Properties   | none        |                            |
| [Datasheet](http://funduino.de/DL/SW-520D.pdf)    |             | ![](http://git.whitecatboard.org/sw520d.png)                           |


# Code

In this example a tilt switch is attached to GPIO26. Sensor changes are processed using a callback:
```lua
s = sensor.attach("TILT_SWITCH", pio.GPIO26)

s:callback(
   function(magnitude)
      if (magnitude["on"] == 1) then
         print("on")
      else
         print("off")
      end
   end
)
```

In this example a tilt switch is attached to GPIO26. Sensor changes are processed using an infinite loop:
```lua
s = sensor.attach("TILT_SWITCH", pio.GPIO26)

while true do
   if (s:read("on") == 1) then
      print("on")
   else
      print("off")
   end
end
```

