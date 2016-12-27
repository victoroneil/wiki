# About this

This module contains functions for send and receive information through [MQTT] (http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html).

Lua RTOS support for MQTT is build over [Eclipse Paho MQTT] (https://github.com/eclipse/paho.mqtt.c).

# What do you need?

For use MQTT you need an internet connection. You can configure an internet connection in Lua RTOS through [Net module] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Net-module).

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
