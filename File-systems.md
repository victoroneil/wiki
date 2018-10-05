## Supported file systems

Lua RTOS has support for the following file systems:

* ROM file system (ROMFS):

  ROMFS is a file system, developed by the Lua RTOS team from the scratch, in which all it's data is stored together with the Lua RTOS firmware.

  Although you can use other general-purpose file systems, such as SPIFFS or LFS (and mount them as read-only), the use of ROMFS has the following advantages:

  * There is no wasted space, since in ROMFS each file consists of a single block of data, that has the same size as the file content.
  * As the file system is builded and linked together with the firmware, it can be updated through OTA.
  * Small footprint, and minimal RAM usage (usually 1K per opened file).
  * ESP32 firmwares based on Lua RTOS and Lua scripts are deployed in the same way as firmwares enterely written in C.

* RAM file system (RAMFS):

  RAMFS is a file system, developed by the Lua RTOS team from the scratch, in which all the data is stored in RAM, without persistence. This means that all the data stored in the file system is lost on each reboot.

* Little file system (LFS):

  LFS is a file system designed to work with a limited amount of memory, and for systems that may have random power failures. Also implements dynamic wear leveling, to extend the lifetime of the underlying storage. In Lua RTOS, LFS uses the SPI FLASH as the underlying storage.
  
* Spiffs file system (SPIFFS):

  SPIFFS is a file system designed to run on embedded systems, using a small quantity of RAM. Also implements static wear leveling, to extend the lifetime of the underlying storage. In Lua RTOS, LFS uses the SPI FLASH as the underlying storage.

* FAT file system (FAT):

  FAT is a legacy file system, which is simple and robust, and commonly used in a large range of devices. In Lua RTOS, FAT uses a SDCard as the underlying storage.

In Lua RTOS, the supported file systems have the following characteristics:

* POSIX-compliant
* Thread-safe
* Support for files and directories (even in case of SPIFFS, where directories are emulated)

## Logical file system and mount points

In Lua RTOS, each file system is mounted into a directory (mount point) within a logical file system. The mount point is physically linked to the file system.

When booting, Lua RTOS mounts the root file system at the root directory ("/") automatically. Secondary file systems can be mounted later, in a [startup script](https://github.com/whitecatboard/Lua-RTOS-ESP32/wiki/Startup-scripts), or in the user application. A typical setup could be:

| Mount point | Linked with | Storage   | Notes   
|-------------|-------------|-----------|------------------|
| /           | LFS         | SPI FLASH | Root file system |
| /sd         | FAT         | SDCard    |
| /ram        | RAMFS       | RAM       |

The mount point must be a subdirectory of the root directory, so /sd and /ram are valid mount points, but /other/sd and /other/ram are invalid mount points.

Any mounted file system can be unmounted at any time. When a file system is unmounted, all pending changes are written to the underlying storage device, and then all the used resources are free.

To mount a file system use the Lua _fs.mount(target, file system)_ function:

  * target: is the mount point.
  * file system: is the file system to mount in the mount point, and can be either romfs, ramfs, lfs, spiffs, or fat.

  ```lua
  -- Mount a SD card (FAT file system) on /sd
  fs.mount("sd", "fat")
  ```

To unmount a file system use the Lua _fs.unmount(target)_ function:

  * target: is the mount point.

  ```lua
  -- Unmount a SD card mounted on /sd
  fs.unmount("/sd")
  ```

## Path resolution

In Lua RTOS some system calls have as parameter one or more pathnames. When one of these system calls is used, Lua RTOS starts the path resolution process. The path resolution process works as follow:

* If the pathname starts with the "/" character (absolute path), the starting lookup directory is the root directory, which is the same for all the threads.

* If the pathname does not start with the "/" character (relative path), the starting lookup directory is the current working directory, which is the same for all the threads.

* For each non-final component of the pathname, where a component is a substring delimited by the '/' character:

  - If the component is "." (current directory), the lookup directory remains intact, and go to the next component.
  - If the component is ".." (previous directory), the lookup up directory is set to the previous component, and go to the next component.
  - If the component is not found, an ENOENT error is returned.
  - If the component is found, but is not a directory, an ENOTDIR error is returned.
  - If the component is found, and is a directory, the current lookup directory is set to that directory, and go to the next component.
  - If the component is a mount point, the current lookup directory is set to the root directory of the linked file system.

* For the final component of the pathname:

  - If the component is "." (current directory), the lookup directory remains intact.
  - If the component is ".." (previous directory), the lookup up directory is set to the previous component.
  - If the component is not found, an ENOENT error is returned.
