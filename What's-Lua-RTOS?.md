Lua RTOS is a real-time operating system designed to run on embedded systems, with minimal requirements of FLASH and RAM memory. Currently Lua RTOS is available for ESP32, ESP8266 and PIC32MZ platforms, and can be easilly ported to other 32-bit platforms.

Lua RTOS has a 3-layer design:

1. In the top layer there is a Lua 5.3.4 interpreter which offers to the programmer all the resources provided by the Lua programming language, plus special modules for access the hardware (PIO, ADC, I2C, RTC, etc …), and middleware services provided by Lua RTOS (Lua Threads, LoRa WAN, MQTT, …).
1. In the middle layer there is a Real-Time micro-kernel, powered by FreeRTOS. This is the responsible for that things happen in the expected time.
1. In the bottom layer there is a hardware abstraction layer, which talk directly with the platform hardware.

![](http://git.whitecatboard.org/luartos.png)

For porting Lua RTOS to other platforms is only necessary to write the code for the bottom layer, because the top and the middle layer are the same for all platforms.
