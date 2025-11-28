# Outback Edge Board Specification and Layout Plan

## A. Official Board Specification (Draft v1.0)

### 1. Overview
Outback Edge is the first development and application board in the Outback ecosystem. It is built around the Renesas RA6M5 MCU and is designed as a general-purpose, secure, network-ready embedded controller.

### 2. MCU
- **Renesas RA6M5 – R7FA6M5AH3CFB#AA0**
- Arm Cortex-M33 @ 200 MHz
- 2 MB code flash (dual-bank), 512 KB SRAM
- 8 KB data flash
- TrustZone-M, TRNG, AES/RSA/ECC/DSA hardware crypto
- QSPI/OSPI/EBI external memory support
- USB FS OTG, Ethernet MAC, CAN, SDHI
- ADC 12-bit (22 ch), DAC (2 ch)

### 3. Power System
- **Primary Input:** USB-C (5 V)
- **Secondary Input:** JST-PH or barrel jack (5–12 V supported via buck)
- **Regulation:** High-efficiency buck to 3.3 V
- Optional Li-ion/Li-Po charger + fuel gauge
- Over-voltage, reverse-polarity, and ESD protection
- Power-good and system-reset supervision

### 4. Connectivity
- USB-C port (USB 2.0 FS OTG; device/host)
- 10/100 Ethernet PHY + RJ45
- CAN transceiver
- 2× UART headers
- 1× I²C breakout
- 1× SPI breakout
- Qwiic/Stemma QT compatible connector
- Optional WiFi/BT M.2 Key-E slot (future)

### 5. Storage
- External QSPI/OSPI flash (8–32 MB)
- microSD card slot (SDHI)
- Optional I²C/SPI EEPROM or FRAM

### 6. User Interface Components
- RGB or tri-color status LED
- Reset button
- Boot/Mode button
- User button
- Optional 0.96" I²C OLED or display connector
- 2–4 capacitive touch pads (CTSU)

### 7. Expansion
- Dual 40-pin expansion headers:
  - GPIO
  - 3V3, GND
  - UART, I²C, SPI
  - PWM channels
  - ADC inputs
- Qwiic/Stemma port
- 10-pin SWD/JTAG header

### 8. Audio (Optional)
- SSI/I²S audio codec header
- Optional Class-D amplifier + speaker

### 9. Mechanical / Form Factor
- PCB Size: TBD (approx. 85×55 mm)
- 4× mounting holes (M2.5/M3)
- Clear silkscreen labeling
- Underside test pads

### 10. Security Features
- TrustZone secure boot
- TRNG + crypto accelerator
- Tamper detection loop/header
- Optional secure element chip

### 11. Intended Use Cases
- Embedded development
- Industrial automation
- Robotics controller
- Sensor hub / data logger
- IoT gateway
- Prototyping platform
- Foundation for the Outback ecosystem

---

## B. Board Layout Plan (Rev A Concept)

### 1. Top-Side Layout

#### Left Side
- USB-C port at top-left
- Ethernet RJ45 below USB-C
- microSD slot below RJ45 or on underside

#### Top Edge
- JST-PH power header
- SWD/JTAG header
- Reset, Boot, User buttons
- RGB LED

#### Center
- RA6M5 MCU
- 3V3 regulator
- 12/24 MHz crystal
- 32 kHz crystal (optional)
- External QSPI/OSPI flash
- CAN transceiver

#### Right Side
- Dual 40-pin expansion headers (vertical stack)
- Qwiic/Stemma connector
- UART/I²C/SPI breakouts

#### Bottom Edge
- Audio header or speaker footprint
- Capacitive touch pads

### 2. Bottom-Side Layout
- Test pads for power rails, SWD, boot mode, and key buses
- Optional microSD slot
- Ground pour for EMC

### 3. Routing & Design Principles
- Keep USB/Ethernet/QSPI paths short
- Separate analog signals from switching nodes
- Star-topology power distribution
- Protect external ports with ESD devices
- Differential routing for USB/Ethernet
- Expansion header pins follow a consistent Outback standard

### 4. Form Factor Options

#### Option A: Slim Pi
- ~85×55 mm
- Ports on left, headers on right

#### Option B: Compact Industrial
- ~70×70 mm
- Ports on two adjacent sides

