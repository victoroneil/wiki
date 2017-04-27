Lua RTOS is the main-core of the Whitecat ecosystem. It's a real-time operating system designed to run on embedded systems, with minimal requirements of FLASH and RAM memory.

Lua RTOS has a 3-layers design:

1. In the top layer there is a Lua 5.3.4 interpreter which offers to the programmer all resources provided by Lua 5.3.2 programming language, plus special modules for access the hardware (PIO, ADC, I2C, RTC, etc ...) and middleware services provided by Lua RTOS (LoRa WAN, MQTT, ...).

2. In the middle layer there is a Real-Time micro-kernel, powered by FreeRTOS. This is the responsible for that things happen in the expected time.

3. In the bottom layer there is a hardware abstraction layer, which talk directly with the platform hardware.

![](http://git.whitecatboard.org/luaos.png)

For porting Lua RTOS to other platforms is only necessary to write the code for the bottom layer, because the top and the middle layer are the same for all platforms.
