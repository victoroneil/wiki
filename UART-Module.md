# About this
 
This module contains functions for accessing the CPU's UART.

UART units are encoded into a byte and are platform-dependent. For this reason the UART module define a numeric constant for each available UART unit. For example in ESP32 UART1 is defined by the constant uart.UART1. Please refer to your platform or board documentation to know which UART units are available. If you refer to an inexistent UART, a nil value is returned.

UART functions are not thread-safe. You must call to the lock / unlock functions for made UART functions thread-safe.

# Utility functions

## uart.pins()

Show available UART units, an it's pins, provided but your platform.
   
```lua
/ > uart.pins()
uart0: rx=040	(pin 40)	tx=041	(pin 41)
uart1: rx=028	(pin 28)	tx=029	(pin 29)
/ >
```


# Setup functions

## uart = uart.setup(id, baud rate, data bits, parity, stop bits, [buffer size])

Setup the UART module.

Arguments:

* id: UART unit identifier. Use uart.UARTx defined for this purpose.
* baud rate: desired baud rate, expressed in bauds.
* data bits: number of data bits, can be 8 or 9. 
* parity: parity, can be either uart.PARNONE (none parity), uart.PAREVEN (even parity) or uart.PARODD (odd parity).
* stop bits: number of stop bits, can be either uart.STOP1 (1 stop bits) or uart.STOP2 (2 stop bits)
* buffer size (optional): size of UART rx buffer, expressed in bytes. If you don't pass any value a 1024 byte-buffer is used.

Returns: the real baud rate set on the UART unit, or an exception. This might have a different value than the desired baud rate argument.


```lua
-- Setup UART3, 115200 bps, 8N1
uart.setup(uart.UART3, 115200, 8, uart.PARNONE, uart.STOP1)
```

# Operation functions

## uart.lock(id)

Lock the UART by the calling thread.

* id: UART unit identifier. Use uart.UARTx defined for this purpose.

Returns: nothing, or an exception.

```lua
-- Lock the console
uart.lock(uart.CONSOLE)

...
...

-- Unlock the console
uart.unlock(uart.CONSOLE)
```

## uart.unlock(id)

Unlock the UART locked by the calling thread.

* id: UART unit identifier. Use uart.UARTx defined for this purpose.

Returns: nothing, or an exception.

```lua
-- Lock the console
uart.lock(uart.CONSOLE)

...
...

-- Unlock the console
uart.unlock(uart.CONSOLE)

```

## uart.write(id, data)

Write data to an UART unit. Data can be a byte (raw data) or a string.

* id: UART unit identifier. Use uart.UARTx defined for this purpose.
* data: data to write can be either a byte (0 from 255) or a string.

Returns: nothing, or an exception.

```lua
-- Setup UART3, 115200 bps, 8N1
uart.setup(uart.UART3, 115200, 8, uart.PARNONE, uart.STOP1)

-- Sends AT
uart.write(uart.UART3, "AT")

-- Sends \n and \r
uart.write(uart.UART3, '\n')
uart.write(uart.UART3, '\r')
```

## uart.read(id, format, timeout)

Read data from an UART unit.

Arguments:

* id: UART unit identifier. Use uart.UARTx defined for this purpose.
* format: a string indicating the data type format to read. Can be "*l" for read a line until \r\n is received or "*c" for read a byte.
* timeout: timeout, expressed in milliseconds. This function blocks the current thread until all data is received in the specified timeout.

Returns: the readed data, or nil if nothing is received in the specified timeout, or an exception.

```lua
-- Setup UART3, 115200 bps, 8N1
uart.setup(uart.UART3, 115200, 8, uart.PARNONE, uart.STOP1)

-- Read line from UART, with a 500 milliseconds timeout
uart.read(uart.UART3, "*l", 500)
```

## uart.consume(id)

Consume all bytes present in an UART's queue and do nothing with them.

Arguments:

* id: UART module identifier. Use uart.UARTx defined for this purpose.

Returns: nothing, or an exception.

```lua
-- Setup UART3, 115200 bps, 8N1
uart.setup(uart.UART3, 115200, 8, uart.PARNONE, uart.STOP1)

-- Do something

...
...

-- Consume all bytes from buffer
uart.consume(uart.UART3)
```