# 🚀 Smart Obstacle Detection System

## 📖 Overview
This project implements an automated, distance-based response system using an Arduino Uno. The system utilizes an HC-SR04 ultrasonic sensor to detect objects within a specific range. Upon successful detection, it triggers a micro servo motor to rotate to a designated angle and illuminates an LED. The project is designed with stability in mind, featuring software-level noise filtering and power-draw mitigation.

## 🛠️ Hardware Components
*   **🧠 Microcontroller:** Arduino Uno R3
*   **👀 Sensor:** HC-SR04 Ultrasonic Distance Sensor (4-pin)
*   **⚙️ Actuator:** SG90 Micro Servo Motor
*   **💡 Indicator:** 5mm Red LED
*   **🔌 Passive Components:** Current-limiting resistor (e.g., 220Ω - 330Ω)
*   **🔋 Power Supply:** Standard USB 5V or External Power Source via VIN
*   **🛹 Prototyping:** Breadboard and Jumper Wires

## 🔌 Wiring & Pin Configuration

> ⚠️ **Note:** All ground (`GND`) connections must be tied to a **Common Ground** on the breadboard to ensure a stable reference voltage.

| Component | Pin / Terminal | Arduino Pin / Connection |
| :--- | :--- | :--- |
| **HC-SR04** | VCC | 5V |
| | GND | Common GND |
| | Trig | Digital Pin 9 |
| | Echo | Digital Pin 8 |
| **Micro Servo** | VCC (Red/Orange) | 5V |
| | GND (Brown/Black)| Common GND |
| | Signal (Yellow) | Digital Pin 5 |
| **LED** | Anode (Long Leg) | Digital Pin 13 |
| | Cathode (Short Leg)| Resistor → Common GND |

## 🧠 Core Logic & Functionality
The system operates based on a continuous loop of ultrasonic distance measurements:
1.  **💤 Idle State:** If no object is detected, or the object is outside the targeted range, the LED remains OFF, and the servo rests at **90 degrees**.
2.  **🚨 Active State:** If an object is detected within the strict range of **> 2 cm and <= 10 cm**, the LED turns ON, and the servo rotates to **160 degrees**.

## 🛡️ System Stability & Troubleshooting Enhancements
*   **🛑 Preventing Servo Stall:** The maximum actuation angle was restricted to `160°` instead of `180°`. This prevents the servo gears from hitting their physical limits.
*   **⏱️ Pulse Timeout Implementation:** A `30,000` microsecond (30 ms) timeout limit was added to the `pulseIn()` function.
*   **🎛️ Distance Filtering:** The detection logic ignores distances of `2 cm` or less to filter out erratic sensor noise.
*   **⚡ Power Management:** To avoid Arduino brownouts, external power sources must be routed through the Arduino's `VIN` pin.

## 💻 Code Setup
1. Open the Arduino IDE.
2. Include the built-in `<Servo.h>` library.
3. Upload the provided `.ino` sketch to the Arduino Uno.
4. Open the Serial Monitor at `9600 baud` to view real-time distance measurements.
