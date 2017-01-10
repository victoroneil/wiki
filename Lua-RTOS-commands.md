In Lua you can access some underlying Operation System functions through the os module. For example, if you want to know the system date you do:

```lua
/ > os.date()
Wed Dec 14 02:23:39 2016
```

Lua RTOS extends the standard Lua os module for allow the programmer to access to all Lua RTOS characteristics.  

Please, refer to (http://www.lua.org/manual/5.3/manual.html#6.9) to know more about the standard features for this module.

# Information commands

## os.cpu()

Get the CPU name installed in your board.

Arguments: nothing

Returns: a string, with the CPU name installed on your board.

```lua
-- Get the CPU model
cpu = os.cpu();

-- Print to screen
print("CPU: "..cpu)
```

```lua
CPU: ESP32
```

## os.version()

Get Lua RTOS version installed in your board.

Arguments: nothing

Returns: the operating system name (Lua RTOS), the version number, and the operation system build time.

```lua
-- Get operating system name and version
oss, version, build = os.version();

-- Print to screen
print("OS: "..oss..", version: "..version..", build: "..build)
```

```lua
OS: Lua RTOS, version: beta 0.1, build: 1481679957
```

# Control commands

## os.sleep(seconds)

Put the board in sleep mode for a time specified in the seconds argument. Once the sleep time ends the CPU is reset.

Arguments:

* seconds: the number of seconds to sleep

Returns: nothing

````lua
-- Sleep for 10 seconds
os.sleep(10)
```

# File system commands

## os.ls([path])

List the path contents.

Arguments:

* path: directory path. This argument it's optional, and if is not provided the contents of the current directory are listed. Path can be absolute or relative to current working directory.

Returns: nothing

```lua
/> os.ls("/")
d              -        tmp
d              -        www
d              -        conf
d              -        log
d              -        lib
f             27        test1.lua
f            956        autorun.lua
f           1871        lcd.lua
```

Directory contents is listed on the screen in columns (separated by tab):

* first column: entry type (d = directory / f = file)
* second column: entry size in bytes
* third column: entry name

## os.cd(path)

Change the current working directory.

Arguments:

* path: directory path. Path can be absolute or relative to current working directory.

Returns: nothing.

```lua
/> os.cd("/examples")
/examples >
```

## os.pwd()

Get the current working directory.

Arguments: nothing

Returns: the current directory

```lua
/examples > os.pwd()
/examples
```

## os.mkdir(path)

Make a directory. A file or directory can be removed with Lua [os.remove()] (http://www.lua.org/manual/5.3/manual.html#6.9) standard function.

Arguments:

* directory path. Path can be absolute or relative to current working directory.

Returns: true if success

```lua
-- Make a new directory named test into the current working directory

os.mkdir("test")
true
```

## os.cp(source path,destination path)

Copy a file.

Arguments:

* source path: file source path
* destination path: file destination path

Returns: nothing

```lua
-- Copy autorun.lua into autorun.old
os.cp("/autorun.lua","/autorun.old")
```

## os.edit(file)

Edits a file.

Arguments:

* file: file path. Can be absolute or relative to current working directory.

Returns: nothing

```lua
/> os.edit("autorun.lua")
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