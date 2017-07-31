The Lua RTOS file system functions provides access to the supported file systems. Some functions, such as create a directory, are provided as an extension of the Lua os and module.

File access functions are provided through the standard Lua [io module](http://www.lua.org/manual/5.1/manual.html#5.7).

The functions of this module are organized in the following categories:

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

Make a directory. A file or directory can be removed with Lua [os.remove()] (http://www.lua.org/manual/5.3/manual.html#6.9) standard function.

Arguments:

* directory path. Path can be absolute or relative to current working directory.

Returns: true if success

```lua
-- Make a new directory named test into the current working directory

os.mkdir("test")
true
```

## os.cp(source path,destination path)

Copy a file.

Arguments:

* source path: file source path
* destination path: file destination path

Returns: nothing

```lua
-- Copy autorun.lua into autorun.old
os.cp("/autorun.lua","/autorun.old")
```

## os.edit(file)

Edits a file.

Arguments:

* file: file path. Can be absolute or relative to current working directory.

Returns: nothing

```lua
/> os.edit("autorun.lua")
```