# Specification

| What         |             | Comments                                 |
|--------------|-------------|------------------------------------------|
| Identifier   | SDS011      |                                          |
| Interface    | UART        |                                          |
| Provides     | PM2.5       | particles per million <= 2.5 micrometers |
|              |             | in micro-grams / m3                      |   
|              | PM10        | particles per million <= 10 micrometers  |
|              |             | in micro-grams / m3                      |   
| Properties   | none        |                                          |
| [Datasheet](http://www.socle-tech.com/doc/IC%20Channel%20Product/Sensors/Distance%20Measuring%20Sensor/Analog%20Output/gp2y0a21yk_e.pdf)    |             | ![](http://git.whitecatboard.org/GP2Y0A21YK.jpg)                           |


# Code

```lua
s = sensor.attach("SDS011", uart.UART1)
while true do
   pm_2_5 = s:read("PM2.5")
   pm_10 = s:read("PM10")
   print("PM2.5: "..pm_2_5..", PM10: "..pm_10)
   tmr.delayms(500)
end
```