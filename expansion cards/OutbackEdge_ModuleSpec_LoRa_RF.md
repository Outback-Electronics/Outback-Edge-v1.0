# Outback Edge Module Spec  
## LoRaWAN / Sub-GHz RF Card  
Version 1.0 – 2025

---

## 1. Purpose  
This module provides long-range, low-power wireless connectivity for the Outback Edge platform using LoRa and/or sub-GHz FSK modulation.

Use cases:

- Remote sensor nodes  
- Agricultural monitoring  
- Long-range environmental telemetry  
- Low-power mesh or star-topology networks  

---

## 2. Electrical Interfaces  

### Required  
- **SPI** – Main control and data interface to radio  
- **GPIO_IRQ** – Radio interrupt line (DIOx)  
- **I2C** – EEPROM + optional configuration / temperature sensor  
- **MOD_EN** – Radio power control  
- **RST** – Hardware reset for radio  
- **CARD_DET**  

### Optional  
- **GPIO_WAKE** – Host wake input from radio  
- Additional GPIOs for multi-DIO pins or RF switches  

---

## 3. Recommended Radio Chipsets  

- Semtech SX1262 / SX1268  
- Semtech SX1302/SX1303 (for gateway-style concentrator)  
- HopeRF modules based on Semtech chipsets  

Frequency bands may include:  
- 433 MHz  
- 868 MHz  
- 915 MHz (Australia/US)  

---

## 4. Power Requirements  

- **3.3V @ 50–200mA** depending on TX power level  
- Sleep current: <5µA target  
- Transmit current: dependent on chipset and PA configuration  

Power states:  
- **OFF**: MOD_EN=LOW, radio fully unpowered  
- **IDLE/SLEEP**: MOD_EN=HIGH, radio in deep-sleep  
- **ACTIVE**: MOD_EN=HIGH, radio in RX/TX  

---

## 5. Antenna  

- External antenna via **u.FL / MHF4** connector  
- Optional dual-band or switchable-band design  
- On-board matching network required for target band(s)  

---

## 6. EEPROM Layout  

- Module Type: **LORA_RF**  
- Vendor ID  
- Region/band configuration (e.g., AU915, EU868, US915)  
- Max TX power level  
- Radio chipset ID  
- Firmware revision (if module has on-board MCU)  

---

## 7. Optional On-Module MCU  

The LoRa card may optionally include an ultra-low-power MCU that:  
- Handles MAC layer (LoRaWAN stack)  
- Exposes a simplified command API over SPI or UART  
- Performs duty-cycle and regulatory management  

In this case, the main RA6M5 treats the module as a high-level modem.

---

## 8. Mechanical  

- M.2-E  
- 30mm card length recommended  
- Antenna connector placed at PCB edge for clearance  

---

## 9. Compliance  

- Must comply with regional RF regulations (ACMA, ETSI, FCC, etc.)  
- Must obey duty-cycle and TX power limits  
- Must follow OutbackEdge-M2e-Mod-Interface-v1.0
