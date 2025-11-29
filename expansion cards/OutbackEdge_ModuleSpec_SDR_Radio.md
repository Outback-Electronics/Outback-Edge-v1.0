# Outback Edge Module Spec  
## Software-Defined Radio (SDR) Card  
Version 1.0 – 2025

---

## 1. Purpose  
This module provides a flexible radio front-end and digitization stage for software-defined radio applications on the Outback Edge platform.

Use cases:

- Spectrum analysis  
- Protocol sniffing / experimentation  
- Amateur radio experimentation  
- Custom RF modulation/demodulation chains  

---

## 2. Electrical Interfaces  

### Required  
- **SPI** or **QSPI** – Control + data streaming (for low to moderate bandwidth SDR)  
- **I2C** – EEPROM + RF front-end configuration  
- **GPIO_IRQ** – Data-ready / event interrupt  
- **MOD_EN**  
- **RST**  
- **CARD_DET**  

### Optional  
- **High-speed streaming link** (reserved pins for future revisions)  
- Additional GPIOs for band selection, LNAs, PA enable, etc.  

---

## 3. Architecture Options  

### Option A: Direct Conversion SDR Front-End  
- RF tuner IC (e.g., RFFC, SiLabs, or integrated RF IC)  
- High-speed ADC/DAC or codec  
- On-module FPGA or MCU handles decimation and streams downsampled IQ over SPI/QSPI  

### Option B: Low-Bandwidth Narrowband SDR  
- Simple RF frontend + ADC  
- All heavy lifting done on-module, compressed/unmodulated data sent to host  

---

## 4. Frequency Range (Example Target)  

- 70 MHz – 1 GHz baseline  
- Optional versions supporting up to ~6 GHz with appropriate RF ICs  

Exact ranges depend on chosen RF front-end.

---

## 5. Power Requirements  

- **3.3V @ 200–400mA** depending on front-end and digital logic  
- Local regulators required for RF (often 1.2V, 1.8V)  

---

## 6. Antenna and RF Path  

- One or more SMA/u.FL connectors for RF input (and possibly output)  
- On-board filters and LNAs as needed  
- Selectable bands via RF switches (GPIO-controlled)  

---

## 7. Data Rate Considerations  

Given link constraints to RA6M5:  

- Raw IQ bandwidth will be limited (kHz to low MHz ranges typical)  
- Module should implement:  
  - Decimation and filtering  
  - Potential demodulation on-module with only symbols / audio / features sent to host  

---

## 8. EEPROM Layout  

- Module Type: **SDR_RF**  
- Vendor ID  
- RF front-end chipset  
- Frequency range  
- Max sample rate / effective bandwidth  
- Presence/absence of on-board FPGA  

---

## 9. Mechanical  

- M.2-E  
- 42mm or 60mm length recommended for RF layout  
- RF connectors at PCB edge  

---

## 10. Compliance  

- Must follow OutbackEdge-M2e-Mod-Interface-v1.0  
- RF path must include appropriate filtering to avoid illegal emissions  
- ESD protection on RF connectors
