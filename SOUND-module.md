# About this

This module contains functions to generate audible tones, attaching a piezo buzzer or a speaker to an output GPIO. The module can be used in two ways:

* **Raw notation**, in which tones are described in terms of their frequency and duration.

* **Musical notation**, in which tones are described in terms of the musical note, note duration, octave, time signature, etc ... 

# Tone generator

Tones are synthesized by the module using a tone generator:

| Generator | Id | Description |
|-----------|----|-------------|
| PWM       | sound.PWM | The tone is synthesized by a PWM hardware module, which generates a square wave with a 50% duty cycle. |
| DAC       | sound.DAC | The tone is synthesized by an I2S / DAC hardware module, which generates a sine wave at a 38 KHz sampling rate.|

# Configuration funcions

## instance = sound.attach(tone_generator, pin)

Attach a tone generator to a piezo buzzer or a speaker.

Arguments:

* **tone_generator:** tone generator used to synthesize the tone.
* **pin:** GPIO where the piezo buzzer or the speaker is attached.

Returns: a sound instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
```

## instance:detach()

Detach the tone generator and free all resources used.

Arguments: none.

Returns: nothing, or an exception.

```lua
```

# Operation functions

## instance:playnote(note, octave)

Play a musical note on the desired octave.

Arguments:

* **note:** a formatted string describing the musical note to play and it's duration.

  - **note name:** the name of the note using the English naming convention.

    | English | German | Latin |
    |---|---|----|
    | A | A | La |
    | B | H | Si |
    | C | C | Do |
    | D | D | Re |
    | E | E | Mi |
    | F | F | Fa |
    | G | G | Sol |

    _Notes in English naming convention, and their correspondence to other naming conventions._

  - **accidental (optional):** can be either **#** to raise the note by a semitone or **b** to lower the note by the same amount.

  - **duration:** 

    | Duration | English | USA | Example |
    |---|-----------|------------|-|
    | 1 | Semibreve | Whole note | ![](http://git.whitecatboard.org/semibrev.gif) |
    | 2 | Minim | Half note | ![](http://git.whitecatboard.org/minim.gif) |
    | 4 | Crotchet | Quarter note | ![](http://git.whitecatboard.org/crotchet.gif |
    | 8 | Quaver | Eighth note | ![](http://git.whitecatboard.org/quaver.gif) |
    | 16 | Semiquaver | Sixteenth note | ![](http://git.whitecatboard.org/semiquav.gif) |
    | 32 | Demisemiquaver | Thirty-second note | ![](http://git.whitecatboard.org/demisemi.gif) |
    | 64 | Hemidemisemiquaver | Sixty-fourth note | ![](http://git.whitecatboard.org/hemidemi.gif) |

* octave: the octave

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
