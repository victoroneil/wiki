# About this

A thread of execution is the smallest sequence of programmed instructions that can be managed independently by a scheduler, which is a part of the operating system. Multiple threads can exist, executing concurrently and sharing resources such as memory.

Lua RTOS can execute Lua functions into FreeRTOS native threads. Unlike Lua coroutines, threads are scheluded by the operating system, allowing to run Lua programs in real time.

The functions of this module are organized in the following categories:

* [Thread management functions](#thread-management-functions)
* [Thread control functions](#thread-control-functions)
* [Mutual exclusion functions](#mutual-exclusion-functions)

# Thread management functions

## thread.list([table, monitor, all])

List all threads.

Arguments:

  * table (optional): if true, thread list is returned in a Lua table, if false thread list is printed on the console.
  * monitor(optional): if true, the thread list is refreshed every 0.5 seconds. Only allowed if table = false.
  * all (optional): if true show all threads. If false (default) shows only the lua threads. There are 3 types of threads:

    * task: is a FreeRTOS task managed directly by FreeRTOS. This types of tasks corresponds to system tasks.
    * thread: is a FreeRTOS task managed by the pthread API.
    * lua: is a FreeRTOS task managed by the Lua thread module.

Returns:

  * if table is false: nothing or an exception.

  * if table is true: a Lua table with the thread list result, or an exception. This table is an array of tables. Each entry corresponds to a thread. Each thread gives the following fields:

    * thid: thread id.
    * type: thread type, can be either task, thread or lua.
    * name: thread name.
    * status: for lua threads can be either run (running) or susp (suspended), and for other thread types is blank.
    * core: CPU in which thread is pinned.
    * stack_size: assigned stack size (in bytes) to the thread.
    * free_stack: number of free bytes in the stack.
    * used_stack: number of bytes used in the stack.

```lua
/ > thread.list()
-----------------------------------------------------------------------------------------
     |        |                  |        |      |      |            STACK               
THID | TYPE   | NAME             | STATUS | CORE | PRIO |   SIZE     FREE     USED       
-----------------------------------------------------------------------------------------
   1   lua      lua                run         0     20    10240     7632     2608 ( 25%)   
   0   task     IDLE                           1      0     1024      600      424 ( 41%)   
   0   task     IDLE                           0      0     1024      596      428 ( 41%)   
   0   task     Tmr Svc                        0      1     2048     1648      400 ( 19%)   
   0   task     ipc0                           0     24     1024      576      448 ( 43%)   
   0   task     esp_timer                      0     22     4096     3652      444 ( 10%)   
   0   task     signal                         0     21      768      312      456 ( 59%)   
   0   task     ipc1                           1     24     1024      500      524 ( 51%)   
```

## thread.start(function, [stack, priority, cpu, name])

Start a new thread.

Arguments:

* function: function to execute in the thread.
* stack (optional): the number of bytes to allocate for use as the thread's stack. Must be >= 2048.
* priority (optional): the priority at which the thread will execute. Must be >= 3 and <= 25, where 3 is the minimal priority.
* cpu (optional): the CPU at which the thread will execute.
* name (optional): name to assign to the thread, for debug purposes.

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

# Thread control functions

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

# Mutual exclusion functions

Mutual exclusion (mutex) is a property of concurrency control, which is instituted for the purpose of preventing race conditions; it is the requirement that one thread of execution never enter to a critical section at the same time that another concurrent thread of execution enters in the critical section.

# instance = thread.createmutex([type])

Creates a mutex instance.

Arguments:

* type (optional): type of mutex, can be either thread.Lock or thread.RecursiveLock. The default mutex type is thread.RecursiveLock.

Returns: a mutex instance, or an exception. You must store this instance into a variable for further operations with it.

# instance:lock()

Locks the mutex instance. If the mutex is locked by other thread, the calling thread is blocked until the mutex is unlocked.

Arguments: nothing.

Returns: nothing.

# instance:unlock()

Unlocks the mutex instance.

Arguments: nothing.

Returns: nothing.

# instance:trylock()

Try to lock the mutex. If the mutex is locked by other thread this functions returns false, and the calling thread is not blocked. If the mutex is not locked by other thread this functions locks the mutex and returns true.

Arguments: nothing.

Returns: true if the mutex has been locked by the calling process, or false if the mutex is locked by other threads.