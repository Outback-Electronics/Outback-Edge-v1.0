## Overview
Outback Edge is the flagship development and control board of the Outback ecosystem. It’s built around the Renesas RA6M5 MCU and includes a full suite of peripherals, connectivity options, security hardware, and expansion features. Nothing is optional — every subsystem is populated and available on the board.

This platform is designed to be the foundation for future Outback products, firmware stacks, and development tooling.

---

## Key Features

### MCU
- Renesas RA6M5 (R7FA6M5AH3CFB#AA0)
- Arm Cortex-M33 @ 200 MHz
- 2 MB dual-bank flash, 512 KB SRAM, 8 KB data flash
- TrustZone-M and full hardware crypto suite
- USB FS OTG, Ethernet MAC, CAN, SDHI
- 12-bit ADC (22 channels) and dual 12-bit DAC

### Connectivity
- USB-C with OTG support
- Ethernet 10/100 with PHY and magnetics
- CAN bus transceiver
- I²C, SPI, UART breakout headers
- Qwiic/Stemma QT connector
- M.2 Key-E slot for WiFi/Bluetooth modules

### Storage
- 32 MB external QSPI/OSPI flash
- microSD slot (SDHI)
- EEPROM
- FRAM for high-endurance non-volatile storage

### Power System
- USB-C 5 V input
- Barrel jack (5–12 V) input
- JST-PH Li-ion/Li-Po battery input
- Integrated battery charger and fuel gauge
- Over-voltage, reverse-polarity, and ESD protection
- Power-good and system supervisor

### Expansion
- Dual 40-pin expansion headers
- Full 10-pin SWD/JTAG header
- Qwiic/Stemma QT connector

### User Interface
- RGB status LED
- Reset button
- Boot/Mode button
- User button
- 0.96" I²C OLED display
- Four capacitive touch pads

### Audio
- I²S/SSI audio codec interface
- Onboard Class-D amplifier
- Speaker footprint

### Security
- Secure element chip
- TRNG
- Hardware crypto acceleration
- TrustZone partitioning
- Secure boot enabled
- Tamper detection header/loop

---

## Intended Use Cases
Outback Edge is suited for:
- Embedded firmware development
- Industrial automation
- Robotics and motion control
- Sensor aggregation and data logging
- IoT gateway applications (wired + wireless)
- Education and prototyping
- Reference hardware for the Outback ecosystem

---

## Board Layout Summary
- Slim-Pi form factor (85 × 55 mm)
- Ports along left edge (USB-C, Ethernet, microSD)
- Power and buttons along top edge
- Dual expansion headers along right edge
- Bottom side includes speaker footprint, touch pads, and test pads

Full schematics, PCB layout, and BOM will be added once Rev A hardware is finalized.

---

## Firmware
The firmware stack will include:
- Secure bootloader
- HAL layer for RA6M5 peripherals
- Middleware for networking, storage, and UI
- Optional RTOS integration
- Example projects covering:
    - USB device/host
    - Ethernet networking
    - CAN bus
    - Audio playback
    - Capacitive touch
    - External expansion modules

Firmware documentation will be located in `/firmware`.

---

## Directory Structure (Planned)
