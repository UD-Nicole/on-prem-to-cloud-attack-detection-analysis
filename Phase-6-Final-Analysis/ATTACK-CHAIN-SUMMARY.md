# Attack Chain Summary – On-Prem to Cloud Attack Simulation

## Overview

This project demonstrates a full attack chain spanning on-premises infrastructure, identity compromise, and cloud exploitation. The environment included Linux systems, Active Directory, PingOne SSO, AWS, and Splunk SIEM for centralized logging and investigation.

The objective was to simulate a real-world hybrid attack path and validate detection and investigation capabilities across multiple environments.

---

## Attack Flow

```
Kali (Attacker)
   ↓
WebHost (DMZ - Initial Access via SSH Brute Force)
   ↓
NMSHost (Internal Pivot & Credential Harvesting)
   ↓
Active Directory (DC1 - Privilege Escalation)
   ↓
PingOne (SSO Authentication Observation)
   ↓
AWS (Cloud Access via Compromised Credentials)
   ↓
S3 Bucket (Data Exfiltration + IAM Persistence)
```

---

## Phase Breakdown

### Phase 1 – Initial Access
- SSH brute force attack against WebHost using Hydra
- Successful authentication achieved
- Splunk detected failed and successful login patterns

**MITRE:**
- T1110 – Brute Force
- T1078 – Valid Accounts

---

### Phase 2 – Lateral Movement & Credential Harvesting
- Internal SSH pivot from WebHost to NMSHost
- Plaintext credentials discovered and harvested
- Credentials included AD, PingOne, AWS access keys

**MITRE:**
- T1021.004 – SSH Remote Services
- T1552.001 – Credentials in Files
- T1078 – Valid Accounts

---

### Phase 3 – Active Directory Compromise
- Direct authentication to Domain Controller using harvested credentials
- Creation of new domain user
- Addition of user to Domain Admins group

**Key Windows Events:**
- 4624 – Successful logon
- 4720 – User creation
- 4728 – Group membership change

**MITRE:**
- T1078 – Valid Accounts
- T1136.002 – Domain Account Creation
- T1098 – Account Manipulation

---

### Phase 4 – Identity & Cloud Pivot (PingOne → AWS)
- PingOne SSO authentication observed
- Attempted SAML-based AWS login (failed)
- AWS access achieved using compromised credentials

**MITRE:**
- T1078 – Valid Accounts
- T1199 – Trusted Relationship (SSO)

---

### Phase 5 – AWS Compromise & Data Exfiltration
- AWS environment accessed using compromised credentials
- New IAM user created with administrative privileges
- S3 bucket enumerated and sensitive data exfiltrated

**MITRE:**
- T1078 – Valid Accounts
- T1136.003 – Cloud Account Creation
- T1098 – Account Manipulation
- T1530 – Data from Cloud Storage

---

## Detection & Visibility

All phases were monitored using Splunk SIEM, ingesting logs from:

- Linux Syslog / Auth logs
- Windows Security Logs & Sysmon
- PingOne Audit Logs
- AWS CloudTrail

Key detections included:
- SSH brute force patterns
- Suspicious authentication sequences
- Privilege escalation events in Active Directory
- Cloud API activity (S3 access, IAM changes)

---

## Key Learnings

- Hybrid attacks require correlation across multiple identity layers
- Not all attacker actions generate direct logs (e.g., plaintext credential discovery)
- Identity provider logs (PingOne) must be correlated with cloud logs (AWS)
- IAM misconfiguration can lead to persistent cloud compromise
- Splunk provides end-to-end visibility when properly configured

---

## Conclusion

This project demonstrates a full end-to-end attack lifecycle across on-premises infrastructure, identity systems, and cloud environments.

It highlights how attackers move from initial access to persistence and data exfiltration, and how SIEM platforms like Splunk can be used to detect, investigate, and visualize these behaviors across a hybrid environment.
