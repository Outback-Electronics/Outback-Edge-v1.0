# Outback Edge Module Spec  
## High-Accuracy Timing / GPSDO Card  
Version 1.0 – 2025

---

## 1. Purpose  
This module provides precision timing capabilities using GNSS discipline of a high-stability oscillator (GPSDO-style).

Use cases:

- Time synchronization for networks  
- SDR and RF experimentation  
- Precision data logging  
- Distributed measurement systems  

---

## 2. Electrical Interfaces  

### Required  
- **UART** or **USB** – GNSS data output (NMEA)  
- **GPIO_PPS** – 1PPS pulse from module to host  
- **I2C** – EEPROM + status/control  
- **MOD_EN**  
- **RST**  
- **CARD_DET**  

### Optional  
- **SPI** – Advanced control / status fetch  
- Additional GPIOs for alarms / lock-status LEDs  

---

## 3. Functional Blocks  

- GNSS receiver (GPS/GLONASS/Galileo/BeiDou as available)  
- High-stability oscillator:  
  - TCXO (minimum) or  
  - OCXO (optional)  
- PLL or discipline loop controlling oscillator based on GNSS  

---

## 4. Power Requirements  

- **3.3V @ 150–400mA** depending on oscillator type (OCXO uses more)  
- 5V may optionally be used for OCXO with on-module regulation  
- Sleep mode allowed when GNSS or timing not required  

---

## 5. Timing Outputs  

- **1PPS** output via dedicated GPIO pin to host  
- Optional: reference clock output (e.g., 10 MHz) on M.2 pin or external connector  

Host can:  
- Align system time to 1PPS  
- Log GNSS-derived time  
- Use reference clock for local oscillators or SDR modules  

---

## 6. GNSS Antenna  

- External antenna via **SMA or u.FL** (depending on design)  
- Active antenna support with bias-T optional  

---

## 7. EEPROM Layout  

- Module Type: **TIMING_GPSDO**  
- Vendor ID  
- GNSS chipset ID  
- Oscillator type (TCXO/OCXO)  
- Reference frequency (e.g., 10 MHz)  
- Accuracy and stability parameters  

---

## 8. Mechanical  

- M.2-E  
- 42mm or 60mm length recommended  
- RF connector placed at board edge  

---

## 9. Compliance  

- Must follow OutbackEdge-M2e-Mod-Interface-v1.0  
- GNSS front-end must be well-filtered and protected  
- ESD and surge protection on RF connector
