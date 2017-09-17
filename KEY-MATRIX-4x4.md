# Specification

| What         |                | Comments                   |
|--------------|----------------|----------------------------|
| Identifier   | KEY_MATRIX_4_4 | ![](http://git.whitecatboard.org/push_button.png) |
| Interface    | 8 GPIO         | GPIO 1: L1<br/>L2<br/>L3<br/>L4<br/>H1<br/>H2<br/>H3<br/>H4<br/><br/>Lx: columns<br/>Hx: rows |
| Provides     | key1<br/>key2<br/>key3<br/>key4<br/>key5<br/>key6<br/>key7<br/>key8<br/>key9<br/>key10<br/>key11<br/>key12<br/>key13<br/>key14<br/>key15<br/>key16<br/>             | 1 = key down<br/>0 = key up|
| Properties   | none           |                            |
| Callbacks?   | yes            | |


# Code

```lua
-- Attach switch to GPIO26
s = sensor.attach("PUSH_SWITCH", pio.GPIO26)

-- Register a callback. Callback is executed when some sensor property changes.
s:callback(
   function(data)
      if (data.on == 1) then
         print("on")
      elseif (data.on == 0) then
         print("off")
      end
   end
)
```