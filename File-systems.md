Lua RTOS has support for the following file systems:

* RAM file system (RFS):

  RFS is a file system enterely developed by the Whitecat Team, in which all the data is stored in RAM, without persistence. This means that all the data stored in the file system is lost on each reboot.

  [Project repository](https://github.com/whitecatboard/Lua-RTOS-ESP32/tree/master/components/ramfs)

* Little file system (LFS):

  LFS is a file system designed to work with a limited amount of memory, and for systems that may have random power failures. Also implements dynamic wear leveling, to extend the lifetime of the underlying storage (SPI FLASH).
  
  [Project repository](https://github.com/ARMmbed/littlefs)  
  
* Spiffs file system (SPIFFS):

  SPIFFS is a file system designed to run on embedded systems, usinng a small quantity of RAM. Also implements static wear leveling, to extend the lifetime of the underlying storage (SPI FLASH).

  [Project repository](https://github.com/pellepl/spiffs)  

* FAT file system (FAT): is a legacy file system which is simple and robust, and commonly used in a large range of devices.

  FAT is a legacy file system which is simple and robust, and commonly used in a large range of devices. In Lua RTOS, FAT uses an SDCard as the underlying storage.

