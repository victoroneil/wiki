# Specification

| What         |                 | Comments                   |
|--------------|-----------------|----------------------------|
| Identifier   | ANALOG_JOYSTICK | ![](http://git.whitecatboard.org/joystick.png)|
| Interface    | 2 ADC<br/>1 GPIO           | ADC 1: X signal<br/>ADC 2: Y signal<br/>GPIO : SW signal (switch) |
| Provides     | x               | -1: left movement<br/>0: no movement<br/>1: right movement         |
|              | y               | -1: up movement<br/>0: no movement<br/>1: down movement         |
|              | sw              | 0: switch released<br/>1: switch pressed        |
| Properties   | none            |                            |
| Callbacks?   | yes             |    |

# Code

```lua
```