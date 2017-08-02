# About this

This module contains functions for accessing the analog to digital converter (ADC) module.

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

# Internal ADC

In ESP32 only one ADC unit is available:

_adc.ADC1:_

  * This is the internal ADC module, with a maximum of 12-bit resolution.
  * VRef- is 0.0V and VRef+ can be either 1.1V, 1.5V, 2.2V, or 3.3V.
  * 8 ADC channels are provided, from adc.ADC_CH0 to adc.ADC_CH7.

In ESP32 voltage references higher than 1.1V are achieved using an attenuation factor that reduces the input voltage, but this attenuation generates imprecise conversions, almost with the current esp-idf. Please, use external ADC hardware if you need to measure voltages higher than 1.1V.

# External ADC

Lua RTOS allows the programmer to access to external ADC units using the same API.

* adc.ADS1115:

  * This unit is mapped to an external ADC converter through the ADS1115 chip (I2C interface), with a maximum of 15-bit resolution.

  * The programmer must to provide VRef+ and VRef- values when using this unit (see adc.attach function). The default VRef+ and VRef- values are 3.3V and 0V respectively.

  * 4 ADC channels are provided.

    [ADS1115 Datasheet](http://www.ti.com/lit/ds/sbas444c/sbas444c.pdf)

* adc.MCP3008:

  * This unit is mapped to an external ADC converter through the MCP3008 chip (SPI interface), with a maximum of 10-bit resolution.

  * The programmer must to provide VRef+ and VRef- values when using this unit (see adc.attach function). The default VRef+ and VRef- values are 3.3V and 0V respectively.

  * 8 ADC channels are provided, from adc.ADC_CH0 to adc.ADC_CH7.

    [MCP3008 Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/21295C.pdf)

* adc.MCP3208:

  * This unit is mapped to an external ADC converter through the MCP3208 chip (SPI interface), with a maximum of 12-bit resolution.

  * The programmer must to provide VRef+ and VRef- values when using this unit (see adc.attach function). The default VRef+ and VRef- values are 3.3V and 0V respectively.

  * 8 ADC channels are provided.

    [MCP3208 Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/21298D.pdf)

# Configuration funcions

## adc = adc.attach(id, channel, [resolution, vref+, vref-])

Attach an ADC device to an ADC channel.

Arguments:

* id: ADC module identifier. Use one of the constants defined in [Internal ADC] or [External ADC] for this purpose.
* channel: ADC channel identifier. Use the constant adc.ADC_CHx for this purpose.
* resolution (optional): resolution to use, can be either 16, 15, 14, 13, 12, 11, 10, 9, 8, 7 or 6 bits. If resolutions is not provided, or it's value is 0 default resolution is applied.
* vref+ (optional): positive voltage reference in millivolts. If you don't provide this argument vref+ is set to the default vref+ for the ADC module.
* vref- (optional): negative voltage reference in millivolts. If you don't provide this argument vref- is set to the default vref- for the ADC module.

Returns: an ADC channel instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Setup channel 0 for ADC1 with 12 bits of resolution, using default
-- reference voltages
channel = adc.attach(adc.ADC1, adc.ADC_CH0, 12)
```

# Operation functions

## raw, millivolts = instance:read()

Read the channel instance's ADC value.

Returns: the raw value, the raw value converted to millivolts, or an exception.

* raw: raw value
* millivolts: raw value converted to millivolts 

```lua
-- Setup channel 0 for ADC1 with 12 bits of resolution
channel = adc.attach(adc.ADC1, adc.ADC_CH0, 12)

-- Read
raw, millivolts = channel:read()
```