# About this

This module contains functions to control RC servo motors.

# Key concepts

A servo is a rotary actuator, and typically consists of a small electric motor, driving a train of reduction gears, controlled by a control circuit. Historically servos have ben used for radio control and small-scale robotics. 

Radio control servos are connected through a standard three-wire connection:

* power: typically the red wire, that must be connected to a +5V power supply.
* ground: typically the black or brown wire, that must be connected to the board's and power's supply ground.
* signal: typically the yellow, orange or white wire, that must be connected to a board's GPIO.

Never connect the power wire to a GPIO, or your board will be permanently damage.

