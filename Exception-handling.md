In Lua RTOS, Lua modules can trigger exceptions (anomalous or exceptional conditions requiring special processing). In general, an exception breaks the normal flow of execution and executes a pre-registered exception handler, which stops the program. For example, if you try to start the wifi network interface without setting it up, this will be occur:

```lua
/ > net.wf.start()
stdin:1: 117440517:wifi is not setup
stack traceback:
	[C]: in field 'start'
	stdin:1: in main chunk
	[C]: in ?
/ > 
```

Lua RTOS has support for the try / catch / finally exception handler model. This model allows to execute a Lua code that can potentially trigger an exception (try part), handle the exceptions without stop the program (catch part), and continue with the normal execution of the program regardless of whether an exception has occurred (finally part).

## try(try_function, [catch_function, finally_function]

This function allow to execute a function that potentially throws exceptions (i.e. an attempt to join to a LoraWAN network), and intercept execution errors without stopping the program.

Programs written using the try function are more readable, so is not necessary to use an "if then else" schema for check errors.

Arguments:

* try_function: a Lua function containing the code that potentially throws exceptions
* catch_function: a Lua function that is called when an exception is throwed
* finally_function: a Lua function that allways is called when try_function or catch_function ends

Returns: nothing

```lua
try(
  function() 
    -- This function executes the code that potentially throws exceptions
  end,
  function(where, line, error, message)
    -- This function is executed when an exception is thrown
  end,
  function()
    -- This function is called always
  end
)
```

```lua
try(
  function() 
    net.wf.start()
  end,
  function(where, line, error, message)
    if (error == 117440517) then
      print(message)
    end
  end,
  function()
    net.wf.stop()
  end
)
```