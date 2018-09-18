## Supported file systems

Lua RTOS has support for the following file systems:

* RAM file system (RFS):

  RFS is a file system, enterely developed by the Lua RTOS team, in which all the data is stored in RAM, without persistence. This means that all the data stored in the file system is lost on each reboot.

* Little file system (LFS):

  LFS is a file system designed to work with a limited amount of memory, and for systems that may have random power failures. Also implements dynamic wear leveling, to extend the lifetime of the underlying storage. In Lua RTOS, LFS uses the SPI FLASH as the underlying storage.
  
* Spiffs file system (SPIFFS):

  SPIFFS is a file system designed to run on embedded systems, using a small quantity of RAM. Also implements static wear leveling, to extend the lifetime of the underlying storage. In Lua RTOS, LFS uses the SPI FLASH as the underlying storage.

* FAT file system (FAT):

  FAT is a legacy file system, which is simple and robust, and commonly used in a large range of devices. In Lua RTOS, FAT uses an SDCard as the underlying storage.

## Logical file system and mount points

In Lua RTOS, each file system is mounted into a directory within a logical file system. This directory is physically linked to the file system.

When booting, Lua RTOS mounts the root file system at the root directory ("/") automatically. Secondary file systems can be mounted later, in a [startup script](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Startup-scripts), or in the user application. A typical setup could be:

| Mount point | Linked with | Storage   | Notes   
|-------------|-------------|-----------|------------------|
| /           | LFS         | SPI FLASH | Root file system |
| /sd         | FAT         | SDCard    |
| /rfs        | RFS         | RAM       |

The mount point must be a subdirectory of the root directory, so /sd and /rfs are valid mount points, but /other/sd and /other/rfs are invalid mount points.

Any mounted file system can be unmounted at any time. When a file system is unmounted all pending changes are written to the underlying storage device, and then all the used resources are free.

## Path resolution

(under construction)

In Lua RTOS some system calls have as parameter one or more pathnames When one of this system calls is invoked, Lua RTOS starts the path resolution process before using the path pathname. The path resolution process works as follow:

* If the pathname starts with the "/" character (absolute path), the starting lookup directory is the root directory, which is the same for all the threads.

* If the pathname does not start with the "/" character (relative path), the starting lookup directory of the resolution process is the current working directory, which is the same for all the threads.

* For each non-final component of the pathname, where a component is a substring delimited by '/' characters: