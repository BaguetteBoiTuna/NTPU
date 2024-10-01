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
