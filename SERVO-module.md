# About this

This module contains functions to control RC servo motors.

# Key concepts

A servo is a rotary actuator, and typically consists of a small electric motor, driving a train of reduction gears, and controlled by a control circuit. Historically servos have ben used in radio control gadgets and in small-scale robotics. 

Radio control servos are connected through a standard three-wire connection:

* power: typically the red wire, that must be connected to a +5V power supply.
* ground: typically the black or brown wire, that must be connected to the board's and power's supply ground.
* signal: typically the yellow, orange or white wire, that must be connected to a board's GPIO.

Never connect the power wire to a GPIO, or your board will be permanently damage.

To use a servo in your program you must do the following:

1. Attach the servo using the servo.attach(..) function. This returns a servo instance that you must store into a variable.

   ```lua
   -- Attach the servo to GPIO26
   s = servo.attach(pio.GPIO26)
   ```

2. Write values to the servo to move it, using the instance's write function.

   ```lua
   -- Move the servo to the 45º position
   s:write(25)
   ```

3. Detach the stepper instance when it is no longer necessary:

   ```lua
   -- Detach the servo
   s:detach()
   ```

# Configuration funcions

## instance = servo.attach(pin)

Create a new servo instance.

Arguments:

* pin: GPIO to use for the servo signal. Use defined constants in the PIO module for this, for example pio.GPIO126.

Returns: a servo instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Attach the servo to GPIO26
s = servo.attach(pio.GPIO26)
```

## instance:detach()

Detach the servo and free all resources used by the servo.

Arguments: none.

Returns: nothing, or an exception.

```lua
-- Detach the servo
s:detach()
```

# Operation functions

## instance:write(value)

Write a value to a servo instance, controlling the servo movement according to the type of servo:

* For standard servos: the value is the servo's absolute position expressed in degrees. Typically, the value goes from 0º to 180º. In this case writing a new value, moves the servo from it's current position to a new position, and then stops.

* For continuous rotation servos: the value is expressed also in degrees, being 0º full-speed counter clock wise, 180º full-speed clock wise, and 90º being no movement. In this case, writing a new value, changes the servo rotation direction, or the rotation speed.

Arguments:

* value: the value to write, expressed in degrees.

Returns: nothing, or an exception.

```lua
-- Attach the servo to GPIO26
s = servo.attach(pio.GPIO26)

-- Move an standard servo to the 45º position
s:write(45)
```

```lua
-- Attach the servo to GPIO26
s = servo.attach(pio.GPIO26)

-- Move a continuous rotation servo clock wise at full-speed
s:write(180)
```
