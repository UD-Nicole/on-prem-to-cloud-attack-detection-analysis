# Lessons Learned

## Technical Lessons

- Successful SIEM investigations require visibility across Linux, Windows, identity providers, and cloud platforms.
- Not every attacker action generates a dedicated log. Some activities, such as plaintext credential discovery, must be inferred through event correlation.
- Windows Security Events and AWS CloudTrail provide valuable evidence for persistence and privilege escalation.
- Identity provider logs should be correlated with cloud-native logs to accurately understand authentication outcomes.

---

## Detection Engineering Lessons

- Baselines are essential before validating detections.
- Multi-source correlation improves investigation accuracy.
- MITRE ATT&CK mapping provides consistent documentation across the attack chain.
- Dashboard tuning improves analyst visibility during investigations.

---

## Future Improvements

- Implement successful SAML federation from PingOne to AWS.
- Expand detection coverage for lateral movement.
- Add risk-based alerting.
- Automate response using Splunk SOAR.
