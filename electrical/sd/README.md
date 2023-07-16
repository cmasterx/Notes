# Design
How to implement SD Card into a PCB. These design considerations may also apply to **MMC** and **eMMC**.

# Protocol Types
SD cards support **[SPI](#spi)** or **[SDIO](#sdio)** **1 bit**, or **4 bit**.

## SPI
Benefit of **SPI** is easy implementation and is readily available in most **MCU** applications.
Disadvantage with this protocol is slower data transfer than **[SDIO](#sdio)**. Transfer speed may be slightly slower than **1 bit** **SDIO** and significantly slower than **4 bit** **SDIO**.

## SDIO
**SDIO** is a dedicated protocol for SD Cards and MMC. The **SDIO** protocol, unlike **SPI**, allows higher data transfer speed - particularly **4 bit**. Not all **MCU** and applications support **SDIO**, thus this protocol may not be suitable for those scenarios. If support is available, **SDIO** may provide significant functional benefits over **SPI**.

### 1 bit vs. 4 bit
In functional difference, **4 bit** allows higher data transfer speed than **1 bit**. In design considerations, **4 bit** requires 3 additional signal pins to the host device than **1 bit**.

# Design Considerations
## Pull Up Resistors
Pull up resistors are highly recommended for every signal pin on a SD card. Pull up resistors are no required per se, but may result in significant power draw from floating pins [[source](https://www.reddit.com/r/AskElectronics/comments/ek1da3/comment/fd506t2/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)].


# References
- [Design Considerations](https://www.acmesystems.it/pcb_microsd)
