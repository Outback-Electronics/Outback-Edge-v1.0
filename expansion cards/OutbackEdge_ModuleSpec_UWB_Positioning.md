# Outback Edge Module Spec  
## UWB (Ultra-Wideband) Positioning Card  
Version 1.0 – 2025

---

## 1. Purpose  
This module provides ultra-wideband ranging and localization capabilities, allowing precise distance and positioning measurements between nodes.

Use cases:

- Indoor positioning  
- Robot localization  
- Asset tracking  
- Gesture or proximity detection  

---

## 2. Electrical Interfaces  

### Required  
- **SPI** – Main control and data interface  
- **GPIO_IRQ** – UWB radio interrupt line  
- **I2C** – EEPROM + optional sensors (IMU)  
- **MOD_EN**  
- **RST**  
- **CARD_DET**  

### Optional  
- Additional GPIOs for sync / time-stamping / LED indicators  

---

## 3. Recommended Chipsets  

- Qorvo (Decawave) DW3000 series  
- Older DW1000 series (legacy)  

These parts support TWR (two-way ranging), TDOA, and various UWB protocols.

---

## 4. Power Requirements  

- **3.3V @ 120–250mA** during ranging operations  
- Deep-sleep current: <10µA target  
- Local LDOs as required for RF sections  

---

## 5. Antenna  

- External UWB antenna via **u.FL / MHF4**  
- Optionally on-board UWB antenna for compact designs  
- Correct antenna design and clearance required for UWB bands (~6–8 GHz)  

---

## 6. Optional On-Module Sensors  

- 3-axis or 6/9-axis IMU for orientation  
- Exposed over I2C with documented register map  

---

## 7. EEPROM Layout  

- Module Type: **UWB_POS**  
- Vendor ID  
- UWB chipset ID  
- Supported channels  
- Calibrated antenna delays  
- Presence of IMU and its model  

---

## 8. Mechanical  

- M.2-E  
- 30mm card length recommended  
- Antenna connector placed near PCB edge  

---

## 9. Compliance  

- Must adhere to regional UWB regulations  
- Must follow OutbackEdge-M2e-Mod-Interface-v1.0  
- ESD protection for RF connector
