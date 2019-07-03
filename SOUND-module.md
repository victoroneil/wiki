# About this

This module contains functions to generate audible tones, attaching a piezo buzzer or a speaker to an output GPIO. The module can be used in two ways:

* **Raw notation**, in which tones are described in terms of their frequency and duration.

* **Musical notation**, in which tones are described in terms of the musical note, note duration, octave, time signature, etc ... 

# Tone generator

| Generator | Description |
|-----------|-------------|
| PWM       | The tone is synthesized using a square wave with 50% duty cycle |

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
