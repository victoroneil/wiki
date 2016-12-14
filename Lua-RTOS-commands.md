# Information commands

## os.cpu()

## os.cpu()

Get the CPU name installed in your board.

Arguments: nothing

Returns: a string, with the CPU name installed on your board.

```lua
-- Get the CPU model
cpu = os.cpu();

-- Print to screen
print("CPU: "..cpu)
```

```lua
/ >
CPU: ESP32
```

## os.version()

Get Lua RTOS version installed in your board.

Arguments: nothing

Returns: the operating system name (Lua RTOS), the version number, the operation system build time.

```lua
-- Get operating system name and version
oss, version, build = os.version();

-- Print to screen
print("OS: "..oss..", version: "..version..", build: "..build)
```

```lua
/ > 
OS: Lua RTOS, version: beta 0.1, build: 1481679957
```

