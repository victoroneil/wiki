ESP32 has 3 available SPI ports, but one of them are usually used for SPI flash. Default pin map are:

|SPI port| SDI   | SDO   | SCK   | CS   |
|--------|-------|-------|-------|------|
|SPI0*   |GPIO7  |GPIO8  |GPIO6  |GPIO11|
|SPI1    |GPIO12 |GPIO13 |GPIO14 |GPIO15|
|SPI2    |GPIO19 |GPIO23 |GPIO18 |GPIO5 |

_(*) Usually SPIO0 is used by SPI flash._