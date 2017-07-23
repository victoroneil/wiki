# About this

This module contains functions for accessing the hardware timers, and include delays in your programs.

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

Attach a hardware timer with a certain period, and calling a callback when the period expires. The timer is reloaded automatically after calling the callback.

Arguments:

* id: the timer id. Can be either tmr.TMR0, tmr.TMR1, tmr.TMR2, or tmr.TMR3.
* period: the timer's period in microseconds.
* callback: the call back function to call when the timer expires.

Returns: the timer instance, or an exception.