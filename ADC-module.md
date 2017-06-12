# About this

This module contains functions for accessing the analog to digital converter (ADC) module.

ADC units are encoded into a byte and are platform-dependent. For this reason the ADC module define a numeric constant for each available ADC unit. For example, in ESP32 only one ADC unit is available, and it is defined by the constant adc.ADC1.

Each ADC unit has one or more ADC channels that are encoded into a byte and are platform-dependent. The ADC module define a numeric constant for each available ADC channel. For example, in ESP32 there are 8 ADC channels, defined by the constants from adc.ADC_CH0 to adc.ADC_CH7. If you refer to an inexistent ADC channel, a nil value is returned.

# Key concepts

An ADC is a system that converts an analog signal, such as a sound picked up by a microphone or light entering a digital camera, into a digital signal.

Internally an ADC is calibrated to operate in a range of voltages defined by VRef- and VRef+, and converts the analog input, at a given resolution, to a binary number, that is proportional to [VRef-, VRef+]. For example, if an ADC has a 12-bit resolution, and VRef- = 0, and VRef+ = 3.3 V, when the analog signal is 0 V the conversion is 0, when the analog signal is 3.3 V the conversion is 4095, and when the input signal is 1,65 V the conversion is 2048.

To use this module you must take into consideration the following:

1. Attach an ADC device to an ADC channel, using the adc.attach function. The attach function returns an instance of the ADC channel where the device is connected. You must store this instance into a variable for further operation with it.

   ```lua
   device = adc.attach(.....)
   ```

2. Read from the ADC.

   ```lua
   device:read()
   ```

# ESP32 notes

In ESP32 only one ADC unit is available:

**adc.ADC1:**

  * This is the internal ADC module, with a maximum 12-bit resolution.
  * VRef- is 0.0V and VRef+ is arround 1.1V.
  * 8 ADC channels are provided, from adc.ADC_CH0 to adc.ADC_CH7.

# External ADC

Lua RTOS allows the programmer to access to external ADC units using the same API.

* adc.MCP3008:

  * This unit is mapped to an external ADC converter through the MCP3008 chip (SPI interface), with a maximum 10-bit resolution.

  * The programmer must to provide VRef+ and VRef- values when using this unit (see adc.setup function). The default VRef+ and VRef- values are 3.3V and 0V respectively.

  * 8 ADC channels are provided, from adc.ADC_CH0 to adc.ADC_CH7.

* adc.MCP3208:

  * This unit is mapped to an external ADC converter through the MCP3208 chip (SPI interface), with a maximum 12-bit resolution.

  * The programmer must to provide VRef+ and VRef- values when using this unit (see adc.setup function). The default VRef+ and VRef- values are 3.3V and 0V respectively.

  * 8 ADC channels are provided, from adc.ADC_CH0 to adc.ADC_CH7.

# Setup funcions

## adc = adc.setup(id, channel, resolution, [vrefpos, vrefneg])

Setup the ADC channel.

Arguments:

* id: ADC module identifier. Use the constant adc.ADCx defined for this purpose.
* channel: ADC channel identifier. Use the constant adc.ADC_CHx for this purpose.
* resolution: resolution to use, can be either 12, 11, 10, 9, 7, 8 or 6 bits.
* vrefpos (optional): positive voltage reference in millivolts. If you don't provide this argument vref+ is set to the default vref+ for the ADC module.
* vrefneg (optional): negative voltage reference in millivolts. If you don't provide this argument vref- is set to the default vref- for the ADC module.

Returns: an ADC channel instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Setup channel 0 for ADC1 with 12 bits of resolution
channel = adc.setup(adc.ADC1, adc.ADC_CH0, 12)
```

# Operation functions

## raw, millivolts = instance:read()

Read the channel instance's ADC value.

Returns: the raw value, the raw value converted to millivolts, or an exception.

* raw: raw value
* millivolts: raw value converted to millivolts 

```lua
-- Setup channel 0 for ADC1 with 12 bits of resolution
channel = adc.setup(adc.ADC1, adc.ADC_CH0, 12)

-- Read
raw, millivolts = channel:read()
```