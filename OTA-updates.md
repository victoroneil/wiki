# About this

The OTA update mechanism allows a device to update itself based on data received via a network connection while the normal firmware is running.

OTA support in Lua RTOS requires to use an OTA enabled firmware.

# Key concepts

By default the last firmware is obtained from https://ota.whitecatboard.org, and the OTA process is started only if the firmware installed in the board differs from the last published firmware in the OTA server. You can customize Lua RTOS and change the default OTA server to use your own server, this is done through Kconfig under the "Component config -> Lua RTOS -> OTA" category.

For security reasons only OTA servers with SSL enabled are supported.

The url for obtain the last firmware is http://ota.whitecatboard.org/?firmware=FIRMWARE_ID&commit=COMMIT, where:

* FIRMWARE_ID is the firmware id installed in the board, that is formed by [brand-]board type[-board subtype]. Some examples for valid FIRMWARE_ID available in the default OTA server are:

  N1ESP32
  N1ESP32-OTA
  ESP32THING
  ESP32THING-OTA

  You can obtain the information about your board in the following way:

  ```lua
  board_type, board_subtype, brand = os.board()
  ```
* COMMIT is the current commit for the installed firmware in the board.