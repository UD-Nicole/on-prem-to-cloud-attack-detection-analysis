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

Detection Rules:

13

Dashboards:

4

MITRE Techniques:

8+

Log Sources:

6
