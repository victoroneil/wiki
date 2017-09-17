# Specification

| What         |                | Comments                   |
|--------------|----------------|----------------------------|
| Identifier   | KEY_MATRIX_4_4 | ![](http://git.whitecatboard.org/key_matrix_4_4.png) |
| Interface    | 8 GPIO         | GPIO 1: L1<br/>GPIO 2: L2<br/>GPIO 3: L3<br/>GPIO 4: L4<br/>GPIO 5: H1<br/>GPIO 6: H2<br/>GPIO 7: H3<br/>GPIO 8: H4<br/><br/>Lx: columns<br/>Hx: rows |
| Provides     | key1<br/>key2<br/>key3<br/>key4<br/>key5<br/>key6<br/>key7<br/>key8<br/>key9<br/>key10<br/>key11<br/>key12<br/>key13<br/>key14<br/>key15<br/>key16<br/>             | 1 = key down<br/>0 = key up|
| Properties   | repeat           | 1 = enable repeat function, 0 = disable. When enabled this sensor fires a callback when you press and hold a key on the key matrix.                            |
|              | repeat delay     | When you press and hold a key on the key matrix, the sensor fires a callback. The pause between pressing the key and when it starts repeating is the repeat delay, expressed in msecs.<br/><br/>Default value is 1500 msecs.
|              | repeat rate      | After you press and hold down a key on the key matrix, the key starts repeating once the repeat delay expires. The speed at which it repeats is the repeat rate, expressed in msecs.<br/><br/>Default value is 500 msecs.
| Callbacks?   | yes            | |


# Notes

* This sensor requires 8 GPIO. We recommend to use an external GPIO with pull-ups like the PCA9505 chip.
* This sensor performs a scan on the entire key matrix every 1 msec. You can find the operating principle in [this article](http://pcbheaven.com/wikipages/How_Key_Matrices_Works/).
* Hardware pull-ups are not required.
* Many cheap key matrix don't include diodes for each key, so you may experiment ghosting and masking problems if you use these key matrix.
* You can use key matrix with diodes with this sensor.

# Code

```lua
-- Attach the key matrix using an external GPIO chip
km = sensor.attach("KEY_MATRIX_4_4", 40, 41, 42, 43, 44, 45, 46, 47)

km:callback(
   function(data)
      if (data.key1 == 1) then
	     print("key1")
	  end

      if (data.key2 == 1) then
	     print("key2")
	  end

      if (data.key3 == 1) then
	     print("key4")
	  end

      if (data.key4 == 1) then
	     print("key4")
	  end

      if (data.key5 == 1) then
	     print("key5")
	  end

      if (data.key6 == 1) then
	     print("key6")
	  end

      if (data.key7 == 1) then
	     print("key7")
	  end

      if (data.key8 == 1) then
	     print("key8")
	  end

      if (data.key9 == 1) then
	     print("key0")
	  end

      if (data.key10 == 1) then
	     print("key10")
	  end

      if (data.key11 == 1) then
	     print("key11")
	  end

      if (data.key12 == 1) then
	     print("key12")
	  end

      if (data.key13 == 1) then
	     print("key13")
	  end

      if (data.key14 == 1) then
	     print("key14")
	  end

      if (data.key14 == 1) then
	     print("key14")
	  end

      if (data.key16 == 1) then
	     print("key16")
	  end
   end
)
```