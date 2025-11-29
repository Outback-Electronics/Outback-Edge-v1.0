# OutbackEdge-M2e-Mod-Interface-v1.0  
Standard Specification for Modular Expansion Cards

---

## 1. Overview  
The **OutbackEdge-M2e-Mod-Interface** defines a unified electrical, mechanical, and signaling standard for expansion modules that connect to the Outback Edge MCU platform via a single **M.2 Key-E connector (75-pin)**.

This standard allows the Outback Edge to support a wide variety of proprietary modules, including:

- WiFi/Bluetooth cards  
- LTE cellular modems  
- Storage expansion cards  
- Neural processing units (NPU)  
- Embedded GPU / accelerator cards  
- Custom MCU/FPGA-based modules  
- Future module categories  

The standard is **not** electrically compatible with PC/laptop PCIe-based M.2 devices. It only uses the Key-E mechanical format and the 75-pin layout as a flexible, compact connector for MCU-oriented expansion.

---

## 2. Design Goals  
1. **Universal slot** – all module types must fit the same connector and mechanical form.  
2. **Flexible signaling** – cards may use SDIO, USB, SPI, QSPI/OSPI, UART, I2C, and GPIO.  
3. **Forward-compatible** – maintain reserved pins for future accelerators or parallel buses.  
4. **MCU-appropriate** – no PCIe required; low/medium bandwidth interfaces are prioritized.  
5. **Safe power design** – modules must be hard-limited to the rails provided.  

---

## 3. Mechanical Specification

### 3.1 Connector Format  
- M.2 75-pin **Key-E** edge connector  
- Standard 30mm card width  
- Supported card lengths: **30mm, 42mm, 60mm**  
- Single screw mounting at the card tail  
- Standard M.2 standoff height / screw spec

### 3.2 Insertion / Removal  
- Hot-plugging is **not** supported  
- Power must be removed before inserting or removing modules  

---

## 4. Power Delivery

### 4.1 Mandatory Rails  
| Rail | Voltage | Max Current | Notes |
|------|---------|--------------|-------|
| 3.3V | 3.3V | 1.0A (board-level limit) | Primary operating rail |

### 4.2 Optional Rails (Provided if Enabled on Baseboard)  
| Rail | Voltage | Max Current | Notes |
|------|---------|--------------|-------|
| 1.8V | 1.8V | 300mA | Used for low-power radios and sensors |
| 5V   | 5.0V | 500mA | Used for LTE modules or USB-powered devices |
| 3.3V AUX | 3.3V | 50mA | Standby rail for wake functions |

### 4.3 Power Control  
- Dedicated **Module Enable** pin  
- Dedicated **Module Reset** pin  
- Startup sequencing handled by the baseboard  

---

## 5. Signal List and Mapping  
The following signals are provided on the OutbackEdge-M2e-Mod interface.  
All pins not listed are reserved for future expansion.

### 5.1 Universal Low-Speed Signals  
| Signal | Type | Notes |
|--------|------|-------|
| I2C_SCL | I2C | Module configuration, EEPROM, sensors |
| I2C_SDA | I2C | 400kHz / 1MHz supported |
| GPIO0..GPIO5 | GPIO | General-purpose |
| IRQ | Input to Host | Module interrupt line |
| RST | Output from Host | Module reset |
| MOD_EN | Output from Host | Power-enable control |
| CARD_DET | Input to Host | Presence-detect |

---

## 5.2 USB 2.0 Interface  
| Signal | Notes |
|--------|-------|
| USB_DP | Full-speed USB |
| USB_DM | Full-speed USB |

Used primarily by:
- LTE modem modules  
- USB WiFi modules  
- MCU/ESP-based cards with USB interfaces  

---

## 5.3 SDIO Interface  
| Signal | Notes |
|--------|-------|
| SDIO_CMD | Command |
| SDIO_CLK | Clock |
| SDIO_D0..D3 | Data lines |

Used by:
- WiFi/Bluetooth combo modules  
- Storage modules (SDIO-based eMMC or SD controller)  

---

## 5.4 SPI Interface  
| Signal | Notes |
|--------|-------|
| SPI_SCK | Clock |
| SPI_MOSI | Host → Module |
| SPI_MISO | Module → Host |
| SPI_CS0 | Dedicated chip-select |
| SPI_CS1 | Optional chip-select for multi-function cards |

Used by:
- Storage cards  
- NPU/ML accelerators  
- Micro-GPU / FPGA modules  
- Sensor modules  

---

## 5.5 QSPI / OSPI Interface (Optional)  
| Signal | Notes |
|--------|-------|
| QSPI_IO0..IO3 | Data |
| QSPI_CLK | Clock |
| QSPI_CS | Chip-select |

For:
- High-speed Flash expansion  
- Parallel-mode accelerators  
- FPGA bitstreams  
- Future module types  

---

## 6. Module Categories and Required Minimum Interfaces  

### 6.1 WiFi/Bluetooth Module  
- Required: SDIO or USB  
- Optional: UART (HCI)  
- Optional: GPIO (wake lines)

### 6.2 LTE Modem Module  
- Required: USB  
- Optional: I2C for control  
- Optional: GPIO for status lines  

### 6.3 Storage Module  
- Required: SPI or QSPI/OSPI  
- Optional: SDIO  

### 6.4 NPU Module  
- Required: SPI or QSPI  
- Optional: USB (for high-speed NPU chips w/ USB interfaces)  

### 6.5 GPU / Accelerator Module  
- Required: SPI or QSPI  
- Optional: EBI-lite (Reserved pins, future spec)  
- Optional: GPIO for sync/interrupt  

### 6.6 MCU/SoC Module (ESP, RP2040, etc.)  
Flexible; module may choose any combination of:
- USB  
- SPI  
- UART  
- I2C  
- GPIO  

---

## 7. Electrical Constraints  
- Maximum module power draw: **1.5W total** unless otherwise approved  
- Modules must present <10µA leakage when MOD_EN is low  
- No PCIe signals allowed  
- No direct high-voltage (>5V) allowed  

---

## 8. Card Detection  
A single **CARD_DET** pin must be pulled low by the module when installed.  
- Detection occurs on boot  
- Optional hot-detach sensing can be implemented by polling  

---

## 9. Firmware Requirements (Host)  
The Outback Edge firmware must:  
1. Probe I2C for optional module EEPROM  
2. Read module type / capabilities  
3. Configure required bus interfaces  
4. Enable power rails in correct order  
5. Configure IRQ and GPIO lines  
6. Load drivers dynamically (if supported)  

This ensures modules can remain plug-and-play within the ecosystem.

---

## 10. Module EEPROM Standard  
Every module should contain a small I2C EEPROM containing:  
- Vendor ID  
- Module Type Code (WIFI / LTE / STORAGE / NPU / GPU / MCU / OTHER)  
- Supported interfaces  
- Power requirements  
- Firmware version (optional)  
- Serial number or unique ID  

EEPROM Address: **0x50**  

---

## 11. Reserved for Future Expansion  
The following features may be added in later revisions:  
- EBI-lite parallel bus option  
- Differential pairs for high-speed custom accelerators  
- Additional power rails (1.2V, VCORE for AI chips)  
- Native high-speed camera interfaces  

Reserved pins must not be used by modules in v1.0.

---

## 12. Compliance  
A module is compliant if:  
- It fits the mechanical dimensions  
- It adheres to pin assignments  
- It follows power limits  
- It defines an EEPROM with a valid module type  
- It does not drive signals when MOD_EN is low  

---

## 13. Revision History  
**v1.0** – Initial release (2025)  
- Base signal set defined  
- Power rails and enable/reset system established  
- Module categories defined  
- EEPROM metadata defined  
