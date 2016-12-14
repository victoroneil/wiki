# Information commands

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
OS: Lua RTOS, version: beta 0.1, build: 1481679957
```

# File system commands

## os.ls([path])

List the path contents.

Arguments:

* path: directory path. This argument it's optional, and if is not provided the contents of the current directory are listed. Path can be absolute or relative to current working directory.

Returns: nothing

```lua
/> os.ls("/")
d              -        tmp
d              -        www
d              -        conf
d              -        log
d              -        lib
f             27        test1.lua
f            956        autorun.lua
f           1871        lcd.lua
```

Directory contents is listed on the screen in columns (separated by tab):

* first column: entry type (d = directory / f = file)
* second column: entry size in bytes
* third column: entry name

## os.cd(path)

Change the current working directory.

Arguments:

* path: directory path. Path can be absolute or relative to current working directory.

Returns: nothing.

```lua
/> os.cd("/examples")
/examples >
```

## os.pwd()

Get the current working directory.

Arguments: nothing

Returns: the current directory

```lua
/examples > os.pwd()
/examples
```

## os.mkdir(path)

Make a directory.

Arguments:

* directory path. Path can be absolute or relative to current working directory.

Returns: true if success

```lua
-- Make a new directory named test into the current working directory

os.mkdir("test")
true
```

## os.edit(file)

Edits a file.

Arguments:

* file: file path. Can be absolute or relative to current working directory.

Returns: nothing

```lua
/> os.edit("autorun.lua")
```


