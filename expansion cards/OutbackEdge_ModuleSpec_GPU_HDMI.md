# Outback Edge Module Spec  
## Micro-GPU / Video Output Card with HDMI  
Version 1.0 – 2025

---

## 1. Purpose  
This module provides hardware-assisted video output (HDMI) for Outback Edge using a dedicated micro-GPU or FPGA-based video pipeline.  
Designed for UI displays, digital signage, dashboards, and embedded screens.

---

## 2. Electrical Interfaces  
### Required  
- **SPI** (Main command + framebuffer stream)  
- **GPIO_IRQ**  
- **I2C** (Display EDID, module config)  
- **MOD_EN / RST / CARD_DET**  

### Optional  
- **QSPI** – For higher throughput framebuffer  
- **USB** – For firmware updates or module-specific debugging  

---

## 3. Recommended Architectures  
### Option A: FPGA-Based GPU  
- Lattice ECP5 or iCE40UP5K  
- HDMI serializer (ADV7513 or TFP410)

### Option B: MCU + HDMI Encoder  
- RP2040 + external HDMI encoder  
- Highly cost-effective, good for UI elements

### Option C: Dedicated 2D Accelerator  
- BT815/BT816 (EVE series)  
- Built-in graphics engine + touch support

---

## 4. Power Requirements  
- **3.3V @ 300–450mA**  
- HDMI transmitter may require **1.8V internal** generated on-module  

---

## 5. HDMI Support  
- **720p60 minimum**  
- Optional: 1080p30/60 depending on module capability  
- EDID read via I2C  

---

## 6. On-Module Memory  
Minimum:  
- 8MB PSRAM (framebuffer)  
Recommended:  
- 16–32MB for larger resolutions

---

## 7. EEPROM Layout  
- Module Type: **GPU_HDMI**  
- Resolution capability flags  
- Framebuffer size  
- Firmware revision  

---

## 8. Mechanical  
- M.2-E Key  
- 42mm or 60mm length (HDMI connector clearance)  
- Side-exit micro-HDMI preferred
