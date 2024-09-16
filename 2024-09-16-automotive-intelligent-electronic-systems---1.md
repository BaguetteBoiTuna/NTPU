---
id: 2024-09-16-automotive-intelligent-electronic-systems---1
aliases:
  - Automotive Intelligent Electronic Systems - 1
tags: []
---

# Automotive Intelligent Electronic Systems - 1

## Validating an Autonomous Vehicle Pipeline

Sensors -> Perception -> Planning -> Trajectory Execution -> Vehicle Control -> Actuators

1. Perception
   - Machine Learning Based Approach
   - ???
2. Planning
   - Randomized and Heuristic Algorithms
   - Run-Time Safety Envelopes
   - Doer/Checker Architecture
3. Trajectory Execution
   - Control Systems
   - Control Software Validation
   - Doer/Checker Architecture
4. Vehicle Control
   - Autonomy Interface To Vehicle
   - Traditional Software Validation

## [Advanced Driver Assistance Systems (ADAS)](2024-09-14-adas.md)

- Sensor Fusion
- Detection and Tracking
- Localization
- HD Maps

And other technologies such as Driving/Planning

## End-to-End Autonomous Driving and Modular Self-Driving Concepts

![[Pasted image 20240916092646.png]]

## Approaches to Autonomous Driving

1. Rule-Based
   - 100% assurance
   - Drawbacks:
     - hard to cover the unlimited traffic scenarios
     - Not scalable
     - increased complexity
2. End-to-End (AI) approach
   - more like the human driver
   - avoid the problem of handcrafting rules
   - tackle more complex traffic scenarios (corner cases, edge cases)
   - Drawbacks:
     - need to filter the training data and control the quality of training dataset
     - the effort to collect the data and data diversity
     - the resource and the time to train the large deep learning AI model
     - the assurance of the AI model robustness and safety
