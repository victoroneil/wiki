Lua RTOS supports two types of file systems:

* SPIFFS: is a file system intended for SPI NOR flash devices on embedded targets. This means that the file system can reside on the same memory where firmware is stored without additional hardware.

  SPIFFS is the default file system in Lua RTOS. Please note that NOR flash technology has the following drawbacks, which you should keep in mind when designing your application:

    * 10.000 - 100.000 erase cycles. Don't use SPIFFS if your application needs to do intensive write operations to the file system.
    * Small sizes (<= 16 Mb).

* FAT: is a legacy file system which is simple and robust, and commonly used in a large range of devices.

  In Lua RTOS FAT file system requires an SDCard, and can coexist with SPIFFS.

