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

* usb_port_exp (string): it's a valid javascript regular expression used to select the right port when the board's USB 2 Serial adapter is a dual adapter. This happens, for example, in the Espressif Systems ESP-WROVER-KIT board, in which the USB adapter provides a port for JTAG (first port) and other port for Serial (second port). Leave this property empty if the board's USB 2 Serial adapter provides only one port.

* firmwares (JSON array): it's an array of firmware versions available for the board in the Whitecat Ecosystem. For example, Whitecat, usually provide a firmware with OTA enabled and other without OTA enabled. Each firmware is defined with a JSON object that has the following properties:

  * id (string): the firmware id, that must be unique.

  * description (string): description of the firmware in natural language.

  * filesystem (string): 

  ```
      {
          "description": "Generic ESP32 board",
          "manufacturer": "Generic",
          .
          .
          .
      },
      {
          "description": "New board description",
          "manufacturer": "New board manufacturer",
          "image": "http://...../board.png",
          "usb_vid_pid": "1XXX:2XXX",
          "usb_port_exp": "",
          "firmwares": [
              {
                  "id": "NEW-BOARD",
                  "description": "New board description",
                  "filesystem": "default"
              },
              {
                  "id": "NEW-BOARD-OTA",
                  "description": "New board description with OTA",
                  "filesystem": "default"
              }
          ]
      }
  ]
  ```

# Step 2: create the sdkconfig configuration files for each firmware of the new board

  For each firmware provided for the new board a sdkconfig file is required. This files are located into the boards folder within the Lua RTOS root folder. The easy way to create these files are copying the configuration files provided for one board that has similarities with the new one. So, imagine that the candidate board is the GENERIC board.

