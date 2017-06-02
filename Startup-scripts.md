When Lua RTOS launches the Lua interpreter, and before the Lua prompt appears, 2 scripts are automatically executed. These scripts must be in the root directory:

1. system.lua:

   This scripts is intended for setup the system, for example enable Lua RTOS configurations disabled by default, change default configurations values, setup a network connection, etc.

1. autorun.lua