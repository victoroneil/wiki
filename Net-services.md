# About this

This module contains the network services provided by Lua RTOS.

# HTTP server

Lua RTOS can serve content to network clients via the HTTP protocol.

## net.service.http.start()

Starts the HTTP service.

## net.service.http.stop()

Ends the HTTP service.

# Captive DNS

Captive DNS is not a DNS server that provides real DNS information.
It is used to trick clients into going to the RTOS' soft-AP IP no matter what http URL the client was about to open. Having the Captive DNS activated an Android client connected to the Lua RTOS soft-AP will automatically open the captive-login screen which can be customized on the SPIFFS to be used e.g. as configuration screen.

## net.service.captivedns.start()

Starts the Captive DNS service.

## net.service.captivedns.stop()

Ends the Captive DNS service.

