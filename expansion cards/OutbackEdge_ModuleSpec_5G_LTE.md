# Outback Edge Module Spec  
## 5G/LTE Cellular Modem Card  
Version 1.0 – 2025

---

## 1. Purpose  
This module adds LTE or 5G cellular connectivity via USB modem chipsets.  
Designed for IoT uplink, SMS, GNSS, and low-power always-on connectivity.

---

## 2. Electrical Interfaces  
### Required  
- **USB 2.0 (DP/DM)** – Primary modem interface  
- **I2C** – EEPROM + optional management  
- **GPIO_IRQ** – Ring indicator / network event  
- **MOD_EN** – Module power control  
- **RST** – Hardware reset  
- **CARD_DET**  

### Optional  
- **UART** – AT command backup interface  
- **SPI** – GNSS auxiliary communication  

---

## 3. Recommended Chipsets  
- Quectel EC25 / BG95 / BG770A  
- SIMCom A7672 series  
- MeiG SLM790  

These USB-based chipsets are ideal with RA6M5 USB FS.

---

## 4. Power Requirements  
- **5V @ 500mA peak** (burst during transmission)  
- **3.3V @ 100mA** for logic (optional)  
- RF power domains must be isolated on-module.

---

## 5. SIM Support  
Two approaches allowed:  
1. **External Nano-SIM slot on the card**  
2. **eSIM embedded on module**  

SIM interface is internal to the module—no SIM signals exposed to the M.2 slot.

---

## 6. GNSS Support  
If chipset includes GNSS:  
- GNSS output via USB  
- Optional UART NMEA stream  

---

## 7. Antenna  
MHF4 or MHF4L connectors x 1–2 depending on MIMO  
GNSS connector optional.

---

## 8. EEPROM Layout  
- Module Type: **CELLULAR_5G**  
- Vendor / chipset ID  
- WWAN band config  
- GNSS capability flag  
- USB descriptors checksum  

---

## 9. Mechanical  
- M.2-E Key  
- 42mm or 60mm length recommended  
- RF connectors must be accessible
