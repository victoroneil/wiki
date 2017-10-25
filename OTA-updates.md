# About this

The OTA update mechanism allows a device to update itself based on data received via a network connection while the normal firmware is running.

OTA support in Lua RTOS requires to use an OTA enabled firmware.

# Key concepts

By default the last firmware is obtained from https://ota.whitecatboard.org, and the OTA process is started only if the firmware installed in the board differs from the last published firmware in the OTA server. You can customize Lua RTOS and change the default OTA server to use your own server, this is done through Kconfig under the "Component config -> Lua RTOS -> OTA" category.

For security reasons only OTA servers with SSL enabled are supported.

The url for obtain the last firmware is http://ota.whitecatboard.org/?firmware=FIRMWARE_ID&commit=COMMIT, that must be posted to the OTA server, where:

* FIRMWARE_ID is the firmware id installed in the board, that is formed by [brand-]board type[-board subtype]. Some examples for valid FIRMWARE_ID available in the default OTA server are:

  * N1ESP32

  * N1ESP32-OTA

  * ESP32THING

  * ESP32THING-OTA

  You can obtain the information about your board in the following way:

  ```lua
  board_type, board_subtype, brand = os.board()
  ```
* COMMIT is the current commit for the installed firmware in the board.

When posting the url http://ota.whitecatboard.org/?firmware=FIRMWARE_ID&commit=COMMIT, the server response with one of the following:

* HTTP 200 response code, when a new firmware is available, meaning that your board has to upgrade.

  In this chase the firmware binary is received after the HTTP headers as an application/octet-stream mime type.

* HTTP 470 response code, when some of the argument values are invalid or are missed.

* HTTP 471 response code, when a new firmware is not available, meaning that your board has the last firmware.

# How to use

For upgrade your board via OTA yo must do the following:

* Setup and start a network connection (WiFi or Ethernet):

```lua
net.wf.setup(net.wf.mode.STA, your ssid, your password)
net.wf.start()
```
* Launch the OTA process

```lua
net.ota()
```