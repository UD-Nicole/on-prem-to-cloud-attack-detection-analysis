# On-Prem to Cloud Attack Chain Detection & Analysis

This project simulates a complete hybrid attack chain spanning:

- Linux DMZ Systems
- Internal Linux Infrastructure
- Active Directory
- PingOne Identity
- AWS Cloud

The objective was to design, validate, and tune Splunk detections capable of identifying an attacker progressing from initial access through cloud persistence.

Attack Flow:

Kali
→ WEBHOST
→ NMSHOST
→ Active Directory
→ PingOne
→ AWS

Telemetry Sources:

- Linux Syslog
- Linux Auth Logs
- Windows Security Logs
- Sysmon
- PingOne Audit Logs
- AWS CloudTrail

Baseline
        ↓
Attack Simulation
        ↓
Log Collection
        ↓
Detection
        ↓
Alert Generation
        ↓
Investigation
        ↓
Dashboard Validation
