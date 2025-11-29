## A. Official Board Specification (Rev A – Finalized Feature Set)

### 1. Overview
Outback Edge is the flagship development and application board of the Outback ecosystem. It is built around the Renesas RA6M5 MCU and includes a complete, fully populated set of peripherals, interfaces, storage options, security systems, and user interface features. Every subsystem listed is standard hardware on the board.

---

## 2. MCU
- Renesas RA6M5 – R7FA6M5AH3CFB#AA0  
- Arm Cortex-M33 @ 200 MHz  
- 2 MB code flash (dual-bank)  
- 512 KB SRAM  
- 8 KB data flash  
- TrustZone-M security  
- TRNG + AES/RSA/ECC/DSA hardware acceleration  
- QSPI/OSPI/EBI external memory support  
- USB FS OTG, Ethernet MAC, CAN, SDHI  
- 22-channel 12-bit ADC, dual 12-bit DAC  

---

## 3. Power System
- 5 V USB-C input  
- 5–12 V barrel jack input  
- JST-PH interface for Li-ion/Li-Po battery  
- High-efficiency 3.3 V buck regulator  
- Battery charger subsystem  
- Battery fuel gauge chip  
- Full electrical protection (OVP, RPP, ESD)  
- Power-good indicator and supervisor IC  

---

## 4. Connectivity
- USB-C port (USB 2.0 FS OTG)  
- Ethernet 10/100 (PHY + magnetics + RJ45)  
- CAN transceiver  
- 2× UART breakout headers  
- 1× I²C breakout header  
- 1× SPI breakout header  
- Qwiic/Stemma QT connector  
- M.2 Key-E slot for WiFi/Bluetooth modules  

---

## 5. Storage
- 32 MB QSPI/OSPI external flash  
- microSD card slot via SDHI  
- EEPROM  
- FRAM for high-endurance non-volatile storage  

---

## 6. User Interface Components
- RGB status LED  
- Reset button  
- Boot/Mode button  
- User button  
- 0.96" I²C OLED display  
- Four capacitive touch pads (CTSU)  

---

## 7. Expansion
- Dual 40-pin expansion headers with:
  - GPIO  
  - 3V3 and GND  
  - UART, I²C, SPI  
  - PWM channels  
  - ADC inputs  
- Qwiic/Stemma QT port  
- Fully populated 10-pin SWD/JTAG header  

---

## 8. Audio System
- SSI/I²S audio codec interface  
- Onboard Class-D amplifier  
- Speaker footprint on PCB  

---

## 9. Mechanical / Form Factor
- Slim-Pi style PCB: 85 × 55 mm  
- Four mounting holes (M2.5/M3)  
- Full silkscreen labeling for all connectors and pins  
- Test pads accessible from underside  
- microSD slot on top, unless layout requires underside positioning  

---

## 10. Security Features
- TrustZone hardware isolation  
- Secure boot enabled  
- TRNG  
- Hardware crypto accelerators  
- Dedicated tamper-detection loop/header  
- Secure element chip for protected key storage  

---

## 11. Intended Use Cases
Outback Edge is designed for:
- Embedded firmware development  
- Industrial control and automation  
- Robotics and motion-control applications  
- Sensor aggregation and data logging  
- IoT gateways (wired and wireless)  
- General prototyping  
- Serving as the reference design for the Outback ecosystem  

---

# B. Board Layout Plan (Rev A – Mandatory Features)

## 1. Top-Side Layout

### Left Side
- USB-C connector (top-left)  
- Ethernet RJ45 connector directly below  
- microSD slot below RJ45 or slightly offset down the left edge  

### Top Edge
- JST-PH battery header  
- Barrel jack input  
- 10-pin SWD/JTAG header  
- Reset, Boot/Mode, and User buttons  
- RGB status LED  

### Center
- RA6M5 microcontroller (central placement for routing symmetry)  
- 3.3 V power regulation circuitry  
- 12/24 MHz high-speed crystal  
- 32.768 kHz RTC crystal  
- 32 MB QSPI/OSPI flash chip  
- CAN transceiver IC  
- Secure element IC  
- Audio codec IC  

### Right Side
- Dual 40-pin expansion headers (stacked vertically)  
- Qwiic/Stemma QT port above headers  
- Clustered UART/I²C/SPI breakout headers  

### Bottom Edge
- Class-D amplifier  
- Speaker footprint  
- Four capacitive touch pads  

---

## 2. Bottom-Side Layout
- Test pads for:
  - Power rails  
  - SWD signals  
  - Boot configuration  
  - UART/I²C/SPI  
  - QSPI/OSPI memory lines  
- Ground pour for noise control and EMI reduction  
- Additional manufacturing pads as needed  

---

## 3. Routing & Design Principles
- USB, Ethernet, and QSPI/OSPI signals routed with minimal trace length  
- Differential routing for USB and Ethernet  
- Isolation between ADC inputs and noisy switching components  
- Strong ESD protection on all ports  
- Star-topology power distribution for clean rails  
- Consistent Outback ecosystem pinout on all expansion headers  
- Battery subsystem kept electrically isolated from high-noise regions  

---

## 4. Form Factor (Final)
- 85 × 55 mm Slim-Pi layout  
- Ports concentrated on left edge  
- UI and power along top  
- Expansion on right  
- Bottom for speakers, touch pads, and test pads  

---

This document reflects the finalized, fully mandatory hardware configuration for the Outback Edge Rev A board. All subsystems described are included in the standard design.
