# OmniPark Systems — Smart Car Park IoT Solution

**BEng (Hons) Electrical and Electronic Engineering — Year 2 Group Project**  
Manchester Metropolitan University | 2023–24  
Team: Handhala Bashir, William Chambers, Ethan Casey, Adil Syed, Joe Musselwhite, Callum Ferretti  
Industry Client: Smart Tech Pvt Limited (Faisal Riaz)

---

## Screenshots

### Vehicle type selection — live availability counts per category
![Vehicle Type Selection](screenshot-vehicle-select.png)

### Parking space grid — real-time availability (green = available, red = occupied)
![Parking Space Grid](screenshot-space-grid.png)

### EV bay grid — Space electric-2 occupied with registered vehicle DE09B0V displayed
![EV Bays with Occupancy](screenshot-occupied.png)

### Booking modal — UK registration input with start/end time picker
![Booking Modal](screenshot-booking.png)

### Booking schedule — confirmed booking logged with space, registration, time, and duration
![Booking Schedule](screenshot-schedule.png)

---

## Overview

OmniPark is a smart parking system that uses ultrasonic distance sensors, IoT connectivity, and a real-time dashboard to automate vehicle detection and parking space management. The system addresses a well-documented urban problem: approximately 30% of urban traffic congestion is caused by drivers searching for parking, generating an estimated 1.3 million tonnes of CO₂ per year from idling vehicles.

The system replaces manual parking management with continuous, automated space monitoring — delivering real-time availability data to drivers and operators without human intervention.

---

## System Architecture

```
HC-SR04 Ultrasonic Sensors (per bay)
        │
        ▼
Raspberry Pi Pico (GPIO)
        │
        ├──▶ Occupancy logic: distance < threshold → Occupied
        │
        ├──▶ IoT cloud transmission (ThingSpeak / LoRaWAN)
        │
        └──▶ Real-time availability dashboard
```

---

## Sensor Selection — Decision Matrix

Three detection technologies were evaluated against six weighted criteria:

| Criteria | Weight | Magnetic Field | **Ultrasonic** | Pressure Plates |
|---|---|---|---|---|
| Accuracy | 1 (highest) | 5 | **5** | 4 |
| Cost | 2 | 3 | **4** | 2 |
| Installation | 3 | 4 | **5** | 3 |
| Maintenance | 4 | 5 | **4** | 3 |
| Weather resistance | 5 | 5 | **5** | 5 |
| Versatility | 6 | 3 | **5** | 4 |
| **Total score** | | 86 | **99** | 78 |

**Ultrasonic sensors selected** (score: 99/120). LiDAR was also evaluated but ruled out due to software development constraints under project scope. Pressure plates were rejected on cost and maintenance grounds. Ultrasonic sensors offer the best balance of accuracy, ease of installation, and all-weather reliability for a retrofit deployment context.

---

## How It Works

Each parking bay has an HC-SR04 ultrasonic distance sensor mounted centrally overhead. The sensor emits a pulse and measures time-of-flight to calculate the distance to the surface below:

- **No vehicle present:** distance reading ≈ full bay height (~200 cm+) → **Available**
- **Vehicle present:** distance reading drops below threshold → **Occupied**

State changes are transmitted to an IoT cloud platform, updating the dashboard in real time.

---

## Hardware Components

| Component | Role |
|---|---|
| Raspberry Pi Pico | Microcontroller — sensor interfacing + data transmission |
| HC-SR04 Ultrasonic Sensors | Per-bay vehicle presence detection |
| Servo motor | Barrier automation |
| ESP32 | Bicycle lock subsystem (BLE + PIR) |
| LEDs | Bay status indicators |

---

## Software & Tools

| Tool | Purpose |
|---|---|
| Python / MicroPython | Firmware — sensor polling, threshold logic, IoT transmission |
| Wokwi | Circuit simulation and firmware validation before hardware build |
| Thonny IDE | MicroPython development and Pico flashing |
| ThingSpeak / LoRaWAN | IoT data aggregation and dashboard |
| Fusion 360 | CAD — physical car park structure design and simulation |

---

## Simulation (Wokwi)

The complete sensor circuit was designed and validated in Wokwi before physical build:
- Raspberry Pi Pico board with ultrasonic sensors connected via GPIO
- Python firmware tested in simulation — distance readings output every second
- Occupancy threshold logic verified in simulation environment
- Confirmed firmware compatibility with target hardware platform before component procurement

---

## Additional Subsystems

### Entrance & Exit Barriers
Three barrier concepts evaluated (arm barrier, sliding gate, bollard). Bollards selected (score: 94/120) for space efficiency, low maintenance, high security, and IoT integration compatibility.

### Bicycle Locking System
ESP32-based smart frame lock with PIR sensor, servo motor, and BLE remote unlock. Smart Frame Lock selected (score: 108/120) over U-lock and cable grid for security, space efficiency, and user experience. Designed for tamper detection, battery monitoring, and mobile app integration.

---

## Team Contribution — Adil Syed

Role: **Coding lead** — responsible for sensor firmware development, Python implementation of occupancy detection logic, and integration with IoT transmission pipeline. Also contributed to system-level testing.

---

## Problem Context

- 30% of urban traffic congestion attributed to parking search behaviour
- ~1.3M tonnes CO₂/year from vehicles idling while searching for spaces
- Existing systems rely on manual processes with no real-time data
- OmniPark addresses this with low-cost, scalable sensor retrofit — no structural modifications required

---

## Limitations & Future Work

- Prototype and simulation validated; physical multi-bay deployment not completed within project scope
- IoT platform selection (ThingSpeak vs. Firebase vs. LoRaWAN) deferred — integration designed to be platform-agnostic
- Outdoor environmental testing (rain, direct sunlight, temperature extremes) not conducted
- Mobile booking and payment integration identified as next development phase
- EV charging bay prioritisation and air quality monitoring identified as future feature extensions

---

## Tech Stack

- **Firmware:** Python / MicroPython
- **Hardware:** Raspberry Pi Pico, HC-SR04, ESP32, servo motors
- **Simulation:** Wokwi
- **CAD:** Fusion 360
- **IoT/Cloud:** ThingSpeak, LoRaWAN (evaluated)
- **IDE:** Thonny
