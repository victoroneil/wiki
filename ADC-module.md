# About this

This module contains functions for accessing the analog to digital converter (ADC) module.

ADC units are encoded into a byte and are platform-dependent. For this reason the ADC module define a numeric constant for each available ADC unit. For example, in ESP32 there are one available ADC unit that is defined by the constant ADC0. Please refer to your platform or board documentation to know which ADC units are available. If you refer to an inexistent ADC, a nil value is returned.

Each ADC unit has one or more ADC channels that are encoded into a byte and are platform-dependent. The ADC module define a numeric constant for each available ADC channel. For example, in ESP32 there are 8 ADC channels. Please refer to your platform or board documentation to know which ADC channels are available. If you refer to an inexistent ADC channel, a nil value is returned.

# Key concepts

An ADC is a system that converts an analog signal, such as a sound picked up by a microphone or light entering a digital camera, into a digital signal.

Internally an ADC is calibrated to operate in a range voltages defined by VRef- and VRef+, and converts the analog input, at a given resolution, to a binary number, that is proportional to [VRef-, VRef+]. For example, if an ADC has a 12-bit resolution, and VRef- = 0, and VRef+ = 3.3 V, when the analog signal is 0 V the conversion is 0, when the analog signal is 3.3 V the conversion is 4095, and when the input signal is 1,65 V the conversion is 2048.

To use this module you must take into consideration the following:

1. Create an ADC instance, using the spi.setup function, and store the instance into a variable.

  ```lua
   instance = adc.setup(.....)
   ```

2. Use the variable instance for create an instance of an ADC channel:

   ```lua
   chan = instance:setupchan()
   ```

3. Use the variable chan for read :

   ```lua
   chan:read(...)
   ```

# Setup funcions

## adc = adc.setup(id)

Setup the ADC module.

Arguments:

* id: ADC module identifier. Use adc.ADCx defined for this purpose.

Returns: an ADC instance or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Setup ADC0
adc0 = adc.setup(adc.ADC0)
```

## channel = instance:setupchan(resolution, channel)

Setup an ADC channel.

Arguments:

* resolution: resolution to use, can be either 12, 11, 10, 9, 8 or 6 bits 
* channel: ADC channel

Returns: an ADC channel instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Setup ADC0
adc0 = adc.setup(adc.ADC0)

-- Setup ADC0 channel 0 to 12-bit resolution
channel = adc0:setupchan(12, 0)
```

# Operation functions

## raw, millivolts = instance:read()

Read the channel instance's ADC value.

Returns:

* raw: raw value
* millivolts: raw value converted to millivolts 

```lua
-- Setup ADC0
adc0 = adc.setup(adc.ADC0)

-- Setup ADC0 channel 0 to 12-bit resolution
channel = adc0:setupchan(12, 0)

-- Read ADC0 channel 0
raw, millivolts = channel:read()
```