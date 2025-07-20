# Water-Quality-Management-Automation-System-using-IoT-and-Telegram
This project is an **automated water quality monitoring and control system** designed to maintain optimal pond conditions using **Arduino**, **ESP32**, and a suite of sensors. It monitors parameters such as **pH**, **temperature**, **turbidity**, and automates tasks like water exchange, heating, and notifications via **Telegram Bot**.
<img src="Images/Front.jpg" alt="Front View" width="600"/>
<table>
  <tr>
    <td align="center">
      <strong>Back View</strong>
      <img src="Images/Back.jpg" alt="Back View" width="200"/>
    </td>
    <td align="center">
      <strong>Right Side View</strong>
      <img src="Images/Right.jpg" alt="Right View" width="200"/>
    </td>
    <td align="center">
      <strong>Left Side View</strong>
      <img src="Images/Left.jpg" alt="Left View" width="200"/>
    </td>
    <td align="center">
      <strong>Top View</strong>
      <img src="Images/Top.jpg" alt="Top View" width="200"/>
    </td>
    <td align="center">
      <strong>Inside View</strong>
      <img src="Images/Inside.jpg" alt="Inside View" width="200"/>
    </td>
  </tr>
</table>

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
<img src="Images/System Overview Design.jpg" alt="System Overview Design" width="600"/>
All the parameters sensors which are pH level sensor (5), temperature sensor (6) and turbidity sensor (7) are placed inside the main water aquarium tank. This water tank functions as a simulated model or replica of a aquaculture pond. Two of the actuators, which are cooling fan (9) and heater are placed inside the tank. An automatic feeder (8) is placed on top of the tank. Other actuator components such as water pumps 3, 4 and 10 are placed outside the tank. There are three other tanks outside the main tank which are the acidic tank (1), alkaline tank (2) and external water tank (12). The arrow in the figure illustrates the water flow.

- **Master (Arduino Uno):**
  - Reads data from turbidity, pH, and temperature sensors
  - Controls water pump and fan using relays
  - Sends sensor data via I2C to the ESP32

- **Slave (ESP32):**
  - Receives sensor data over I2C
  - Connects to WiFi and sends updates to Telegram
  - Handles alert notifications and basic Telegram bot interface

> 📂 The full source code for both Arduino Uno (Master) and ESP32 (Slave) can be found in the `Source Codes` folder.

## 🧠 Why Two Microcontrollers?

Using two separate microcontrollers improves:
- **Performance**: Avoids overloading a single device
- **Modularity**: Easier to debug and maintain
- **Scalability**: Easy to add new features

## 🔗 Communication (I2C)

- I2C Bus: SDA and SCL lines
- **Arduino Uno**:
  - SDA: Pin A4
  - SCL: Pin A5
- **ESP32**:
  - SDA: GPIO 21
  - SCL: GPIO 22

Data is converted to byte format before being transmitted over I2C using the `Wire` library.

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

## ⚙️ Components

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

## 🔌 Wiring connection (schematic diagram)
<img src="Images/Schematic Diagram.jpg" alt="Schematic Diagram" width="600"/>

## 🛠 Libraries Used
- `UniversalTelegramBot.h` – for Telegram Bot integration
- `WiFi.h` or `WiFiClientSecure.h` – for ESP32 network connectivity
- `OneWire.h`, `DallasTemperature.h` – for DS18B20
- `Wire.h` – for I2C communication
