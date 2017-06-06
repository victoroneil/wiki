Lua RTOS has an integrated editor that allows you to edit files. You can edit a file typing _os.edit("file")_ in the Lua prompt, or typing _edit file_ in the shell.

```lua
-- system.lua
--
-- This script is executed after a system boot or a system reset and is intended-- for setup the system.

---------------------------------------------------
-- Main setups
---------------------------------------------------
os.loglevel(os.LOG_INFO)   -- Log level to info
os.logcons(true)           -- Enable/disable sys log messages to console
os.shell(true)             -- Enable/disable shell
os.history(false)          -- Enable/disable history











/system.lua                                     Ctrl+Y=Help   Ln 1     Col 1   
```

In the table below you will find all available functions of the editor:

|Key| Function |
|---|----------|
| Ctrl+S | Save file |
| Ctrl+Q | Quit |
| up | Move one line up |
| down | Move one line down |
| left | Move one character left |
| right | Move one character right |
| right | Move one character right |
| page up | Move one page up |
| page down | Move one page down |
| Ctrl+left | Move to previous word |
| Ctrl+right | Move to next word |
| home | Move to start of line |
| end | Move to end of line |
| Ctrl+home | Move to start of file |
| Ctrl+ end | Move to end of file |
| backspace | Delete previous character |
| delete | Delete current character |
| tab | Indent selection |
| Shift+tab | Unindent selection |