---
id: 2024-09-16-automotive_electronic_systems
aliases: []
tags: []
---

# Automotive Electronic Systems

## Unmanned Ground Vehicles (UGVs)

### Key Features

1. **Remote Operation**
   - Operate remotely without a crew.
2. **Autonomous Tasks**
   - Perform repetitive or dangerous work independently.

### Motivations

1. **Safety Limitations**
   - Cannot guarantee 100% safety with current autonomous systems.
2. **Real-Time Remote Control**
   - Remote control systems help solve traffic corner cases through video transmission.

- Self-driving vehicles struggle with awkward or unusual situations.
- **Need for Low-Latency Systems**
  - Essential for control and transmission.
- **Reliable Control Servers**
  - Must be cloud-based, secure, and dependable.
- **Reference Video**: [Control of Unmanned Ground Vehicles](https://www.youtube.com/watch?v=0i7xzM9ybNk)

## Current State of Automotive Electronic Systems

### Example: VW Phaeton

- **Electrical Components**: 11,136 components.

#### Communication Systems

- **ECUs**: 61 [ECUs](2024-09-09-ecu.md) in total.
  - External diagnosis for 31 [ECUs](2024-09-09-ecu.md) via serial communication.
- **Optical Bus**
  - Used for high-bandwidth infotainment data.
- **Proprietary Serial Bus**
  - Sub-networks based on proprietary technology.
- **[CAN Buses](2024-09-09-can.md)**
  - 35 [ECUs](2024-09-09-ecu.md) connected via 3 [CAN buses](2024-09-09-can.md).

#### Data Sharing

- Approximately 2,500 signals in 250 [CAN](2024-09-09-can.md) messages.

## Expansion of Automotive Electronics

- **Innovation Source**
  - Over 90% of automotive innovation comes from electronics.
- **Trend**
  - Embedding electronic systems and silicon components (transistors, microprocessors, diodes) into vehicles.

## Automotive Electronic Applications

### Electronics Content Cost in Manufacturing

- **2002**: 20-25%
- **2010**: 30-35%
- **2020**: 35-40%
- **2030 (Estimated)**: Around 50%

## Drive-by-Wire Technology

### Benefits

- **Weight and Cost Reduction**
- **Energy Saving**
  - Less mass means lower energy consumption.
- **Improved Performance**
  - Faster response times.
- **Accurate Vehicle Control**
- **Intelligent Functions**
- **Enhanced Stability and Safety**

### Challenges

- **Design Complexity**
  - Function verification is intricate.
- **Real-Time Constraints**
- **Fault Tolerance**
- **Robustness and Safety Validation**
  - Requires advanced design platforms and tool frameworks.
- **Safety Standards**
  - Compliance with evolving regulations.

#### Industry Impact

- **Safety Concerns**
  - Hinder widespread adoption of smart vehicles globally.
- **Government Hesitation**
  - Reluctance due to reliability issues.
- **Maturity of Systems**
  - Electronic systems need to be fully reliable.
- **Regulatory Requirements**
  - Companies must prove 100% safety and reliability.
- **Focus on Safety**
  - Increased emphasis on safety standards and reliability in development.

## Global Megatrends in Automotive Industry

1. **Connectivity**
   - Average of one hour per day spent in vehicles.
2. **Autonomy**
   - 1.3 million global road fatalities annually.
3. **Electrification**
   - U.S. mandates:
     - 163 grams/mile CO₂ emissions.
     - 54.5 mpg fuel efficiency by 2025.

## Automotive Advancements

### Today

- **Distributed Architectures**
- **Incompatible Silicon and Software**
- **Security Challenges**
  - Over-the-air updates are not fully secure.
- **Inefficient Development**
- **Limited Upgradeability**
  - Systems are not easily scaled or updated.

### Tomorrow

- **High-Performance Domain Architectures**
- **Increased Network Capacity**
- **Secure Over-the-Air Updates**
- **Efficient Development Processes**
- **Upgradable Platforms**
  - Scalable and future-proof solutions.

## Levels of Driving Automation

0. **No Automation**
   - Driver only; dashboard warnings.
1. **Driver Assistance**
   - Features: Adaptive cruise control, lane centering, autonomous braking.
2. **Partial Automation**
   - Features: Traffic jam assist, parking assist.
3. **Conditional Automation**
   - Features: Highway pilot, traffic jam pilot, parking pilot.
4. **High Automation**
   - Self-driving car (SDC) with driver control.
5. **Full Automation**
   - Driverless car (DLC); no driver control.
   - Concept: Car as a Service (CaaS).
