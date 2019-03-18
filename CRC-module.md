This module contains functions for creating a [CRC](https://en.wikipedia.org/wiki/Cyclic_redundancy_check) for a Lua string.
It currently supports the following different crcs:

## pack.crc8(text [, init-value])

Create an 8-bit crc code for the text.

Arguments:

* text: the lua string to create the crc for
* init-value (optional): init value to begin the crc calculation with. default is 0xFF
* ....

Returns: crc-code of the lua string

```lua
/ > crc.crc8("test")
140
```

## pack.crc16(text [, init-value])

Create an 16-bit crc code for the text.

Arguments:

* text: the lua string to create the crc for
* init-value (optional): init value to begin the crc calculation with. default is 0xFF
* ....

Returns: crc-code of the lua string

```lua
/ > crc.crc16("test")
1193
```

## pack.crc32(text [, init-value])

Create an 32-bit crc code for the text.

Arguments:

* text: the lua string to create the crc for
* init-value (optional): init value to begin the crc calculation with. default is 0xFF
* ....

Returns: crc-code of the lua string

```lua
/ > crc.crc32("test")
113532655
```

