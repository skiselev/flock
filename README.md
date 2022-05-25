# Flock
Floppy Disk Controller and Real Time Clock for RC2014 compatible systems

## Table of Content
* [Overview](#overview)
  * [Specifications](#specifications)
* [Assembly Instructions](#assembly-instructions)
* [Hardware Documentation](#hardware-documentation)
  * [Schematic and PCB Layout](#schematic-and-pcb-layout)
  * [Input/Output Ports](#inputoutput-ports)
  * [Connectors](#connectors)
  * [Bill of Materials](#bill-of-materials)
* [Release Notes](#release-notes)
  * [Changes](#changes)
  * [Known Issues](#known-issues)
* [Red Tape](#red-tape)
  * [Licensing](#licensing)
  * [Trademarks](#trademarks)

## Overview
Flock is an RC2014*-compatible floppy disk controller (FDC) and real time clock (RTC) module. It designed to work with RomWBW firmware, supporting CP/M, ZSDOS, and various applications under these OSes.

![Flock Assembled Board](images/Flock-Assembled_Board-800px.jpg)

### Specifications
* Floppy Disk Controller: Western Digital* WD37C65 or compatible
  * NEC uPD765 compatible with an integrated data separator and floppy interface drivers and buffers
* Real Time Clock: Maxim Integrated DS1302
* Supported floppy disk formats:
  * 3.5", 720 KB
  * 3.5", 1.44 MB
  * 5.25", 360 KB (in 5.25", 360 KB drives only)
  * 5.25", 1.2 MB
* Bus: RC2014* compatible

## Assembly Instructions

Please refer to [Assembly Instructions](Assembly_Instructions.md) document

## Hardware Documentation

### Schematic and PCB Layout

[Schematic - Version 1.0](KiCad/Z80-FDC-Schematic-1.0.pdf)

[PCB Layout - Version 1.0](KiCad/Z80-FDC-Board-1.0.pdf)

### Input/Output Ports

Flock uses the following I/O ports:

#### 0x48 - FDC CCR/DIR

Write: Floppy disk controller control configuration register (CCR)
Read: Floppy disk controller digital input register (DIR)

#### 0x50 - FDC MSR

Read: Floppy disk controller master status register (MSR)

#### 0x51 - FDC Data Register

Read/Write: Data from/to floppy disk controller

#### 0x58 - FDC DOR / TC

Write: Floppy disk controller digital output register (DOR)
Read: Toggle floppy disk controller transfer complete (TC) line

#### 0xC0 - RTC

Read/Write: Access real time clock (RTC)

### Connectors

#### J1 - Floppy
Connect to floppy drive interface connector.

#### J2 - Floppy 5V
Connect to floppy 5V power supply connector.

**Important: J2 is an unfused 5V power supply for a single 3.5" floppy disk drive. Avoid overloading and short-circuiting**

Pin | Signal Name | Description
--- | ----------- | -----------
1   | 5V          | Positive terminal - +5V
2   | GND         | Negative terminal - ground


#### J3, J4 - RC2014* Bus
Pin   | Signal Name | Description         | Pin  | Signal Name | Description
----- | ----------- | --------------------------------------- | ----- | ----------- | -----------
J3-1  | A15         | Address A15; Output                     |       |             |
J3-2  | A14         | Address A14; Output                     |       |             |
J3-3  | A13         | Address A13; Output                     |       |             |
J3-4  | A12         | Address A12; Output                     |       |             |
J3-5  | A11         | Address A11; Output                     |       |             |
J3-6  | A10         | Address A10; Output                     |       |             |
J3-7  | A9          | Address A9; Output                      |       |             |
J3-8  | A8          | Address A8; Output                      |       |             |
J3-9  | A7          | Address A7; Output                      |       |             |
J3-10 | A6          | Address A6; Output                      |       |             |
J3-11 | A5          | Address A5; Output                      |       |             |
J3-12 | A4          | Address A4; Output                      |       |             |
J3-13 | A3          | Address A3; Output                      |       |             |
J3-14 | A2          | Address A2; Output                      |       |             |
J3-15 | A1          | Address A1; Output                      |       |             |
J3-16 | A0          | Address A0; Output                      |       |             |
J3-17 | GND         | Ground                                  | J4-1  | GND         | Ground
J3-18 | VCC         | Power Supply - +5V                      | J4-2  | VCC         | Power Supply - +5V
J3-19 | /M1         | Machine Cycle One; Output               | J4-3  | /RFSH       | DRAM refresh; Output
J3-20 | /RESET      | Reset; Output                           | J4-4  | N/C         | Not connected
J3-21 | CLK1        | CPU Clock; Output                       | J4-5  | CLK2        | UART Clock (programmable); Output
J3-22 | /INT        | Interrupt; Input                        | J4-6  | /BUSACK     | DMA Bus Acknowledge; Output
J3-23 | /MREQ       | Memory Request; Output                  | J4-7  | /HALT       | Halt; Output
J3-24 | /WR         | Write Request; Output                   | J4-8  | /BUSREQ     | DMA Bus Request; Input
J3-25 | /RD         | Read Request; Output                    | J4-9  | /WAIT       | Wait; Input
J3-26 | /IORQ       | Input/Output Request; Output            | J4-10 | /NMI        | Non-maskable Interrupt; Input
J3-27 | D0          | Data D0; Input/Output                   |       |             |
J3-28 | D1          | Data D1; Input/Output                   |       |             |
J3-29 | D2          | Data D2; Input/Output                   |       |             |
J3-30 | D3          | Data D3; Input/Output                   |       |             |
J3-31 | D4          | Data D4; Input/Output                   |       |             |
J3-32 | D5          | Data D5; Input/Output                   |       |             |
J3-33 | D6          | Data D6; Input/Output                   |       |             |
J3-34 | D7          | Data D7; Input/Output                   |       |             |
J3-35 | TXDA        | Channel A, Transmit Data; Not Connected |       |             | 
J3-36 | RXDA        | Channel A, Receive Data; Not Connected  |       |             | 
J3-37 | USR1        | User Pin 1; Not connected               |       |             |
J3-38 | USR2        | User Pin 2; Not connected               |       |             |
J3-39 | USR3        | User Pin 3; Not connected               |       |             |

### Bill of Materials

#### Version 1.0

[Flock project on Mouser.com](https://www.mouser.com/ProjectManager/ProjectDetail.aspx?AccessID=xxxxxxxxxx) - View and order all components except of the FDC and the PCB.

[Flock project on OSH Park](https://oshpark.com/shared_projects/xxxxxxx) - View and order the PCB.

Flock project on Tindie: [Complete kit](https://www.tindie.com/products/weird/flock-rc2014-compatible-module-kit/); [Flock PCB and an FDC](https://www.tindie.com/products/weird/flock-rc2014-compatible-module-pcb-and-fdc/).

Component type     | Reference | Description                                 | Quantity | Possible sources and notes 
------------------ | --------- | ------------------------------------------- | -------- | --------------------------
PCB                |           | Flock PCB - Version 1.0                     | 1        | Buy from my Tindie store: [Complete kit](https://www.tindie.com/products/weird/flock-rc2014-compatible-module-kit/); [Flock PCB and an FDC](https://www.tindie.com/products/weird/flock-rc2014-compatible-module-pcb-and-fdc/), or order from a PCB manufacturer of your choice using provided Gerber or KiCad files
Integrated Circuit | U1        | WD37C65BJM - FDC, CMOS, 44 pin PLCC         | 1        | eBay
Integrated Circuit | U2        | DS1302+ - RTC, 8 pin DIP                    | 1        | Mouser
Integrated Circuit | U3        | 74HCT174 - Hex D-type flip-flop with reset, 16 pin DIP | 1 | Mouser
Integrated Circuit | U4        | 74HCT138 - 3-Line to 8-Line decoders/demultiplexers, 16 pin DIP| 1 | Mouser
Integrated Circuit | U5        | 74HCT125 - Quadruple bus buffer gates with 3-state outputs, 14 pin DIP | 1 | Mouser
Integrated Circuit | U6        | 74HCT32 - Quadruple 2-input positive-OR gates, 14 pin DIP | 1 | Mouser
Quartz Crystal     | Y1        | 16 MHz, series                              | 1        | Mouser
Quartz Crystal     | Y2        | 32768 Hz, 6 pF                              | 1        | Mouser
Connector          | J1        | 2x17 pin header, shrouded  , 2.54 mm pitch  | 1        | Mouser
Connector          | J2        | 2 pin header with friction lock, right angle | 1       | Mouser
Pin Header         | J3, J4    | 2x40 pin header, 2.54 mm pitch, right angle | 1        | Mouser [517-5121TG](https://www.mouser.com/ProductDetail/517-5121TG), or two [649-77315-118-16LF](https://www.mouser.com/ProductDetail/649-77315-118-16LF) and one [649-77317-104-20LF](https://www.mouser.com/ProductDetail/649-77317-104-20LF)
Capacitor          | C1 - C6   | 0.1 uF, 50V, MLCC, 5 mm pitch               | 6        | Mouser
Capacitor          | C7        | 47 uF, 25V, Electrolytic Polymer, 6.3 mm diameter, 2.5 mm pitch| 1 | Mouser
Capacitor          | C8        | 0.22 F, 5V, Supercapacitor, X mm diameter, 5 mm pitch| 1 | Mouser
Capacitor          | C9        | 47 pF, 50V, MLCC, 5 mm pitch                | 6        | Mouser
Capacitor          | C10       | 15 pF, 50V, MLCC, 5 mm pitch                | 6        | Mouser
Resistor Array     | RN1       | 1 kohm, bussed, 6 pin SIP                   | 1        | Mouser
Resistor           | R1,  R2   | 4.7 kohm, 0.25 W, 1% tolerance, axial       | 2        | Mouser
IC Socket          | U1        | 44 pin PLCC, through hole                   | 1        | Mouser [517-8444-11B1-RK-TP](https://www.mouser.com/ProductDetail/517-8444-11B1-RK-TP)
IC Socket          | U2        | 8 pin DIP                                   | 1        | Mouser [517-4808-3000-CP](https://www.mouser.com/ProductDetail/517-4808-3000-CP)
IC Socket          | U3, U4    | 16 pin DIP                                  | 1        | Mouser [517-4816-3000-CP](https://www.mouser.com/ProductDetail/517-4816-3000-CP)
IC Socket          | U5, U6    | 14 pin DIP                                  | 1        | Mouser [517-4814-3000-CP](https://www.mouser.com/ProductDetail/517-4814-3000-CP)
Connector          | J2        | 2 pin connector                             | 1        |
Connector          | J2        | Floppy disk power connector                 | 1        |

## Release Notes

### Changes

* Version 1.0
  * Initial version

### Known Issues

* Version 1.0
  * No known issues

### Wishlist
* Consider using JST connector for the battery
  * Lower profile than TE latchable connector
  * Ready-made battery holders with JST connectors, such as [Adafruit 4191](https://www.adafruit.com/product/4191) can be used

## Red Tape

### Licensing

Flock is an open source hardware project certified by [Open Source Hardware Association](https://www.oshwa.org/), certification UID is [US00XXXX](https://certification.oshwa.org/us00XXXX.html). The hardware design itself, including schematic and PCB layout design files are licensed under the strongly-reciprocal variant of [CERN Open Hardware Licence version 2](license-cern_ohl_s_v2.txt). The CPLD VHDL code is licensed under [GNU General Public License v3](license-gpl-3.0.txt). Documentation, including this file, is licensed under the [Creative Commons Attribution-ShareAlike 4.0 International License](license-cc-by-sa-4.0.txt).

![CERN-OHL-2.0-S, GPL-3.0, CC-BY-SA-4.0](images/CERN-OHL-2.0-S_GPL-3.0-only_CC-BY-SA-4.0.svg)

### Trademarks

* "RC2014" is a registered trademark of RFC2795 Ltd.
* Other names and brands may be claimed as the property of others.
