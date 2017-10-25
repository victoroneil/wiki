# About this

The OTA update mechanism allows a device to update itself based on data received via a network connection while the normal firmware is running.

OTA support in Lua RTOS requires to use an OTA enabled firmware.

# Key concepts

By default latest firmware is obtained from https://ota.whitecatboard.org. You can customize Lua RTOS for change the default server and use your own server through Kconfig under the "Component config -> Lua RTOS -> OTA" category.