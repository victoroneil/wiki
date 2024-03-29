The Lua RTOS configuration functions allows to configure some aspects of Lua RTOS. These functions are provided as an extension of the Lua os module.

## os.factoryreset()

Performs a factory reset of your installed firmware. The factory reset performs the following actions:

  * Erase the ota data partition for OTA enabled firmwares, so in the next reboot the factory app is executed.

Arguments: nothing.

Returns: nothing.

```lua
os.factoryreset()
```

## os.history([enable])

If enabled Lua RTOS records the commands entered by the programmer. The programmer can access the previous entered commands with the up & down keys. This function is only available if an SD Card is attached to your board or if the system was built with support for a RAM FS. In that latter case, make sure the RAM FS has properly been mounted using fs.mount("/rfs","ramfs")

Arguments:

* enable (optional): true for enable / false for disable. If this argument is not provided the function returns the current history setting.

Returns: nothing, or the current history setting (true/false) if the enable argument is not provided.

```lua
-- Enable history
os.histrory(true)
```

## os.logcons([enable])

Enable or disable Lua RTOS log to the console. If it's enabled log messages are displayed in the console and written to the /log/messages.log file if an SD Card is attached. If it's disabled log mesages are written to the /log/messages.log file if an SD Card is attached.

Arguments:

* enable (optional): true for enable / false for disable. If this argument is not provided the function returns the current logcons setting.

Returns: nothing, or the current logcons setting (true/false) if the enable argument is not provided.

```lua
-- Disable logs on the console
os.logcons(false)
```

## os.loglevel([level])

Sets the log level. The log level controls the amount of log information that Lua RTOS show in the console, and puts in the /log/messages.log file (is an SD Card is attached).

Arguments:

* level (optional): the log level, can be either os.LOG_ALL, os.LOG_INFO, os.LOG_EMERG, os.LOG_ALERT, os.LOG_CRIT, os.LOG_ERR, os.LOG_WARNING, os.LOG_NOTICE, os.LOG_DEBUG. If this argument is not provided the function returns the current loglevel setting.

Returns: nothing, or the current loglevel setting if the enable argument is not provided.

```lua
-- Show only error logs
os.loglevel(os.LOG_ERR)
```

## os.syslog(message[, level])

Logs a message to the syslog.

Arguments:

* message: the message to log to the syslog
* level (optional): the log level, can be either os.LOG_ALL, os.LOG_INFO, os.LOG_EMERG, os.LOG_ALERT, os.LOG_CRIT, os.LOG_ERR, os.LOG_WARNING, os.LOG_NOTICE, os.LOG_DEBUG. If this argument is not provided the function returns the current loglevel setting.

Returns: nothing

```lua
-- Log an informative message
os.syslog("foo", os.LOG_INFO)
```

## os.rsyslog([server])

Enables or disables logging to a remote rsyslog server.

Arguments:

* server (optional): the name or ip address of the remote syslog server. Empty string or 0.0.0.0 to disable.

Returns: the currently set rsyslog server

```lua
-- Retrieve the currently set rsyslog server
/ > os.rsyslog()
0.0.0.0
-- Set a new rsyslog server
/ > os.rsyslog("10.0.0.1")
10.0.0.1
-- Retrieve the currently set rsyslog server
/ > os.rsyslog()
10.0.0.1
-- Disable logging to a remote syslog server
/ > os.rsyslog("0.0.0.0")
0.0.0.0
```

## os.shell([enable])

Enable or disable Lua RTOS shell. If shell is enabled the programmer can interact with Lua RTOS in a friendly way:

```lua
/ > ls
f	     370		abp.lua
d	       -		examples
d	       -		sys
f	     468		system.lua
f	     388		wifi.lua
f	      40		autorun.lua
/ > cd examples
/examples > ls
d	       -		blocks
d	       -		lua
d	       -		a
f	       0		system.lua
/examples >
```

Arguments:

* enable (optional): true for enable / false for disable. If this argument is not provided the function returns the current shell setting.

Returns: nothing, or the current shell setting (true/false) if the enable argument is not provided.
