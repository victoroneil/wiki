The Lua RTOS & board status functions provides information about the operation system and board status. This functions are provided as an extension of the Lua os module.

## os.cpu()

Get the CPU name and CPU revision number, installed in your board.

Arguments: nothing

Returns: a string, with the CPU name installed on your board.

```lua
-- Get the CPU model
cpu = os.cpu();

-- Print to screen
print("CPU: "..cpu)
```

```lua
CPU: ESP32 rev 0
```

## os.version()

Get Lua RTOS version installed in your board.

Arguments: nothing

Returns: the operating system name (Lua RTOS), the version number,the system build time (expressed in EPOCH time) and the commit's hash (from github) used in build.

```lua
-- Get operating system name and version
oss, version, build, commit = os.version();

-- Print to screen
print("OS: "..oss..", version: "..version..", build: "..build..", commit: "..commit)
```

```lua
OS: Lua RTOS, version: beta 0.1, build: 1495574689, commit: 4d92804451cbec7d3ad545c66a92ffab35c63871
```

## os.bootcount()

Get the number of boots from the deep sleep state.

Arguments: nothing
Returns: the number of boots.

## os.resetreason()

Get the reset reason.

Arguments: nothing
Returns: reset reason.