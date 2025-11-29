# Outback Edge Module Spec  
## Audio DSP / Codec Card  
Version 1.0 – 2025

---

## 1. Purpose  
This module provides high-quality audio input/output and optional DSP processing for the Outback Edge platform.

Use cases:

- Voice interfaces  
- Audio playback/recording  
- Acoustic sensing and beamforming  
- Signal processing / filtering  

---

## 2. Electrical Interfaces  

### Required  
- **I2S/SSI** – Primary digital audio interface (from RA6M5 SSI)  
- **I2C** – Codec/DSP control, EEPROM  
- **MOD_EN** – Power enable  
- **RST** – Codec/DSP reset  
- **CARD_DET**  

### Optional  
- **GPIO_IRQ** – For DSP events, buffer notifications  
- **SPI** – For advanced DSP control or firmware updates  

---

## 3. Functional Blocks  

The card may include:

- Stereo or multi-channel **audio codec**  
- Integrated or external **headphone amplifier**  
- One or more **microphone inputs** (analog and/or digital MEMS)  
- Optional **DSP core** for:  
  - Echo cancellation  
  - Noise reduction  
  - Beamforming  
  - Equalization and filters  

---

## 4. Recommended Components  

### Audio Codec Examples  
- TI TLV320AIC32x series  
- NXP SGTL5000  
- Cirrus Logic CS42xx series  

### DSP Examples  
- Analog Devices ADAU17xx SigmaDSP  
- On-chip DSP in some codecs  

---

## 5. Power Requirements  

- **3.3V @ 100–250mA** depending on amplifiers and number of channels  
- Local LDOs for analog rails (e.g., 3.3V analog, 1.8V)  
- Must support low-power mode with audio path disabled  

---

## 6. Audio Connectivity  

Typical options:  

- 3.5mm TRRS or TRS jack(s) for:  
  - Headphones  
  - Line-out  
  - Mic-in  

- On-board digital MEMS microphones (PDM or I2S)  

Signal options:  
- Stereo out (L/R)  
- Mono or stereo mic in  

---

## 7. EEPROM Layout  

- Module Type: **AUDIO_DSP**  
- Vendor ID  
- Codec type  
- Number of channels  
- Supported sample rates  
- DSP features flags (AEC, NR, EQ, etc.)  

---

## 8. Mechanical  

- M.2-E  
- 42mm length recommended (for connector placement)  
- Audio jacks placed at board edge for easy access  

---

## 9. Compliance  

- Must route analog audio traces with proper grounding and isolation  
- Must follow OutbackEdge-M2e-Mod-Interface-v1.0  
- Populated ESD protection on exposed jacks
