UNDER CONSTRUCTION!!

## Step 1: add a new entry to the boards/supported_boards.json file

This file is a JSON file that defines an array of boards supported by Lua RTOS, in which each item contains a JSON object that registers the board into the Whitecat Ecosystem. This object has the following properties:

* description (string): description of the board in natural language.

* manufacturer (string): manufacturer name of the board.

* image (string): valid url that points to an image of the board.

* usb_vid_pid (string): the USB ID of the board's USB 2 Serial adapter. This ID is formed by the concatenation of the VID (Vendor ID) and the PID (Product ID), using the ":" character as separator.

  To get the VID/PID of your board you can use the following command:



* usb_port_exp (string):

