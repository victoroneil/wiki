# About this

This module contains functions for accessing the hardware timers, and include delays in your programs.

# Delay functions

The delay functions introduces a delay in the program for a specified  period of time. The delay is executed in the current thread, and no context switch is done, at least until the next context switch. 

# Sleep functions

The sleep functions suspend the program's execution for a specified period of time by suspending the current thread.