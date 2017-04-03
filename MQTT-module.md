# About this

This module contains functions for send and receive information through [MQTT] (http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html).

Lua RTOS support for MQTT is build over [Eclipse Paho MQTT] (https://github.com/eclipse/paho.mqtt.c).

# What do you need?

For use MQTT you need an internet connection, and credentials to connect to a MQTT broker. You can configure an internet connection in Lua RTOS through [Net module] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Net-module).

# Key concepts

MQTT (Message Queue Telemetry Transport) is an ISO standard (ISO/IEC PRF 20922) publish-subscribe-based "lightweight" messaging protocol for use on top of the TCP/IP protocol. It is designed for connections with remote locations where a "small code footprint" is required or the network bandwidth is limited.

The publish-subscribe messaging pattern requires a message broker. The broker is responsible for distributing messages to interested clients based on the topic of a message.

# Setup functions

## client = mqtt.client(clientid, host, port, secure)

Creates a new mqtt client instance.

Arguments:

* clientid: client identifier
* host: broker domain name or ip
* port: broker port (tipically 1883)
* secure: true for secure communicacition (not tested), false for non-secure comunication

Returns: a client instance, or an exception. You must store this instance into a variable for further operations with it.

```lua
-- Creates an mqtt instance. Broker domain is xxxx.xx, at port 1883
client = mqtt.client("100", "xxxx.xx", 1883, false)
```

# Operation functions

## instance:connect(username,password)

Connects the client instance to the broker.

Arguments:

* username: user name
* password: password
* Returns: nothing

Returns: nothing, or an exception.

```lua
-- Creates an mqtt instance. Broker domain is xxxx.xx, at port 1883
client = mqtt.client("100", "xxxx.xx", 1883, false)

-- Connect
client:connect("","")
```

## instance:disconnect()

Disconnects the client instance from the broker.

Arguments: nothing
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

## client:publish(topic, payload, qos)

Publish a message to a topic.

Arguments:

* topic: topic name.
* payload: payload, a string with the information to publish packed on it.
* qos: quality of service, according to MQTT specs, can be either mqtt.QOS0, mqtt.QOS1, or mqtt.QOS2

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

* topic: topic name.
* qos: quality of service, according to MQTT specs, can be either mqtt.QOS0, mqtt.QOS1, or mqtt.QOS2
* function: callback function that will be executed when a message is received on topic. This function takes 2 arguments: the message length, and the message.

Returns: nothing or an exception

```lua
-- Creates an mqtt instance. Broker domain is xxxx.xx, at port 1883
client = mqtt.client("100", "xxxx.xx", 1883, false)

-- Connect
client:connect("","")

-- Subscribe to topic
client:subscribe("/100", mqtt.QOS0, function(len, message)
  print("new message received")
  print("message length: "..len)
  print("message: "..message)
end)
```
