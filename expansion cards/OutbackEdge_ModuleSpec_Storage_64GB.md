# Outback Edge Module Spec  
## 64GB Solid State Storage Card  
Version 1.0 – 2025

---

## 1. Purpose  
Provides non-volatile high-speed storage for Outback Edge.  
This is MCU-class storage, not SATA/PCIe—implemented using QSPI/OSPI Flash or managed NAND.

---

## 2. Electrical Interfaces  
### Required  
- **QSPI or OSPI** – Primary data interface  
- **I2C** – EEPROM  
- **GPIO_IRQ** (optional for ready/busy)  
- **MOD_EN**  
- **CARD_DET**  

### Optional  
- **SPI** fallback mode  

---

## 3. Storage Architecture Options  
### Option A: Direct QSPI NAND/Flash  
- 64GB via stacked die NAND  
- On-module wear-leveling MCU recommended

### Option B: Managed NAND with SPI Interface  
- Similar to SPI-based eMMC  
- Internal controller handles bad blocks

### Option C: SDIO-based eMMC controller  
- Uses SDIO interface instead of SPI/QSPI  

Preferred: **QSPI/OSPI with small controller MCU**.

---

## 4. Power Requirements  
- **3.3V @ 200mA peak**  
- Must meet standby current < 20µA  

---

## 5. Performance Targets  
- Sequential read: 20–40 MB/s  
- Sequential write: 10–25 MB/s  
- Random read/write depending on controller  

---

## 6. Endurance & Reliability  
- Wear leveling required  
- ECC required (BCH, LDPC, or internal Flash ECC)  
- Optional: onboard capacitor for safe writes  
- SMART-like metadata in EEPROM or exposed via SPI registers  

---

## 7. EEPROM Layout  
- Module Type: **STORAGE_64GB**  
- Vendor ID  
- Storage type (NAND/QSPI/SDIO)  
- Capacity  
- Wear-leveling flags  
- Controller firmware revision  

---

## 8. Mechanical  
- M.2-E Key  
- 30mm length recommended  
- No external ports
