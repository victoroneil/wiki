UNDER CONSTRUCTION!!

## Step 1: add a new entry to the boards/boards.json file

This file is a JSON file that defines an array of boards supported by Lua RTOS, in which each item contains a JSON object that registers the board's entry point into the Whitecat Ecosystem. This object has the following properties:

* description (string): a string that contains a description of the board in natural language. This description is used when:

   - Building Lua RTOS from the scratch, to select the board:

     ```
     Please, enter your board type:

      1: Whitecat ESP32N1
      2: Whitecat ESP32N1 with OTA

     34: Generic ESP32 board
     35: Generic ESP32 board with OTA

     Board type: 
     ```

* manufacturer (string):

* type (string):

* subtype (string):

* id (string):

* eol (string):

* filesystem (string):

* usb_vid_pid (string):

* usb_port_exp (string):

* image (string):