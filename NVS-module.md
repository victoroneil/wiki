This module contains functions for store key-value pairs in flash without the need to have a file system. Although Lua RTOS has support for SPIFFS and FAT file systems the use of the NVS module can be useful for store small pieces of information, such as configuration parameters, without the overhead of a file system.

## nvs.write(namespace, key, value)

Write key-value pair into a namesapace.

Arguments:

* namespace (string): the namespace to store the key-value pair.
* key (string): the key name
* value (Lua value): the value. Can be any Lua type: nil, integer, number, boolean, or string.

Returns: nothing, or an exception.

```lua
nvs.write("settings","timeout", 10)
```


## nvs.read(namespace, key)

Read a key-value pair from namesapace.

Arguments:

* namespace (string): the namespace to read the key-value pair.
* key (string): the key name to read

Returns: linked value, or an exception.

```lua
nvs.read("settings","timeout")
```