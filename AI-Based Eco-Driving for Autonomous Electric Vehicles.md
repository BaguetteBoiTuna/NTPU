# AI-Based Eco-Driving for Autonomous Electric Vehicles

- **Authors**:
  - Dante Guillemain (711382799)
  - Jules Trolle (711333199)

## Abstract

This report explores the application of AI-powered eco-driving strategies in autonomous electric vehicles (EVs) to enhance energy efficiency, reduce emissions, and improve urban mobility. By leveraging Vehicle-to-Environment (V2E) communication systems and advanced machine learning algorithms, the project demonstrates how real-time data-driven decisions can optimize driving patterns, extend battery life, and reduce operational costs. A simulation-based approach validates the feasibility and impact of the proposed solution, comparing AI-driven eco-driving to conventional methods. The findings underscore the potential of integrating intelligent systems in EVs to address pressing environmental and economic challenges while advancing sustainable transportation.

## Introduction

### Problem Statement

The rapid adoption of electric vehicles has brought forth new challenges in optimizing energy efficiency to reduce operational costs and environmental impact. While artificial intelligence (AI) offers promising strategies for real-time eco-driving in autonomous EVs, developing fully functional AI systems requires significant resources and infrastructure. For this project, we focused on implementing a simplified algorithm within a simulated environment to demonstrate the feasibility and impact of AI-like eco-driving strategies.

### Objectives

This project aims to:

1. Explore the principles of energy-efficient eco-driving using algorithmic approaches.
2. Leverage Vehicle-to-Environment (V2E) communication concepts to improve driving efficiency in real-time within a simulated environment.
3. Validate the proposed solution through a simulation built in [Godot](https://godotengine.org/), showcasing the energy-saving potential of intelligent driving patterns.

### Importance and Value

Efficient energy management is critical for increasing EV adoption, lowering operational costs, and supporting global sustainability goals. By reducing energy consumption and emissions, eco-driving strategies contribute to cleaner urban environments and mitigate the environmental impact of transportation. Although the project’s scope is limited to a simplified simulation, the insights gained highlight the potential for future integration of fully AI-powered systems in real-world applications.

## Related Work

### AI-Driven Control Methods

AI has been extensively applied to enhance eco-driving strategies in autonomous electric vehicles. Recent studies have developed AI-based frameworks that utilize deep learning models for better control in autonomous driving, aiming to improve energy efficiency.

- Source:
  - [Artificial Intelligence Enabled Future Wireless Electric Vehicles with Multi-Model Learning and Decision Making Models](https://ieeexplore.ieee.org/document/10566002)

### Vehicle-to-Everything (V2X) Communication Systems

V2X communication enables vehicles to interact with their environment, including other vehicles, infrastructure, and pedestrians. This technology is foundational for autonomous driving, enhancing safety, efficiency, and driving experience.

- Sources:
  - [Vehicle-to-Everything Communication—The Future of Autonomous Connectivity](https://www.eetasia.com/vehicle-to-everything-communication-the-future-of-autonomous-connectivity/)
  - [Vehicle-to-Everything (V2X) Communication: A Roadside Unit for Adaptive Intersection Control of Autonomous Electric Vehicles](https://arxiv.org/abs/2409.00866)

### Challenges in Full AI Integration

Despite advancements, fully integrating AI into autonomous vehicles presents challenges, including computational complexity and real-time data accuracy. A critical evaluation of eco-driving strategies for connected autonomous electric vehicles at signalized intersections highlighted the need for efficient algorithms suitable for real-time applications.

- Source:
  - [A Critical Evaluation of Eco-Driving Strategies for Connected Autonomous Electric Vehicles at Signalized Intersections](https://ieeexplore.ieee.org/document/10294498)

## Relevance to Our Project

In our project, we utilized the Godot Engine a free and open-source game engine renowned for its versatility in 2D and 3D game development to create a simulation environment for testing eco-driving strategies in autonomous EVs.

While our approach did not involve complex machine learning models, the flexibility of Godot enabled us to script decision-making algorithms that adjust driving behaviors based on simulated environmental inputs, such as traffic signals and road conditions.

Employing Godot provided a practical platform to demonstrate the principles of eco-driving and the potential benefits of AI integration in autonomous EVs. This approach facilitated a hands-on understanding of how intelligent systems can enhance vehicle energy efficiency, even within a simplified simulation framework.

## Methodology

### 1. Problem Analysis

We identified key factors impacting energy consumption, including:

- Inefficient driving behaviors (e.g., excessive acceleration and braking).
- Lack of real-time communication between vehicles and the environment.
- Limited integration of eco-driving strategies in current systems.

This analysis informed the design of our simulation, which replicates these challenges in a controlled environment.

### 2. Solution Design

Our solution integrates:

- **Algorithmic Eco-Driving**:
  - Developed a simplified algorithm to adjust acceleration and braking based on real-time inputs.
  - Focused on optimizing driving patterns with minimal computational overhead.
- **Vehicle-to-Environment Communication**:
  - Simulated real-time data exchange (traffic lights) to influence vehicle behavior dynamically.

### 3. Simulation Development

- **Scenario Design**:
  - Created road conditions to test the algorithm, including a stop-and-go and steady cruising scenario.
- **Algorithm Integration**:
  - Integrated decision-making logic into vehicle models, fine-tuning parameters to prioritize energy efficiency.

### 4. Testing and Analysis

- **Metrics**:
  - Energy Savings: Compared energy consumption with and without the algorithm.
  - Time Efficiency: Measured scenario completion times.
