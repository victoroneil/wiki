ESP32 has 4 available SPI ports, but one of them are usually used by SPI flash. Default pin map are:

|SPI port| SDI   | SDO   | SCK   | CS   |
|--------|-------|-------|-------|------|
|SPI1    |GPIO7  |GPIO8  |GPIO6  |GPIO11|
|SPI2    |GPIO12 |GPIO13 |GPIO14 |GPIO15|
|SPI3    |GPIO19 |GPIO23 |GPIO18 |GPIO5 |

_Usually SPIO0 is used by SPI flash._