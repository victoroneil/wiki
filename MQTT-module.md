# About this

This module contains functions for send and receive information through [MQTT] (http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html).

Lua RTOS support for MQTT is build over [Eclipse Paho MQTT] (https://github.com/eclipse/paho.mqtt.c).

# What do you need?

For use MQTT you need an internet connection. You can configure an internet connection in Lua RTOS through [Net module] (https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Net-module).

# Key concepts

MQTT (Message Queue Telemetry Transport) is an ISO standard (ISO/IEC PRF 20922) publish-subscribe-based "lightweight" messaging protocol for use on top of the TCP/IP protocol. It is designed for connections with remote locations where a "small code footprint" is required or the network bandwidth is limited.

The publish-subscribe messaging pattern requires a message broker. The broker is responsible for distributing messages to interested clients based on the topic of a message.