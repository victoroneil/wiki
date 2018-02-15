# About this

This module contains functions to control RC servo motors.

# Key concepts

A servo is a rotary actuator, and typically consists of a small electric motor, driving a train of reduction gears, controlled by a control circuit. Historically servos have ben used for radio control and small-scale robotics. 

Radio control servos are connected through a standard three-wire connection:

* power: typically the red wire, that must be connected to a +5V power supply.
* ground: typically the black or brown wire, that must be connected to the board's and power's supply ground.
* signal: typically the yellow, orange or white wire, that must be connected to a board's GPIO.

Never connect the power wire to a GPIO, or your board will be permanently damage.

To use a servo in your program you must do the following:

1. Attach the servo using the servo.attach(..) function. This returns a servo instance that you must store into a variable.

```
-- Attach the servo to GPIO26
s = servo.attach(pio.GPIO26)
```

2. Write values to the servo to move it, using the instance's write function.

```
-- Move the servo to the 45º position
s:write(25)
```