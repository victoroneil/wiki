Lua RTOS has support for the following file systems:

* RAM file system (RFS):

  RFS is a file system, enterely developed by the Lua RTOS team, in which all the data is stored in RAM, without persistence. This means that all the data stored in the file system is lost on each reboot.

* Little file system (LFS):

  LFS is a file system designed to work with a limited amount of memory, and for systems that may have random power failures. Also implements dynamic wear leveling, to extend the lifetime of the underlying storage. In Lua RTOS, LFS uses the SPI FLASH as the underlying storage.
  
* Spiffs file system (SPIFFS):

  SPIFFS is a file system designed to run on embedded systems, using a small quantity of RAM. Also implements static wear leveling, to extend the lifetime of the underlying storage. In Lua RTOS, LFS uses the SPI FLASH as the underlying storage.

* FAT file system (FAT):

  FAT is a legacy file system, which is simple and robust, and commonly used in a large range of devices. In Lua RTOS, FAT uses an SDCard as the underlying storage.

In Lua RTOS, each file system is mounted into a folder of a logical file system. This folder is physically linked to the file system. When booting, Lua RTOS mounts the root file system at the "/" folder automatically. Secondary file systems can be mounted later, in a startup script, or from the user application. A typical setup could be:

| Mount point | Linked with | Storage   | Notes   
|-------------|-------------|-----------|------------------|
| /           | LFS         | SPI FLASH | Root file system |
| /sd         | FAT         | SDCard    |
| /rfs        | RFS         | RAM       |



