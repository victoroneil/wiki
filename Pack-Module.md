This module contains functions for packing data into a Lua string and unpacking data from a Lua string. Data is encoded in an hexadecimal's string representation (i.e. a 0x0102 binary value is represented with the string "0102").

Pack functions are useful, for example, for packing data prior to send through LoraWAN protocol, and for unpacking data received from LoraWan protocol.

This module works under the following assumptions:

* Data is in little-endian format (least significant byte, is at the lowest address)
* Integers have a length of 32 bits
* Floats are represented in IEEE 754 single-precision format, and have a length of 32 bits
* Booleans are represented in a byte (1 = true, 0 = false)
* Strings are ended by the NULL char (0x00)

Data is packed in an hexadecimal's string representation, with this format:

* Header
  * First byte: number of values packed in the string
  * N bytes with the information about the data type of each packed value. Each byte have information about 2 packed values, one for each nibble. Data types are coded in this way:
    * 0b0000: Number
    * 0b0001: Integer
    * 0b0010: Nil
    * 0b0011: Boolean
    * 0b0100: String

* N bytes of data


```text
The pack string (without spaces) for 1 (integer), true (boolean), nil and 4 (integer) are:

03 13 20 01000000 01 04000000

03 is the number of packed values, in this case 3
13 is the type of the first and second packed values: integer and boolean
21 is the type of the third and fourth packed values: nil and integer

01000000: 1 (integer)
01      : true (boolean)
04000000: 4 (integer)

Take note that the nil value is only present in the header and has not representation in the data.
```

## pack.pack(val1 [, val2, ..., valn])

Packs the values in an hexadecimal's string representation. 

Arguments:

* val1: first value
* val2: second value (optional)
* ....

Returns: a string with the values packed in, or an exception.

```lua
-- Pack the values 1 (integer), true (boolean) and 1.2 (number)
pack.pack(1, true, 1.2)
```

## pack.unpack(string, [only first])

Unpack the values coded in an hexadecimal's string representation. 

Arguments:

* string: a string with the values packed in
* only first: only unpack first value (optional)
* ....

Returns:

* if only first argument is true, the unpacked value and a string with the rest of values packed (or nil if there are not more values), or an exception

* if only first argument is false or is not present, the unpacked value, or an exception

```lua
-- Pack the values 1 (integer), true (boolean) and 1.2 (number)
p = pack.pack(1, true, 1.2)

-- Unpack the values
a, b, c = pack.unpack(p)
```

```lua
-- Pack the values 1 (integer), true (boolean) and 1.2 (number)
p = pack.pack(1, true, 1.2)

-- Unpack the values

-- Unpack first value, a = 1
a, p = pack.unpack(p, true)

-- Unpack next value, b = true
b, p = pack.unpack(p, true)

-- Unpack next value, c = 1.2
c, p = pack.unpack(p, true)

-- Unpack next value, d = nil, p = nil
d, p = pack.unpack(p, true)
```
