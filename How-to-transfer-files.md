The Lua RTOS & board is supported by the Whitecat Console
See https://github.com/whitecatboard/whitecat-console/

## list files on the esp32
wcc -p /dev/ttyUSB0 -ls /

## upload file to esp32
wcc -p /dev/ttyUSB0 -up /path/to/file-on-pc.lua /path/to/file-on-esp.lua

## download file from esp32
wcc -p /dev/ttyUSB0 -down /path/to/file-on-esp.lua /path/to/file-on-pc.lua

