# About this

This module contains functions for accessing the hardware timers, and include delays in your programs.

# Delay functions

The delay functions introduces a delay in the program for a specified  period of time. The delay is executed in the current thread, and no context switch is done, at least until the next context switch. 

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