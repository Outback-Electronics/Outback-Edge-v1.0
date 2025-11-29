# Outback Edge Module Spec  
## FPGA Logic Accelerator / Co-Processor Card  
Version 1.0 – 2025

---

## 1. Purpose  
This module provides a reconfigurable FPGA-based logic and compute accelerator for the Outback Edge platform.  
Primary use cases:

- Custom digital peripherals and protocols  
- High-speed signal processing  
- Parallel computation tasks  
- Prototyping of new hardware features  
- Hardware-accelerated state machines and control logic  

---

## 2. Electrical Interfaces  

### Required  
- **SPI** or **QSPI** – Primary control and configuration interface  
- **GPIO[0..N]** – General-purpose FPGA I/O exposed via M.2  
- **I2C** – EEPROM + module configuration, basic management  
- **GPIO_IRQ** – Interrupt from FPGA to host  
- **MOD_EN** – Module power enable  
- **RST** – FPGA reset signal  
- **CARD_DET** – Card presence detect  

### Optional  
- **Secondary SPI** – For high-speed data streaming separate from configuration interface  
- **Extra GPIO banks** – For additional external I/O  
- **Dedicated clock input** from host (for synchronisation)  

---

## 3. Recommended FPGA Families  

### Low/Medium Density (Low Power)  
- Lattice iCE40UP5K/UP5K+  
- Lattice MachXO3 series  

### Higher Density  
- Lattice ECP5  
- Gowin GW1N / GW2A series  

---

## 4. Power Requirements  

- **3.3V @ 150–400mA** depending on FPGA size and logic utilization  
- On-module regulators generate lower core voltages (1.0–1.2V)  
- Module must draw <10µA when MOD_EN=LOW  

Power modes:  
- **OFF**: MOD_EN=LOW, FPGA unpowered  
- **ON-RESET**: MOD_EN=HIGH, RST asserted, configuration not yet loaded  
- **RUN**: MOD_EN=HIGH, RST released, FPGA configured  

---

## 5. Configuration & Bitstream Handling  

- Primary configuration via **QSPI** or **SPI** from RA6M5  
- Bitstreams stored in on-module Flash  
- Host can:  
  - Trigger reconfiguration  
  - Upload new bitstreams to configuration Flash  
  - Select between multiple bitstream images  

---

## 6. I/O Mapping  

At least 8–16 FPGA I/O pins should be routed to the M.2 connector as generic GPIO lines:  

- **FPGA_IO0..FPGA_IO15** – Bidirectional lines, 3.3V tolerant  
- Pin usage defined per design / per bitstream  

---

## 7. EEPROM Layout  

- Module Type: **FPGA_ACCEL**  
- Vendor ID  
- FPGA model and density  
- Configuration Flash size  
- Bitstream compatibility version  
- Default bitstream ID  

---

## 8. Mechanical  

- M.2-E Key  
- 30mm or 42mm length  
- No external ports required  
- Ensure thermal dissipation (copper pours, vias) for larger FPGAs  

---

## 9. Compliance  

- Must follow OutbackEdge-M2e-Mod-Interface-v1.0  
- Must not expose core voltages to connector  
- All I/O must be 3.3V-tolerant or properly level-shifted  
- Must not exceed defined current limits on 3.3V rail
