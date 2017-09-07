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

# Supported ADC devices

## Internal ADC

In ESP32 only one ADC unit is available:

_adc.ADC1:_

  * This is the internal ADC module.
  * ADC1 can work at 9, 10, 11 and 12 bits of resolution.
  * VRef- is 0.0V and VRef+ is set to 1.1V. This reference voltages can't be set by the programmer.
  * 8 ADC channels are provided, but only 6 are available: 0, 3, 4, 5, 6, 7.

When using the internal ADC the programmer can reference the channel by it's number (from 0 to 7) or by GPIO:

| Channel | GPIO |
|---------|------|
| 0       | 36   |
| 3       | 39   |
| 4       | 32   |
| 5       | 32   |
| 6       | 34   |
| 7       | 35   |

In ESP32 readings higher than 1.1V are achieved using an attenuation factor that reduces the input voltage, but the tests performed by the Whitecat Team shows that using attenuation can cause imprecise readings. Our recommendation is to use a voltage divider or external ADC hardware if you need to measure voltages higher than 1.1V.

## External ADC

Lua RTOS allows the programmer to access to external ADC units using the same API.

* adc.ADS1115:

  * This unit is mapped to an external ADS1115 chip (I2C interface).
  * Working resolution is 15 bits.
  * The internal voltage reference that cannot be set by hardware or software.
  * ADC input values can vary from 0 to 6144 mVolts.
  * 4 ADC channels are provided, from 0 to 4.

    [ADS1115 Datasheet](http://www.ti.com/lit/ds/sbas444c/sbas444c.pdf)

* adc.MCP3008:

  * This unit is mapped to an external MCP3008 chip (SPI interface), with a maximum of 10-bit resolution.
  * Working resolution is 10 bits.
  * The programmer can provide the VRef+ and VRef- values when using this unit (see adc.attach function). The default VRef+ and VRef- values are 3.3V and 0V.
  * 8 ADC channels are provided, from 0 to 7.

    [MCP3008 Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/21295C.pdf)

* adc.MCP3208:

  * This unit is mapped to an external MCP3208 chip (SPI interface), with a maximum of 12-bit resolution.
  * Working resolution is 12 bits.
  * The programmer can provide the VRef+ and VRef- values when using this unit (see adc.attach function). The default VRef+ and VRef- values are 3.3V and 0V.
  * 8 ADC channels are provided, from 0 to 7.

    [MCP3208 Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/21298D.pdf)

# Configuration funcions

## adc = adc.attach(id, channel, [resolution, vref, max value])

Attach an ADC device to an ADC channel.

Arguments:

* id: ADC module identifier. Use one of the constants defined in [Internal ADC](#internal-adc) or [External ADC](#external-adc) for this purpose.
* channel: ADC channel identifier. Use the constant adc.ADC_CHx for this purpose.
* resolution (optional): resolution to use.

  This is not allowed in all ADC supported devices (see [Supported ADC devices](ADC-module#supported-adc-devices)).
  If resolution is not provided, or it's value is 0 or nil the default resolution is applied.

* vref (optional): positive voltage reference in millivolts.

  This is not allowed in all ADC supported devices (see [Supported ADC devices](ADC-module#supported-adc-devices)).
  If vref is not provided,  or it's value is 0 or nil the default vref is applied.
* max value (optional): max input voltage applied to the channel.
  
  This is not allowed in all ADC supported devices (see [Supported ADC devices](ADC-module#supported-adc-devices)).
  If max value is not provided, or it's value is 0 or nil the default vref is applied.

  This value is used internally for configure the ADC for get the best measure. For example if we need to measure a sensor value that gives a max voltage of 1100 mVolts and we are using an external ADS1115 chip this will be set the PGA setting to +/- 2048.

Returns: an ADC channel instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Setup device attached to ADC1 on GPIO32
channel = adc.attach(adc.ADC1, pio.GPIO32)
```

# Operation functions

## raw, millivolts = instance:read()

Read the channel instance's ADC value.

Returns: the raw value, the raw value converted to millivolts, or an exception.

* raw: raw value
* millivolts: raw value converted to millivolts 

```lua
-- Setup device attached to ADC1 on GPIO32
channel = adc.attach(adc.ADC1, pio.GPIO32)

-- Read
raw, millivolts = channel:read()
```