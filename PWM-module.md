# About this

This module contains functions for accessing the CPU's PWM (Pulse Width Modulation).

# Key concepts

To use this module you must take into consideration the following:

1. Attach a device to a PWM pin, using the pwm.attach function, and store the instance into a variable.

   ```lua
   device = pwm.attach(.....)
   ```

2. Use the variable device for operate:

   ```lua
   device:start(...)
   ...
   device:stop(...)
   ```

3. Detach the device if it is no longer used:

   ```lua
   device:start(...)
   ...
   device:detach(...)
   ```

# Configuration functions

## device = pwm.attach(pin, frequency, initial duty)

Attach a device to a PWM pin.

Arguments:

* pin: the GPIO identifier to use. Use pio.GPIOx defined for this purpose.
* frequency: pulse frequency, expressed in hertzs
* initial duty: initial duty value, a decimal number beetween 0 and 1, where 0 is 0%, and 1 is 100%.

Returns: the PWM instance or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Attach a device to PWM pin at GPIO16, at 10 Khz, with initial duty value of 50%.
device = pwm.attach(pio.GPIO16, 10000, 0.5)
```

# Operation functions

## device:start()

Start the PWM generation.

Returns: nothing, or an exception.

```lua
-- Attach a device to PWM pin at GPIO16, at 10 Khz, with initial duty value of 50%.
device = pwm.attach(pio.GPIO16, 10000, 0.5)

-- Start the PWM generation
device:start()
```

## device:stop()

Stop the PWM generation.

Returns: nothing, or an exception.

```lua
-- Attach a device to PWM pin at GPIO16, at 10 Khz, with initial duty value of 50%.
device = pwm.attach(pio.GPIO16, 10000, 0.5)

-- Start the PWM generation
device:start()

....

-- Stop the PWM generation
device:stop()
```

## device:setduty(duty)

Set a new duty value.

Arguments:

* duty: new duty value, a decimal number beetween 0 and 1, where 0 is 0%, and 1 is 100%.

Returns: nothing, or an exception.

```lua
-- Attach a device to PWM pin at GPIO16, at 10 Khz, with initial duty value of 50%.
device = pwm.attach(pio.GPIO16, 10000, 0.5)

-- Start the PWM generation
device:start()

....

-- Set duty to 25%
device:setduty(0.25)

....

-- Stop the PWM generation
device:stop()
```

## device:setfreq(frequency)

Set a new frequency value.

Arguments:

* frequency: pulse frequency, expressed in hertzs

Returns: nothing, or an exception.

```lua
-- Attach a device to PWM pin at GPIO16, at 10 Khz, with initial duty value of 50%.
device = pwm.attach(pio.GPIO16, 10000, 0.5)

-- Start the PWM generation
device:start()

....

-- Set frequency to 5 khz
device:setfreq(5000)

....

-- Stop the PWM generation
device:stop()
```

# device:detach()

Detach a device to a PWM pin. When detaching, the PWM generation is stopped. The device can be also detached if it is assigned to the nil value.

Arguments: nothing.

Returns: nothing.

```lua
-- Attach a device to PWM pin at GPIO16, at 10 Khz, with initial duty value of 50%.
device = pwm.attach(pio.GPIO16, 10000, 0.5)

-- Start the PWM generation
device:start()

....

-- Detach the device
device:detach()
```