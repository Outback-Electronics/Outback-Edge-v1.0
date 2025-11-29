# Outback Edge Module Spec  
## Neural Processing Unit (NPU) Accelerator Card  
Version 1.0 – 2025

---

## 1. Purpose  
Provides on-board AI acceleration for tasks such as:  
- Keyword spotting  
- Sensor analysis  
- TinyML inference  
- Low-power neural networks  

Aimed at offloading compute from the RA6M5 MCU.

---

## 2. Electrical Interfaces  
### Required  
- **SPI** or **QSPI** (Primary command/inference data pipe)  
- **GPIO_IRQ**  
- **I2C** (EEPROM + module control)  
- **MOD_EN**  
- **RST**  
- **CARD_DET**  

---

## 3. Recommended Chip Options  
- Syntiant NDP101 / NDP120  
- Hailo-8L (SPI variants)  
- Himax WE-I Plus  
- Custom FPGA-based micro-NPU  

---

## 4. Power Requirements  
- **3.3V @ 150–300mA**  
- Local regulation to 1.2V/1.1V for NPU core  

---

## 5. On-Module Memory  
- Minimum 2MB SRAM or PSRAM  
- Optional 8–16MB memory for model storage  

---

## 6. Supported Model Types  
Depends on chipset but common:  
- CNN inference  
- Audio keyword spotting  
- Low-resolution vision (optional)  
- ML feature extraction  

---

## 7. EEPROM Layout  
- Module Type: **NPU_AI**  
- Model compatibility flags  
- RAM size  
- Supported data widths  
- Firmware revision  

---

## 8. Mechanical  
- M.2-E  
- 30mm or 42mm card length  
- Minimal external connectors
