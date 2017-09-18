# About this

GP2Y0A21YK0F is a distance measuring sensor unit, composed of an integrated combination of PSD (position sensitive detector), IRED (infrared emitting diode) and signal processing circuit.

The variety of the reflectivity of the object, the environmental temperature and the operating duration are not influenced easily to the distance detection because of adopting the triangulation method.

This device outputs the voltage corresponding to the detection distance. So this sensor can also be used as a proximity sensor.

Distance measuring range : 10 to 80 cm

**Power supply:**

* Consumption current : Typ. 30 mA
* Supply voltage : 4.5 to 5.5 V

# Specification

Infrared sensor.

| What         |             | Comments                   |
|--------------|-------------|----------------------------|
| Identifier   | 2Y0A21      | ![](http://git.whitecatboard.org/GP2Y0A21YK.jpg)            |
| Interface    | ADC         |                            |
| Provides     | distance    | centimeters                |
| Properties   | none        |                            |
| [Datasheet](http://www.socle-tech.com/doc/IC%20Channel%20Product/Sensors/Distance%20Measuring%20Sensor/Analog%20Output/gp2y0a21yk_e.pdf)    |             |                            |


# Code

```lua
-- Attach sensor using an external ADC (ADS1115) / channel 0
s = sensor.attach("2Y0A21", adc.ADS1115, 0)

while true do
  print("distance: "..s:read("distance").." cm")
  tmr.delayms(500)
end
```

[Back to sensor list](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Sensor-module#supported-sensors)