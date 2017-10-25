# About this

The OTA update mechanism allows a device to update itself based on data received via a network connection while the normal firmware is running.

OTA support in Lua RTOS requires to use an OTA enabled firmware.

# Key concepts

By default the last firmware is obtained from https://ota.whitecatboard.org, and the OTA process is started only if the current firmware differs from the last firmware. You can customize Lua RTOS and change the default server to use your own server, this is done through Kconfig under the "Component config -> Lua RTOS -> OTA" category.

For security reasons only OTA servers with SSL enabled are supported.
