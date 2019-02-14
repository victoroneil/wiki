The Lua RTOS file system functions provides access to the supported file systems. Some functions, such as create a directory, are provided as an extension of the Lua os and module.

File access functions are provided through the standard Lua io module. This functions are not documented in this wiki, please refer to [this link](http://www.lua.org/manual/5.1/manual.html#5.7) for give more information.

The functions of this module are organized in the following categories:

* [Format functions](#format-functions)
* [File and directory management functions](#file-and-directory-management-functions)

# Format functions

## os.format(filesystem)

Format a file system. Because all data is removed in the format process the function ask for a confirmation.

Arguments:

* file system: a string identifying the file system. Can be either spiffs or fat.

Returns: nothing or an exception.

```lua
/ > os.format("fat")
All data in fat will be deleted. Continue? [y/n]: y
Formatting...
Initializing FAT area: 4% completed
```

# File and directory management functions

## os.cat(filename)

Show (but not modify) the contents of a text file to the screen.

Arguments:

* filename: file path to show. Path can be absolute or relative to current working directory.

Returns: nothing or an error.

## os.cd(path)

Change the current working directory.

Arguments:

* path: directory path. Path can be absolute or relative to current working directory.

Returns: nothing.

```lua
/> os.cd("/examples")
/examples >
```

## os.dmseg()

Show (but not modify) the contents of the system log file one screen at a time. The content is paging through text one screenful at a time.

**Note:** os.dmseg() is not available in file systems that use NOR flash technology for store it's data, such as SPIFFS.

## os.edit(file)

Edits a file.

Arguments:

* file: file path. Can be absolute or relative to current working directory.

Returns: nothing

```lua
/> os.edit("autorun.lua")
```

## os.ls([path])

List the path contents. Limited wildcard support.

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

```lua
/examples/lua > os.ls("/*.lua")
f	    2407	                        	config.lua
f	    1034	                        	autorun.lua
f	    2446	                        	system.lua
f	    1105	                        	settings.lua
/examples/lua > 
```

Directory contents is listed on the screen in columns (separated by tab):

* first column: entry type (d = directory / f = file)
* second column: entry size in bytes
* third column: entry name

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

## os.more(filename)

Show (but not modify) the contents of a text file one screen at a time. The content is paging through text one screenful at a time.

Arguments:

* filename: file path to show. Path can be absolute or relative to current working directory.

Returns: nothing or an error.


## os.pwd()

Get the current working directory.

Arguments: nothing

Returns: the current directory

```lua
/examples > os.pwd()
/examples
```

## os.remove(path)

Remove a file or a directory. Limited wildcard support.

Arguments:

* path: file or directory path to remove. Path can be absolute or relative to current working directory.

Returns: nothing or an error.

```lua
/examples/lua > os.remove("*.bak")
/examples/lua > 
```

## os.rename(old path, new path)

Rename a file or a directory.

Arguments:

* old path: file or directory path to rename. Path can be absolute or relative to current working directory.
* new path: file or directory new path. Path can be absolute or relative to current working directory.

Returns: nothing or an error.

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
