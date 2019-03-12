1. Install ESP32 toolchain for your desktop platform. Please, follow the instructions provided by ESPRESSIF:
   * [Windows](http://esp-idf.readthedocs.io/en/latest/get-started/windows-setup.html)
   * [Mac OS]( http://esp-idf.readthedocs.io/en/latest/get-started/macos-setup.html)
   * [Linux](http://esp-idf.readthedocs.io/en/latest/get-started/linux-setup.html)

1. Clone esp-idf repository from ESPRESSIF:

   ```lua
   git clone --recursive https://github.com/espressif/esp-idf.git
   ```

1. Clone Lua RTOS repository:

   ```lua
   git clone --recursive https://github.com/whitecatboard/Lua-RTOS-ESP32
   ```
   
1. Setup the build environment:
   
   Go to Lua-RTOS-ESP32 folder:
   
   ```lua
   cd Lua-RTOS-ESP32
   ```
   
   Edit the env file and change PATH, IDF_PATH, LIBRARY_PATH, PKG_CONFIG_PATH, CPATH for fit to your installation locations.
   
   Now do:
   
   ```lua
   source ./env
   ```

1. Set the default configuration for your board:

   | Board              | Run this command                                     |
   |--------------------|------------------------------------------------------|
   | WHITECAT ESP32 N1  | make SDKCONFIG_DEFAULTS=WHITECAT-ESP32-N1 defconfig  |
   | ESP32 CORE         | make SDKCONFIG_DEFAULTS=ESP32-CORE-BOARD defconfig   |
   | ESP32 THING        | make SDKCONFIG_DEFAULTS=ESP32-THING defconfig        |
   | GENERIC            | make SDKCONFIG_DEFAULTS=GENERIC defconfig            |

1. Change the default configuration:

   You can change the default configuration doing:
   
   ```lua
   make menuconfig
   ```
   
   Remember to check the device name for your board's USB-TO-SERIAL adapter under the "Serial flasher config / Default serial port" category.
   
1. Compile:

   Build Lua RTOS, and flash it to your ESP32 board:

   ```lua
   make flash
   ```

   Flash the spiffs file system image to your ESP32 board:
   
   ```lua
   make flashfs
   ```
