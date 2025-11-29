# Outback Edge Module Spec  
## WiFi/Bluetooth Combo Card  
Version 1.0 – 2025

---

## 1. Purpose  
This module provides 2.4GHz/5GHz WiFi and Bluetooth connectivity for the Outback Edge platform using the OutbackEdge-M2e-Mod-Interface-v1.0.  
The card is intended to be the default wireless option for the ecosystem.

---

## 2. Electrical Interfaces  
### Required  
- **SDIO** (Primary WiFi data interface)  
- **I2C** (EEPROM + configuration)  
- **GPIO** (IRQ, optional wake lines)  
- **MOD_EN** (Module enable)  
- **RST** (Module reset)  
- **CARD_DET**  

### Optional  
- **UART** (Bluetooth HCI alternative to SDIO coexistence modes)  
- **USB 2.0** (If module uses USB instead of SDIO; not recommended)  

---

## 3. Recommended Chipsets  
- Infineon CYW43455 / 4373 (SDIO)  
- ESP32-C6 (SPI + UART + BLE + 2.4GHz WiFi)  
- ESP32-S3-MINI (WiFi + BLE via USB or UART/SPI)  

Preferred: **SDIO-based chipset** for direct RA6M5 SDHI integration.

---

## 4. Power Requirements  
- **3.3V @ up to 400mA peak**  
- Optional 1.8V internal regulation allowed  
- Module must present <10µA when MOD_EN=LOW  

---

## 5. Signals Used  
- SDIO_CMD, SDIO_CLK, SDIO_D0..D3  
- I2C_SCL, I2C_SDA  
- GPIO_IRQ  
- GPIO_WAKE (optional)  
- UART_TX/RX (optional)  
- USB_DP/DM (if using USB radio)  

---

## 6. Antenna Options  
- On-board PCB antenna  
- On-board chip antenna  
- External u.FL / MHF4 connector  

External connector recommended for performance.

---

## 7. EEPROM Layout  
- Module Type: **WIFI_BT**  
- Vendor ID  
- Radio chipset ID  
- Calibration data  
- Country/region data  

---

## 8. Mechanical Spec  
- M.2-E Key  
- 30mm length  
- Max height: 2.5mm components on top side  

---

## 9. Compliance  
- Must conform to OutbackEdge-M2e-Mod-Interface-v1.0  
- Must not exceed power budget  
- Must obey radio regulatory requirements
