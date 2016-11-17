# pio module
 
This module contains functions for accessing the CPU's PIO (Programmable Input 
Output) pins. Access can be at port level (all port i/o pins at the same time)
or at pin level (only one port i/o pin). Port access are made using pio.port 
functions and pin access are made using pio.pin functions.

I/O ports are encoded into a byte and are platform-dependent. For this reason PIO module define a numeric constant for each I/O port available. For example in ESP32 platform I/O GPIO15 pin is defined by the constant pio.GPIO15. Please refer to your platform or board documentation to know which I/O pins are available. If you refer to an inexistent I/O, a nil value is returned.

Usually, when working with micro-controllers one I/O pin can be overlapped with other functions (such as ADC, SPI, UART, etc ...). In Lua RTOS you don't need to worry about this, so PIO functions take this on 
consideration, and do the necessary actions to configure the pin as input / output.

## pio.pin.setdir(direction, pin1 [, pin2, ..., pinn])

Set direction (input / output) for pins.

No assumption should be made on the direction of a pin after a restart of the 
whitecat. Before using a pin you must set it's direction using this function.

Arguments:

* direction: the pin direction, can be either pio.INPUT or pio.OUTPUT
* pin1: first pin
* pin2: second pin (optional)
* ....

Returns: nothing


## pio.pin.setpull(type, pin1 [, pin2, ..., pinn])

Enable/disable pullups/pulldowns on the specified pins.

Arguments:

* type: can be either pio.PULLUP to enable pullups, pio.PULLDOWN to enable 
pulldowns, or pio.NOPULL to disable both pullups and pulldowns
* pin1: first pin
* pin2: second pin (optional)
* ....

Returns: nothing


## pio.pin.sethigh(pin1 [, pin2, ..., pinn])

Set pins to 1 (high).

Arguments:

* pin1: first pin
* pin2: second pin (optional)
* ....

Returns: nothing


## pio.pin.setlow(pin1 [, pin2, ..., pinn])

Set pins to 0 (low).

Arguments:

* pin1: first pin
* pin2: second pin (optional)
* ....

Returns: nothing


## pio.pin.setval(value, pin1 [, pin2, ..., pinn])

Set pins to 0 (low).

Arguments:

* value: value for pins (0 or 1)
* pin1: first pin
* pin2: second pin (optional)
* ....

Returns: nothing


## val1, val2, ..., valn = pio.pin.getval( pin1, pin2, ..., pinn )

Get the values of the pins (0 or 1 for each one).

Arguments:

* pin1: first pin
* pin2: second pin (optional)
* ....

Returns:

* val1: value of pin1 (0 or 1)
* val2: value of pin2 (0 or 1)
* ....


## pio.pin.num(pin1 [, pin2, ..., pinn])

Gets pio's CPU pin number for pin. This function can get different values for
the same pin in different CPU variations for the same family. For example, in a
PIC32MZ2048EFH064 pio.PB_4 it's on pin number 12 and on a PIC32MZ2048EFH144
it's on pin number is 26.

Arguments:

* pin1: first pin
* pin2: second pin (optional)
* ....

Returns: CPU pin number


## port, pin = pio.decode(pin)

Decodes pin codification into it's components (port and pin).

Arguments:

* pin: pin to decode

Returns:

* port: port number (A = 1, B = 2, ...)
* pin: port pin number


## pio.port.setdir(direction, port1 [, port2, ..., portn])

Set direction (input / output) for ports.

No assumption should be made on the direction of a port after a restart of the 
whitecat. Before using a port you must set it's direction using this function.

Arguments:

* direction: the port direction, can be either pio.INPUT or pio.OUTPUT
* port1: first port1
* port2: second port (optional)
* ....

Returns: nothing


## pio.port.setpull(type, port1 [, port2, ..., portn])

Enable/disable pullups/pulldowns on the specified ports.

Arguments:

* type: can be either pio.PULLUP to enable pullups, pio.PULLDOWN to enable 
pulldowns, or pio.NOPULL to disable both pullups and pulldowns
* port1: first port
* port2: second port (optional)
* ....

Returns: nothing


## val1, val2, ..., valn = pio.port.getval(port1 [, port2, ..., portn])

Get value of ports.

Arguments:

* port1: first port
* port2: second port (optional)
* ....

Returns:

* val1: first port value
* val2: second port value (optional)
* ....

## pio.port.sethigh(port1 [, port2, ..., portn])

Set ports to 1 (high).

Arguments:

* port1: first port
* port2: second port (optional)
* ....

Returns: nothing


## pio.port.setlow(port1 [, port2, ..., portn])

Set ports to 0 (low).

Arguments:

* port1: first port
* port2: second port (optional)
* ....

Returns: nothing


## Example: configure for output and set high

```lua
led_pin = pio.PB_4
pio.pin.setdir(pio.OUTPUT, led_pin)
pio.pin.sethigh(led_pin)
```