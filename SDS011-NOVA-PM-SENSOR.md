The SDS011 using principle of laser scattering, can get the particle concentration between 0.3 to 10μm in the air. It with digital output and built-in fan is stable and reliable.

**Characteristics:**

1. Accurate and reliable: laser detection, stable, good consistency.
2. Quick response: response time is less than 10 seconds when the scene changes.
3. High resolution: resolution of 0.3μg/m3.

**Scope of application:**

Detector of PM2.5. Purifier.

**Working principle:**

Using laser scattering principle. Light scattering can be induced when particles go through the detecting area. The scattered light is transformed into electrical signals and these signals will be amplified and processed. The number and diameter of particles can be obtained by analysis because the signal waveform has certain relations with the particles diameter.

**Power requirement:**

Power Voltage：4.7~5.3V
Power supply：>1W
Supply voltage ripple：<20mV

# Specification

| What         |             | Comments                                 |
|--------------|-------------|------------------------------------------|
| Identifier   | SDS011      | ![](http://git.whitecatboard.org/sds011.png)                                         |
| Interface    | UART        |                                          |
| Provides     | PM2.5       | particles per million <= 2.5 micrometers |
|              |             | in micro-grams / m3                      |   
|              | PM10        | particles per million <= 10 micrometers  |
|              |             | in micro-grams / m3                      |   
| Properties   | none        |                                          |
| [Datasheet](http://breathe.indiaspend.org/wp-content/uploads/2015/11/nova_laser_sensor.pdf)    |             |                            |


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

[Back to sensor list](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Sensor-module#supported-sensors)