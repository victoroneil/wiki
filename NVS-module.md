This module contains functions for store key-value pairs in flash without the need to have a file system. Although Lua RTOS has support for SPIFFS and FAT file systems the use of the NVS module can be useful for store small pieces of information, such as configuration parameters, without the overhead of a file system.

## nvs.write(namespace, key, value)

Write key-value pair into a namespace.

Arguments:

* namespace (string): the namespace to store the key-value pair.
* key (string): the key name.
* value (Lua value): the value. Can be any Lua type: nil, integer, number, boolean, or string.

Returns: nothing, or an exception.

```lua
nvs.write("settings","timeout", 10)
```


## nvs.read(namespace, key)

Read a key-value pair from namespace.

Arguments:

* namespace (string): the namespace to read the key-value pair.
* key (string): the key name to read.

Returns: linked value, or an exception.

```lua
nvs.read("settings","timeout")
```

## nvs.exists(namespace, key)

Check if a key-value pair exists in namespace.

Arguments:

* namespace (string): the namespace to check the key-value pair existence.
* key (string): the key name to to check.

Returns: linked value, or an exception.

```lua
nvs.exists("settings","timeout")
```

## nvs.rm(namespace, key)

Remove key-value pair in namespace.

Arguments:

* namespace (string): the namespace where the key is.
* key (string): the key name remove in namespace.

Returns: a boolean indicating if the key has been removed (true), or an exception.

```lua
nvs.rm("settings","timeout")
```