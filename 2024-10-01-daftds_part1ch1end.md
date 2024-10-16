---
id: 2024-10-01-daftds_part1ch1end
aliases:
  - DAFTDS_Part1Ch1END
tags: []
---

# DAFTDS_Part1Ch1END

## Hardware and Software Redundancy

### Hardware Redundancy

Hardware redundancy involves adding extra or spare components to override the effects of a faulty or failed component, ensuring continued operation. It is a key technique in [Fault Tolerance](2024-09-10-fault-tolerance.md).

#### Types of Hardware Redundancy

- **Static Hardware Redundancy**: Redundant components are always active and immediately take over in the event of a failure. Example: using three processors where their outputs are compared to detect a faulty processor.
- **Dynamic Hardware Redundancy**: Redundant components are only activated upon failure. Example: a spare processor activated when the primary processor fails.
- **Hybrid Hardware Redundancy**: A combination of both static and dynamic redundancy.

#### Common Redundancy Configurations

- **TMR (Triple Modular Redundancy)**: Uses three copies of the same hardware, with the output determined by majority voting.
- **NMR (N Modular Redundancy)**: Extends TMR to N copies, using majority voting for output.
- **Duplication with Comparison**: Involves two copies of the hardware for fault detection by comparing their outputs. This method only detects faults but does not tolerate them.

### Software Redundancy

Software redundancy is another [fault tolerance](2024-09-10-fault-tolerance.md) technique that involves writing multiple versions of software that perform the same function. The outputs of these versions are compared to detect discrepancies, allowing the system to take corrective action. This approach is used in safety-critical systems, such as aircraft control.

#### Key Points

- **N-version Programming**: Multiple teams develop different versions of software to increase fault tolerance.
- **Cost Considerations**: Software redundancy can be less expensive than hardware redundancy when hardware is costly, but it is more complex to implement and requires multiple development teams.

### Information Redundancy

Information redundancy involves adding extra data to detect and correct errors, often used in error detection and correction codes. For example, a parity bit can be added to a byte of data. Information redundancy is commonly used in RAID systems to enhance fault tolerance, and it typically requires hardware redundancy to process additional check bits.

### Time Redundancy

Time redundancy involves processing the same data multiple times to detect and correct errors. For instance, a system might process the same data twice and compare the results to detect discrepancies. Time redundancy is often used alongside other redundancy techniques to enhance fault tolerance. It is especially useful in dealing with transient failures, where re-executing an operation can resolve the issue.

However, it can increase overhead and latency, making it a trade-off in systems with time-sensitive operations.

### Dependability and Security Attributes

- **Availability**: Readiness for correct service.
- **Reliability**: Continuity of correct service.
- **Safety**: Absence of catastrophic consequences for users and the environment.
- **Integrity**: Protection against improper system alterations.
- **Maintainability**: The system's ability to undergo modifications and repairs.

---

## Goals of Fault Tolerance

### Reliability

- **Assumption**: Faults are inevitable in complex systems. The system can be in one of two states: "up" and "down"
- **Examples**:

  - A Light Bulb is either functional or burnt out.
  - A Wire is either connected or broken.

- **Reliability, R(t)**: The probability that the system is up during the whole interval [0, t], given it was up at time 0.

- **Related measure**:
  - **Mean Time To Failure (MTTF)**: Average time the system remains up before it goes dow and has to be repaired or replaced.

### Availability

Availability is used in systems with downtime.

- **Availability, A(t)**: Fraction of time system is up during the interval [0, t].

- **Availability Point, Ap(t)**: Probability that the system is up at time t, given it was up at time 0.

- **Long-Term Availability, A**: ![[Pasted image 20241001115041.png]]

- **Related measures**:
  - **Mean Time To Repair (MTTR)**: Average time to repair a failed system.
  - **Mean Time Between Failures (MTBF)**: Average time between failures. MTBF = MTTF + MTTR.
    ![[Pasted image 20241001115319.png]]

### Safety

- **Safety, S(t)**: Probability that the system is either up or in a failure state but safe, i.e. the failure won't cause the hazard during the whole interval [0, t], given it was up at time 0.

