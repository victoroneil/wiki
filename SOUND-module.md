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

## instance:detach()

Detach the tone generator and free all the resources used.

Arguments: none.

Returns: nothing, or an exception.

# Operation functions

## instance:playnote(note, octave)

Play a musical note on the desired octave.

Arguments:

* **note:** a formatted string (**name [accidental] duration**) describing the musical note to play and it's duration.

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

  - **duration:** note duration, relative to a semibreve of 1 time unit.

    | Duration | Time units | English | USA | Spanish | Example |
    |---|-------|----|------------|-|-|
    | 1 | 1 | Semibreve | Whole note | Redonda | ![](http://git.whitecatboard.org/semibrev.gif) |
    | 2 | 1/2 | Minim | Half note | Blanca | ![](http://git.whitecatboard.org/minim.gif) |
    | 4 | 1/4 | Crotchet | Quarter note | Negra | ![](http://git.whitecatboard.org/crotchet.gif) |
    | 8 | 1/8 | Quaver | Eighth note | Corchea | ![](http://git.whitecatboard.org/quaver.gif) |
    | 16 | 1/16 | Semiquaver | Sixteenth note | Semi-corchea | ![](http://git.whitecatboard.org/semiquav.gif) |
    | 32 | 1/32 | Demisemiquaver | Thirty-second note | Fusa | ![](http://git.whitecatboard.org/demisemi.gif) |
    | 64 | 1/64 | Hemidemisemiquaver | Sixty-fourth note | Semi-fusa | ![](http://git.whitecatboard.org/hemidemi.gif) |

    The duration of the note can be increasing by the half of the note duration adding a dot (**.**).

* **octave:** the octave in which the note must be played.

Returns: nothing, or an exception.

## instance:timesignature(upper, lower, bpm)

Set the time signature for the future notes to play. 

Arguments:

* **upper:** upper value of the signature, which specifies how many beats are contained in each bar.

* **lower:** lower value of the signature, which specifies which note duration is equivalent to 1 beat.

* **bpm:** beats per minute.

   | Tempo | bpm |
   |-------|-----|
   | Adagio| 66–76 | 
   | Adagietto | 70–80 |   
   | Andante | 76–108 |
   | Andantino | 80–108 |
   | Marcia moderato | 83–85 |
   | Andante moderato | 92–112 |
   | Moderato | 108–120 |
   | Allegretto | 112–120 |
   | Allegro moderato | 116–120 |
   | Allegro | 120–156 |

   _Some basic tempo markings an their correspondence to bpm._

Returns: nothing, or an exception.

   **Examples:**

   | Example | How to code|
   |---------|-|
   |![](http://git.whitecatboard.org/rhythm1.gif) | instance:timesignature(3,4,120) |
   |![](http://git.whitecatboard.org/timesig2.gif) | instance:timesignature(4,4,120) |
   |![](http://git.whitecatboard.org/timesig5.gif) | instance:timesignature(4,4,120) |

## instance:playsilence(duration)

Play a silence of a specified duration.

Arguments:

  - **duration:** silence duration, relative to a semibreve of 1 time unit.

    | Duration | Time units | English | USA | Spanish | Example |
    |---|-------|----|------------|-|-|
    | 1 | 1 | Semibreve | Whole note | Redonda | ![](http://git.whitecatboard.org/semibrev.gif) |
    | 2 | 1/2 | Minim | Half note | Blanca | ![](http://git.whitecatboard.org/minim.gif) |
    | 4 | 1/4 | Crotchet | Quarter note | Negra | ![](http://git.whitecatboard.org/crotchet.gif) |
    | 8 | 1/8 | Quaver | Eighth note | Corchea | ![](http://git.whitecatboard.org/quaver.gif) |
    | 16 | 1/16 | Semiquaver | Sixteenth note | Semi-corchea | ![](http://git.whitecatboard.org/semiquav.gif) |
    | 32 | 1/32 | Demisemiquaver | Thirty-second note | Fusa | ![](http://git.whitecatboard.org/demisemi.gif) |
    | 64 | 1/64 | Hemidemisemiquaver | Sixty-fourth note | Semi-fusa | ![](http://git.whitecatboard.org/hemidemi.gif) |

    The duration of the silence can be increasing by the half of the note duration adding a dot (**.**).

## instance:playtone(frequency, duration)

Play a tone of a specified frequency an duration.

Arguments:

* **frequency:** the frequency of the tone to play in hertz.

* **duration:** the duration of the tone in milliseconds.

Returns: nothing, or an exception.

```lua
-- Play an audible tone at 440 Hz during 1 second
buzzer = sound.attach(sound.DAC, pio.GPIO26)

buzzer:playtone(440, 1000)
```

# Example

In the following example it is shown how to translate the first 8 bars of the Harry Potter's music sheet.

![](http://git.whitecatboard.org/harry1.png)
![](http://git.whitecatboard.org/harry2.png)

```lua
buzzer = sound.attach(sound.DAC, pio.GPIO26)

buzzer:timesignature(3, 4, 240)

buzzer:playsilence("4")
buzzer:playsilence("4")
buzzer:playnote("B4",   4)
buzzer:playnote("E4.",  5)
buzzer:playnote("G8",   5)
buzzer:playnote("F#4",  5)
buzzer:playnote("E2",   5)
buzzer:playnote("B4",   5)
buzzer:playnote("A2.",  5)
buzzer:playnote("F#2.", 5)
buzzer:playnote("E4.",  5)
buzzer:playnote("G8",   5)
buzzer:playnote("F#4",  5)
buzzer:playnote("D2",   5)
buzzer:playnote("F4",   5)
buzzer:playnote("B2.",  4)
```