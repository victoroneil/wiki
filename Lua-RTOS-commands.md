In Lua you can access some underlying Operation System functions through the os module. For example, if you want to know the system date you do:

```lua
/ > os.date()
Wed Dec 14 02:23:39 2016
```

Lua RTOS extends the standard Lua os module for allow the programmer to access to all Lua RTOS characteristics.  

Please, refer to (http://www.lua.org/manual/5.3/manual.html#6.9) to know more about the standard features for this module.

# Control commands

## os.sleep(seconds)

Put the board in sleep mode for a time specified in the seconds argument. Once the sleep time ends the CPU is reset.

Arguments:

* seconds: the number of seconds to sleep

Returns: nothing

```lua
-- Sleep for 10 seconds
os.sleep(10)
```

# Configuration commands

## os.shell(enable)

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

Lua RTOS shell is experimental and it's implementation is not finished!!.

Arguments:

* enable: true for enable / false for disable

Returns: nothing

## os.loglevel(level)

Sets the log level. The log level controls the amount of log information that Lua RTOS show in the console, and puts in the /log/messages.log file (is an SD Card is attached).

Arguments:

* level: the log level, can be either os.LOG_ALL, os.LOG_INFO, os.LOG_EMERG, os.LOG_ALERT, os.LOG_CRIT, os.LOG_ERR, os.LOG_WARNING, os.LOG_NOTICE, os.LOG_DEBUG

Returns: nothing

```lua
-- Show only error logs
os.loglevel(os.LOG_ERR)
```

## os.logcons(enable)

Enable or disable Lua RTOS log to the console. If it's enabled log messages are displayed in the console and written to the /log/messages.log file if an SD Card is attached. If it's disabled log mesages are written to the /log/messages.log file if an SD Card is attached.

Arguments:

* enable: true for enable / false for disable

Returns: nothing

```lua
-- Disable logs on the console
os.logcons(false)
```

## os.history(enable)

If enabled Lua RTOS records the commands entered by the programmer. The programmer can access the previous entered commands with the up & down keys. This functions is only available if an SD Card is attached to your board.

Arguments:

* enable: true for enable / false for disable

Returns: nothing

```lua
-- Enable history
os.histrory(true)
```

# Other functions

## os.clear()

Clears the console.

Arguments: nothing
Returns: nothing
