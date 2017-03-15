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