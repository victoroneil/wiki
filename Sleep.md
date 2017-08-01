The Lua RTOS sleep functions allows to put the CPU in sleep mode. This functions are provided as an extension of the Lua os module.

# os.sleep(seconds)

Put the board in sleep mode for a time specified in the seconds argument. Once the sleep time ends the CPU is reset.

Arguments:

seconds: the number of seconds to sleep
Returns: nothing

```lua
-- Sleep for 10 seconds
os.sleep(10)
```