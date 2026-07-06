# 🌐 OSPF Configuration Guide

> *Open Shortest Path First (OSPF) routing protocol fundamentals, multi-area design, and hands-on configuration for enterprise networks.*

---

## 📖 Overview

OSPF is a link-state Interior Gateway Protocol (IGP) used for dynamic routing in enterprise networks. This guide covers:

- **OSPF Basics** — Single-area and multi-area topologies
- **Configuration** — Router setup, network advertisements, and area design
- **Optimization** — Cost metrics, priority, and convergence tuning
- **Troubleshooting** — Common issues and verification techniques

---

## 🎯 Prerequisites

- Basic understanding of IP addressing and subnetting
- Cisco router or Packet Tracer simulation environment
- Familiarity with CLI configuration mode

---

## 📚 Part 1: OSPF Fundamentals

### What is OSPF?

**OSPF (Open Shortest Path First)** is:
- **Link-state protocol** — Uses SPF (Shortest Path First) algorithm
- **Dynamic routing** — Automatically adapts to network changes
- **Classless** — Supports CIDR and variable-length subnet masks (VLSM)
- **Fast convergence** — Detects failures and recalculates routes in seconds
- **Open standard** — RFC 2328 (OSPFv2) and RFC 5340 (OSPFv3)

### OSPF Metrics: Cost

```
Cost = 100 Mbps / Interface Bandwidth (in Mbps)

Examples:
- 10 Mbps link:  Cost = 100 / 10 = 10
- 100 Mbps link: Cost = 100 / 100 = 1
- 1 Gbps link:   Cost = 100 / 1000 = 0.01 (rounded to 1)
```

Lower cost = preferred path

### OSPF Areas

OSPF uses **hierarchical areas** to scale to large networks:

```
┌──────────────────────────────────┐
│      Backbone Area (Area 0)      │
│  (All inter-area traffic passes) │
├──────────────────────────────────┤
│   Area 1        │   Area 2       │
│  (Intraarea)    │ (Intraarea)    │
└──────────────────────────────────┘
```

- **Area 0 (Backbone)** — Central area connecting all others
- **Non-backbone areas** — Connected to backbone via Area Border Router (ABR)

---

## 🔧 Part 2: Basic OSPF Configuration

### Single-Area OSPF (Area 0)

#### Step 1: Enable OSPF Process

```cisco
Router(config)# router ospf 1
Router(config-router)# 
```

Process ID (1) is locally significant; doesn't need to match other routers.

#### Step 2: Define Networks to Advertise

```cisco
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# network 192.168.2.0 0.0.0.255 area 0
Router(config-router)# network 10.0.0.0 0.0.0.255 area 0
```

**Wildcard Mask** = Inverse of subnet mask
- Subnet: 255.255.255.0 → Wildcard: 0.0.0.255
- Subnet: 255.255.0.0 → Wildcard: 0.0.255.255

#### Step 3: Configure Router ID (Optional)

```cisco
Router(config-router)# router-id 192.168.1.1
```

Router ID is used to identify the router in OSPF adjacencies. Best practice: use a loopback address.

#### Step 4: Save Configuration

```cisco
Router# write memory
```

---

## 🌳 Part 3: Multi-Area OSPF Configuration

### Scenario: Two Areas Connected via Backbone

**Topology:**
```
Area 1                  Area 0 (Backbone)              Area 2
┌────────┐             ┌──────────────┐             ┌────────┐
│ Router1├─────────────┤ ABR Router   ├─────────────┤Router3│
│ (Area1)│             │ (Area 0 & 1) │             │(Area2)│
└────────┘             └──────────────┘             └────────┘
```

### Configuration on Area 1 Router (R1)

```cisco
Router1(config)# router ospf 1
Router1(config-router)# router-id 1.1.1.1
Router1(config-router)# network 192.168.1.0 0.0.0.255 area 1
Router1(config-router)# network 10.0.1.0 0.0.0.255 area 1
```

### Configuration on ABR Router (Backbone)

```cisco
ABR(config)# router ospf 1
ABR(config-router)# router-id 10.0.0.1
ABR(config-router)# network 10.0.0.0 0.0.0.255 area 0
ABR(config-router)# network 10.0.1.0 0.0.0.255 area 1
ABR(config-router)# network 10.0.2.0 0.0.0.255 area 0
```

### Configuration on Area 2 Router (R3)

```cisco
Router3(config)# router ospf 1
Router3(config-router)# router-id 3.3.3.3
Router3(config-router)# network 192.168.3.0 0.0.0.255 area 2
Router3(config-router)# network 10.0.2.0 0.0.0.255 area 2
```

---

## 🎛️ Part 4: Advanced Configuration

### Interface-Level Priority (Election of Designated Router)

```cisco
Router(config-if)# ip ospf priority 100
```

Higher priority wins DR election (default: 1). Priority 0 = never become DR.

### Changing OSPF Cost

```cisco
Router(config-if)# ip ospf cost 50
```

Manual cost override for fine-tuning path selection.

### OSPF Timers: Hello & Dead Intervals

```cisco
Router(config-if)# ip ospf hello-interval 5
Router(config-if)# ip ospf dead-interval 20
```

- **Hello interval** — Frequency of hello packets (default: 10s)
- **Dead interval** — Time before neighbor is considered down (default: 40s, typically 4× hello)

### Default Route Propagation

```cisco
Router(config-router)# default-information originate
```

Advertises 0.0.0.0/0 to all OSPF neighbors (useful for edge routers).

---

## ✅ Part 5: Verification Commands

### View OSPF Neighbors

```cisco
Router# show ip ospf neighbor

Neighbor ID     Pri   State           Dead Time   Address         Interface
10.0.0.1        1     FULL/DR         00:00:38    10.0.1.2        FastEthernet0/0
```

**States:**
- **DOWN** — No hello received
- **ATTEMPT** — Initial contact
- **INIT** — One-way communication
- **2-WAY** — Bidirectional communication
- **EXSTART** — Database synchronization starting
- **EXCHANGE** — Exchanging DBD packets
- **LOADING** — Requesting LSAs
- **FULL** — Fully adjacent (ready to exchange data)

### View OSPF Routes

```cisco
Router# show ip route ospf

O       192.168.2.0 [110/100] via 10.0.1.2, 00:05:12, FastEthernet0/0
O IA    10.0.2.0 [110/150] via 10.0.1.2, 00:05:12, FastEthernet0/0
```

- **O** — OSPF intra-area route
- **O IA** — OSPF inter-area route
- **[110/X]** — Administrative Distance 110, Metric X

### View OSPF Database

```cisco
Router# show ip ospf database

OSPF Router with ID (192.168.1.1) (Process ID 1)

Router Link States (Area 1)

  LS age: 120
  Options: (No TOS-capability, DC)
  LS Type: Router Links
  Link State ID: 192.168.1.1
  Advertising Router: 192.168.1.1
```

### Debug OSPF Adjacency

```cisco
Router# debug ip ospf adj

OSPF: Rcv hello from 10.0.0.1 area 0 from FastEthernet0/0 10.0.1.2
OSPF: 2 Way Communication to 10.0.0.1, state 2WAY
OSPF: End of hello processing
```

---

## 🔍 Part 6: Troubleshooting

### Issue: Neighbors Not Forming (Stuck in DOWN/ATTEMPT)

**Verify:**
1. Physical connectivity
```cisco
Router# ping 10.0.1.2
```

2. OSPF enabled on interface
```cisco
Router# show ip ospf interface
```

3. Network statements correct
```cisco
Router# show ip ospf
```

4. Hello/Dead intervals match
```cisco
Router# show ip ospf interface detail
```

5. MTU (Maximum Transmission Unit) mismatch
```cisco
Router# show ip ospf interface | include MTU
```

### Issue: Routes Not Appearing

**Check:**
1. Neighbors are FULL state
```cisco
Router# show ip ospf neighbor
```

2. Networks advertised
```cisco
Router# show ip ospf database router
```

3. Routing table
```cisco
Router# show ip route
```

### Issue: Slow Convergence

**Optimize:**
- Reduce hello interval (faster detection)
- Reduce dead interval accordingly
- Lower SPF timers (advanced tuning)

```cisco
Router(config-router)# timers throttle spf 50 300 5000
```

---

## 📊 OSPF Packet Types

| Packet Type | Purpose |
|------------|---------|
| **Hello** | Neighbor discovery and keepalive |
| **DBD** | Database description (initial sync) |
| **LSR** | Link State Request |
| **LSU** | Link State Update (route propagation) |
| **LSAck** | Acknowledgment |

---

## 🎓 Best Practices

1. **Use loopback interfaces for Router IDs** — Stable, never goes down
2. **Place ABRs in backbone** — Simplifies multi-area design
3. **Limit area size** — Keep areas under 50-100 routers
4. **Monitor convergence time** — Critical for failover scenarios
5. **Use OSPF cost strategically** — Prefer higher-bandwidth links
6. **Match timers across neighbors** — Prevents adjacency flapping

---

## 🔗 Related Resources

- **[Cisco OSPF Fundamentals](https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/)** — Official documentation
- **[RFC 2328 - OSPFv2](https://tools.ietf.org/html/rfc2328)** — Protocol specification
- **[network-labs-documentation](https://github.com/Dinaverse/network-labs-documentation)** — Hands-on labs

---

*OSPF: The foundation of enterprise routing. Design, configure, optimize.*
