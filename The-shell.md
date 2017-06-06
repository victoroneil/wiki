Lua RTOS has an integrated shell that allows you to execute certain commands in a linux similar way. The shell is disabled by default, but you can enable it typing os.shell(true) in the prompt or putting os.shell(true) in the system.lua file.

The following explains all the commands supported by the shell.

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