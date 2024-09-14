---
id: 2024-09-14-network-topologies
aliases: []
tags: []
---

# Network Topologies: Passive Bus vs. Active Star

## Passive Bus Topology ^passive-bus-topology

### Description

- **Structure**: A linear communication medium where all nodes are connected to a single shared bus.
- **Communication**: Nodes transmit data over the shared bus one at a time.

### Advantages

- **Cost-Effective**
  - Minimal hardware requirements.
- **Simplicity**
  - Easy to implement and understand.

### Disadvantages

- **Single Point of Failure**
  - A fault in the bus can disrupt the entire network.
- **Limited Bandwidth**
  - Shared medium can become a bottleneck.
- **Babbling Idiot Problem**
  - A faulty node continuously transmits, monopolizing the bus and preventing others from communicating.

### Use Cases

- Suitable for small, low-cost networks where high reliability is not critical.

## Active Star Topology ^active-star-topology

### Description

- **Structure**: A central hub (active star) connects individually to each node.
- **Communication**: The hub manages data transmission between nodes.

### Advantages

- **Fault Isolation**
  - Faulty nodes can be isolated without affecting the entire network.
- **High Performance**
  - Centralized control can manage data traffic efficiently.
- **Scalability**
  - Easier to add or remove nodes without disrupting the network.

### Disadvantages

- **Higher Cost**
  - Additional hardware required for the central hub.
- **Complexity**
  - More sophisticated implementation and maintenance.

### Use Cases

- Preferred for networks requiring high reliability and fault tolerance, such as safety-critical systems in automotive and aerospace industries.

## Comparison Table

| Feature             | Passive Bus | Active Star        |
| ------------------- | ----------- | ------------------ |
| **Cost**            | Low         | High               |
| **Complexity**      | Simple      | Complex            |
| **Fault Tolerance** | Low         | High               |
| **Scalability**     | Limited     | Good               |
| **Performance**     | Moderate    | High               |
| **Maintenance**     | Easy        | Requires Expertise |

## Babbling Idiot Problem

- **Explanation**
  - Occurs when a faulty node continuously transmits data, occupying the shared bus.
- **Impact**
  - Prevents other nodes from communicating.
- **Solution in Active Star**
  - The central hub can detect and isolate the faulty node, maintaining network functionality.

## Conclusion

- **Passive Bus**
  - Best for simple, cost-sensitive applications with minimal fault tolerance requirements.
- **Active Star**
  - Ideal for complex systems where reliability and performance are critical.
