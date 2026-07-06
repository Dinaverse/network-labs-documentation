# 🛡️ ACL Best Practices Guide

> *Access Control Lists (ACLs) for network security, traffic filtering, and firewall rule design in enterprise environments.*

---

## 📖 Overview

Access Control Lists (ACLs) are fundamental security tools for controlling traffic flow through routers and switches. This guide covers:

- **ACL Basics** — Standard, extended, and named ACLs
- **Best Practices** — Rule ordering, efficiency, and security design
- **Common Use Cases** — Traffic filtering, security policies, QoS marking
- **Troubleshooting** — Debugging and verification techniques

---

## 🎯 Prerequisites

- Basic understanding of IP addresses, protocols, and ports
- Cisco router or Packet Tracer simulation environment
- Familiarity with CLI configuration

---

## 📚 Part 1: ACL Fundamentals

### What is an ACL?

An **Access Control List (ACL)** is:
- A set of permit/deny rules applied to router interfaces
- **Ordered list** — Rules evaluated top-to-bottom; first match wins
- **Direction-based** — Applied inbound or outbound on an interface
- **Stateless** — Each packet evaluated independently (no connection tracking)

### ACL Types

| Type | Number Range | Matches | Use Case |
|------|----------|---------|----------|
| **Standard** | 1-99, 1300-1399 | Source IP only | Simple blocking |
| **Extended** | 100-199, 2000-2699 | Source, destination, protocol, port | Precise filtering |
| **Named** | Text name | Same as standard/extended | Readable, maintainable |

### ACL Logic

```
Inbound ACL                    Outbound ACL
┌──────────────────┐          ┌──────────────────┐
│ Incoming Packet  │          │  Outgoing Packet │
└────────┬─────────┘          └────────┬─────────┘
         │                             │
    Check ACL Rules              Check ACL Rules
    (Top to Bottom)              (Top to Bottom)
         │                             │
    ┌────┴────┐                   ┌────┴────┐
    │ Match?  │                   │ Match?  │
    └────┬────┘                   └────┬────┘
         │                             │
    Permit/Deny                   Permit/Deny
         │                             │
    ┌────┴────┐                   ┌────┴────┐
    │ Forward │                   │  Send   │
    │ to Next │                   │ Out Int │
    │ Hop     │                   │         │
    └─────────┘                   └─────────┘
```

**Critical Rule:** If no match found → implicit deny (default)

---

## 🔧 Part 2: Standard ACLs

### Use Case: Block a Specific Subnet

**Scenario:** Block traffic from 192.168.5.0/24 network

```cisco
Router(config)# access-list 10 deny 192.168.5.0 0.0.0.255
Router(config)# access-list 10 permit any
Router(config)# interface FastEthernet0/0
Router(config-if)# ip access-group 10 in
```

### Explanation

```
ACL 10:
  Line 1: deny 192.168.5.0 0.0.0.255   ← Packets from 192.168.5.0/24 → DROPPED
  Line 2: permit any                    ← All other packets → ALLOWED
  
Implicit: deny any                       ← Default (if no explicit permit)
```

### Best Practice: Always End with Permit Any

```cisco
access-list 10 deny 192.168.10.0 0.0.0.255
access-list 10 permit any
```

Without `permit any`, all traffic is implicitly denied after the first rule.

---

## 🔧 Part 3: Extended ACLs

### Extended ACL Syntax

```cisco
access-list 100 {permit|deny} {protocol} {source} {source-wildcard} 
                 {destination} {destination-wildcard} 
                 {protocol-options} [log]
```

### Use Case 1: Allow Web Traffic Only

**Scenario:** Allow HTTP (port 80) and HTTPS (port 443) from any source to 10.0.1.5

```cisco
Router(config)# access-list 101 permit tcp any 10.0.1.5 eq 80
Router(config)# access-list 101 permit tcp any 10.0.1.5 eq 443
Router(config)# access-list 101 deny ip any any log
Router(config)# interface FastEthernet0/0
Router(config-if)# ip access-group 101 in
```

### Use Case 2: Block P2P Applications

**Scenario:** Block BitTorrent (ports 6881-6889)

```cisco
Router(config)# access-list 102 deny tcp any any range 6881 6889
Router(config)# access-list 102 deny udp any any range 6881 6889
Router(config)# access-list 102 permit ip any any
```

### Use Case 3: Deny SSH from Specific Subnet

**Scenario:** Block SSH (port 22) from 192.168.10.0/24 to internal servers

```cisco
Router(config)# access-list 103 deny tcp 192.168.10.0 0.0.0.255 any eq 22
Router(config)# access-list 103 permit ip any any
Router(config)# interface FastEthernet0/1
Router(config-if)# ip access-group 103 out
```

---

## 📛 Part 4: Named ACLs (Best Practice)

Named ACLs are more readable and maintainable than numbered ACLs.

### Named Extended ACL Example

```cisco
Router(config)# ip access-list extended ALLOW_WEB_TRAFFIC
Router(config-ext-nacl)# permit tcp any 10.0.1.5 eq 80
Router(config-ext-nacl)# permit tcp any 10.0.1.5 eq 443
Router(config-ext-nacl)# deny ip any any
Router(config-ext-nacl)# exit

Router(config)# interface FastEthernet0/0
Router(config-if)# ip access-group ALLOW_WEB_TRAFFIC in
```

### Advantages of Named ACLs

✅ **Readable** — `ALLOW_WEB_TRAFFIC` vs `101`  
✅ **Modifiable** — Edit rules without recreating  
✅ **Maintainable** — Self-documenting code  

### Modifying a Named ACL

```cisco
Router(config)# ip access-list extended ALLOW_WEB_TRAFFIC
Router(config-ext-nacl)# no 3
Router(config-ext-nacl)# 3 permit tcp any 10.0.1.6 eq 443
Router(config-ext-nacl)# exit
```

---

## 🎛️ Part 5: ACL Best Practices

### Rule 1: Order Rules from Specific to General

❌ **Bad:**
```cisco
access-list 100 permit any any any
access-list 100 deny 192.168.10.0 0.0.0.255 any
```
(First rule permits everything; second rule never executes)

✅ **Good:**
```cisco
access-list 100 deny 192.168.10.0 0.0.0.255 any
access-list 100 permit any any any
```

### Rule 2: Place ACLs Close to Source

**For deny rules:** Place on interface near the **source** of unwanted traffic  
**For permit rules:** Place on interface near the **destination** of required traffic

```
                    Router A
                    (Has ACL)
                       │
         Source ─────────┘  ← Deny rule here (close to source)
        
        vs.
        
                   Router A ──── Router B ──── Router C
                                (Has ACL)
                                   │
                           Destination ← Permit rule here (close to destination)
```

### Rule 3: Use Descriptive Rule Logging

```cisco
access-list 100 deny tcp 192.168.10.0 0.0.0.255 10.0.1.5 eq 22 log
access-list 100 permit ip any any
```

**`log`** keyword logs denied packets (useful for troubleshooting).

### Rule 4: Avoid Overlapping Ranges

❌ **Bad:**
```cisco
access-list 100 permit tcp any any range 80 443
access-list 100 permit tcp any any range 400 500
```
(Overlapping if traffic uses ports 400-443)

✅ **Good:**
```cisco
access-list 100 permit tcp any any range 80 443
access-list 100 permit tcp any any range 444 500
```

### Rule 5: Document Every ACL

```cisco
! ===== ALLOW_WEB_TRAFFIC =====
! Purpose: Allow HTTP/HTTPS to web server 10.0.1.5
! Applied: FastEthernet0/0 inbound
! Last modified: 2026-07-05
! ==============================
access-list 100 permit tcp any 10.0.1.5 eq 80
access-list 100 permit tcp any 10.0.1.5 eq 443
access-list 100 deny ip any any log
```

---

## 📊 Part 6: Common Protocols & Ports

| Protocol | Port | Service |
|----------|------|---------|
| **TCP 21** | FTP | File Transfer |
| **TCP 22** | SSH | Secure Shell |
| **TCP 23** | Telnet | Insecure Remote Access |
| **TCP 25** | SMTP | Email Sending |
| **TCP 53** | DNS | Domain Names (TCP) |
| **UDP 53** | DNS | Domain Names (UDP) |
| **TCP 80** | HTTP | Web |
| **TCP 443** | HTTPS | Secure Web |
| **TCP 3306** | MySQL | Database |
| **TCP 3389** | RDP | Remote Desktop (Windows) |

---

## ✅ Part 7: Verification & Troubleshooting

### View Applied ACLs

```cisco
Router# show access-list

Standard IP access list 10
    10 deny 192.168.5.0, wildcard bits 0.0.0.255
    20 permit any

Extended IP access list 100
    10 permit tcp any 10.0.1.5 eq http (2 matches)
    20 permit tcp any 10.0.1.5 eq 443 (1 match)
    30 deny ip any any log (5 matches)
```

### View ACL on Interface

```cisco
Router# show ip access-list interface FastEthernet0/0

FastEthernet0/0:
  Inbound access list is 100
  Outbound access list is not set
```

### Check Packet Match

```cisco
Router# show access-list 100

Extended IP access list 100
    10 permit tcp any 10.0.1.5 eq 80 (7 matches)
    20 permit tcp any 10.0.1.5 eq 443 (3 matches)
    30 deny ip any any log (5 matches)
```

Matches show how many packets matched each rule.

### Debug ACL

```cisco
Router# debug ip packet detail

*Mar  1 00:15:23.456: IP: s=192.168.10.5 (FastEthernet0/0), 
    d=10.0.1.5, len 60, access denied
```

---

## 🚨 Common Issues & Solutions

### Issue: Traffic Being Blocked When It Should Pass

**Check:**
1. Verify ACL exists
```cisco
show access-list ACL_NAME
```

2. Verify ACL applied to correct interface/direction
```cisco
show ip access-list interface
```

3. Verify rule order (first match wins)
```cisco
show access-list
```

4. Check for implicit deny
```cisco
access-list 100 permit ...
access-list 100 permit any  ← Add if missing
```

### Issue: ACL Matches Not Incrementing

**Cause:** ACL may not be applied to interface
```cisco
show ip access-list interface FastEthernet0/0
```

**Solution:** Apply ACL to interface
```cisco
interface FastEthernet0/0
ip access-group 100 in
```

### Issue: Performance Degradation

**Cause:** Large ACLs processed on every packet  
**Solution:** Place ACLs closer to source, use hardware ACL processing (ASA)

---

## 🎓 Security Design Patterns

### Pattern 1: Default Deny (Zero Trust)

```cisco
! Deny everything by default, explicitly permit what's needed
access-list 100 permit tcp 10.0.0.0 0.0.0.255 10.0.1.5 eq 80
access-list 100 permit tcp 10.0.0.0 0.0.0.255 10.0.1.5 eq 443
access-list 100 deny ip any any log
```

### Pattern 2: DMZ Segregation

```cisco
! Allow web traffic to DMZ servers
access-list 100 permit tcp any 10.0.2.0 0.0.0.255 eq 80
access-list 100 permit tcp any 10.0.2.0 0.0.0.255 eq 443

! Block DMZ from accessing internal network
access-list 101 deny ip 10.0.2.0 0.0.0.255 10.0.1.0 0.0.0.255 log
access-list 101 permit ip any any
```

### Pattern 3: Stateful Firewall Simulation

```cisco
! Allow established connections back
access-list 100 permit ip any any established
access-list 100 permit tcp any 10.0.1.0 0.0.0.255 eq 80
access-list 100 permit tcp any 10.0.1.0 0.0.0.255 eq 443
access-list 100 deny ip any any log
```

---

## 🔗 Related Resources

- **[Cisco ACL Documentation](https://www.cisco.com/c/en/us/support/docs/security/access-lists/)** — Official guide
- **[network-labs-documentation](https://github.com/Dinaverse/network-labs-documentation)** — Hands-on labs
- **[OSPF Configuration Guide](OSPF-Configuration-Guide.md)** — Routing fundamentals

---

*ACLs: The foundation of network security. Design, implement, monitor.*
