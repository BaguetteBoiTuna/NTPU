---
id: 2024-09-24-daftds_part1ch1re
aliases:
  - DAFTDS_Part1Ch1RE
tags: []
---

# DAFTDS_Part1Ch1RE

## Functional Safety Concept

IEC 61508 is an international standard that provides a framework for ensuring the functional safety of electrical, electronic and programmable electronic systems.

![[IEC-61508.png]]

The key feature of IEC 61508 is the concept of [**Safety Integrity Levels (SILs)**](2024-09-24-sil.md), which categorize the required safety measures based on the likelihood and potential severity of system failures. There are four [SIL](2024-09-24-sil.md) levels, from [SIL](2024-09-24-sil.md) 1 (lowest safety level) to [SIL](2024-09-24-sil.md) 4 (highest), each associated with a progressively lower probability of dangerous failures.

## [Faults](2024-09-24-fault.md), [Errors](2024-09-24-error.md) and [Failures](2024-09-24-failure.md) Detailed to the Core

If you want to know more about the concepts of [Faults](2024-09-24-fault.md), [Errors](2024-09-24-error.md) and [Failures](2024-09-24-failure.md) in depth, you can check the following links:

**[Fault](2024-09-24-fault.md)** -> **[Error](2024-09-24-error.md)** -> **[Failure](2024-09-24-failure.md)**

## The domain of service failure

In the domain of **service failure**, the following are key failure types that impact system reliability and functionality:

1. **Content Failures**: These occur when the system provides incorrect or corrupt outputs. The service continues to operate, but the content it delivers is erroneous. An example would be a system returning incorrect data due to calculation errors.

2. **Timing Failures**: These happen when a system fails to meet its required timing constraints, such as deadlines. Even if the correct data is generated, delivering it too late or too early can make the service unusable. Real-time systems, like control systems in aircraft, are particularly vulnerable to timing failures.

3. **Halt Failures**: In this type of failure, the service stops functioning entirely. The system halts without providing further output or progress. This can be due to critical software errors or hardware malfunctions.

4. **Erratic Failures**: These occur when the system behaves unpredictably or inconsistently, such as delivering random outputs or oscillating between functioning and failing states. This type of failure is particularly dangerous because it is hard to diagnose and resolve.

These failure modes are critical in designing reliable, [fault-tolerant](2024-09-10-fault-tolerance.md) systems, especially in safety-critical environments.

