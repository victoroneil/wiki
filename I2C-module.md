# About this

This module contains functions for accessing the CPU's I2C module.

I2C units are encoded into a byte and are platform-dependent. For this reason the I2C module define a numeric constant for each available I2C unit. For example in ESP32 I2C0 is defined by the constant i2c.I2C0. Please refer to your platform or board documentation to know which I2C units are available. If you refer to an inexistent I2C, a nil value is returned.

I2C module can work in master or slave mode, each of then identified by i2c.MASTER and i2C.SLAVE constants. For now only i2c.MASTER is allowed.

The functions of this module are organized in the following categories:

* [Information functions](#information-functions)
* [Configuration functions](#configuration-functions)
* [Operation functions](#operation-functions)