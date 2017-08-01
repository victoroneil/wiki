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



# Other functions

## os.clear()

Clears the console.

Arguments: nothing
Returns: nothing
