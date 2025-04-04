---
id: 2024-09-16-automotive-intelligent-electronic-systems---1
aliases:
  - Automotive Intelligent Electronic Systems - 1
tags: []
---

# Automotive Intelligent Electronic Systems - 1

## Vehicle Control and Software Validation

### Control Systems

- Key focus on the **Doer/Checker Architecture** used in controlling vehicle operations, ensuring that actions are both planned and executed with checks to avoid faults.

### Control Software Validation

- Validation of control software is critical for ensuring reliability, especially in autonomous and semi-autonomous driving systems.

### Autonomy Interface

- Discusses the interface between autonomous driving software and traditional vehicle control systems.
- **Traditional Software Validation** is applied to ensure compatibility between traditional and autonomous systems.

## [Advanced Driver Assistance Systems (ADAS)](2024-09-14-adas.md)

- **Sensor Fusion**: Integrating data from multiple sensors (cameras, LiDAR, radar) for a comprehensive view of the environment.
- **Detection and Tracking**: Identifying and following objects such as vehicles, pedestrians, and road signs.
- **Localization**: Determining the precise position of the vehicle using GPS and other sensor data.
- **HD Maps**: High-definition maps that provide detailed road and environment data essential for autonomous driving.

These technologies are fundamental to **Driving and Planning** systems that make decisions based on real-time data.

---

## End-to-End Autonomous Driving and Modular Self-Driving Concepts

### Approaches to Autonomous Driving

1. **Rule-Based Approach**

   - Guarantees **100% assurance** in predictable environments but struggles with scalability.
   - **Challenges**: Unable to cover unlimited scenarios, leading to increased system complexity.

2. **End-to-End AI Approach**
   - Mimics human drivers by learning from large datasets.
   - Tackles complex traffic scenarios, including edge and corner cases.
   - **Challenges**:
     - Requires extensive and diverse training data.
     - Resource-intensive (up to 2 years to fully train an AI model).
     - Assurance and robustness of the model need rigorous testing.

![[Pasted image 20240916092646.png]]

---

## In-Vehicle Networks

In modern vehicles, communication between electronic control units (ECUs) and sensors relies on networks such as:

- **[Controller Area Network (CAN)](2024-09-09-can.md)**: Traditional protocol for reliable in-vehicle communication.
- **[FlexRay](2024-09-09-flexray.md)**: High-speed communication for drive-by-wire systems.
- **[Automotive Ethernet AVB Systems](2024-09-16-automotive-ethernet-avb-systems.md)**:
  - **Advantages**: High bandwidth, low latency, and scalability.
  - **Use**: Enables adding more sensors and computing power for real-time decision-making.

These networks are linked by **gateways** that convert data between protocols.

![[Pasted image 20240916103222.png]]

---

## The Increasing Role of Software in Vehicles

Modern vehicles are becoming more software-driven, with many traditional mechanical components being replaced by electronic systems.

![[Pasted image 20240916105452.png]]

---

## Autonomous Driving Robustness Test

- **Miles of Testing**: Extensive road testing is necessary, but most tests involve standard driving conditions, which do not fully explore critical edge cases.
- **Challenges**:
  - High cost of real-world testing.
  - Time-consuming to cover all scenarios on real roads.

### Solution

- Use **simulations** and **closed field tests** to simulate rare, critical conditions before conducting final tests on real roads, reducing costs and speeding up the process.
  [Example of Virtual test drive from NVIDIA](https://www.youtube.com/watch?v=k54P6-Innt0)

---

## Five-Layered Scenario-Based Testing

### Layered Approach to Autonomous Vehicle Testing

Testing autonomous vehicles requires simulating various scenarios that can affect vehicle behavior. This **five-layered model** provides a comprehensive approach to scenario-based testing by accounting for all the elements an autonomous vehicle might encounter.

#### **Layer 1: Roadbase**

- **Elements**: Road topology, geometry, boundaries, and surface conditions.
- **Description**: The foundational layer of the testing scenario, focusing on road structure and its physical characteristics, including elevation, curves, and surface quality.

#### **Layer 2: Infrastructure**

- **Elements**: Traffic signs, traffic lights, crosswalks, road markings.
- **Description**: This layer focuses on the permanent infrastructure that governs vehicle movement and interaction with the environment.

#### **Layer 3: Temporary Influences**

- **Examples**: Construction materials, roadblocks, and temporary signs.
- **Description**: Includes any temporary or dynamic elements introduced to the driving environment, such as roadworks or lane closures.

#### **Layer 4: Movable Objects**

- **Elements**: Vehicles, pedestrians, animals, cyclists.
- **Description**: Represents all movable objects that the vehicle must detect and react to, including other road users.

#### **Layer 5: Environmental Conditions**

- **Elements**: Weather conditions (snow, rain, fog, sunlight, wind), time of day, and seasons.
- **Description**: This layer involves environmental variables that affect visibility, road conditions, and the interaction with other layers. Environmental factors may also influence the behavior of movable objects or the visibility of infrastructure.

#### Bonus Layer 6: [Internet of Things (IoT)](2024-09-23-iot.md) and Connectivity

- Elements: Connectivity to other vehicles, infrastructure, and cloud services.
- Description: The integration of [IoT](2024-09-23-iot.md) and connectivity elements that enable V2X (Vehicle-to-Everything) communication, enhancing the vehicle's awareness and decision-making capabilities.
