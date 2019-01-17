# About this

This module contains functions for send and receive information through [MQTT](http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html).

Lua RTOS support for MQTT is build over [Eclipse Paho MQTT](https://github.com/eclipse/paho.mqtt.c).

# What do you need?

For use MQTT you need an internet connection, and credentials to connect to a MQTT broker. You can configure an internet connection in Lua RTOS through [Net module](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Net-module).

# Key concepts

MQTT (Message Queue Telemetry Transport) is an ISO standard (ISO/IEC PRF 20922) publish-subscribe-based "lightweight" messaging protocol for use on top of the TCP/IP protocol. It is designed for connections with remote locations where a "small code footprint" is required or the network bandwidth is limited.

The publish-subscribe messaging pattern requires a message broker. The broker is responsible for distributing messages to interested clients based on the topic of a message.

To use this module you must take into consideration the following:

1. Create a MQTT client instance, and store the instance into a variable.

  ```lua
   client = mqtt.client("100", "xxxx.xx", 1883, false)
   ```

2. Connect to the broker:

   ```lua
   client:connect("","")
   ```

3. Publish to a topic, or subscribe to a topic using client:publish or client:subcribe functions.

4. Disconnect from the broker:

   ```lua
   client:disconnect()
   ```

# Setup functions

## client = mqtt.client(clientid, host, port, secure, [CA file, persistence, persistence path])

Creates a new MQTT client instance.

Arguments:

* clientid: client identifier.
* host: broker domain name or ip.
* port: broker port (typically 1883).
* secure: true for secure communication, false for non-secure communication.
* CA file (optional): path to CA file, used only if secure argument it's true.
* persistence (optional): if true use persistence, if false don't use persistence.
* persistence path (optional): the path to a file system's folder where persistence data will be stored. If the folder doesn't exists it is created the first time.

Returns: a client instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Creates an mqtt instance. Broker domain is xxxx.xx, at port 1883
client = mqtt.client("100", "xxxx.xx", 1883, false)
```

# Operation functions

## instance:connect(username,password,[clean session])

Connects the client instance to the broker.

Arguments:

* username: user name.
* password: password.
* clean session (optional): a boolean that indicates if the session must be cleaned when connected. If true the session is cleaned, and not cleaned if it's false. If not provided, the argument is set to false (no clean the session).

Returns: nothing.

Returns: nothing, or an exception.

```lua
-- Creates an mqtt instance. Broker domain is xxxx.xx, at port 1883
client = mqtt.client("100", "xxxx.xx", 1883, false)

-- Connect
client:connect("","")
```

## instance:disconnect()

Disconnects the client instance from the broker.

Arguments: nothing.
Returns: nothing, or an exception.

```lua
-- Creates an mqtt instance. Broker domain is xxxx.xx, at port 1883
client = mqtt.client("100", "xxxx.xx", 1883, false)

-- Connect
client:connect("","")

...
...

-- Disconnect
client:disconnect()
```

## client:publish(topic, payload, qos, [retained])

Publish a message to a topic.

Arguments:

* topic: topic name.
* payload: payload, a string with the information to publish packed on it.
* qos: quality of service, according to MQTT specs, can be either mqtt.QOS0, mqtt.QOS1, or mqtt.QOS2. To use mqtt.QOS1, or mqtt.QOS2 you must enable the persistence when calling to the mqtt.client function.
* retained (optional): a boolean to set the retained flag for the message. If it's true the retained flag is set, and if it's false the retained flag is clear. If not provided, the default value for this argument is false (not retained).

Returns: nothing or an exception

```lua
-- Creates an mqtt instance. Broker domain is xxxx.xx, at port 1883
client = mqtt.client("100", "xxxx.xx", 1883, false)

-- Connect
client:connect("","")

-- Publish to topic
client:publish("/100", "hello", mqtt.QOS0)
```

## client:subscribe(topic, qos, callback)

Subscribe to a topic.

Arguments:

* topic: topic name. The topic name can contain wildcard characters:

  - A '#' character represents a complete sub-tree of the hierarchy and thus must be the last character in the topic name, such as SENSOR/#. This will match any topic starting with SENSOR/, such as SENSOR/1/TEMP and SENSOR/2/HUMIDITY.

  - A '+' character represents a single level of the hierarchy and is used between delimiters. For example, SENSOR/+/TEMP will match SENSOR/1/TEMP and SENSOR/2/TEMP.

* qos: quality of service, according to MQTT specs, can be either mqtt.QOS0, mqtt.QOS1, or mqtt.QOS2
* callback: callback function, fired when a message is received on topic. This function takes the following arguments:

  * len: the length of the received message (integer).
  * message: the received message (string).
  * topic len: the length of the topic where message has been received (integer).
  * topic name: the name of the topic where message has been received (string).

Returns: nothing or an exception

```lua
-- Creates an mqtt instance. Broker domain is xxxx.xx, at port 1883
client = mqtt.client("100", "xxxx.xx", 1883, false)

-- Connect
client:connect("","")

-- Subscribe to topic
client:subscribe("/100", mqtt.QOS0, function(len, message, topic_len, topic_name)
  print("new message received on topic "..topic_name.." (length: "..topic_len..")")
  print("message length: "..len)
  print("message: "..message)
end)
```
