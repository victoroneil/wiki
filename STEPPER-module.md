# About this

This module contains functions for controlling stepper motors.

Please, take in advance that you need a stepper motor driver for connect the motor to your board. Stepper motors works at voltages and currents that are not compatible with your board. Never connect a stepper motor to the board without a stepper motor driver, or your board will be permanently damage.

Stepper module can handle up to 8 motors, each motor needs 2 GPIO, for control the step and direction signals.

# Key concepts

In real applications, steppers are connected to a kinematic system. Before using an stepper you must attach the stepper (using the attach function) and set the variables defined by your kinematic system:

   1. Units, for example 1 cm
   1. Number of steps per unit
   1. Minimum speed, measured in units / minutes
   1. Maximum speed, measured in units / minutes

Once attached, the programmer can move the steppers specifying:

   1. How many units to move, for example 10 centimeter.
   1. At which speed, for example, 5 centimeter / minute.
   1. At which acceleration, for example, 0.1 centimeters / seconds ^ 2

# Setup functions

## instance = stepper.attach(direction pin, step pin, [stpu, min spd, max spd, accel])

Create a new instance for a stepper.

Arguments:

* direction pin: GPIO to use for the direction signal. Use defined constants in the PIO module for this, for example pio.GPIO26.

* step pin: GPIO to use for the step signal. Use defined constants in the PIO module for this, for example pio.GPIO14.

* stpu (optional): a decimal number that sets the number of steps per unit.
* min spd (optional): a decimal number that sets the minimum speed (in units / minutes).
* max spd (optional): a decimal number that sets the maximum speed (in units / minutes).
* accel (optional): a decimal number that sets the default acceleration(in units / seconds ^2).

By default (if you don't use the optional arguments) the stepper is defined as follows:

* Units are revolutions
* stpu = 200 (200 steps per revolution)
* min spd = 60 rpm (60 revolutions per minute) 
* max spd = 1000 rpm (1000 revolutions per minute) 
* accl = 2 revolutions / seconds ^ 2

Returns: a stepper instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Attach 2 steppers, using the default configuration
--
--   stepper1: dir pin at GPIO26, step pin at GPIO14
--   stepper2: dir pin at GPIO12, step pin at GPIO13

s1 = stepper.attach(pio.GPIO26, pio.GPIO14)
s2 = stepper.attach(pio.GPIO12, pio.GPIO13)
```

## instance:move(units, [speed, accel])

Setup the next movement for the stepper instance. You must call to the start function for start the movement.

Movement is specified by:

* units: a decimal number that indicates how many units to move.
* speed (optional): a decimal number that indicates the speed of the movement.
* accel (optional): a decimal number that indicates the acceleration of the movement.

Returns: noting, or an exception.

```lua
-- Attach 2 steppers, using the default configuration
--
--   stepper1: dir pin at GPIO26, step pin at GPIO14
--   stepper2: dir pin at GPIO12, step pin at GPIO13

s1 = stepper.attach(pio.GPIO26, pio.GPIO14)
s2 = stepper.attach(pio.GPIO12, pio.GPIO13)

-- Move s1 10 revolutions
s1:move(10)

-- Move s2 5 revolutions
s2:move(5)
```

## stepper.start(instance1, [instance2, instance3, ...])

Start the movement for a group of stepper defined by the move function. This function blocks until the movement is done.

Arguments: noting

Returns: noting, or an exception.

```lua
-- Attach 2 steppers, using the default configuration
--
--   stepper1: dir pin at GPIO26, step pin at GPIO14
--   stepper2: dir pin at GPIO12, step pin at GPIO13

s1 = stepper.attach(pio.GPIO26, pio.GPIO14)
s2 = stepper.attach(pio.GPIO12, pio.GPIO13)

-- Move s1 10 revolutions
s1:move(10)

-- Move s2 5 revolutions
s2:move(5)

-- Start the movement
stepper.start(s1, s2)
```

# Full example

```lua
dir = 1

-- Attach 2 steppers
--
--   stepper1: dir pin at GPIO26, step pin at GPIO14
--   stepper2: dir pin at GPIO12, step pin at GPIO13
--
-- Steppers are configured by default:
--
--   steps per unit (revolutions): 200
--   min speed: 60 rpm
--   max speed: 800 rpm
--   acceleration: 2 revolutions / secs^2
s1 = stepper.attach(pio.GPIO26, pio.GPIO14)
s2 = stepper.attach(pio.GPIO12, pio.GPIO13)

-- Move the steppers (10 revolutions), in bucle, changing the
-- direction
while true do
	s1:move(dir * 10)
	s2:move(dir * 10)

	stepper.start(s1,s2)

	if (dir == 1) then
		dir = -1
	else
		dir = 1
	end
end
```