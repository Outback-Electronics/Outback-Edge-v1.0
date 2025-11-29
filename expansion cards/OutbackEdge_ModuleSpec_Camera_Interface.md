# Outback Edge Module Spec  
## Camera Interface Card  
Version 1.0 – 2025

---

## 1. Purpose  
This module provides camera input capabilities for the Outback Edge platform, using an on-module bridge (MCU/FPGA or dedicated ISP) to translate sensor data to an interface the RA6M5 can handle.

Use cases:

- Basic computer vision  
- QR/barcode scanning  
- Remote video monitoring (low frame rate)  
- Still image capture  

---

## 2. Electrical Interfaces  

### Required  
- **SPI** or **QSPI** – Control + image data streaming  
- **I2C** – Sensor control, EEPROM, ISP configuration  
- **GPIO_IRQ** – Frame-ready or event interrupt  
- **MOD_EN**  
- **RST**  
- **CARD_DET**  

### Optional  
- **USB** – If camera pipeline uses USB device to host  
- Additional GPIOs for trigger, strobe, or exposure sync  

---

## 3. Architecture Options  

### Option A: Sensor + Bridge MCU  
- Image sensor (e.g., OV2640/OV5640)  
- On-module MCU captures frames and exposes them via SPI/QSPI  

### Option B: Sensor + FPGA  
- FPGA receives parallel camera bus  
- Buffers frames and streams via QSPI or custom protocol  

---

## 4. Power Requirements  

- **3.3V @ 150–300mA** (sensor + MCU/FPGA + regulators)  
- Local regulators for sensor rails (1.2V, 1.8V, 2.8V)  

---

## 5. Camera Capabilities (Typical)  

- Resolution: 640x480 up to 1920x1080 (module dependent)  
- Frame rate: 5–30 fps (depending on bandwidth and mode)  
- Output modes:  
  - Raw frames  
  - Compressed (MJPEG)  
  - Subsampled / low-res preview  

---

## 6. Lens and Connector  

- On-board fixed-focus lens OR  
- Board-to-board socket for camera module (e.g., FFC connector)  

Rolling shutter sensors are acceptable; global shutter optional.

---

## 7. EEPROM Layout  

- Module Type: **CAMERA_IF**  
- Vendor ID  
- Sensor model  
- Max resolution / fps  
- Compression support flags  
- Lens type / FOV info  

---

## 8. Mechanical  

- M.2-E  
- 42mm or 60mm length recommended  
- Camera lens or FFC connector positioned to face case opening  

---

## 9. Compliance  

- Must follow OutbackEdge-M2e-Mod-Interface-v1.0  
- Must isolate noisy switching supplies from sensor if possible  
- ESD protection on any external connectors
