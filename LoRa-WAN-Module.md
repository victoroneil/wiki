This module contains functions for send and receive information through [LoRa WAN] (https://www.lora-alliance.org/What-Is-LoRa/Technology).

Lua RTOS support for LoRa WAN is build over [LMIC] (https://www.research.ibm.com/labs/zurich/ics/lrsc/lmic.html) stack from IBM. Currently only LoRa WAN class A end-devices are supported in Lua RTOS (support for LoRa WAN class B end-devices are scheluded to 2017 Q2).

Please, take note that build a LoRa WAN network involves a lot of things, such as the end-device, the gateway, the network coordinator, etc ... In this page we only talk about the end-device and how is programmed, you can know more about our work on LoRa WAN in [whitecatboard.org] (http://whitecatboard.org).

For use this module you need a SPI LoRa WAN transceiver, such as [RFM95] (http://www.hoperf.com/rf_transceiver/lora/RFM95W.html). Currently we are working on a board that will integrate this chip and ESP32.

It's highly recommended to read the [LoRa WAN specification] (https://www.lora-alliance.org/portals/0/specs/LoRaWAN%20Specification%201R0.pdf).

## lora.setup(band)

Setup the LoRa WAN stack.

Arguments:

* band: the ISM band, can be either lora.BAND868 (Europe) or lora.BAND433 (United States)

Returns: nothing, or an exception.

```lua
-- Setup LoRa WAN stack using ISM band 868 Mhz (Europe)
lora.setup(lora.BAND868)
```

## lora.setAppEui(appEui)

Sets the AppEUI. The AppEUI is a global application ID in IEEE EUI64 address space that uniquely identifies
the application provider of the end-device. It must be set before the activation procedure.

Arguments:

* appEui (8 bytes coded in an hex-string): the AppEUI.

Returns: nothing, or an exception.

```lua
-- Setup LoRa WAN stack using ISM band 868 Mhz (Europe)
lora.setup(lora.BAND868)

-- Sets the AppEUI
lora.setAppEui("70XXX57ED0000XX0")
```

## lora.setAppKey(appKey)

Sets the AppKey. The AppKey is an AES-128 application key specific for the end-device that is assigned by
the application owner to the end-device. It must be set before the activation procedure.

Arguments:

* appKey (16 bytes coded in an hex-string): the AppKey.

Returns: nothing, or an exception.

```lua
-- Setup LoRa WAN stack using ISM band 868 Mhz (Europe)
lora.setup(lora.BAND868)

-- Sets the AppEUI
lora.setAppEui("70XXX57ED0000XX0")

-- Sets the AppKEY
lora.setAppKey("8CXXXX5A80XXXX0FXX18XXBCXX41XXXX")
```

## lora.setDevEui(devEui)

Sets the DevEUI. The DevEUI is a global end-device ID in IEEE EUI64 address space that uniquely identifies
the end-device.

ATTENTION!! it's your responsibility to assign an IEEE EUI64 that you own.

Arguments:

* devEui (8 bytes coded in an hex-string): the DevEUI.

Returns: nothing, or an exception.

```lua
-- Setup LoRa WAN stack using ISM band 868 Mhz (Europe)
lora.setup(lora.BAND868)

-- Sets the AppEUI
lora.setAppEui("70XXX57ED0000XX0")

-- Sets the AppKEY
lora.setAppKey("8CXXXX5A80XXXX0FXX18XXBCXX41XXXX")

-- Sets the DevEUI
lora.setDevEui("XXB3XX7E000XX000")
```


## lora.setDr(data_rate)

Sets the maximum data rate to use in the next transmission. This value is ignored if the adaptive data rate is enabled.

Arguments:

* data_rate (integer): the data rate, a number between 0 (lowest data rate) and 7 (highest data rate).

Returns: nothing, or an exception.

```lua
-- Setup LoRa WAN stack using ISM band 868 Mhz (Europe)
lora.setup(lora.BAND868)

-- Sets the AppEUI
lora.setAppEui("70XXX57ED0000XX0")

-- Sets the AppKEY
lora.setAppKey("8CXXXX5A80XXXX0FXX18XXBCXX41XXXX")

-- Sets the DevEUI
lora.setDevEui("XXB3XX7E000XX000")

-- Sets the data rate
lora.setDr(5)
```


## lora.setAdr(enable)

Enables or disables the adaptive data rate function.

Arguments:

* enable (boolean): if true adaptive data rate is enabled.

Returns: nothing, or an exception.

```lua
-- Setup LoRa WAN stack using ISM band 868 Mhz (Europe)
lora.setup(lora.BAND868)

-- Sets the AppEUI
lora.setAppEui("70XXX57ED0000XX0")

-- Sets the AppKEY
lora.setAppKey("8CXXXX5A80XXXX0FXX18XXBCXX41XXXX")

-- Sets the DevEUI
lora.setDevEui("XXB3XX7E000XX000")

-- Sets the data rate
lora.setDr(5)

-- Disable the ADR function
lora.setAdr(false)
```