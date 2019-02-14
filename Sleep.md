The Lua RTOS sleep functions allows to put the CPU in sleep mode. These functions are provided as an extension of the Lua os module.

## os.bootcount()

Get the number of boots from the deep sleep state.

Arguments: nothing.

Returns: the number of boots.

## os.sleep(seconds) Deprecated. Use cpu.sleep()

Put the board in deep sleep mode for a time specified in the seconds argument. Once the sleep time ends the CPU is reset.

Arguments:

seconds: the number of seconds to sleep
Returns: nothing

```lua
-- Sleep for 10 seconds
os.sleep(10) --deprecated, use cpu.sleep(10)
```
