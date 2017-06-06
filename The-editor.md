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

|Key| Function |Key| Function |
|---|----------|---|----------|
| up | Move one line up | Ctrl+S | Save file |
| down | Move one line down | Ctrl+Q | Quit |
| left | Move one character left | Ctrl+O | Open file |
| right | Move one character right | Ctrl+W | Close file |
| right | Move one character right | Ctrl+A | Select all |
| page up | Move one page up | Ctrl+C | Copy selection to cliboard |
| page down | Move one page down | Ctrl+X | Cut selection to clipboard |
| Ctrl+left | Move to previous word | Ctrl+V | Paste from clipboard |
| Ctrl+right | Move to next word | Ctrl+Z | Undo |
| home | Move to start of line | Ctrl+R | Redo |
| end | Move to end of line | Ctrl+F | Find text |
| Ctrl+home | Move to start of file | Ctrl+G | Find next |
| Ctrl+ end | Move to end of file | Ctrl+L | Goto line |
| backspace | Delete previous character | Shift+left/right | Select text |
| tab | Indent selection | Shift+tab | Unindent selection |
| delete | Delete current character |
