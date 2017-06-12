# About this

This module contains functions for send and receive information through [LoRa WAN](https://www.lora-alliance.org/What-Is-LoRa/Technology).

Lua RTOS support for LoRa WAN is build over [LMIC](https://www.research.ibm.com/labs/zurich/ics/lrsc/lmic.html) stack from IBM.

Please, take note that build a LoRa WAN network involves a lot of things, such as the end-device, the gateway, the network coordinator, etc ... In this page we only talk about the end-device and how is programmed, you can know more about our work on LoRa WAN in [whitecatboard.org](https://whitecatboard.org).

# What do you need?

For use this module you need a SPI LoRa WAN transceiver. If you need a ready-to-use LoRa WAN board based on ESP32 you can buy the [Whitecat ESP32 N1 board](https://whitecatboard.org/whitecat-esp32-n1-board).

It's highly recommended to read the [LoRa WAN specification](https://www.lora-alliance.org/portals/0/specs/LoRaWAN%20Specification%201R0.pdf).

# Key concepts

To participate in a LoRaWAN network, each end-device has to be personalized and activated. This can be achieved in two ways, either via Over-The-Air Activation (OTAA) or via Activation By Personalization (ABP). After activation, the following information is stored in the end-device: a device address (DevAddr), an application identifier (AppEUI), a network session key (NwkSKey), and an application session key (AppSKey):

* OTAA: end-devices must follow a join procedure (calling the lora.join function) prior to participating in data exchanges with the network server. The following data must be provided:

   * DevEUI: use lora.setDevEui for this
   * AppEUI: use lora.setAppEui for this
   * AppKey: use lora.setAppKey for this

* ABP: end-devices don't need to follow a join procedure to participate in data exchanges with the network server. The following data must be provided:

   * DevAddr: use lora.setDevAddr for this
   * NwkSKey: use lora.setNwkSKey for this
   * AppSKey: use lora.setAppSKey for this

# Configuration functions

Configuration functions are used for configure the LoRa WAN stack, such as init the stack, set the stack configuration, etc ...

## lora.attach(band)

Attach the Lora Transceiver.

Arguments:

* band: the ISM band, can be either lora.BAND868 (Europe) or lora.BAND915 (United States)

Returns: nothing, or an exception.

```lua
-- Attach LoRa transceiver using ISM band 868 Mhz (Europe)
lora.attach(lora.BAND868)
```

# End-device activation functions

This functions set the data that must be provided for the end-device activation. Remember that for OTAA you must provide DevEUI, AppEUI, and AppKey, and for ABP you must provide DevAddr, NwkSKey and AppSKey. Use the functions described in this section for that.


## lora.setAppEui(appEui)

Sets the AppEUI. The AppEUI is a global application ID in IEEE EUI64 address space that uniquely identifies
the application provider of the end-device. It must be set before the activation procedure via OTAA.

Arguments:

* appEui (8 bytes coded in an hex-string): the AppEUI.

Returns: nothing, or an exception.

```lua
....
....

-- Sets the AppEUI
lora.setAppEui("70XXX57ED0000XX0")
```

## lora.setAppKey(appKey)

Sets the AppKey. The AppKey is an AES-128 application key specific for the end-device that is assigned by
the application owner to the end-device. It must be set before the activation procedure via OTAA.

Arguments:

* appKey (16 bytes coded in an hex-string): the AppKey.

Returns: nothing, or an exception.

```lua
....
....

-- Sets the AppKEY
lora.setAppKey("8CXXXX5A80XXXX0FXX18XXBCXX41XXXX")
```

## lora.setDevEui(devEui)

Sets the DevEUI. The DevEUI is a global end-device ID in IEEE EUI64 address space that uniquely identifies
the end-device. It must be set before the activation procedure via OTAA.

ATTENTION!! it's your responsibility to assign an IEEE EUI64 that you own.

Arguments:

* devEui (8 bytes coded in an hex-string): the DevEUI.

Returns: nothing, or an exception.

```lua
....
....

-- Sets the DevEUI
lora.setDevEui("XXB3XX7E000XX000")
```

## lora.setDevAddr(devAddr)

Sets the DevAddr. The DevAddr identifies the end-device within the current network, and is provided by the network owner.

Arguments:

* devAddr (4 bytes coded in an hex-string): the DevAddr.

Returns: nothing, or an exception.

```lua
....
....

-- Sets the DevAddr
lora.setDevAddr("03XXEXXA")
```

## lora.join()

Joins the end-device via OTAA.

Arguments: nothing

Returns: nothing, or an exception.

```lua
....
....

-- Join to the network
lora.join()
```

# Stack configuration functions

This functions configure certain operating parameters of the stack, such us the data rate. This parameters are configured automatically when you attach the LoRa transceiver with the lora.attach function, and can be changed using one of the functions that we describe in this section.


## lora.setDr(data_rate)

Sets the maximum data rate to use in the next transmission. This value is ignored if the adaptive data rate is enabled.

Arguments:

* data_rate (integer): the data rate, a number between 0 (lowest data rate) and 7 (highest data rate).

Returns: nothing, or an exception.

```lua
....
....

-- Sets the data rate
lora.setDr(5)
```


## lora.setAdr(enable)

Enables or disables the adaptive data rate function.

Arguments:

* enable (boolean): if true adaptive data rate is enabled.

Returns: nothing, or an exception.

```lua
....
....

-- Disable the ADR function
lora.setAdr(false)
```

## lora.setReTx(retransmissions)

Set the number of retransmissions for confirmed up-link frames. If no confirmation is received by the end-device the frame will be retransmitted a maximum of "retransmissions" times.

Arguments:

* retransmissions (integer): number of retransmissions, between 0 and 8.

Returns: nothing, or an exception.

```lua
....
....

-- Disable the ADR function
lora.setAdr(false)
```