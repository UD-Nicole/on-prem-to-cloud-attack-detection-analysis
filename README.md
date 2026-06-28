# On-Prem to Cloud Attack Chain Detection & Analysis (SOC Simulation)

## Overview

This project simulates a full end-to-end cyber attack chain spanning on-prem Linux systems, Active Directory, identity providers (PingOne), and AWS cloud infrastructure. The objective was to design and validate Splunk-based detection rules to identify attacker progression across hybrid environments.

The project focuses on:
- Attack chain reconstruction
- Multi-source log correlation
- Detection engineering using Splunk SPL
- MITRE ATT&CK mapping
- SOC-style investigation workflows

---

## Attack Scenario

**Attacker:** Kali Linux  
**Target Environment:**

- WebHost (DMZ Linux system)
- NMSHost (Internal Linux system)
- Active Directory (DC1)
- PingOne Identity Provider
- AWS Cloud (IAM + S3)

---

## Attack Flow

Kali → WebHost → NMSHost → Active Directory → PingOne → AWS

---

## Detection Coverage

The following telemetry sources were analyzed in Splunk:

- Linux Authentication Logs (Syslog / Auth.log)
- Windows Security Logs (Event ID 4624, 4720, 4728)
- PingOne Authentication Logs
- AWS CloudTrail Logs 

---

## Key Attack Phases

### Phase 1 – Initial Access
- SSH brute force attack against WebHost
- Successful authentication using valid credentials

### Phase 2 – Lateral Movement & Credential Discovery
- SSH pivot into internal systems
- Discovery of plaintext credentials (AD, PingOne, AWS)

### Phase 3 – Active Directory Compromise
- Unauthorized domain authentication
- User creation and privilege escalation (Domain Admins)

### Phase 4 – Identity Pivot (PingOne → AWS)
- Authentication via identity provider
- Attempted AWS access using federated credentials

### Phase 5 – Cloud Access & Persistence
- AWS IAM activity simulation
- S3 data access and persistence behavior

---

## Detection Engineering

A total of **12 Splunk detection rules (DR-001 to DR-012)** were developed and mapped to MITRE ATT&CK techniques.

Key detections include:
- SSH brute force detection
- Successful login after failed attempts
- Lateral movement detection
- Active Directory privilege escalation
- Cloud authentication monitoring
- S3 data access detection
- IAM persistence detection

---

## Key Challenges

- Not all attack actions generated direct log events
- Detection required correlation across multiple data sources
- Some rules validated logically but not executed due to missing ingestion

---

## Lessons Learned

- Effective detection engineering depends on complete telemetry coverage
- Not all attacker actions are directly observable in logs
- Multi-source correlation is critical in hybrid environments
- Splunk SPL must be adapted based on actual field availability

---

## Final Outcome

This project demonstrates the ability to:
- Simulate real-world attack chains
- Build SIEM detection rules using Splunk SPL
- Map detections to MITRE ATT&CK framework
- Perform SOC-style investigation across hybrid environments
