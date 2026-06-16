# Smart Child Safety Lock (Prototype)

## 📋 Project Overview

### Problem
Young children can unintentionally unlock doors and leave the house unsupervised, creating serious safety risks. Standard passive locks can be bypassed or forgotten, requiring an automated, intelligent intervention.

### Goal
Design and build a microcontroller-based system that:
* Detects when a child is near a door
* Physically prevents the door from opening
* Allows manual adult override
* Filters out environmental noise (like adults walking past) to prevent false-alarm triggers. Or any other possible triggers.

### Version 1 Scope
* **Proximity Detection:** Ultrasonic sensor detects proximity at child height (~3–3.5 ft).
* **Processing Unit:** ESP32 microcontroller processes detection logic and sensor time-of-flight calculus.
* **Actuation:** Servo motor physically blocks door handle movement upon threat detection.
* **Override:** Manual push button for secure adult override.
* **Feedback:** LED status indicators for testing, diagnostics, and lock state representation.

---

## 🛠️ Hardware & Software Architecture

### Hardware (Planned & In-Use)
* ESP32 Development Board (38-pin NodeMCU variant)
* Ultrasonic Distance Sensor (HC-SR04)
* Servo Motor Actuator
* Breadboard and Jumper Wires
* Tactile Push Button
* Light Emitting Diodes (LEDs) & Current-Limiting Resistors
* USB Data Cable / Power Supply

### Software & Toolchain
* **IDE:** VS Code (Visual Studio Code)
* **Ecosystem:** PlatformIO IDE extension (Arduino Framework Core)
* **Version Control:** Git & GitHub

---

## 📈 Engineering Journey & Milestone Logs

### 🔹 Phase 1: Environment Baseline & Physical Layer Diagnostics
**Status: COMPLETE & VERIFIED**

* **The Goal:** Establish a stable software-to-hardware pipeline using VS Code and PlatformIO to flash a basic timing loop (`Blink`) onto the microcontroller, verifying external component power delivery.

#### Key Roadblocks & Troubleshooting

##### 1. The Mechanical Connection Trap (The "Dead" LED)
* **The Problem:** The ESP32 code compiled and uploaded with a `SUCCESS` status, and the onboard chip LED blinked, but the external green LED on the breadboard remained completely dark. 
* **The Diagnostics:** Systematically isolated variables by cross-referencing video tutorials, modifying code loop frequencies, and verifying PlatformIO framework paths. 
* **The Resolution:** Discovered that the physical width of the ESP32 housing caused tight tolerances inside the breadboard channels. The microcontroller pins were hovering inside the plastic slots without seating deeply enough into the internal metal clips. Firmly pushing the chip completely flush with the board immediately restored electrical continuity, and the LED began blinking.
* **Engineering Takeaway:** Sit patiently with hardware anomalies, don't panic, and always verify the simplest mechanical connections before over-complicating the software logic.

##### 2. Unlabeled Pin Configurations (The Pinout Discovery)
* **The Problem:** The physical development board arrived without clear silk-screened labels for the individual GPIO pins, making accurate wire mapping impossible.
* **The Resolution:** Located and referenced the exact 38-pin hardware configuration datasheet/pinout schematic. 
* **The Mapping:** Successfully mapped **GPIO2 (Pin 24)** as the dedicated internal LED line to drive the signal wire, and matched **Pin 38 (GND)** to establish a common ground with the breadboard's negative rail.