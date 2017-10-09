# About this
 
This module contains functions for accessing the CPU's UART.

UART units are encoded into a byte and are platform-dependent. For this reason the UART module define a numeric constant for each available UART unit. For example in ESP32 UART1 is defined by the constant uart.UART1. Please refer to your platform or board documentation to know which UART units are available. If you refer to an inexistent UART, a nil value is returned.

UART functions are not thread-safe. You must call to the lock / unlock functions for made UART functions thread-safe.

The functions of this module are organized in the following categories:

* [Information functions](#information-functions)
* [Configuration functions](#configuration-functions)
* [Operation functions](#operation-functions)

# Information functions

## uart.pins([table])

List the pins assigned to the UART ports. The initial assignments are defined in Kconfig under the Component config -> Lua RTOS -> Hardware -> UART pin map. Prior to use any UART module function you can change the assigned pins through the [uart.setpins](#uartsetpinsid-rx-tx) function.

Arguments:

* table: if true, pin list is returned in a Lua table, if false pin list is printed on the console.

Returns:

* if table is false: nothing or an exception.

* if table is true: a Lua table with the pin list, or an exception. This table is an array of tables. Each entry corresponds to an UART port. Each port gives the following fields:

  * id: the UART port id.
  * rx: the GPIO number assigned to the rx signal.
  * tx: the GPIO number assigned to the tx signal.

```lua
/ > uart.pins()
UART0: rx=GPIO3 tx=GPIO1 
UART1: rx=GPIO26 tx=GPIO25 
UART2: rx=GPIO2 tx=GPIO15 
```

# Configuration functions

## uart.setpins(id, rx, tx)

Sets the pins assigned to an UART port. Use this function if you need to change the initial assignments. The initial assignments are defined in Kconfig under the Component config -> Lua RTOS -> Hardware -> UART pin map.

Arguments:

* id: SPI unit identifier. Use any uart.UARTx defined for this purpose.
* rx: GPIO number assigned to the rx signal. Use any pio.GPIOxx constant for this.
* tx: GPIO number assigned to the tx signal. Use any pio.GPIOxx constant for this.

## uart = uart.attach(id, baud rate, data bits, parity, stop bits, [buffer size, flags])

Attach an UART device to the UART module.

Arguments:

* id: UART unit identifier. Use uart.UARTx defined for this purpose.
* baud rate: desired baud rate, expressed in bauds.
* data bits: number of data bits, can be 8 or 9. 
* parity: parity, can be either uart.PARNONE (none parity), uart.PAREVEN (even parity) or uart.PARODD (odd parity).
* stop bits: number of stop bits, can be either uart.STOP1 (1 stop bits) or uart.STOP2 (2 stop bits)
* buffer size (optional): size of UART rx buffer, expressed in bytes. If you don't pass any value a 1024 byte-buffer is used.
* flags (optional): a bit mask formed by the following constants
   * uart.READ: attach the uart device as read only (only RX is used)
   * uart.WRITE: attach the uart device as write only (only TX is used)
   * default value is uart.READ | uart.WRITE: attach the uart device as read / write (RX and TX are used)

Returns: the real baud rate set on the UART unit, or an exception. This might have a different value than the desired baud rate argument.


```lua
-- Attach an UART device to UART2, 115200 bps, 8N1
uart.attach(uart.UART2, 115200, 8, uart.PARNONE, uart.STOP1)
```

## uart = uart.setup(id, baud rate, data bits, parity, stop bits, [buffer size, flags])

_**This function is deprecated**, and will be removed in the future. Please, use uart.attach instead._

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
-- Attach an UART device to UART2, 115200 bps, 8N1
uart.attach(uart.UART2, 115200, 8, uart.PARNONE, uart.STOP1)

-- Sends AT
uart.write(uart.UART2, "AT")

-- Sends \n and \r
uart.write(uart.UART2, '\n')
uart.write(uart.UART2, '\r')
```

## uart.read(id, format, timeout)

Read data from an UART unit.

Arguments:

* id: UART unit identifier. Use uart.UARTx defined for this purpose.
* format: a string indicating the data type format to read. Can be "*l" for read a string without waiting for a line break, "*el" for read a string until a line break is received, or "*c" for read a byte.
* timeout: timeout, expressed in milliseconds. This function blocks the current thread until all data is received in the specified timeout.

Returns: the readed data, or nil if nothing is received in the specified timeout, or an exception.

```lua
-- Attach an UART device to UART2, 115200 bps, 8N1
uart.attach(uart.UART2, 115200, 8, uart.PARNONE, uart.STOP1)

-- Read line from UART, with a 500 milliseconds timeout
uart.read(uart.UART2, "*l", 500)
```

## uart.consume(id)

Consume all bytes present in an UART's queue and do nothing with them.

Arguments:

* id: UART module identifier. Use uart.UARTx defined for this purpose.

Returns: nothing, or an exception.

```lua
-- Attach an UART device to UART2, 115200 bps, 8N1
uart.attach(uart.UART2, 115200, 8, uart.PARNONE, uart.STOP1)

-- Do something

...
...

-- Consume all bytes from buffer
uart.consume(uart.UART2)
```