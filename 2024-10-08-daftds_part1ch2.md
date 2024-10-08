---
id: 2024-10-08-daftds_part1ch2
aliases:
  - DAFTDS_Part1Ch2
tags: []
---

# DAFTDS_Part1Ch2

## Fault Behavior Diagram: Simplified Overview

### What is a Fault Behavior Diagram?

A Fault Behavior Diagram (FBD) is a graphical representation used to illustrate how faults impact a system. It helps visualize the flow from a fault occurring to how the system responds or fails.

### Key Components of an FBD:

- **Fault Sources**: Points where faults may originate, such as hardware failures, software errors, or external disturbances.
- **Fault Propagation Paths**: Arrows or lines showing how a fault moves through the system, potentially affecting different components.
- **System Reactions**:
  - **Detection**: When the system identifies the occurrence of a fault.
  - **Isolation**: Mechanisms that isolate the fault to prevent it from spreading.
  - **Recovery**: How the system attempts to recover, such as switching to backup components.
- **Failure States**: Represent the final state if the system fails to recover from the fault.

### Understanding the Flow

- **Fault Occurrence → Detection → (Isolation or Mitigation) → Recovery or Failure**
  - If the system successfully detects and handles the fault, it can often **recover**.
  - If the fault is not handled correctly, the system may reach a **failure state**.

### Example Scenario

Imagine a **power supply failure** in a computer.

- The **detection** unit recognizes the issue.
- The system attempts to **switch** to an alternative power supply.
- If successful, the system **recovers**. If not, it results in a **system shutdown** (failure state).
