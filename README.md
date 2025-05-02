# smartenergymeter
A Smart Energy Meter project using ESP32, ACS712, ZMPT101B, LCD, EEPROM, and Blynk IoT. It monitors real-time voltage, current, power, and energy consumption with remote access and data logging.

# 🔌 Smart Energy Meter with IoT

This project is a Smart Energy Meter built using **ESP32**, **ACS712 (Current Sensor)**, **ZMPT101B (Voltage Sensor)**, **16x2 I2C LCD**, **EEPROM**, and integrated with the **Blynk IoT platform**. It monitors and displays voltage, current, power, and energy consumption in real-time, both locally on an LCD screen and remotely via Blynk.

---

## 📷 Features

- 📊 Real-time measurement of **Voltage**, **Current**, **Power**, and **Energy (kWh)**
- 📲 Remote monitoring via **Blynk IoT App**
- 💾 Energy unit stored in **EEPROM** every 30 seconds to prevent data loss
- 🔍 Auto noise filtering using ACS712 noise voltage
- 🖥️ Local display on **16x2 I2C LCD**
- 🧮 RMS calculation for accurate sensor readings
- 🔌 Designed to measure loads up to 5A (extendable)

---

## 🛠️ Components Used

| Component           | Quantity | Description                            |
|--------------------|----------|----------------------------------------|
| ESP32 Dev Board     | 1        | Microcontroller with Wi-Fi             |
| ACS712 (5A)         | 1        | Hall-effect based current sensor       |
| ZMPT101B            | 1        | Voltage sensor for AC mains            |
| 16x2 LCD (I2C)      | 1        | Display module                         |
| EEPROM (on ESP32)   | -        | Used to store energy units             |
| AC Bulb Load        | 1        | Testing with 60W, 100W, etc.           |
| Resistors, Wires    | -        | General circuit assembly               |

---

## 🧾 Functional Flow

1. Sensor reads AC current (ACS712) and voltage (ZMPT101B).
2. Values are filtered and averaged.
3. Power = Voltage × Current is calculated.
4. Energy (in kWh) is accumulated over time.
5. Values are displayed on LCD and sent to Blynk.
6. Energy unit is saved in EEPROM every 30 seconds.

---

## 🔗 Blynk Integration

- Add virtual pins:  
  - `V0`: Voltage  
  - `V1`: Current  
  - `V2`: Power  
  - `V3`: Energy Unit

- Use `Blynk Template ID`, `Device Name`, and `Auth Token` from your Blynk Dashboard.

---

## 💻 Code Snippet (Main Loop Example)

```cpp
float voltage = voltageSensor.getRmsVoltage();
float current = ACS.mA_AC() / 1000.0;
float power = voltage * current;
float kWh = power / 3600000;
unit += kWh;
EEPROM.writeFloat(0, unit);
EEPROM.commit();



---

