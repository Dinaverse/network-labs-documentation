# Lab: Examen Intra (Avril 2026)

## Overview
- **Student:** Mufungizi Dina Cima
- **Duration:** 4h
- **Topic:** Cisco Packet Tracer Network Implementation

## 1. Network Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **R1** | Gi0/0 | 192.168.10.1 | 255.255.255.224 | 192.168.10.30 |
| **R1** | Gi0/1 | 172.16.20.33 | 255.255.255.224 | 172.16.20.62 |
| **SW1**| VLAN 1 | 192.168.10.2 | 255.255.255.224 | 192.168.10.30 |
| **SW2**| VLAN 1 | 172.16.20.34 | 255.255.255.224 | 172.16.20.62 |
| **PC0**| NIC | 192.168.10.3 | 255.255.255.224 | 192.168.10.30 |
| **Laptop0**| NIC | 192.168.10.4 | 255.255.255.224 | 192.168.10.30 |
| **PC1**| NIC | 172.16.20.35 | 255.255.255.224 | 172.16.20.62 |
| **Laptop1**| NIC | 172.16.20.36 | 255.255.255.224 | 172.16.20.62 |

## 2. Configuration Steps
1. Design the network in Packet Tracer.
2. Default gateways are the last valid addresses in each subnet.
3. Apply standard naming conventions to all equipment.
4. Configure interface IPs and default gateways based on the table.
5. Encrypt all plain-text passwords.
6. Set enable secret password to `class1234` on all devices.
7. Configure a MOTD banner on all devices.
8. Enable and secure VTY lines with password `CISCOVTY`.
9. Backup all configurations.

## 3. Theoretical Study Notes
1. **OSI Model & PDUs:** Application (Data), Presentation (Data), Session (Data), Transport (Segments), Network (Packets), Data Link (Frames), Physical (Bits).
2. **Broadcast Addresses:**
   - 172.16.1.0/25 -> 172.16.1.127
   - 10.10.2.8/30 -> 10.10.2.11
   - 192.168.10.192/29 -> 192.168.10.199
   - 192.168.1.0/28 -> 192.168.1.15
3. **OSI Layer 3 Encapsulation:** Adds Source and Destination IP addresses.
4. **CRC Calculation:** The CRC is calculated at each hop (7 times between host A and server B) when using store-and-forward switching.
5. **MAC Address Table:** Unknown destination MAC results in flooding (broadcasting) the frame on all ports except the ingress port to locate the destination.
