Lua RTOS has an integrated shell that allows you to execute certain commands in a linux similar way. The shell is disabled by default, but you can enable it typing os.shell(true) in the [prompt](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/The-Lua-prompt) or putting os.shell(true) in the [system.lua](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Startup-scripts) file.

The following explains all the commands supported by the shell.

# Utility commands

## clear

Clear the terminal screen.

## luac _source_ _[destination]_

**luac** is the Lua compiler. It translates programs written in the Lua programming language (**_source_** argument) into binary files (**_[destination]_** argument) that can be later loaded and executed.

The main advantages of precompiling chunks are: faster loading, protecting source code from accidental user changes, and off-line syntax checking.

Precompiling does not imply faster execution because in Lua chunks are always compiled into bytecodes before being executed. luac simply allows those bytecodes to be saved in a file for later execution.

**_destination_** argument is optional, and if it's not provided the compiled filename is the _source_ filename postfixed with the "c" character.

Example:

```lua
-- Compile test.lua into test.luac file
luac test.lua test.luac

-- Compile test.lua into test.luac file
luac test.lua
```

# File system commands

## cat _file_

Print the _file_ on the standard output.

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

## cd _directory_

Change the working directory to _directory_.

```lua
/ > cd examples
/examples > 
````

## cp _source_ _destination_

Copy the _source_ file to the _destination_ file.

```lua
/ > cp autorun.lua autorun.old
```

## ls _pattern_

Lists directory contents of files and directories that matches the _pattern_.

```lua
/ > ls *.lua
f	       0		autorun.lua
f	    2446		system.lua
f	    2445		config.lua
f	     252		test.lua
f	     280		test2.lua
```

## mkdir _directory_

Creates a new directory named _directory_ in the current directory.

## more _file_
	
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

## dmesg

Print the syslog contents on the standard output.

**Note:** dmesg is only available if the underlying storage for your root filesystem is not the SPI FLASH.

## reboot

Reboot the system.
