**SD Card (MMC interface):**

| Signal | GPIO |
|--------|------|
| CD/DAT3/CS | GPIO13 |
| CMD/DI | GPIO15 |
| CLK/SCLK | GPIO14 |
| DAT0/DO | GPIO2 |
| DAT1/RES | GPIO4 |
| DAT2/RES | GPIO12 |

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
|      | CS     | | |
| 3    | MISO   | GPIO25 | |
|      | MOSI   | GPIO23 | |
|      | CLK    | GPIO19 | |
|      | CS     | | Not assigned |

**I2C:**

| Unit | Signal | GPIO   | Notes |
|------|--------|--------|-------|
| 0    | SDA    | | |
|      | SCL    | | |
| 1    | SDA    | | |
|      | SCL    | | |
