
# 💧 Water Quality Monitoring System (Arduino)

## 🌟 Overview
This project implements an Arduino-based water quality monitoring system using several sensors (Temperature, Turbidity, TDS, pH, and Color/Clarity via IR sensor). Data is displayed on a 16x2 LCD and streamed to the Serial Monitor. A logic check determines if the water is "Safe to use" for domestic purposes.

---

## ⚙️ Hardware Components

* Microcontroller: Arduino Uno (or compatible).
* Display: 16x2 Liquid Crystal Display (LCD).
* Temperature Sensor: TMP36 Analog Temperature Sensor.
* Turbidity Sensor: Analog Turbidity Sensor.
* TDS Sensor: TDS Meter Module or Potentiometer.
* pH Sensor: pH Electrode/Module or Potentiometer.
* Clarity Sensor: Analog IR Sensor.
* Control Input: Push Button/Switch on Digital Pin 6 (for mode selection).

---

## 🔌 Wiring and Connections

| Component | Arduino Pin(s) | Notes |
| :--- | :--- | :--- |
| **LCD** | D12, D11, D5, D4, D3, D2 | (RS, Enable, D4, D5, D6, D7) |
| **Temperature** | **A0** (Alias 14) | Analog Input |
| **Turbidity** | **A1** (Alias 15) | Analog Input |
| **TDS** | **A2** (Alias 16) | Analog Input |
| **pH** | **A3** (Alias 17) | Analog Input |
| **IR Sensor** | **A4** (Alias 18) | Analog Input |
| **Mode Switch** | **D6** | Digital Input |

---

## 💻 Key Calculation Formulas

1.  **Temperature (TMP36):**
    Voltage (V) = (Analog Reading / 1024.0) * 5.0
    Temp (°C) = (Voltage (V) - 0.5) * 100.0

2.  **Turbidity Calibration:**
    The $0-5$ range is mapped using $0-471$ as the input range, where 471 is the maximum expected reading for the highest turbidity level (5).

3.  **Water Safety Thresholds:**
    * Turbidity (turl): < 4 (Assuming this is the corrected safe limit)
    * TDS (TDS1): < 600 ppm
    * pH (PH1): >= 6.5 AND < 7.2

---

## 🏃 Operation Modes

Controlled by the switch on Digital Pin **D6**:

1.  **Status Mode (D6 = LOW):** Displays "Safe to use" or "Dangerous" on the LCD.
2.  **Display Mode (D6 = HIGH):** Cycles through and displays each sensor reading (TEMP, TURB, PH, TDS, Clarity Status).

