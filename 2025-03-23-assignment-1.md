---
id: 2025-03-23-assignment-1
aliases:
  - Assignment 1
tags: []
---

# Assignment 1

Student ID: 711382799

## Objective

The goal of this assignment is to build a smart room automation system using IoT principles. This project demonstrates how to monitor and regulate environmental conditions (temperature, light, and humidity) using sensors and actuators integrated with an Arduino.

## Components Overview

#### NOTE /!\

Since I did not find a humidity sensor in tinkercad, I used a potentiometer to simulate humidity changes.

### Sensors

- **Temperature Sensor: TMP36**

  - **Measurement Range:** Approximately -40°C to +125°C
  - **Output:** Analog voltage
  - **Conversion Formula:**

    ```cpp
    float temperature = (voltage - 0.5) * 100.0;
    ```

  - **Wiring:**
    - Left pin → **5V**
    - Middle pin → **A0**
    - Right pin → **GND**

- **Light Sensor: Photoresistor**

  - **Function:** Varies its resistance with ambient light
  - **Wiring as Voltage Divider:**
    - One terminal → **5V**
    - Other terminal → **A1** (via junction with a resistor)
    - The free end of the resistor → **GND**

- **Humidity Sensor (Simulated): Potentiometer**
  - **Function:** Acts as a variable resistor, simulating humidity changes
  - **Wiring:**
    - One outer pin → **5V**
    - Middle (wiper) → **A2**
    - Other outer pin → **GND**

### Actuators

These are simulated with **LEDs** to represent:

- **Fan** (Digital Pin 3) – turns on when temperature > **25°C**
- **Room Light** (Digital Pin 4) – turns on when light level is low (reading < **500**)
- **Dehumidifier** (Digital Pin 5) – turns on when humidity (simulated) is low (reading < **300**)

Each LED is connected as follows:

- **Anode (long leg)** → Assigned Arduino pin
- **Cathode (short leg)** → **resistor** → **GND**

### Flowchart

No included flowchart since the circuit is simple and the code is straightforward.
