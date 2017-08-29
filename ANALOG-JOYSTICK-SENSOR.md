# Specification

| What         |                 | Comments                   |
|--------------|-----------------|----------------------------|
| Identifier   | ANALOG_JOYSTICK |                            |
| Interface    | 2 ADC<br/>1 GPIO           | ADC 1: X signal<br/>ADC 2: Y signal<br/>GPIO : SW signal (switch) |
| Provides     | x               | -1: right movement<br/>0: no movement<br/>1: left movement         |
|              | y               | -1: up movement<br/>0: no movement<br/>1: down movement         |
|              | sw              | 0: switch released<br/>1: switch pressed        |
| Properties   | none            |                            |
|              |                 | ![](http://git.whitecatboard.org/joystick.png)         |

# Code

```lua
```