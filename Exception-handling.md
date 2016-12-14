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
