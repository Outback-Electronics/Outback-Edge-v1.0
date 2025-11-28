Outback Edge Board Specification and Layout Plan

A. Official Board Specification (Rev A – Finalized Feature Set)

1. Overview

Outback Edge is the flagship development and application board of the Outback ecosystem. It is built around the Renesas RA6M5 MCU and includes a fully equipped set of peripherals, interfaces, and hardware subsystems with no optional components. Every feature described is standard on the board.


---

2. MCU

Renesas RA6M5 – R7FA6M5AH3CFB#AA0

Arm Cortex-M33 @ 200 MHz

2 MB code flash (dual-bank), 512 KB SRAM

8 KB data flash

TrustZone-M, TRNG, AES/RSA/ECC/DSA hardware crypto

QSPI/OSPI/EBI external memory support

USB FS OTG, Ethernet MAC, CAN, SDHI

ADC 12-bit (22 ch), DAC (2 ch)



---

3. Power System

Primary Input: USB-C (5 V)

Secondary Inputs: JST-PH and barrel jack (5–12 V)

High-efficiency buck regulator to 3.3 V

Li-ion/Li-Po charger

Battery fuel gauge

Over-voltage, reverse-polarity, and ESD protection

Power-good indicators and supervisor IC



---

4. Connectivity

USB-C (USB 2.0 FS OTG; device/host)

10/100 Ethernet PHY with RJ45 and magnetics

CAN bus transceiver

2× UART headers

1× I²C breakout

1× SPI breakout

Qwiic/Stemma QT connector

WiFi/Bluetooth M.2 Key-E slot



---

5. Storage

32 MB QSPI/OSPI external flash

microSD slot (SDHI)

I²C/SPI EEPROM

FRAM for high-endurance persistent data



---

6. User Interface Components

RGB status LED

Reset button

Boot/Mode button

User button

0.96" I²C OLED display

4 capacitive touch pads



---

7. Expansion

Dual 40-pin expansion headers:

GPIO

3V3, GND

UART, I²C, SPI

PWM channels

ADC inputs


Qwiic/Stemma port

Full 10-pin SWD/JTAG header



---

8. Audio System

SSI/I²S audio codec interface

Onboard Class-D amplifier

Onboard speaker footprint



---

9. Mechanical / Form Factor

PCB Size: ~85 × 55 mm

4× M2.5/M3 mounting holes

Clear silkscreen labeling

Underside test pads

Top-side microSD unless routing requires underside



---

10. Security Features

TrustZone isolation

Secure boot enabled

TRNG + crypto accelerator

Tamper detection loop/header

Secure element chip for protected key storage



---

11. Intended Use Cases

Embedded firmware prototyping

Industrial automation

Robotics

Sensor aggregation

IoT gateway

General-purpose prototyping

Reference platform for the Outback ecosystem



---

B. Board Layout Plan (Rev A – Mandatory Features)

1. Top-Side Layout

Left Side

USB-C at upper left

Ethernet RJ45 directly below

microSD slot below RJ45


Top Edge

JST-PH battery header

Barrel jack input

SWD/JTAG header

Reset, Boot, User buttons

RGB LED


Center

RA6M5 MCU

3.3 V power regulation

12/24 MHz crystal

32.768 kHz RTC crystal

External QSPI/OSPI flash

CAN transceiver

Secure element chip

Audio codec


Right Side

Dual 40-pin expansion headers

Qwiic/Stemma QT port

UART/I²C/SPI breakouts


Bottom Edge

Class-D amplifier

Speaker footprint

Capacitive touch pads



---

2. Bottom-Side Layout

Test pads for:

Power rails

SWD

Boot configuration

UART/I²C/SPI

QSPI/OSPI lines


Ground pour for EMI control



---

3. Routing & Design Principles

Minimize trace length for USB, Ethernet, QSPI/OSPI

Differential routing for USB and Ethernet

Separation of analog and digital domains

Strong ESD protection at all external connectors

Star-topology power distribution

Consistent Outback pinout standard on headers

Battery circuitry isolated from switching noise



---

4. Form Factor (Final)

85 × 55 mm Slim-Pi style

Ports on left edge

UI elements on top edge

Expansion on right edge

Bottom reserved for speaker, touch pads, and test points
