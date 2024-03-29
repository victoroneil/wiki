# About this

This module contains functions for access the [sensors supported by Lua RTOS](#supported-sensors)
. Although with Lua RTOS you can access sensors using the provided hardware access modules, mostly used sensors in education and industry are supported directly by the operating system. Please feel free to send us any suggestion for include new sensors in Lua RTOS.

Sensor module allows the programmer to access sensors in an unified way from a common programming interface, programs are written faster, and source code is more clearly:

```lua
-- Attach a DHT11 sensor connected to GPIO4
s1 = sensor.attach("DHT11", pio.GPIO4)

-- Read temperature and humidity
s1:read("temperature")
s1:read("humidity")
```

By default all sensors are included in the Lua RTOS firmware. You can select the sensors to include in Lua RTOS build through Kconfig under the Component config -> Lua RTOS -> Hardware -> Sensors category.

The functions of this module are organized in the following categories:

* [Enumeration functions](#enumeration-functions)
* [Configuration functions](#configuration-functions)
* [Read functions](#read-functions)
* [Set functions](#set-functions)

# Key concepts

A sensor is a device that measures some type of magnitude from the physical environment, and generates an output signal  that can be process by other devices. The magnitude could be temperature, humidity, motion, sound, a switch status, etc.

To use a sensor in your program you must do the following:

1. Attach the sensor to it's hardware interface, using the sensor.attach(..) function. This returns a sensor instance that you must store into a variable.

   ```lua
   -- Attach a DHT11 sensor connected to GPIO4
   s1 = sensor.attach("DHT11", pio.GPIO4)
   ````

1. Use the sensor instance for read data provided by the sensor:

   ```lua
   -- Read data provided by sensor
   s1:read("temperature")
   s1:read("humidity")
   ```
1. Detach the sensor instance when it is no longer necessary:

   ```lua
    s1:detach()
   ```

In some cases you need to configure your sensor, for example, set the measure resolution, set an alarm, etc. Sensor configuration are made using the set function:

```lua
-- Instantiate a DS1820 sensor connected to GPIO4
s1 = sensor.attach("DS1820", pio.GPIO4, 0x28ff900f, 0xb316041a)

-- Configure sensor resolution
s1:set("resolution", 10)

-- Read temperature
s1:read("temperature")
````

# Enumeration functions

Enumeration functions allows you to know which sensors are supported by your Lua RTOS firmware. Remember that through Kconfig options you can build your own firmware with the sensors that you need for your project.

These functions are usually used by the Whitecat IDE in order to know which sensors are supported by your board, but in some cases they will be useful for you.
 
## sensor.list([table])

List the sensors supported by your Lua RTOS firmware.

Arguments:

* table: if true, sensor's list is returned in a Lua table, if false sensor's list is printed on the console.

Returns:

* if table is false: nothing or an exception.

* if table is true: a Lua table with the sensor's list result, or an exception. This table is an array of tables. Each entry corresponds to a sensor. Each sensor gives the following fields:

  * id: the sensor's id.
  * interface: the sensor's interface name.

  * provides: an array with magnitudes provided by the sensor. Each magnitude have the following fields:
    * id: name of the magnitude.
    * type: data type of the magnitude. Can be either int, float or double.

  * settings: an array with setting parameters supported by the sensor. Each setting have the following fields:
    * id: name of the setting.
    * type: data type of the magnitude. Can be either int, float or double.

```lua
-- List the sensors supported by the Lua RTOS firmware on the console
/ > sensor.list()
SENSOR      INTERFACE   PROVIDES                    SETTINGS                   
-------------------------------------------------------------------------------
DHT11       GPIO        temperature,humidity        
PING28015   GPIO        distance                    temperature
TMP36       ADC         temperature                 
```

```lua
-- List the sensors supported by the Lua RTOS firmware to a table
sensors = sensor.list(true)
```

## sensor.enumerate(type, interface, [table])

In some cases, such as the 1-WIRE interface, sensors present in the 1-WIRE bus can be enumerated. Using the enumerate function allow you to known which sensors are present in the bus, and know for example, the sensor address needed for the attach function.

Arguments:

* type: enumeration type. For now only sensor.OWire are allowed.
* interface: the interface to enumerate. For now, a valid gpio.
* table: if true, enumeration list is returned in a Lua table, if false enumeration list is printed on the console.

Returns:

* if table is false: nothing or an exception.

* if table is true: a Lua table with the enumeration list result, or an exception. This table is an array of tables. Each entry corresponds to a sensor. Each sensor gives the following fields for 1-WIRE:

  * id: the sensor's id.
  * device: device number in the bus.
  * addressh: the most significant word device address.
  * addressl: the less significant word device address.
  * model: a string containing the device's model name.

```lua
-- Enumerate the sensors connected to GPIO4 using 1-WIRE bus
/ > sensor.enumerate(sensor.OWire, pio.GPIO4)
SENSOR      DEVICE   ADDRESS             MODEL         
-------------------------------------------------------
DS1820      01       28ff900fb316041a    DS18B20
DS1820      02       28ffc1acb2160596    DS18B20
DS1820      03       28fff919b316034a    DS18B20
DS1820      04       28ffad17b31603d5    DS18B20
```

```lua
-- Enumerate the sensors connected to GPIO4 using 1-WIRE bus to a table
owire = sensor.enumerate(sensor.OWire, pio.GPIO4, true)
```

# Configuration functions

## s = sensor.attach(id, ...)

Attach a sensor to it's hardware interface.

Arguments:

The arguments for this function varies according to the hardware interface type.

   For GPIO:

   * id: a string containing the sensor id, for example DHT11.
   * gpio: the GPIO which sensor is attached. Use pio.GPIOx defined for this purpose.

   For ADC:

   * id: a string containing the sensor id, for example TMP36.
   * adc: ADC unit. Use adc.xxx defined for this purpose, for example adc.ADC1.
   * channel: ADC channel.

   For UART:

   * id: a string containing the sensor id, for example GPS.
   * uart: UART unit identifier. Use uart.UARTx defined for this purpose.
   * baud rate (optional): desired baud rate, expressed in bauds. If not provided, the baud rate is set to 9600.
   * data bits (optional): number of data bits, can be 8 or 9. If not provided, the data bits are set to 8.
   * parity (optional): parity, can be either uart.PARNONE (none parity), uart.PAREVEN (even parity) or uart.PARODD (odd parity). If not provided, the parity is set to uart.PARNONE.
   * stop bits (optional): number of stop bits, can be either uart.STOP1 (1 stop bits) or uart.STOP2 (2 stop bits). If not provided, the stop bits are set to uart.STOP1.

   For I2C:

   * id: a string containing the sensor id, for example BME280.
   * i2c: i2c unit. Use i2c.I2Cx defined for this purpose.
   * address: i2c device address. If 0 the default device address is applied.

   For 1-WIRE:

   * id: a string containing the sensor id, for example DS1820.
   * gpio: the GPIO which sensor is attached. Use pio.GPIOx defined for this purpose.
   * position: the device position that the device occupies in the bus

Returns: a sensor instance or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Attach a DHT11 (gpio sensor) sensor to GPIO4
s = sensor.attach("DHT11", pio.GPIO4)
```

```lua
-- Attach a TMP36 (adc sensor) sensor using ADC1 module, channel 6
s = sensor.attach("TMP36", adc.ADC1)
```

```lua
-- Attach a DS1820 (1-WIRE sensor) sensor to GPIO26 at position 3 
s = sensor.attach("DS1820",pio.GPIO26, 3)
```

## instance:detach()

Detach the sensor and free all resources used by the sensor.

Arguments: none.

Returns: nothing, or an exception.

## instance:callback(function)

Registers a callback for a sensor instance previously created with the sensor.attach function. The callback function is executed when a new value is available from the sensor (now only for driven interrupt sensors). Programmer can register up to 4 callbacks for sensor instance.

Callbacks allow programmers to program alarm functions in an easy and clear way. Example: do something when a hall effect switch is "on".

Arguments:

* function: the callback function. This function has only 1 argument, where a table with all the magnitude values provided by the sensor is passed. You can use an [enumeration function](#enumeration-functions) for know what magnitudes are provided by a sensor.

Returns: nothing, or an exception.

```lua
-- Attach a hall switch to GPIO26
s = sensor.attach("HALL_SWITCH", pio.GPIO26)

-- Register a callback
s:callback(
   function(magnitude)
      if (magnitude["on"] == 1) then
         print("on")
      else
         print("off")
      end
   end
)
```

# Read functions

## instance:read(magnitude)

Reads a specified magnitude from a sensor instance previously created with the sensor.attach function.

Arguments:

* magnitude: the magnitude name to read. You can use an [enumeration function](#enumeration-functions) for know what magnitudes are provided by a sensor. The special magnitude "all" is defined for read all the magnitudes provided by the sensor.

Returns: the magnitude value or an exception.

```lua
-- Attach BME280 to I2C0, with default values
s1 = sensor.attach("BME280", i2c.I2C0)

-- Read temperature
temp = s1:read("temperature")

-- Read pressure
press = s1:read("pressure")

-- Read all properties
temp, hum, press = s1:read("all")
```

# Set functions

## instance:set(property, value)

Sets the value for a specified property for a sensor instance previously created with the sensor.attach function. With the set function you can set the resolution you want for a DS1820 sensor.

Arguments:

* property: the property name to set. You can use an [enumeration function](#enumeration-functions) for know what properties are provided by a sensor.

* value: the property value.

```lua
-- Attach the second DS1820 sensor connected to GPIO26
s1 = sensor.attach("DS1820", pio.GPIO26, 2)

-- Set resolution to 8 bits
s1:set("resolution", 8)

-- Read the temperature
s1:read("temperature")
```

# Supported sensors

Here is the list of sensors currently natively supported in Lua RTOS.

  | Type                     | Sensor                                                             |
  |--------------------------|--------------------------------------------------------------------|
  | Air Quality  |[SDS011](./SDS011-NOVA-PM-SENSOR) |
  | Distance     |[2Y0A21](./2Y0A21-SENSOR)<br/>[PING))) 28015 ultrasonic sensor](./PING-28015-ultrasonic-sensor)<br/>[US015 ultrasonic sensor](./US015-ultrasonic-sensor)|
  | Geographic position | [GPS](./GPS-SENSOR) |
  | Humidity | [BME280](./BME280-SENSOR)<br/>[DHT11](./DHT11-SENSOR)<br/>[DHT22](./DHT22-SENSOR)<br/>[DHT23](./DH23-SENSOR) |
  | Illuminance | [BH1620FVC](./BH1620FVC-SENSOR)<br/>[BH1721FVC](./BH1721FVC-SENSOR)<br/>[LDR](./LDR-SENSOR)|
  | Magnetic field | [AH49E](./AH49E-LINEAR-HALL-EFFECT-SENSOR)|
  | Moisture | [VH400](./VH400-soil-moisture-sensor) |
  | Potentiometers | [Linear potentiometer](./LINEAR-POT-SENSOR)|
  | Presence | [AM412](./AM412-PIR-SENSOR)|
  | Pressure | [BME280](./BME280-SENSOR)|
  | Rotation | [Relative rotary encoder](./Relative-Rotary-Encoder-SENSOR)|
  | Switches | [4x4 key matrix](./KEY-MATRIX-4x4)<br/>[2 POSITION TOGGLE SWITCH](./2-POSITION-TOGGLE-SWITCH)<br/>[3 POSITION TOGGLE SWITCH](./3-POSITION-TOGGLE-SWITCH)<br/>[ANALOG JOYSTICK](./ANALOG-JOYSTICK-SENSOR)<br/>[HALL EFECT](./HALL-EFFECT-SWITCH-SENSOR)<br/>[PUSH SWITCH](./PUSH-SWITCH-SENSOR)<br/>[TILT SWITCH](./TILT-SWITCH)|
  | Temperature | [BDE0600G](./BDE0600G-SENSOR)<br/>[BME280](./BME280-SENSOR)<br/>[DHT11](./DHT11-SENSOR)<br/>[DHT22](./DHT22-SENSOR)<br/>[DHT23](./DH23-SENSOR)<br/>[DS1820](./DS1820-SENSOR)<br/>[LM35](./LM35-SENSOR)<br/>[10K THERMISTOR](./10K-THERMISTOR-SENSOR)<br/>[TMP36](./TMP36-SENSOR)
  | UV | [GUVA-S12SD](./GUVA-S12SD-SENSOR)<br/>[ML8511](./ML8511-SENSOR)|
