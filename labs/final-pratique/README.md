# Lab: Final Pratique (Mai 2026)

## Overview
- **Duration:** 3h
- **Topic:** Cisco Packet Tracer Infrastructure & Services

## 1. Network Subnets
| Network | Network Address | CIDR |
| :--- | :--- | :--- |
| **Lan 1** | 192.168.1.0 | /27 |
| **Lan 2** | 192.168.1.32 | /27 |
| **Lan 3** | 192.168.1.64 | /26 |
| **Lan 4** | 192.168.1.130 | /27 |

## 2. General Configuration Steps
1. Assign the first address of each network as the default gateway.
2. Configure device hostnames.
3. Set enable secret password to `class1234` on all equipment.
4. Configure static IPs for all servers.
5. Configure MOTD banners.
6. Secure console and VTY lines with password `CLASSCISCO`.

## 3. Service Configurations

### A. DNS Service
- Configure to resolve: `ftp.qc.ca`, `mail1.qc.ca`, `mail2.qc.ca`, `www.exemple1.com`, `www.exemple2.com`.

### B. FTP Service
- **Task 1:** Create a text file (name/surname) on PC3 and upload to `ftp.qc.ca`.
- **Task 2:** Retrieve the file on PC5.
- **Credentials:** `user3`, `user5` (password `1234`), full access granted.

### C. SMTP Mail Service
- **Setup:** Create `USER1` on `mail1.qc.ca` and `USER2` on `mail2.qc.ca` (password `1234`).
- **Test:** Exchange emails between PC1 and PC2.

### D. DHCP Service
- Configure DHCP on the server to automatically assign IP addresses in **Lan 3**.

### 4. Backups
- Backup all configurations to the TFTP server.
