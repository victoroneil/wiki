Lua RTOS has an integrated shell that allows you to execute certain commands in a linux similar way. The shell is disabled by default, but you can enable it typing os.shell(true) in the [prompt](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/The-Lua-prompt) or putting os.shell(true) in the [system.lua](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Startup-scripts) file.

The following explains all the commands supported by the shell.

# Utility commands

## luac _SOURCE_ _[DESTINATION]_

Translates programs written in the Lua programming language into binary files that can be later loaded and executed.

_DESTINATION_ is optional, and if it's not provided the compiled filename is the _SOURCE_ filename postfixed with the "c" character.

Example:

```lua
-- Compile test.lua into test.luac file
luac test.lua test.luac

-- Compile test.lua into test.luac file
luac test.lua
```

# File system commands

## cat _FILE_

Print _FILE_ on the standard output.

```lua
/ > cat system.lua
-- system.lua
--
-- This script is executed after a system boot or a system reset and is intended
-- for setup the system.

---------------------------------------------------
-- Main setups
---------------------------------------------------
os.loglevel(os.LOG_INFO)   -- Log level to info
os.logcons(true)           -- Enable/disable sys log messages to console
os.shell(true)             -- Enable/disable shell
os.history(false)          -- Enable/disable history
/ > 
```

## cd _DIRECTORY_

Change the working directory.

```lua
/ > cd examples
/examples > 
````

## cp _SOURCE_ _DESTINATION_

Copy the _SOURCE_ file to the _DESTINATION_ file.

```lua
/ > cp autorun.lua autorun.old
/ > 
```

## ls _PATTERN_

## mkdir _DIRECTORY_

## more _FILE_
	
## mv _SOURCE_ _DESTINATION_

Move (rename) _SOURCE_ to _DESTINATION_.

## pwd

Print name of current/working directory.

```lua
/examples > pwd
/examples	
/examples > 
```

## rm _FILE_

Remove _FILE_.

# Network commands

# System commands

## clear

Clear the terminal screen.

## dmesg

Print the syslog contents on the standard output.

**Note:** dmesg is only available if the underlying storage for your root filesystem is not the SPI FLASH.

## reboot

Reboot the system.
