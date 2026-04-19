# ProxiWave-D (PWD-v010A)
### Touchless Proximity-Based AC Relay Controller — Open Source Hardware by Ampnics

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
![Hardware](https://img.shields.io/badge/Hardware-KiCad%209.0-blue)
![MCU](https://img.shields.io/badge/MCU-ATmega328--A-green)
![Version](https://img.shields.io/badge/Version-PWD--v010A-red)
![Made in India](https://img.shields.io/badge/Engineered%20in-India-ff9933)

> An open-source, touchless proximity-based AC relay controller built on ATmega328-A with a VL53L0X Time-of-Flight sensor — designed for contactless switching of 220VAC loads by detecting hand proximity within 10–30mm range.

---

## 📸 Board Preview

| PCB Top View (Sensor Side) | PCB Bottom View (Power Side) |

<img width="1684" height="947" alt="Screenshot 2026-01-31 101725" src="https://github.com/user-attachments/assets/6ede0bd7-b72f-4823-8d11-09c537356c5c" />

---
<img width="1597" height="943" alt="Screenshot 2026-01-31 102038" src="https://github.com/user-attachments/assets/7fe757b4-4c0d-4f44-9f15-2e33f758f456" />

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [How It Works](#-how-it-works)
- [Hardware Specifications](#-hardware-specifications)
- [GPIO Mapping](#-gpio-mapping)
- [Pin Description](#-pin-description)
- [Repository Structure](#-repository-structure)
- [Getting Started](#-getting-started)
- [Firmware Setup](#-firmware-setup)
- [Calibration](#-calibration)
- [Manufacturing](#-manufacturing)
- [Safety Warning](#️-safety-warning)
- [Contributing](#-contributing)
- [Support Us](#-support-us)
- [Connect With Us](#-connect-with-us)
- [License](#-license)

---

## 🔍 Overview

The **ProxiWave-D** is an open-source, touchless proximity relay controller designed for contactless switching of 220VAC loads. It uses a **VL53L0X Time-of-Flight (ToF) distance sensor** to detect hand proximity within a calibrated range of **10mm to 30mm**, triggering an onboard relay to switch AC loads — no physical contact required.

The board runs on **220VAC mains input**, converting it to **5V DC** via an onboard HLK-5M05 power supply module, and further to **3.3V** via an AMS1117-3.3 LDO — powering the ATmega328 and the VL53L0X sensor.

A **backup IR sensor connector (J3)** is also provided for redundancy or alternative sensing modes.

Designed in **KiCad 9.0.1** as part of the open-source hardware series by Ampnics.

---

## ✨ Features

- ✅ Touchless relay switching via VL53L0X ToF proximity sensor
- ✅ ATmega328-A microcontroller (8MHz crystal, 3.3V operation)
- ✅ 220VAC to 5VDC onboard power supply (HLK-5M05)
- ✅ 5V to 3.3V LDO regulator (AMS1117-3.3)
- ✅ SPDT relay for AC load switching
- ✅ MOV surge protection (10D561K)
- ✅ Fuse protection (0.5A / 250VAC)
- ✅ Backup IR sensor connector (J3)
- ✅ Buzzer feedback (MLT-8530)
- ✅ Power LED (Red) + Relay LED (Blue) + Status LED (Green)
- ✅ ICSP / SPI programming port (J2 — 2x3 header)
- ✅ Reset button (SW1)
- ✅ 5x screw terminal AC connector (J1)
- ✅ Test points — 5V, 3V3, GND, AVDD
- ✅ Fiducial markers + 4x mounting holes
- ✅ Sensing area clearly marked on PCB silkscreen
- ✅ Fully open-source — KiCad files included

---

## 🔄 How It Works

```
Hand approaches sensing area (10mm–30mm range)
              │
              ▼
   VL53L0X ToF Sensor detects distance
              │
              ▼
   ATmega328 reads I2C data from sensor
              │
              ▼
   Distance within calibrated threshold?
         ┌────┴────┐
        YES        NO
         │          │
         ▼          ▼
   Relay toggles  No action
   AC load ON/OFF
         │
         ▼
   Buzzer beeps + Status LED updates
```

---

## 🔧 Hardware Specifications

| Parameter | Details |
|---|---|
| Microcontroller | ATmega328-A |
| MCU Clock | 8MHz (External Crystal Y1) |
| MCU Operating Voltage | 3.3V |
| Proximity Sensor | VL53L0X ToF (I2C) |
| Sensor Operating Voltage | 2.6V – 3.6V (3.3V) |
| Detection Range | 10mm – 30mm (calibrated) |
| Input Voltage | 220V AC |
| Power Supply Module | HLK-5M05 (220VAC → 5VDC) |
| LDO Regulator | AMS1117-3.3 (5V → 3.3V) |
| Relay | G5LE-1 (SPDT) |
| Surge Protection | MOV 10D561K |
| Fuse | 0.5A / 250VAC |
| Buzzer | MLT-8530 |
| Status LEDs | Red (Power), Blue (Relay), Green (Status) |
| Programming | ICSP / SPI (J2 — 2x3 header) |
| Backup Sensor Port | J3 — 3-pin connector |
| PCB Tool | KiCad 9.0.1 |
| Board Revision | PWD-v010A |

---

## 📌 GPIO Mapping

| GPIO | Label | Function |
|---|---|---|
| PC1 / A1 | RIN / STS | Status indication |
| PC2 / A2 | RLY | Relay control |
| PC3 / A3 | BUZZER | Buzzer (MLT-8530) |
| PC4 / A4 | SDA | VL53L0X I2C SDA |
| PC5 / A5 | SCL | VL53L0X I2C SCL |
| PD2 / D2 | XSHUT | VL53L0X shutdown pin |
| PD4 / D4 | IR-BKP | Backup IR sensor (J3) |

---

## 🔌 Pin Description

### J1 — AC Screw Terminal (5-pin)

| Pin | Label | Description |
|---|---|---|
| 1 | AC/L | AC Line (Live) input |
| 2 | AC/N | AC Neutral input |
| 3 | NO | Relay Normally Open |
| 4 | C | Relay Common |
| 5 | NC | Relay Normally Closed |

### J2 — ICSP Programming Port (2x3)

| Pin | Label | Description |
|---|---|---|
| 1 | MISO | SPI MISO |
| 2 | VCC | 5V |
| 3 | SCK | SPI Clock |
| 4 | MOSI | SPI MOSI |
| 5 | RST | Reset |
| 6 | GND | Ground |

### J3 — Backup IR Sensor (3-pin)

| Pin | Label | Description |
|---|---|---|
| 1 | SIG | IR sensor signal |
| 2 | GND | Ground |
| 3 | 5V | Power |

### Signal Connector (3-pin)

| Pin | Label | Description |
|---|---|---|
| 1 | SIG | Signal output |
| 2 | GND | Ground |
| 3 | 3V3 | 3.3V output |

---

## 📁 Repository Structure

```
ProxiWave-D/
├── docs/                    # Datasheets and reference documents
├── imgs/                    # PCB renders and product images
├── manufacturing-files/     # Gerbers, BOM, CPL for fabrication
├── schematic/               # KiCad schematic & PCB files
├── ext-3d-models/           # External 3D models for KiCad
├── ext-lib/                 # External KiCad footprints & symbols
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- [KiCad 9.0.1](https://www.kicad.org/) — to open schematic and PCB files
- [Arduino IDE](https://www.arduino.cc/en/software) — for firmware
- USBasp / AVRISP programmer — for flashing ATmega328
- [VL53L0X Arduino Library](https://github.com/pololu/vl53l0x-arduino)

### Clone the Repository
```bash
git clone https://github.com/ampnics/Proxiwave-D.git
cd Proxiwave-D
```

---

## 💻 Firmware Setup

### 1. Add ATmega328 (3.3V / 8MHz) Board Support

In Arduino IDE → **Preferences** → Additional Boards Manager URLs → add:
```
https://raw.githubusercontent.com/MCUdude/MiniCore/master/package_MCUdude_MiniCore_index.json
```
Then: **Tools → Board → Boards Manager → search "MiniCore" → Install**

Select these settings:
- Board: `ATmega328`
- Clock: `External 8MHz`
- Voltage: `3.3V`

### 2. Install Required Libraries
```
VL53L0X    → by Pololu
Wire       → built-in
```

### 3. Basic Firmware Structure

```cpp
#include <Wire.h>
#include <VL53L0X.h>

#define RELAY_PIN   A2   // PC2
#define BUZZER_PIN  A3   // PC3
#define XSHUT_PIN   2    // PD2
#define STATUS_PIN  A1   // PC1

#define MIN_RANGE   10   // mm
#define MAX_RANGE   30   // mm

VL53L0X sensor;

void setup() {
  pinMode(RELAY_PIN, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  pinMode(XSHUT_PIN, OUTPUT);
  pinMode(STATUS_PIN, OUTPUT);

  digitalWrite(XSHUT_PIN, HIGH);
  Wire.begin();
  sensor.init();
  sensor.setTimeout(500);
  sensor.startContinuous();
}

void loop() {
  uint16_t distance = sensor.readRangeContinuousMillimeters();

  if (distance >= MIN_RANGE && distance <= MAX_RANGE) {
    digitalWrite(RELAY_PIN, !digitalRead(RELAY_PIN)); // Toggle relay
    digitalWrite(BUZZER_PIN, HIGH);
    delay(100);
    digitalWrite(BUZZER_PIN, LOW);
    delay(500); // Debounce delay
  }
}
```

### 4. Flash Using USBasp (ICSP)
```
Tools → Programmer → USBasp
Tools → Burn Bootloader (first time only)
Sketch → Upload Using Programmer
```

---

## 🎯 Calibration

> The VL53L0X sensor **must be calibrated** for reliable touchless operation.

- Default detection range: **10mm – 30mm**
- Adjust `MIN_RANGE` and `MAX_RANGE` in firmware based on your enclosure depth
- Mount sensor so the **sensing area circle** marked on PCB silkscreen is fully exposed
- Avoid reflective surfaces directly behind the sensing area
- Test under ambient light conditions before final deployment

---

## 🏭 Manufacturing

Fabrication files are available in `manufacturing-files/`:

- **Gerber files** — for PCB fabrication (JLCPCB / PCBWay)
- **BOM** — Bill of Materials with part numbers
- **CPL** — Component Placement List for SMT assembly

| Parameter | Value |
|---|---|
| Layers | 2 |
| Board Thickness | 1.6mm |
| Copper Weight | 1oz |
| Surface Finish | HASL / ENIG |
| Min Trace Width | 0.2mm |

---

## ⚠️ Safety Warning

> **This board operates at 220V AC mains voltage.**

- ⚠️ Do **NOT** touch the board while connected to mains power
- ⚠️ AC and DC sections are separated on the PCB — always respect this boundary
- ⚠️ Always use proper insulation and an enclosure before deployment
- ⚠️ Fuse (F1 — 0.5A/250VAC) must always be populated
- ⚠️ Intended for use by qualified engineers only

---

## 🤝 Contributing

Contributions are welcome from the community!

1. Fork the repository
2. Create your branch: `git checkout -b feature/your-feature`
3. Commit: `git commit -m "hw: your change"`
4. Push: `git push origin feature/your-feature`
5. Open a **Pull Request**

---

## ☕ Support Us

If this project helped you, consider buying us a coffee!

**[☕ Buy Me a Coffee — Support Ampnics](https://buymeacoffee.com/Ampnics)**

Your support helps us create more open-source hardware for the community!

---

## 🌐 Connect With Us

| Platform | Link |
|---|---|
| 📺 YouTube | [youtube.com/@ampnics](https://youtube.com/@ampnics?si=e0dvaRhfExjZXtJc) |
| 📸 Instagram | [instagram.com/ampnics](https://www.instagram.com/ampnics/) |
| 🐦 X (Twitter) | [twitter.com/ampnics](https://twitter.com/ampnics) |
| 💼 LinkedIn | [linkedin.com/company/ampnics](https://www.linkedin.com/company/ampnics/) |
| 🐙 GitHub | [github.com/ampnics](https://github.com/ampnics) |
| 💬 WhatsApp Community | [Join Here](https://chat.whatsapp.com/HgWOoxyOgLfGEkAPHPM01k) |
| 🌐 Website | [ampnics.com](https://ampnics.com) |

---

## 📄 License

This project is licensed under the **MIT License**.

You are free to use, modify, and distribute this design for personal and commercial purposes with attribution.

---

## 👨‍💻 Designed By

**Md Ammar Maniyar** — [Ampnics](https://github.com/ampnics)

*Engineered in India 🇮🇳*

---

⭐ **Star this repo** if it helped you — it motivates us to release more open-source hardware!
