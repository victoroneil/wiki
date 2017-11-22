**Ethernet (RMII interface):**

| Signal | GPIO |
|--------|------|
| EMAC_TXD0 | GPIO19 |
| EMAC_TXD1 | GPIO22 |
| EMAC_TX_EN | GPIO21 |
| EMAC_RXD0 | GPIO25 |
| EMAC_RXD1 | GPIO26 |
| EMAC_RX_CRS_DV | GPIO27 |
| CLKIN | GPIO 0 |
| MDC | GPIO23 |
| MDIO | GPIO18 |

PHY is LAN8720 at address 0. Power GPIO is not used.

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
| 3    | MISO   | | |
|      | MOSI   | | |
|      | CLK    | | |
|      | CS     | | |

**I2C:**

| Unit | Signal | GPIO   | Notes |
|------|--------|--------|-------|
| 0    | SDA    | | |
|      | SCL    | | |
| 1    | SDA    | | |
|      | SCL    | | |
