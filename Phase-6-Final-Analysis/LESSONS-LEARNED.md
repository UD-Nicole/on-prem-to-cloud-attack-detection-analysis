# Lessons Learned

## Technical Lessons

- End-to-end attack investigations require correlating telemetry across Linux, Windows, identity providers, and cloud platforms rather than relying on a single log source.
- Not every adversary action produces a distinct security event. Activities such as credential discovery often require investigators to infer attacker behavior by correlating authentication, process, and timeline evidence.
- Windows Security Events, Sysmon, Linux authentication logs, PingOne audit logs, and AWS CloudTrail each provide part of the attack narrative; combining these sources produces a much more complete investigation.
- Lateral movement and privilege escalation become significantly easier to detect when host logs are enriched with identity and cloud telemetry.
---

## Detection Engineering Lessons

- Establishing a clean baseline is critical for validating detections and reducing false positives.
- Detection logic should prioritize attacker behaviors instead of individual tools, making rules more resilient to changes in attacker techniques.
- MITRE ATT&CK mapping provides a consistent framework for documenting detections, identifying coverage gaps, and communicating findings.
- Dashboards are most valuable when they support investigations with correlated timelines, authentication activity, and high-value security events rather than simply displaying raw log volume

---

## Project Takeaways

- Building the lab provided practical experience in detection engineering, log analysis, incident investigation, and attack simulation across hybrid environments.
- Writing detection rules and validating them against simulated attacker activity reinforced the importance of testing detections with realistic scenarios.
- Thorough documentation of architecture, detections, investigations, and lessons learned is as important as the technical implementation because it enables repeatability and demonstrates analytical thinking.

## Future Improvements

- Complete a successful PingOne SAML federation into AWS and validate additional identity-based detections.
- Expand lateral movement scenarios to include additional techniques and corresponding detection coverage.
- Integrate Splunk SOAR playbooks to automate alert triage and incident response workflows.
- Simulate additional attacker behaviors such as Kerberoasting, Pass-the-Hash, or other cloud persistence techniques to broaden ATT&CK coverage.
