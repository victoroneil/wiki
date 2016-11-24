When an ESP32 board, with Lua RTOS firmware installed is powered-on, the board enters in boot mode, executing the following steps:

1. First esp-idf bootloader is executed. In this stage firmware can be uploaded as usual (esptool).

2. If there is no a firmware upgrade, esp-idf start_cpu is executed as usual.

3. Lua RTOS system init is executed:

  3.1. Init of Lua RTOS structures

  3.2. Initial drivers are setup

  3.3. File systems are mounted

  3.4. Lua interpreter is started, executing the system.lua file and he autorun.lua file if they are present in main file system (SPIFFS if enabled, or FAT if enabled and SPIFFS disabled).

4. Lua is able for process user commands

In steps 3.1, 3.2, and 3.3 Lua RTOS user can abort initial scripts execution (system.lua / autotun.lua)sending the 0x04 character to the console. This can be used for boot the board in case of problems with a script during the development process.