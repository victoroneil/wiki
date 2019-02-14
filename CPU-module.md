# About this

This module contains functions for accessing the CPU.

## cpu.model()

Get the CPU name and revision number installed in your board.

Arguments: nothing

Returns: a string, with the CPU name installed on your board.

```lua
-- Get the CPU model
cpu = cpu.model();

-- Print to screen
print("CPU: "..cpu)
```

## cpu.board()

Get the information of the board that Lua RTOS is running on.

Arguments: nothing

Returns: the board type, the board subtype, and the board brand. Board subtype and board brand can be empty.

```lua
-- Get board information
type, subtype, brand = cpu.board();

-- Print to screen
print("Type: "..type)
print("Subtype: "..subtype)
print("Brand: "..brand)
```

## cpu.speed([speed [, dynamic]])

Gets and optionally sets the current CPU speed in MHz.

Arguments:

* speed: one of cpu.SPEED_DEFAULT, cpu.SPEED_FAST, cpu.SPEED_MEDIUM, cpu.SPEED_SLOW OR any actual MHz value supported by the system
* dynamic: default: false. which sets the new cpu speed as a fixed value. set dynamic to true to use the new cpu speed as a maximum speed, allowing the system to dynamically switch the actual speed on demand.

Returns: CPU speed in MHz.

```lua
-- Get CPU speed
speed = cpu.speed();

-- Print to screen
print("Speed: "..speed.." MHz")
```

## cpu.temperature()

Get the current CPU temperature in celsius degrees.

Arguments: nothing

Returns: CPU temperature in celsius degrees.

```lua
-- Get CPU temperature
temp = cpu.temperature();

-- Print to screen
print("Temp: "..temp.." ºC")
```

## cpu.resetreason()

Get the reset reason.

Arguments: nothing

Returns: reset reason. one of

cpu.RESET_POWERON
cpu.RESET_SW
cpu.RESET_DEEPSLEEP
cpu.RESET_SDIO
cpu.RESET_TG0WDT_SYS
cpu.RESET_TG1WDT_SYS
cpu.RESET_RTCWDT_SYS
cpu.RESET_INTRUSION
cpu.RESET_TGWDT_CPU
cpu.RESET_SW_CPU
cpu.RESET_RTCWDT_CPU
cpu.RESET_EXT_CPU
cpu.RESET_RTCWDT_BROWN_OUT
cpu.RESET_RTCWDT_RTC

## cpu.wakeupreason()

Get the wakeup reason.

Arguments: nothing
Returns: wakeup reason. one of

cpu.WAKEUP_NONE
cpu.WAKEUP_EXT0
cpu.WAKEUP_EXT1
cpu.WAKEUP_TIMER
cpu.WAKEUP_TOUCHPAD
cpu.WAKEUP_ULP

## cpu.wakeupon()

Set allowed wakeup reasons. May be called several times to allow several wakeup sources.

Arguments: one of

cpu.WAKEUP_NONE
cpu.WAKEUP_EXT0
cpu.WAKEUP_EXT1
cpu.WAKEUP_TIMER
cpu.WAKEUP_TOUCHPAD
cpu.WAKEUP_ULP

Returns: nothing

Additional arguments depend on the chosen wakeup type:

cpu.WAKEUP_EXT0
* gpio
* level

cpu.WAKEUP_EXT1
* mask
* wakeup_mode

cpu.WAKEUP_TIMER
* time_in_us

cpu.WAKEUP_TOUCHPAD
-

WAKEUP_ULP
-

```lua
-- allow wakeup by ULP
cpu.wakeupon(cpu.WAKEUP_ULP)
-- allow wakeup by EXT0
cpu.wakeupon(cpu.WAKEUP_EXT0, pio.GPIO26, 1)
```

## cpu.sleep(seconds)

Put the cpu in deep sleep mode for a time specified in the seconds argument. Once the sleep time ends the CPU is reset.

Arguments:

seconds: the number of seconds to sleep
Returns: this function does not return.

```lua
-- Sleep for 10 seconds
cpu.sleep(10)
```

## cpu.deepsleep()

Put the cpu into deep sleep mode. The CPU is reset as soon as one of the events configured via cpu.wakeupon occurs.

Arguments:

Returns: this function does not return.

```lua
-- Sleep now
cpu.deepsleep()
```

## cpu.wakeupext1pin()

If the cpu.wakeupreason is cpu.WAKEUP_EXT1 then this function can be used to query the GPIO that the event occured on.

```lua
-- Read the GPIO that woke the CPU
pin = cpu.wakeupext1pin()

-- Print to screen
print("Pin that woke the CPU: "..pin)
```

## cpu.wakeupext1mask()

If the cpu.wakeupreason is cpu.WAKEUP_EXT1 then this function can be used to query the mask of all EXT1 GPIOs to find out which GPIO the event occured on.

```lua
-- Read the GPIO mask
mask = cpu.wakeupext1mask()

-- Print to screen
print("EXT1 wake GPIO mask: "..mask)
```

## cpu.watchpoint(addr [, size [, flags]])

Enables to set a watchpoint to a specific address, on LOAD, STORE or ACCESS.

Arguments:

* addr: the address to watch
* size: the size of the address, default 4, must be one of 2^n, with n in [0..6]
* flags: one of cpu.WATCHPOINT_LOAD, cpu.ESP_WATCHPOINT_STORE, cpu.ESP_WATCHPOINT_ACCESS

Returns: nothing

## cpu.backtrace()

If the system has been restarted after a crash/panic/abort the callstack of the crash will be preserved in a special area of the memory. Use this function to get that callstack.

Arguments: none

Returns: nothing or a lua table containing the backtrace

```lua
/examples/lua > cpu.backtrace()
Backtrace: none
```

