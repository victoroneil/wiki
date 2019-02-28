UNDER CONSTRUCTION!!

## Step 1: add a new entry to the boards/supported_boards.json file

This file is a JSON file that defines an array of boards supported by Lua RTOS, in which each item contains a JSON object that registers the board into the Whitecat Ecosystem. This object has the following properties:

* description (string): description of the board in natural language.

* manufacturer (string): manufacturer name of the board.

* image (string): valid url that points to an image of the board. Leave this property empty if no image for the board is available.

* usb_vid_pid (string): the USB ID of the board's USB 2 Serial adapter. This ID is formed by the concatenation of the VID (Vendor ID) and the PID (Product ID), using the ":" character as separator.

  To get the VID:PID of your board you can use the following command:

  ```
  $ python -m serial.tools.list_ports -v
  /dev/cu.Bluetooth-Incoming-Port
      desc: n/a
      hwid: n/a
  /dev/cu.SLAB_USBtoUART
      desc: CP2102N USB to UART Bridge Controller
      hwid: USB VID:PID=10C4:EA60 SER=049bb399844fe811942337fdc2460985 LOCATION=20-1
  2 ports found
  ```

  In the above example the VID:PID is 10C4:EA60. Leave this property empty if the board hasn't a USB 2 Serial adapter.

* usb_port_exp (string): it's a valid javascript regular expression used to select the right port when the board's USB 2 Serial adapter is a dual adapter. This happens, for example, in the Espressif Systems ESP-WROVER-KIT board, in which the USB adapter provides a port for JTAG (first port) and other port Serial (second port).

