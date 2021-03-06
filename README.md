# Build OP-TEE, U-Boot and Linux for RK3229

### Introduction

This documentation details my experience in installing *mainline versions of OP-TEE, U-Boot, Linux and Devuan* on a few devices that are based on Rockchip's RK3229 System-on-Chip.

If you choose to follow this guide, please think for yourself and acknowledge that you take full responsibility for your own actions. If you choose to log an issue, please provide a description of the system you are using for cross-compilation along with the appropriate build logs and a clear explanation of the problem you are experiencing.


### Documentation

- #### Build

     - [Compile OP-TEE, U-Boot and Linux for RK3229](COMPILE.md)


- #### Full Installation

     This approach does not rely on any software that was shipped by the vendor.

     *This will not work for devices that have onboard NAND flash instead of an eMMC, as neither mainline U-Boot nor mainline Linux have support for the Rockchip NAND controller.*

     - [U-Boot + Linux Installation (eMMC)](EMMC-INSTALL.md)
     - [U-Boot + Linux Installation (SD/MMC)](SDMMC-INSTALL.md)


- #### Partition Replacement

     This approach uses the bootloader and Rockchip partitioning scheme shipped by the vendor. I do not pursue this approach since enjoying success via Full Installation. 

     *This will not work for devices that have onboard NAND flash instead of an eMMC, as mainline Linux does not have a driver for the Rockchip NAND controller.*

     - [Onboard Flash Partition Replacement](PARTITION-REPLACEMENT.md)


### Device Findings

- #### Mecer Xtreme Mini S6
    | Procedure                            | Status  | Remarks                       |
    |--------------------------------------|---------|-------------------------------|
    | U-Boot + Linux Installation (eMMC)   | OK      | -                             |
    | U-Boot + Linux Installation (SD/MMC) | OK      | -                             |
    | Onboard Flash Partition Replacement  | OK      | Unresponsive after 30 minutes |


- #### MXQ 4K / MXQ-Pro 4K
    | Procedure                            | Status         | Remarks                                       |
    |--------------------------------------|----------------|-----------------------------------------------|
    | U-Boot + Linux Installation (eMMC)   | Not Applicable | Device does not have an eMMC                  |
    | U-Boot + Linux Installation (SD/MMC) | OK             | -                                             |
    | Onboard Flash Partition Replacement  | Pending        | No kernel driver for Rockchip NAND controller |


### Hardware Support

- #### CPUs
    - All 4 cores brought up via PSCI.

- #### Ethernet
    - 10/100Mbps Full Duplex.

- #### GPU
    - Hardware rendering via lima and mesa.

- #### HDMI
    - Works well if the HDMI connector is forced into the enabled state, and an EDID firmware override is used to compensate for problematic EDID responses from the HDMI sink or for DRM issues.
    - Unfortunately, an unhandled IRQ request message (possibly related to CEC) is generated by the kernel when the display is powered down but does not hinder further use.

- #### MMC
    - Onboard eMMC and SD/MMC cards.

- #### USB
    - Host and OTG modes.

- #### Wireless
    - WLAN provided by a RTL8723BS attached via SDIO works using the r8723bs staging driver, at least for the Mecer Xtreme Mini S6.


### Acknowledgement

Thank you to the following people for their assistance in making this process possible.

- Heiko Stübner, for answers and recommendations
- Fabio Bassa, for testing
