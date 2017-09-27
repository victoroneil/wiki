# About this

This module contains functions for accessing the ESP32 ULP coprocessor. The ULP (Ultra Low Power) coprocessor is a simple FSM which is designed to perform measurements using ADC, temperature sensor, and external I2C sensors, while main processors are in deep sleep mode. ULP coprocessor can access RTC_SLOW_MEM memory region, and registers in RTC_CNTL, RTC_IO, and SARADC peripherals. ULP coprocessor uses fixed-width 32-bit instructions, 32-bit memory addressing, and has 4 general purpose 16-bit registers.

## ulp.load(filename [, load_address])

Load the binary ULP program.

Arguments:

* filename: binary ULP program to load.
* load_address (optional): address to load the binary to (default: 0).

Returns: nothing

```lua
-- Load the ULP program
ulp.load('/examples/ulp/adc-ch4.ulp')
```

## ulp.settimer(tmr1us [, tmr2us, tmr3us, tmr4us])

Set the ULP program timer values. The ULP coprocessor is started by a timer. The timer is started once ulp_run is called. The timer counts a number of RTC_SLOW_CLK ticks (by default, produced by an internal 150kHz RC oscillator). The number of ticks is set for each timer using this function. When starting the ULP for the first time, tmr1us will be used to set the number of timer ticks. Later the ULP program can select another timer register (SENS_ULP_CP_SLEEP_CYCx_REG) using sleep instruction.

Arguments: 

* tmr1us (optional): number of us before firing timer 1
* tmr2us (optional): number of us before firing timer 2
* tmr3us (optional): number of us before firing timer 3
* tmr4us (optional): number of us before firing timer 4

Returns: nothing

```lua
-- Set timer to 100ms
ulp.settimer(100000)
```

## ulp.run([entry_point])

Run the ULP coprocessor program.

Arguments:

* entry_point (optional): entry point to run the binary from (default: 0).

Returns: nothing

```lua
-- Run the ULP coprocessor program
ulp.Run()
```

## ulp.stop()

Stop the ULP coprocessor program.

Arguments: nothing
Returns: nothing

```lua
-- Stop running the ULP coprocessor program
ulp.stop()
```

## ulp.enableadc(channel, [resolution, vref, max value])

Set up an internal ADC channel to be used by the ULP coprocessor.

Arguments:

* channel: ADC channel identifier. Use the constant adc.ADC_CHx for this purpose.
* resolution (optional): resolution to use.
  If resolution is not provided, or it's value is 0 or nil the default resolution is applied.

* vref (optional): positive voltage reference in millivolts.
  If vref is not provided,  or it's value is 0 or nil the default vref is applied.
* max value (optional): max input voltage applied to the channel.
  If max value is not provided, or it's value is 0 or nil the default vref is applied.

Returns: nothing

```lua
-- Enable GPIO32 to be used by the ULP coprocessor
ulp.enableadc(pio.GPIO32)
```

## ulp.valueat(address [, value])

Reads ULP program variable values from the RTC memory or writes new values to ULP program variables in the RTC memory.

Arguments:

* address: the address of the ULP variable as found in the .ld file during building the ULP program binary.
* value (optional): if value is given the content of address is set to this value

Returns:

If value is given then nothing is returned. If value is not given as a parameter then the value of the ULP program variable is returned.

```lua
-- Load the ULP program
ulp.load('/examples/ulp/adc-ch4.ulp')

-- Set the ULP ADC Sample variable ulp_low_thr to 0
ulp.valueat(0x50000070, 0)
-- Set the ULP ADC Sample variable ulp_high_thr to 2000
ulp.valueat(0x50000074, 2000)

-- Run the ULP coprocessor program
ulp.Run()

-- Read the ULP ADC Sample variable ulp_last_result
ulp_last_result = ulp.valueat(0x5000007c)
```

## ulp.assign(address)

Assigns ULP program variables to Lua variables.
This enables easier-to-read Lua code without having to repeat the RTC variable addresses over and over.

Arguments:

address: the address of the ULP variable as found in the .ld file during building the ULP program binary.

Returns: the ulp-variable object

```lua
-- Assign the ULP ADC Sample variable ulp_last_result to the lua variable ulp_last_result
ulp_last_result = ulp.assign(0x5000007c)
```

## ulp:value([value])

Reads the assigned variable's value from the RTC memory or writes a new value to the assigned variable's RTC memory address.

Arguments:

* value (optional): if value is given the content of address is set to this value

Returns:

If value is given then nothing is returned. If value is not given as a parameter then the value of the ULP program variable is returned.

```lua
-- Load the ULP program
ulp.load('/examples/ulp/adc-ch4.ulp')

-- Assign the ULP ADC Sample variable ulp_low_thr to the lua variable ulp_low_thr
ulp_low_thr = ulp.assign(0x50000070)

-- Set the ULP ADC Sample variable ulp_low_thr to 0
ulp_low_thr:value(0)

-- Assign the ULP ADC Sample variable ulp_high_thr to the lua variable ulp_high_thr
ulp_high_thr = ulp.assign(0x50000074)

-- Set the ULP ADC Sample variable ulp_high_thr to 2000
ulp_high_thr:value(2000)

-- Run the ULP coprocessor program
ulp.Run()

-- Assign the ULP ADC Sample variable ulp_last_result to the lua variable ulp_last_result
ulp_last_result = ulp.assign(0x5000007c)

-- Print the RTC memory value at address 0x5000007c
print( ulp_last_result:value() )
```

## ulp:address([address])

Reads the RTC memory address from the Lua variable or sets the Lua variable to a new RTC memory address.

Arguments:

* address (optional): if value is given the Lua variable is set to this address

Returns:

If address is given then nothing is returned. If address is not given as a parameter then the currently assigned RTC memory address is returned.

```lua
-- Print the RTC memory address that ulp_last_result is assigned to
print( ulp_last_result:address() )
```

