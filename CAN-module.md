# About this

This module contains functions for accessing the Controller Area Network (CAN) module.

CAN modules are encoded into a byte and are platform-dependent. For this reason the CAN module defines a numeric constant for each available CAN module.

In ESP32 only one CAN module is available, and it's defined by the constant can.CAN0.

# Key concepts

A Controller Area Network (CAN bus) is a vehicle bus standard designed to allow MCUs and devices to communicate with each other in applications without a host computer. It is a message-based protocol, designed originally for multiplex electrical wiring within automobiles, but is also used in many other contexts.

# ESP32 Notes

The ESP32 CAN module is based on the [SJA100](https://www.nxp.com/documents/data_sheet/SJA1000.pdf).
 
# Setup functions

## can.setup(id, speed)

Setup the CAN module.

Arguments:

* id: CAN module identifier, for example can.CAN0.
* speed: speed for the CAN bus expressed in KBits/s.

Returns: noting, or an exception.

```lua
-- Setup CAN at 1000 KBits/s
can.setup(can.CAN0, 1000)
```

# Operation functions

## can.send(id, frame id, frame type, len, data)

Send a CAN data frame over the CAN bus.

Arguments:

* id: CAN module identifier.
* frame id: frame identifier.
* frame type: frame type, can be either can.STD for a 11-bit identifier, or can.EXT for a 29-bit identifier.
* len: length of the frame (maximum of 8 byte according to CAN specs).
* data: a string with the data to send.

Returns: nothing, or an exception.


```lua
-- Setup CAN at 1000 KBits/s
can.setup(can.CAN1, 1000)

-- Send a data frame with standard identifier 100 and contents 1234
can.send(can.CAN0, 100, can.STD, 4, "1234")
```

## frame id, frame type, len, data = can.receive(id)

Receives a CAN data frame from the CAN bus. It's the programmer's responsibility to filter the received frames, because filter capabilities are not currently implemented.

Arguments:

* id: CAN module identifier.

Returns:

* frame id: frame identifier.
* frame type: frame type, can be can.STD, or can.EXT.
* len: length of the received frame.
* data: a string with the received frame data.


```lua
-- Setup CAN at 1000 KBits/s
can.setup(can.CAN1, 1000)

-- Receive data frame
id, type, len, data = can.recv(can.CAN0)
```