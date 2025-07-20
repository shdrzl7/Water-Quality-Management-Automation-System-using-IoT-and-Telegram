# Water-Quality-Management-Automation-System-using-IoT-and-Telegram
This project is an **automated water quality monitoring and control system** designed to maintain optimal pond conditions using **Arduino**, **ESP32**, and a suite of sensors. It monitors parameters such as **pH**, **temperature**, **turbidity**, and automates tasks like water exchange, heating, and notifications via **Telegram Bot**.

## 🔧 Features
- 📡 Real-time data monitoring: pH, temperature, turbidity
- 🔄 Automated actions based on sensor thresholds
- 📲 Telegram Bot integration for alerts and remote commands
- 📊 Data logging to Microsoft Excel using **Data Streamer Add-in**
- 🛠️ Low-cost hardware setup (~RM240)

## 🧠 System Overview

| Sensor       | Condition                | Action                                  |
|--------------|--------------------------|-----------------------------------------|
| **pH**       | < 7.5                    | Turn ON alkaline pump                   |
|              | > 8.5                    | Turn ON acidic pump                     |
| **Turbidity**| > 25 NTU                | Turn ON both input and output pumps     |
| **Temp**     | < 26°C                  | Turn ON cooling fan                     |
|              | > 30°C                  | Turn ON heater  

## 🖥️ Telegram Integration
- Telegram bot created via **BotFather**
- Controlled remotely via smartphone or PC
- Receives alerts:
  - Water too acidic/alkaline
  - Water too turbid
  - Temperature out of range
- Responds to commands:
  - `/status`
  - `/alkalinePump_ON`, `/OFF`
  - `/acidicPump_ON`, `/OFF`
  - `/heater_ON`, `/OFF`, etc.
 
## 📈 Excel Data Logging (via Data Streamer)
This system pushes sensor readings directly into **Microsoft Excel** in real-time for logging and visualization. Requires:
1. Excel Data Streamer COM Add-in
2. Serial communication over USB
3. Arduino sketch formatted for streaming

## 🔌 Components

| No | Component                         | Qty | Price (RM) | Total (RM) |
|----|-----------------------------------|-----|------------|------------|
| 1  | Arduino Uno R3                    | 1   | 30.50      | 30.50      |
| 2  | PH4502C pH Sensor                 | 1   | 69.99      | 69.99      |
| 3  | DFRobot Turbidity Sensor         | 1   | 34.99      | 34.99      |
| 4  | DS18B20 Temperature Sensor       | 1   | 8.30       | 8.30       |
| 5  | Submersible Water Pump (5V)      | 4   | 4.20       | 16.80      |
| 6  | Ceramic Heater (12V)             | 1   | 5.50       | 5.50       |
| 7  | DC Cooling Fan (5V)              | 1   | 12.50      | 12.50      |
| 8  | Relay Module (1-channel)         | 6   | 3.15       | 18.90      |
| 9  | ESP32 Board                       | 1   | 35.00      | 35.00      |
| 10 | Servo Motor                       | 1   | 6.80       | 6.80       |
|    | **Total**                         |     |            | **239.28** |

## 🛠 Libraries Used

- `UniversalTelegramBot.h` – for Telegram Bot integration
- `WiFi.h` or `WiFiClientSecure.h` – for ESP32 network connectivity
- `OneWire.h`, `DallasTemperature.h` – for DS18B20
- `Wire.h` – for I2C communication
