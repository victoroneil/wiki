
**CAN:**

| Signal | GPIO   |
|--------|--------|
| TX     | GPIO5  |
| RX     | GPIO35 |

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
| CLK/SCLK | GPI14 |
| CMD/DI | GPIO15 |
| DAT0/DO | GPIO2 |

CD and WP signals are not used.

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
