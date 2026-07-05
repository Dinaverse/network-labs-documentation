# 🌐 Network Labs Documentation & CTF Writeups

> *Enterprise networking fundamentals, Cisco Packet Tracer labs, and Capture-The-Flag (CTF) challenge solutions for security research and certification preparation.*

---

## 🎯 Dual Purpose Repository

This repository serves **two complementary functions**:

1. **📖 Cisco Networking Labs** — Hands-on lab exercises for routing, switching, security, and WAN design
2. **🚩 CTF Challenge Documentation** — Detailed writeups and methodologies from Root-Me and other platforms

---

## 📚 Part 1: Cisco Packet Tracer Labs

### 🏗️ Lab Categories

| Category | Focus | Status |
|----------|-------|--------|
| **Basic Topology** | Foundational network designs (2-5 routers, switching) | ✅ Complete |
| **Routing Protocols** | OSPF, BGP, RIP, dynamic routing | ✅ Complete |
| **Switching & VLANs** | VLAN segmentation, trunking, STP, inter-VLAN routing | ✅ Complete |
| **Network Security** | ACLs, firewall rules, threat mitigation | ✅ Complete |
| **WAN Design** | Point-to-point, frame relay, VPN concepts | 🔄 In Progress |

### 🎓 Quick Navigation

**Starting out?**
- Begin: `cisco-packet-tracer-labs/basic-topology/`
- Progress: `cisco-packet-tracer-labs/routing-protocols/ospf-basic/`
- Practice: `cisco-packet-tracer-labs/security-acls/`

**CCST Preparation?**
- Core networking fundamentals
- Routing & switching operations
- Basic security configurations

**CCNA Preparation?**
- Multi-area OSPF design
- BGP fundamentals
- Advanced ACL filtering
- WAN optimization

### 📂 Lab Structure

```
cisco-packet-tracer-labs/
├── basic-topology/
│   ├── README.md                      Lab objectives
│   ├── topology.pkt                   Packet Tracer file
│   ├── topology-diagram.png           Network diagram
│   ├── configuration.md               CLI commands
│   └── verification.md                Expected results
├── routing-protocols/
│   ├── ospf-basic/
│   ├── ospf-multi-area/
│   ├── bgp-fundamentals/
│   └── rip-configuration/
├── switching-vlans/
│   ├── vlan-configuration/
│   ├── stp-optimization/
│   ├── etherchannel/
│   └── inter-vlan-routing/
├── security-acls/
│   ├── standard-acls/
│   ├── extended-acls/
│   ├── named-acls/
│   └── firewall-zones/
└── wan-design/
    ├── point-to-point/
    ├── frame-relay/
    └── vpn-tunnels/
```

### 🧪 Using the Labs

```bash
# 1. Download Cisco Packet Tracer
# https://www.netacad.com/resources/packet-tracer

# 2. Open lab file
open cisco-packet-tracer-labs/basic-topology/topology.pkt

# 3. Study configuration
cat cisco-packet-tracer-labs/basic-topology/configuration.md

# 4. Practice in simulation mode
# - Enter Simulation mode in Packet Tracer
# - Verify connectivity with ping/traceroute
# - Test configurations

# 5. Validate results
cat cisco-packet-tracer-labs/basic-topology/verification.md
```

---

## 🚩 Part 2: CTF Challenge Documentation

### 🏆 Progress Tracking

#### Root-Me PRO: Discovery Program

| Category | Progress | Status |
|----------|----------|--------|
| Programming | 4/4 | ✅ Complete |
| Network | 3/3 | ✅ Complete |
| Web Client | 4/4 | ✅ Complete |
| Web Server | 4/4 | ✅ Complete |
| Cryptography | 3/3 | ✅ Complete |
| Steganography | 3/3 | ✅ Complete |

#### Root-Me PRO: CTF Training

| Difficulty | Progress | Status |
|-----------|----------|--------|
| Easy | 15/15 | ✅ Complete |
| Medium | 10/14 | 🔄 In Progress |
| Hard | 2/7 | 🔄 In Progress |

### 📁 CTF Structure

```
ctf/
├── README.md                          (this file)
├── ctf-root-me/
│   ├── challenges/
│   │   ├── ctf-training-easy/
│   │   │   ├── challenge-001.md
│   │   │   ├── challenge-002.md
│   │   │   └── ...
│   │   ├── ctf-training-medium/
│   │   │   └── (writeups in progress)
│   │   ├── discovery-program/
│   │   │   ├── programming/
│   │   │   ├── network/
│   │   │   ├── web-client/
│   │   │   ├── web-server/
│   │   │   ├── cryptography/
│   │   │   └── steganography/
│   │   └── solutions/
│   │       └── writeups/
│   └── progress.md                   Tracking & methodology notes
└── other-platforms/                  (Future expansion)
```

### 📝 Writing a Writeup

Each writeup follows this structure:

```markdown
# Challenge Name

## Problem Statement
[Description of the challenge]

## Reconnaissance
[Information gathering phase]

## Solution Approach
[Step-by-step methodology]

## Key Concepts
- Concept 1
- Concept 2
- Concept 3

## Tools Used
- Tool 1
- Tool 2

## Lessons Learned
[Takeaways and applications]

## Resources
[References and documentation]
```

---

## 🔧 Configuration Examples

### OSPF Configuration

```cisco
router ospf 1
 network 192.168.1.0 0.0.0.255 area 0
 network 192.168.2.0 0.0.0.255 area 0
 network 10.0.0.0 0.0.0.255 area 1
 default-information originate
```

### VLAN & Trunk Configuration

```cisco
vlan 10
 name Management
vlan 20
 name Data

interface range GigabitEthernet0/1-2
 switchport mode trunk
 switchport trunk allowed vlan 10,20
```

### ACL Security

```cisco
access-list 101 permit tcp any 192.168.1.0 0.0.0.255 eq 443
access-list 101 permit tcp any 192.168.1.0 0.0.0.255 eq 80
access-list 101 deny ip any 192.168.0.0 0.0.255.255
access-list 101 permit ip any any

interface GigabitEthernet0/0
 ip access-group 101 in
```

---

## 📖 Study Guides

| Guide | Purpose |
|-------|---------|
| **[SSD Clone & GPT Guide](guides/SSD-Clone-GPT-Guide.md)** | Disk cloning & partition recovery |
| **[OSPF Configuration Guide](guides/OSPF-Configuration-Guide.md)** | Routing deep-dive |
| **[ACL Best Practices](guides/ACL-Best-Practices.md)** | Security design patterns |

---

## 🎓 Certification Targets

- **Cisco CCST** — Q3 2026
- **Cisco CCNA** — Q4 2026

### Study Path

1. Complete all basic topology labs
2. Master routing protocols (OSPF, BGP)
3. Practice switching and VLAN configurations
4. Implement security (ACLs, firewalls)
5. Design WAN topologies

---

## 🔗 Related Repositories

| Repository | Purpose |
|------------|---------|
| **[sovereign-ai-infrastructure](https://github.com/Dinaverse/sovereign-ai-infrastructure)** | Lab architecture |
| **[proxmox-homelab-setup](https://github.com/Dinaverse/proxmox-homelab-setup)** | Physical infrastructure |
| **[infrastructure-as-code-lab](https://github.com/Dinaverse/infrastructure-as-code-lab)** | Network automation |

---

## 📊 Lab Architecture Overview

```
┌──────────────────────────────────────────────────────────┐
│                  ISP / Internet                          │
└────────────────────┬─────────────────────────────────────┘
                     │
         ┌───────────┴───────────┐
         │                       │
   ┌─────▼──────┐        ┌──────▼──┐
   │ Router R1  │────────│ Router R2│  (OSPF/BGP)
   │ (Core)     │        │ (Border)│
   └──┬──────┬──┘        └──┬──────┬┘
      │      │              │      │
   ┌──▼──┐ ┌─▼──┐       ┌──┐ │   ┌─▼──┐
   │ SW1 │ │SW2 │       │FW│ │   │ SW3│
   └──┬──┘ └────┘       └──┘ │   └────┘
      │ VLAN 10,20,30        │
   ┌──┴────────────┐     ┌───▼────┐
   │   Hosts       │     │ DMZ    │
   │   PCs/Server  │     │Servers │
   └───────────────┘     └────────┘
```

---

## ✅ Operational Status

| Component | Status | Last Updated |
|-----------|--------|---|
| Cisco Labs | ✅ Active | 2026-07-05 |
| Basic Topology | ✅ Complete | 2026-07-05 |
| OSPF & BGP | ✅ Complete | 2026-07-05 |
| VLANs & Switching | ✅ Complete | 2026-07-05 |
| Security/ACLs | ✅ Complete | 2026-07-05 |
| WAN Design | 🔄 In Progress | 2026-07-05 |
| CTF Training | ✅ Active | 2026-07-05 |

---

## 📖 Documentation

| Document | Purpose |
|----------|---------|
| **[Lab Guide](guides/)** | Detailed lab instructions |
| **[Configuration Reference](configs/)** | CLI command reference |
| **[Topology Diagrams](assets/diagrams/)** | Network visualizations |
| **[CTF Writeups](ctf/)** | Challenge solutions |

---

*Network engineering fundamentals. Hands-on practice. Certification preparation. CTF methodology refinement.*
