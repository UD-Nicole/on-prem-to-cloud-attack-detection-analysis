# Attack Timeline

The following timeline summarizes the progression of the attack based on timestamps observed in Splunk, Windows Event Logs, PingOne audit logs, and AWS CloudTrail.

| Time (UTC) | Phase | Activity | Evidence |
|------------|-------|----------|----------|
| 2026-06-24 18:39:12 | Phase 1 | Hydra brute force and successful SSH authentication to webhost | Linux Auth Logs (`04-dr003-investigation-result.png`) |
| 2026-06-25 12:00:39 | Phase 2 | Plaintext credentials discovered (`cat /home/nicole/credentials.txt`) | System Audit Logs (`11-dr006-investigation.png`) |
| 2026-06-25 17:36:18 | Phase 3 | New domain user created (`Burke`) | Event ID 4720 (`16-ad-investigation-timeline.png`) |
| 2026-06-25 17:37:04 | Phase 3 | User added to Domain Admins group | Event ID 4728 (`16-ad-investigation-timeline.png`) |
| 2026-06-25 19:20:21 | Phase 4 | Successful PingOne portal authentication | PingOne Audit Logs (`20-pingone-investigation.png`) |
| 2026-06-25 19:20:44 | Phase 4 | AWS login via Federated Single Sign-On (SSO) | AWS IAM Audit Logs (`20-pingone-investigation.png`) |
| 2026-06-26 13:21:18 | Phase 5 | AWS admin user policies attached via CloudShell from external IP (`199.249.111.229`) | AWS CloudTrail (`25-aws-investigation.png`) |
| 2026-06-26 13:22:25 | Phase 5 | Persistent IAM cloud user created (`CreateUser`) | AWS CloudTrail (`25-aws-investigation.png`) |
