---
id: 2024-10-01-daftds_part1ch1end
aliases:
  - DAFTDS_Part1Ch1END
tags: []
---

# DAFTDS_Part1Ch1END

## Hardware Redundancy

To override the effects of a faulty failed component we can add extra hardware/spare components, that is called hardware redundancy. It is a technique of [Fault Tolerance](2024-09-10-fault-tolerance.md).

- **Static Hardware Redundancy**: for immediate making of a failure, the redundant components are always active. For example using 3 processors that check the output to find if a single processor is faulty.
- **Dynamic Hardware Redundancy**: the redundant components are activated only when a failure occurs. For example, a spare processor that is activated when the main processor fails.
- **Hybrid Hardware Redundancy**: a combination of both static and dynamic redundancy.

You can also have different types of hardware redundancy like:

- TMR (Triple Modular Redundancy): 3 copies of the same hardware, the output is decided by majority voting.
- NMR (N Modular Redundancy): N copies of the same hardware, the output is decided by majority voting.
- Duplication with Comparison: 2 copies of the same hardware that are compared. It provides fault detection but not fault tolerance.

---

## Software Redundancy

Another [fault tolerant](2024-09-10-fault-tolerance.md) technique. It involves writing multiple versions of the software that perform the same function. The outputs of these versions are compared to detect any discrepancies. If a discrepancy is found, the system can take corrective action. It is used in safety-critical systems like aircraft control systems.

It can be cheaper than hardware redundancy if the hardware is expensive. However, it can be more complex to implement and may introduce additional overhead. You also have to hire multiple teams of developers to write the redundant software.

It is also called N-version programming.

---

## Information Redundancy

Adding extra information to the data to detect and correct errors. It is used in error detection and correction codes. For example, adding a parity bit to a byte of data. Information redundancy is also used in RAID systems to provide fault tolerance. Information redundancy often requires hardware redundancy to process the additional check bits.

---

## Time Redundancy

Processing the same data multiple times to detect and correct errors. For example, a system can process the same data twice and compare the results. If the results are different, the system can take corrective action. Time redundancy can be used in conjunction with other redundancy techniques to improve fault tolerance. Most failures are transient and can be corrected by re-executing the operation.

If enough slack time is available, the system can re-execute the operation multiple times to ensure the correct result. Time redundancy can be used to improve the reliability of critical operations. However, it can introduce additional overhead and latency.

---

## Dependability and Security attributes

- **Availability**: readiness for correct service.
- **Reliability**: continuity of correct service.
- **Safety**: absence of catastrophic consequences on the user(s) and the environment.
- **Integrity**: absence of improper system alterations.
- **Maintainability**: ability to undergo modifications and repairs.
