# Specification

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | HALL_SWITCH |                            |
| Interface    | GPIO        |                            |
| Provides     | on          | 1 = switch active          |
|              |             | 0 = switch inactive        |
| Properties   | none        |                            |
|              |             | ![](http://git.whitecatboard.org/push_button.png)                           |


# Code

In this example a push switch is attached to GPIO26. Sensor changes are processed using a callback:
```lua
s = sensor.attach("PUSH_SWITCH", pio.GPIO26)

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

In this example a push switch is attached to GPIO26. Sensor changes are processed using an infinite loop:
```lua
s = sensor.attach("PUSH_SWITCH", pio.GPIO26)

while true do
   if (s:read("on") == 1) then
      print("on")
   else
      print("off")
   end
end
```