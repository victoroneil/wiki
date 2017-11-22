**SD Card (MMC interface):**

| Signal | GPIO |
|--------|------|
| CD/DAT3/CS | GPIO21 |
| CMD/DI | GPIO15 |
| CLK/SCLK | GPIO14 |
| DAT0/DO | GPIO2 |
| DAT1/RES | Not used |
| DAT2/RES | Not used |

**UART:**

| Unit | Signal | GPIO   | Notes |
|------|--------|--------|-------|
| 0    | RX     | GPIO3  | |
|      | TX     | GPIO1  | |
| 1    | RX     | GPIO4  | Mapped to UEXT connector |
|      | TX     | GPIO36 | Mapped to UEXT connector |
| 2    | RX     | | |
|      | TX     | | |

**SPI:**

| Unit | Signal | GPIO   | Notes |
|------|--------|--------|-------|
| 2    | MISO   | GPIO15 | Mapped to UEXT connector |
|      | MOSI   | GPIO2  | Mapped to UEXT connector |
|      | CLK    | GPIO14 | Mapped to UEXT connector |
|      | CS     | GPIO17 | Mapped to UEXT connector|
| 3    | MISO   | | |
|      | MOSI   | | |
|      | CLK    | | |
|      | CS     | | |

**I2C:**

| Unit | Signal | GPIO   | Notes |
|------|--------|--------|-------|
| 0    | SDA    | GPIO13 | Mapped to UEXT connector |
|      | SCL    | GPIO16 | Mapped to UEXT connector |
| 1    | SDA    | GPIO13 | |
|      | SCL    | GPIO16 | |
