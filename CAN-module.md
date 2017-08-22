# About this

This module contains functions for accessing the Controller Area Network (CAN) module.

CAN modules are encoded into a byte and are platform-dependent. For this reason the CAN module defines a numeric constant for each available CAN module.

In ESP32 only one CAN module is available, and it's defined by the constant can.CAN0.

The functions of this module are organized in the following categories:

* [Configuration functions](#configuration-functions)
* [Operation functions](#operation-functions)

# Key concepts

A Controller Area Network (CAN bus) is a vehicle bus standard designed to allow MCUs and devices to communicate with each other in applications without a host computer. It is a message-based protocol, designed originally for multiplex electrical wiring within automobiles, but is also used in many other contexts.

# ESP32 Notes

The ESP32 CAN module is based on the [SJA100 CAN controller](https://www.nxp.com/documents/data_sheet/SJA1000.pdf), and needs an external CAN transceiver, such as the [VP231](https://upverter.com/datasheet/fb1ba5237f33ad28b4f78a053c64762efe576adc.pdf).

Proposed connection:

| ESP32                  | VP231 | Description |
|------------------------|-------|-------------|
|GPIO5 / GPIO12 / GPIO25 | D     | CAN TX      |
|GPIO4 / GPIO14 / GPIO35 | R     | CAN RX      |
 
CAN TX / CAN RX pin assignment is done in build-time through Kconfig under Lua RTOS -> Hardware -> CAN pin map.

# Configuration functions

## can.attach(id, speed)

Attach a CAN device to a CAN module. When the device is attached no filters are defined, and all CAN packets are accepted.

Arguments:

* id: CAN module identifier, for example can.CAN0.
* speed: speed for the CAN bus expressed in KBits/s.

Returns: noting, or an exception.

```lua
-- Attach the CAN device to CAN0 at 1000 KBits/s
can.attach(can.CAN0, 1000)
```

## can.addfilter(id, from, to)

Add a filter. Only CAN packets that match the filter will be accepted.

Arguments:

* id: CAN module identifier, for example can.CAN0.
* from: first id.
* to: last id.

Returns: noting, or an exception.

```lua
-- Attach the CAN device to CAN0 at 1000 KBits/s
can.attach(can.CAN0, 1000)

-- Accept only packets from 200 to 250
can.addfilter(can.CAN0, 200, 250)
```

## can.removefilter(id, from, to)

Remove a filter. If all filters are removed, all CAN packets will be accepted.

Arguments:

* id: CAN module identifier, for example can.CAN0.
* from: first id.
* to: last id.

Returns: noting, or an exception.

```lua
-- Attach the CAN device to CAN0 at 1000 KBits/s
can.attach(can.CAN0, 1000)

-- Accept only packets from 200 to 250
can.addfilter(can.CAN0, 200, 250)

....

-- Remove filter from 200 to 250
can.removefilter(can.CAN0, 200, 250)
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
-- Attach the CAN device to CAN0 at 1000 KBits/s
can.attach(can.CAN0, 1000)

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
-- Attach the CAN device to CAN0 at 1000 KBits/s
can.attach(can.CAN0, 1000)

-- Receive data frame
id, type, len, data = can.recv(can.CAN0)
```

# Utility functions

## can.dump(id)

This function let you sniff CAN packets from the CAN interface. For exit, press Ctrl-c.

Arguments:

* id: CAN module identifier.

Returns: nothing, or an exception.

```lua
-- Attach the CAN device to CAN0 at 1000 KBits/s
can.attach(can.CAN0, 1000)

can.dump(can.CAN0)
can0  00000064  [8] 10 bf ba 52 4d 3f dd 80
can0  00000064  [8] 9e cf e2 09 aa 2f 29 1e
can0  00000064  [8] fa 38 e3 9b 2f 31 0d 17
can0  00000064  [8] 4e af a4 dd b6 94 fb d0
can0  00000064  [8] df e7 61 e2 9b 62 4c c3
can0  00000064  [8] ba 4e ed 46 20 5e 45 9c
can0  00000064  [8] f9 55 e7 60 c3 b0 3f a7
can0  00000064  [8] 9d 5c 17 c3 53 dd ec 15
can0  00000064  [8] d5 c6 39 3c 36 c1 dd b9
can0  00000064  [8] 1c 72 95 d4 01 d3 b3 e6
can0  00000064  [8] 34 5d 14 a7 f9 92 7a 1e
can0  00000064  [8] 56 f8 01 2f 3e a6 3b 1b
can0  00000064  [8] 16 64 a5 85 5e 03 10 43
can0  00000064  [8] 58 87 ec 33 b7 0e a1 7e
can0  00000064  [8] bc 85 ed 8a ec fc ae 61
can0  00000064  [8] 5b da b9 63 19 a7 62 07
can0  00000064  [8] 9a 8c 9d 69 3a 9f b6 6e
can0  00000064  [8] a5 ea 9b 72 a9 d5 cc 73
can0  00000064  [8] 6e 40 73 23 a0 cf 7e 61
can0  00000064  [8] 08 91 93 d4 56 21 f9 57
can0  00000064  [8] 5a b1 2f 5d 3c b0 3a 56
can0  00000064  [8] a2 89 b5 98 cf 18 08 a8
can0  00000064  [8] 2e e4 b8 d8 b6 15 66 72
can0  00000064  [8] 49 3f 2b e7 a6 7a 8e b2
can0  00000064  [8] c3 99 9f fd 0f 63 08 47
can0  00000064  [8] 71 e8 0a 42 74 21 37 81
can0  00000064  [8] 05 f1 e7 41 e1 52 42 40
can0  00000064  [8] 67 c8 2f 5d ea 86 53 55
```