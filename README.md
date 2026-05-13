# Smart Parking System — IoT Group Project

**BEng (Hons) Electrical and Electronic Engineering — Year 2 Group Project**  
Manchester Metropolitan University | 2023–24

---

## Overview

A Raspberry Pi–based smart parking system that uses ultrasonic sensors to detect vehicle presence in real time and displays live parking availability on a touchscreen dashboard. The system demonstrates an end-to-end IoT pipeline from physical sensor input to user-facing display output.

---

## System Architecture

```
Ultrasonic Sensors (HC-SR04)
        │
        ▼
Raspberry Pi (GPIO)
        │
        ├──▶ Availability logic (occupied / free per bay)
        │
        └──▶ Touchscreen dashboard (live status display)
```

---

## Features

- Real-time vehicle detection via HC-SR04 ultrasonic sensors
- Parking bay status: **Occupied / Available** per bay
- Live dashboard deployed on touchscreen display
- System demonstrated to academic staff during project presentation

---

## Hardware

| Component | Role |
|---|---|
| Raspberry Pi | Central controller + display host |
| HC-SR04 Ultrasonic Sensor(s) | Vehicle presence detection |
| Touchscreen display | Live availability output |

**Sensor principle:** HC-SR04 measures time-of-flight of ultrasonic pulse to calculate distance. A vehicle present within threshold distance (typically <200 cm) triggers an Occupied status for that bay.

---

## Software

- **Language:** Python
- **Interface:** Custom dashboard (GPIO + display output)
- **Development approach:** AI-assisted code generation used for initial scaffolding; debugging, sensor integration logic, and interface design developed and validated independently

---

## Implementation Notes

- GPIO pin configuration handled per sensor, with each bay mapped to a dedicated input
- Distance threshold calibrated to distinguish vehicle presence from background reflection
- Dashboard updates in real time as sensor state changes

---

## Limitations & Future Work

- Prototype scale — demonstrated across a small number of bays; production deployment would require sensor fusion or camera validation to reduce misclassification from non-vehicle objects within detection range
- No persistent data logging in current version — occupancy history and peak-usage analytics would be a natural extension
- Outdoor environmental testing (rain, direct sunlight, temperature variation) not conducted

---

## Tech Stack

- **Hardware:** Raspberry Pi, HC-SR04 ultrasonic sensors, touchscreen display
- **Firmware/Software:** Python
- **Development tools:** AI-assisted scaffolding (Copilot-style); manual debugging and integration
