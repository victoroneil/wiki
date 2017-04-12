# About this

This module contains functions for accessing the Controller Area Network (CAN) module.

CAN modules are encoded into a byte and are platform-dependent. For this reason the CAN module define a numeric constant for each available CAN module.

In ESP32 only one CAN module is available, and it is defined by the constant can.CAN0.

# Key concepts

A Controller Area Network (CAN bus) is a vehicle bus standard designed to allow MCUs and devices to communicate with each other in applications without a host computer. It is a message-based protocol, designed originally for multiplex electrical wiring within automobiles, but is also used in many other contexts.

# Setup functions

## can.setup(id, speed)

Setup the CAN module.

Arguments:

* id: CAN module identifier, for example can.CAN0.
* speed: speed for the CAN bus expressed in KBits/s.

Returns: noting, or an exception.

```lua
-- Setup CAN at 1000 KBits/s
can.setup(can.CAN1, 1000)
```