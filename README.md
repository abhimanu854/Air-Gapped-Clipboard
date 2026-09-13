<img width="1280" height="640" alt="git (1)" src="https://github.com/user-attachments/assets/8920b256-2ba8-4988-b824-5351134eb4bd" />



# Air-Gapped Clipboard 🎯


## Basic Details
### Team Name: Air-Gapped Absurdity


### Team Members
- Team Lead: Abhimanu S - Saintgits College of Engineering
- Member 2: Harigovind KR - Saintgits College of Engineering

### Project Description
An absurd, physically air-gapped clipboard transport vehicle. It intercepts local copy (`Ctrl+C`) events on a Windows laptop, wipes the local OS clipboard immediately to prevent cheating, transmits the text payload over a private ESP32 Wi-Fi SoftAP network, physically drives an autonomous 4WD robot car across the room, and injects the text into a target Fedora Linux laptop's clipboard upon physical bumper collision!

### The Problem (that doesn't exist)
In an era of rampant cybersecurity paranoia, traditional digital clipboards, cloud clipboard syncs, and local network sockets are "fundamentally untrustworthy" — packets flying through the air could theoretically be sniffed by malicious actors. Why trust invisible, frictionless digital transmissions across wires or Wi-Fi when you can make data transfer slow, loud, and physically collision-prone?

### The Solution (that nobody asked for)
Physical Kinetic Air-Gapping! When you press `Ctrl+C`, your clipboard is immediately hijacked and erased from local OS memory. The text payload is dispatched to a 4WD ESP32 robot car that literally drives across the floor carrying your data on an OLED display. When it reaches the receiving laptop and rams into the IR bumper sensor at the dock, the receiving script downloads the payload and injects it straight into the target laptop's clipboard — unless our 30% "Goldfish Memory" kicks in upon impact and the car completely forgets why it drove over!

## Technical Details
### Technologies/Components Used
For Software:
- Languages: Python 3.10+, C++ (Arduino)
- Frameworks: Arduino IDE (ESP32 Core v3.x), Tkinter (GUI)
- Libraries: `requests`, `pyperclip`, `keyboard`, `<WebServer.h>`, `<WiFi.h>`, `<Wire.h>`, `<Adafruit_GFX.h>`, `<Adafruit_SSD1306.h>`
- Tools: Arduino IDE, VS Code, Git

For Hardware:
- Main Components:
  - ESP32 Development Board (Microcontroller)
  - L298N Dual H-Bridge Motor Driver Module
  - 4WD Robot Car Chassis with 4x BO Motors and Wheels
  - 0.96-inch I2C SSD1306 OLED Display (128x64)
  - Active-LOW IR Obstacle Sensor (Bumper Collision Detection)
  - 7.4V - 9V Rechargeable Battery Pack
- Specifications:
  - ESP32 Wi-Fi SoftAP: SSID `AirGappedClipboard`, IP `192.168.4.1`, Port 80 HTTP Web Server
  - Motor Control: 4-wheel drive parallel wired, GPIOs 26, 27 (Left) and 14, 12 (Right)
  - Bumper Sensor: Active LOW digital trigger on GPIO 33
  - OLED Display: I2C on SDA GPIO 21, SCL GPIO 22
- Tools Required:
  - Screwdriver set, jumper wires, soldering kit, USB data cable, battery charger

### Implementation
For Software:
# Installation
```bash
# Clone the repository
git clone https://github.com/abhimanu854/Air-Gapped-Clipboard.git
cd Air-Gapped-Clipboard

# Setup for Windows Sender (Laptop A):
cd client_hijacker
pip install -r requirements.txt

# Setup for Fedora Linux Receiver (Laptop B):
sudo dnf install -y python3-tkinter xclip wl-clipboard
pip install requests pyperclip
```

# Run
```bash
# 1. Power on the ESP32 Car (Connect both laptops to Wi-Fi: AirGappedClipboard / Password: 12345678)

# 2. On Fedora Linux (Laptop B / Receiver):
python3 client_hijacker/receiver.py

# 3. On Windows (Laptop A / Sender):
python client_hijacker/client.py

# 4. Press Ctrl+C on Laptop A to watch the robot physically transport your clipboard to Laptop B!
```

### Project Documentation
For Software:

# Screenshots (Add at least 3)
![Sender Dashboard](client_hijacker/screenshots/sender_dashboard.png)
*Windows Sender App (client.py) capturing Ctrl+C, wiping local clipboard, and displaying live transit stopwatch and telemetry*

![Receiver Radar](client_hijacker/screenshots/receiver_radar.png)
*Fedora Linux Receiver App (receiver.py) actively scanning ESP32 status and auto-injecting received payload into local clipboard*

![OLED Display](client_hijacker/screenshots/oled_display.png)
*0.96" SSD1306 OLED display showing the in-transit payload and the confused ( O_o ) Goldfish Memory face*

# Diagrams
![Workflow](diagrams/workflow.png)
*Kinetic Clipboard Dataflow: Windows Sender (Ctrl+C intercept & wipe) -> HTTP POST /copy -> ESP32 4WD Kinetic Car -> Physical Bumper Collision (IR Pin 33) -> 70% Success / 30% Goldfish Memory Roll -> Fedora Receiver (HTTP GET /data & inject)*

```
[ Windows Sender ]                      [ ESP32 Robot Car ]                     [ Fedora Receiver ]
 Ctrl+C Intercept                      AirGappedClipboard AP                       Radar Listener
        |                                  (192.168.4.1)                                  |
        |--- HTTP POST /copy (Payload) -------->|                                         |
        |    (Local Clipboard WIPED)            |                                         |
                                                |-- 4WD Drive Forward --->                |
                                                |   (Text on OLED)                        |
                                                |                                         |
                                                |-- [ Physical Collision ] --------------->|
                                                |   IR Sensor Pin 33 LOW                  |
                                                |                                         |
                                                |-- 70% Remembered -> Status = ARRIVED -->|
                                                |   (Receiver fetches /data & injects)    |
                                                |                                         |
                                                |-- 30% Goldfish Memory -> ( O_o ) ------>|
                                                    (Memory wiped, "Uhh... I forgot.")
```

For Hardware:

# Schematic & Circuit
![Circuit](hardware/circuit.png)
*Wiring connections: ESP32 to L298N (IN1: 26, IN2: 27, IN3: 14, IN4: 12), IR Sensor (GPIO 33), and I2C OLED (SDA: 21, SCL: 22)*

![Schematic](hardware/schematic.png)
*Power circuit: External 7.4V battery pack powering L298N and ESP32 with common ground*

# Build Photos
![Components](hardware/components.png)
*ESP32 Dev Module, L298N motor driver, 4x BO motors + chassis wheels, SSD1306 OLED display, and IR obstacle sensor*

![Build](hardware/build.png)
*Mechanical assembly of the 4WD chassis and parallel motor wiring for left and right motor pairs*

![Final](hardware/final.png)
*Completed kinetic clipboard transport vehicle with mounted OLED display and front bumper sensor*

### Project Demo
# Video
[Air-Gapped Clipboard Demo Video](https://youtu.be/)
*Full physical demonstration showing Ctrl+C interception on Windows, physical kinetic transport across the floor, bumper collision, and clipboard injection on Fedora Linux.*

# Additional Demos
*Live two-laptop demonstration at TinkerHub Useless Projects 3.0 Hackathon.*

## Team Contributions
- Abhimanu S: ESP32 C++ firmware architecture, motor control & driver logic, WebServer HTTP endpoints, hardware assembly and testing.
- Harigovind KR: Client hijacker application (Windows sender & Fedora receiver), Tkinter UI dashboards, global clipboard interception, documentation.

---
Made with ❤️ at TinkerHub Useless Projects 

![Static Badge](https://img.shields.io/badge/TinkerHub-24?color=%23000000&link=https%3A%2F%2Fwww.tinkerhub.org%2F)
![Static Badge](https://img.shields.io/badge/UselessProjects--26-26?link=https%3A%2F%2Ftinkerhub.org%2Fevents%2F1M8ORET9A1%2Fuseless-projects-3.0)
