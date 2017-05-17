# thread module

This module contains functions for running Lua functions into native threads. 
Unlike Lua coroutines, native threads are scheluded by the operating system, 
allowing to run operations in real time.


## thread.start(function, [stack, priority, cpu])

Start a new thread.

Arguments:

* function: function to execute in the thread.
* stack (optional): the number of bytes to allocate for use as the thread's stack. Must be >= 2048.
* priority (optional): the priority at which the thread will execute. Must be >= 3 and <= 25, where 3 is the minimal priority.
* cpu (optional): the CPU at which the thread will execute.

Returns: the thread identifier, or an exception. You must store this identifier into a variable for further operations with it.


```lua
-- Function to execute
f1 = function()
    local led_pin = pio.GPIO4
    pio.pin.setdir(pio.OUTPUT, led_pin)

    while true do
	pio.pin.sethigh(led_pin)
	tmr.delayms(250)
	pio.pin.setlow(led_pin)
	tmr.delayms(250)
    end
end

-- Start thread
th1 = thread.start(f1)
```


## thread.suspend([thread id])

Suspend all threads or a specific thread. This function suspends the execution
of the underline operating system thread remaining in memory until it's resumed 
or stopped.

Arguments:

* thread id: this argument it's optional. If not present function suspend all
threads, and if present suspend the specified thread.

Returns: nothing.


```lua
-- Function to execute
f1 = function()
    local led_pin = pio.GPIO4
    pio.pin.setdir(pio.OUTPUT, led_pin)

    while true do
	pio.pin.sethigh(led_pin)
	tmr.delayms(250)
	pio.pin.setlow(led_pin)
	tmr.delayms(250)
    end
end

-- Start thread
th1 = thread.start(f1)

....

-- Suspend thread
thread.suspend(th1)
```


## thread.resume([thread id])

Resume all threads or a specific thread. This function resume the execution
of the underline operating system thread.

Arguments:

* thread id: this argument it's optional. If not present function resume all
threads, and if present resume the specified thread.

Returns: nothing.


```lua
-- Function to execute
f1 = function()
    local led_pin = pio.GPIO4
    pio.pin.setdir(pio.OUTPUT, led_pin)

    while true do
	pio.pin.sethigh(led_pin)
	tmr.delayms(250)
	pio.pin.setlow(led_pin)
	tmr.delayms(250)
    end
end

-- Start thread
th1 = thread.start(f1)

....

-- Suspend thread
thread.suspend(th1)

....

-- Resume thread
thread.resume(th1)
```


## thread.stop([thread id])

Stop all threads or a specific thread.

Arguments:

* thread id: this argument it's optional. If not present function stop all
threads, and if present stop the specified thread. This function stop the 
execution of the underline operating system thread and removes it from memory.

Returns: nothing.


```lua
-- Function to execute
f1 = function()
    local led_pin = pio.GPIO4
    pio.pin.setdir(pio.OUTPUT, led_pin)

    while true do
	pio.pin.sethigh(led_pin)
	tmr.delayms(250)
	pio.pin.setlow(led_pin)
	tmr.delayms(250)
    end
end

-- Start thread
th1 = thread.start(f1)

....

-- Stop thread
thread.stop(th1)
```


## thread.status(thread id)

Get the status of a specific thread.

Arguments:

* thread id: thread identifier.

Returns: thread status (running, suspended or nil).


```lua
-- Function to execute
f1 = function()
    local led_pin = pio.GPIO4
    pio.pin.setdir(pio.OUTPUT, led_pin)

    while true do
	pio.pin.sethigh(led_pin)
	tmr.delayms(250)
	pio.pin.setlow(led_pin)
	tmr.delayms(250)
    end
end

-- Start thread
th1 = thread.start(f1)

....

-- Suspend thread
thread.suspend(th1)

-- Get thread status
thread.status(th1)

> suspended
```


## thread.sleep(seconds)

Sleep current thread a number of seconds.

Arguments:

* seconds: seconds to sleep.

Returns: nothing.


```lua
-- Sleep for 4 seconds
thread.sleep(4)
```

## thread.sleepms(milliseconds)

Sleep current thread a number of milliseconds.

Arguments:

* milliseconds: milliseconds to sleep.

Returns: nothing.


```lua
-- Sleep for 4 milliseconds
thread.sleepms(4)
```

## thread.sleepus(useconds)

Sleep current thread a number of micro seconds.

Arguments:

* useconds: micro seconds to sleep.

Returns: nothing.


```lua
-- Sleep for 500000 micro seconds (0,5 seconds)
thread.sleepus(500000)
```