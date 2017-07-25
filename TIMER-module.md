# About this

This module contains functions for accessing the hardware timers, and include delays in your programs. The functions of this module are organized in the following categories:

* [Delay functions](#delay-functions)
* [Hardware timers](#hardware-timers)
* [Software timers](#software-timers)

# Delay functions

The delay functions introduces a delay in the program for a specified  period of time. The delay is executed in the current thread, and no context switch is done, at least until the next context switch scheduled by Lua RTOS.

## tmr.delay(seconds)

Waits for the specified seconds, then returns.

Arguments:

* seconds: number of seconds to wait.

Returns: nothing, or an exception.

## tmr.delayms(milliseconds)

Waits for the specified milliseconds, then returns.

Arguments:

* milliseconds: number of milliseconds to wait.

Returns: nothing, or an exception.

## tmr.delayus(microseconds)

Waits for the specified microseconds, then returns.

Arguments:

* microseconds: number of microseconds to wait.

Returns: nothing, or an exception.

# Sleep functions

The sleep functions suspend the program's execution for a specified period of time by suspending the current thread.

## tmr.sleep(seconds)

Sleeps for the specified seconds, then returns.

Arguments:

* seconds: number of seconds to sleep.

Returns: nothing, or an exception.

## tmr.sleepms(milliseconds)

Sleeps for the specified milliseconds, then returns.

Arguments:

* milliseconds: number of milliseconds to sleep.

Returns: nothing, or an exception.

## tmr.sleepus(microseconds)

Sleeps for the specified microseconds, then returns.

Arguments:

* microseconds: number of microseconds to sleep.

Returns: nothing, or an exception.

# Hardware timers

## instance = tmr.attach(id, period, callback)

Attach a hardware timer, calling a callback at regular intervals defined by the period argument. The timer is reloaded automatically after calling the callback.

Arguments:

* id: the timer id. Can be either tmr.TMR0, tmr.TMR1, tmr.TMR2, or tmr.TMR3.
* period: the timer's period in microseconds.
* callback: the call back function to call when the timer expires.

Returns: the timer instance, or an exception. You must store the timer instance into a variable for further operations with it.

## instance:detach()

Detach a hardware timer, and free all resources used by timer.

Arguments: nothing.
Returns: nothing, or an exception.

## instance:start()

Start the timer.

Arguments: noting.
Returns: nothing, or an exception.

## instance:stop()

Stop the timer.

Arguments: noting.
Returns: nothing, or an exception.

## Full example

This example use a hardware timer for blink a led every 50 milliseconds
```lua
-- Blink function
function blink()
   if (led_on) then
      pio.pin.sethigh(pio.GPIO26)
      led_on = false
   else
      pio.pin.setlow(pio.GPIO26)
      led_on = true
   end
end

-- Configure the GPIO where the led is attached
pio.pin.setdir(pio.OUTPUT, pio.GPIO26)

-- Variable for store the led status
led_on = false

-- Attach the timer. 50 milliseconds = 50000 micro seconds
t0 = tmr.attach(tmr.TMR0, 50000, blink)

-- Start the timer (the led blinks)
t0:start()

...

-- Stop the timer
t0:stop()
```

# Software timers

## instance = tmr.attach(period, callback)

Attach a software timer, calling a callback at regular intervals defined by the period argument. The timer is reloaded automatically after calling the callback.

Arguments:

* period: the timer's period in milliseconds.
* callback: the call back function to call when the timer expires.

Returns: the timer instance, or an exception. You must store the timer instance into a variable for further operations with it.

## instance:detach()

Detach a software timer, and free all resources used by timer.

Arguments: nothing.
Returns: nothing, or an exception.

## instance:start()

Start the timer.

Arguments: noting.
Returns: nothing, or an exception.

## instance:stop()

Stop the timer.

Arguments: noting.
Returns: nothing, or an exception.

## Full example

This example use a software timer for blink a led every 50 milliseconds
```lua
-- Blink function
function blink()
   if (led_on) then
      pio.pin.sethigh(pio.GPIO26)
      led_on = false
   else
      pio.pin.setlow(pio.GPIO26)
      led_on = true
   end
end

-- Configure the GPIO where the led is attached
pio.pin.setdir(pio.OUTPUT, pio.GPIO26)

-- Variable for store the led status
led_on = false

-- Attach the timer
t0 = tmr.attach(50, blink)

-- Start the timer (the led blinks)
t0:start()

...

-- Stop the timer
t0:stop()
```