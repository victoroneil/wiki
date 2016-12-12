# About this

This module contains functions for accessing the CPU's PWM (Pulse Width Modulation).

PWM units are encoded into a byte and are platform-dependent. For this reason the PWM module define a numeric constant for each available PWM unit. For example, in ESP32 there are two available PWM unit that is defined by the constants PWM0 and PWM1. Please refer to your platform or board documentation to know which PWM units are available. If you refer to an inexistent PWM, a nil value is returned.

Each PWM unit has one or more PWM channels that are encoded into a byte and are platform-dependent. The PWM module define a numeric constant for each available PWM channel. For example, in ESP32 there are 16 PWM channels in PWM0. Please refer to your platform or board documentation to know which PWM channels are available. If you refer to an inexistent PWM channel, a nil value is returned.

Note:

In ESP32 implementation only PWM0 is allowed in current version. This module is only suitable for drive leds.


# Key concepts

To use this module you must take into consideration the following:

1. Create a PWM instance, using the pwm.setup function, and store the instance into a variable.

  ```lua
   instance = pwm.setup(.....)
   ```

2. Use the variable instance for create an instance of a PWM channel:

   ```lua
   chan = instance:setupchan()
   ```

3. Use the variable chan for operate with the channel :

   ```lua
   chan:start(...)
   ...
   chan:stop(...)
   ```

# Setup functions

## pwm.setup(id)

Arguments:

* id: PWM module identifier. Use pwm.PWMx defined for this purpose.

Returns: PWM instance or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Setup PWM0 unit
pwm0 = pwm.setup(pwm.PWM0)
```

## chan = instance:setupchan(channel, pin, frequency, initial duty)

Setup a PWM channel.

Arguments:

* channel: a PWM channel identifier. Use pwm.PWM_CHx defined for this purpose. If channel is -1 channel assignment is made by Lua RTOS.
* pin: the GPIO identifier to use. Use pio.GPIOx defined for this purpose.
* frequency: pulse frequency, expressed in hertzs
* initial duty: initial duty value, a decimal number beetween 0 and 1, where 0 is 0%, and 1 is 100%.

Returns: the PWM channel instance or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Setup PWM0 unit
pwm0 = pwm.setup(pwm.PWM0)

-- Setup PWM0's channel 0 connected to GPIO16, at 10 Khz, with initial duty value of 50%.
chan = pwm0:setup(0, pio.GPIO16, 10000, 0.5)
```

# Operation functions

## chan:start()

Start the PWM channel.

Returns: nothing, or an exception.

```lua
-- Setup PWM0 unit
pwm0 = pwm.setup(pwm.PWM0)

-- Setup PWM0's channel 0 connected to GPIO16, at 10 Khz, with initial duty value of 50%.
chan = pwm0:setup(0, pio.GPIO16, 10000, 0.5)

-- Start the PWM channel
chan:start()
```

## pwm.stop()

Stop the PWM channel.

Returns: nothing, or an exception.

```lua
-- Setup PWM0 unit
pwm0 = pwm.setup(pwm.PWM0)

-- Setup PWM0's channel 0 connected to GPIO16, at 10 Khz, with initial duty value of 50%.
chan = pwm0:setup(0, pio.GPIO16, 10000, 0.5)

-- Start the PWM channel
chan:start()

....

-- Stop the PWM channel
chan:stop()

```

## chan:setduty(duty)

Set a new duty value.

Arguments:

* duty: new duty value, a decimal number beetween 0 and 1, where 0 is 0%, and 1 is 100%.

Returns: nothing, or an exception.

```lua
-- Setup PWM0 unit
pwm0 = pwm.setup(pwm.PWM0)

-- Setup PWM0's channel 0 connected to GPIO16, at 10 Khz, with initial duty value of 50%.
chan = pwm0:setup(0, pio.GPIO16, 10000, 0.5)

-- Start the PWM channel
chan:start()

....

-- Now duty is 25 %
chan:setduty(0.25)

....

-- Stop the PWM channel
chan:stop()

```