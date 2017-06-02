After executing the [startup scripts](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Startup-scripts), Lua RTOS runs the Lua interpreter in interactive mode, and the prompt is showed:

   ```lua
   / > 
   ```

The Lua prompt is formed by the current directory, followed by the "/" character. For example, if the current directory is the /examples folder the prompt is:

   ```lua
   /examples > 
   ```
When the prompt is available Lua interprets each line that you type, for example:

   ```lua
   / > 2 + 2
   4
   ```

   ```lua
   / > print("Hello")
   Hello
   ```