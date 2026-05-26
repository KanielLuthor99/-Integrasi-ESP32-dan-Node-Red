# -Integrasi-ESP32-dan-Node-Red

# IoT Environmental Monitor & Actuator Control System

This project is a Cyber-Physical System (CPS) implementation that combines an **ESP32** microcontroller and a **Node-RED** dashboard to perform real-time environmental monitoring and remote hardware control. 

The system utilizes the **MQTT protocol** (via `broker.emqx.io`) for bidirectional communication: publishing sensor data and subscribing to control commands.

---

## 🚀 Features

* **Real-time Monitoring:** Collects ambient temperature and humidity from a DHT11 sensor and publishes data every 5 seconds.
* **Remote Actuation:** * Toggle an LED remotely from the dashboard.
    * Trigger a non-blocking 3-second buzzer alert.
* **Interactive Dashboard:** Built with Node-RED, featuring live Gauges and Charts for data visualization and Switches/Buttons for control.

---

## 🛠️ Hardware Requirements

1. ESP32 Development Board
2. DHT11 Temperature & Humidity Sensor
3. 1x LED (Internal Pin 2 or External)
4. 1x Active Buzzer
5. Jumper Wires & Breadboard

---

## 📋 Prerequisites & Installation

### 1. Arduino IDE Setup
Before uploading the code, ensure you have installed the ESP32 board support and the following libraries via the Library Manager (**Sketch -> Include Library -> Manage Libraries**):
* **PubSubClient** (by Nick O'Leary)
* **DHT sensor library** (by Adafruit)
* **Adafruit Unified Sensor** (dependency for DHT)

### 2. Node-RED Setup
Ensure Node-RED is installed locally or hosted on a server. You will need the dashboard palette:
1. Open Node-RED.
2. Click the menu icon (top right) -> **Manage palette**.
3. Go to the **Install** tab, search for `@flowfuse/node-red-dashboard` or `node-red-dashboard`, and click install.

---

## 🔧 How to Run the Program

### Step 1: Flash the ESP32
1. Open the provided `.ino` file in your Arduino IDE.
2. Update the WiFi credentials with your own network parameters:
   ```cpp
   const char* ssid = "YOUR_WIFI_SSID";
   const char* password = "YOUR_WIFI_PASSWORD";

3.**CRITICAL**: Change the NIM variable to your student ID or a unique identifier to avoid topic collision on the public broker:

C++
const char* NIM = "YOUR_UNIQUE_ID_HERE";

4. Connect your ESP32 to your computer, select the correct Board and Port, then click Upload.

5. Open the Serial Monitor (set to 115200 baud rate) to verify the connection status.

Step 2: Configure Node-RED Dashboard

1.Open your Node-RED flow editor (typically http://localhost:1880).

2. Drag and drop the following nodes to configure your workspace:

- MQTT Out Node (for LED Control): Set topic to YOUR_NIM/LED. Connect to a Switch Node (Payload 1 for true, 0 for false).
- MQTT Out Node (for Buzzer): Set topic to YOUR_NIM/BUZZER. Connect to a Button Node (Payload 1).
- MQTT In Node (for Temperature): Set topic to YOUR_NIM/SUHU. Connect to a Gauge Node and Chart Node.
- MQTT In Node (for Humidity): Set topic to YOUR_NIM/KELEMBAPAN. Connect to a Gauge Node and Chart Node.

3. Double-click any MQTT node, add a new MQTT broker configuration, and set the Server to broker.emqx.io with Port 1883.

4. Click the Deploy button (top right).

5. Access your dashboard interface at http://localhost:1880/ui.

**(Note: Replace NIM with your unique identifier as configured in the ESP32 code).**
