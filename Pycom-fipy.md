![](http://git.whitecatboard.org/fipy.png)

**SD Card (MMC interface):**

| Signal | GPIO |
|--------|------|
| CD/DAT3/CS | GPIO13 |
| CLK/SCLK | GPIO14 |
| DAT0/DO | GPIO2 |

**UART:**

| Unit | Signal | GPIO   | Notes |
|------|--------|--------|-------|
| 0    | RX     | GPIO3  | |
|      | TX     | GPIO1  | |
| 1    | RX     | | |
|      | TX     | | |
| 2    | RX     | | |
|      | TX     | | |

**SPI:**

| Unit | Signal | GPIO   | Notes |
|------|--------|--------|-------|
| 2    | MISO   | | |
|      | MOSI   | | |
|      | CLK    | | |
| 3    | MISO   | GPIO19 | |
|      | MOSI   | GPIO27 | |
|      | CLK    | GPIO5  | |

**I2C:**

| Unit | Signal | GPIO   | Notes |
|------|--------|--------|-------|
| 0    | SDA    | GPIO25 | |
|      | SCL    | GPIO26 | |
| 1    | SDA    | | |
|      | SCL    | | |