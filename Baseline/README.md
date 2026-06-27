Before simulating the attack chain, I verified that all systems were forwarding logs to Splunk and that the environment was operating normally.

The screenshots in this folder demonstrate:

- Normal activity from WebHost
- Normal activity from NMSHost
- Normal activity from DC1
- Normal activity from PingOne
- Normal activity from AWS
- Successful log ingestion from all configured sources
- Initial dashboard state before attack execution
- 
Establishing this baseline ensured that all telemetry sources were functioning correctly before attack simulation and detection testing.
---

### 🖼️ Baseline Telemetry Evidence

#### WebHost Baseline
![WebHost Baseline](webhost-baseline.png)

#### NMSHost Baseline
![NMSHost Baseline](nmshost-baseline.png)

#### DC1 Baseline
![DC1 Baseline](DC1-baseline.png)

#### PingOne Baseline
![PingOne Baseline](pingone-baseline.png)

#### AWS Baseline
![AWS Baseline](AWS-%20baseline.png)

#### Splunk Log Ingestion Validation
![Splunk Log Ingestion Validation](Splunk-log-ingestion-validation)

#### Pre-Attack Dashboard State
![Baseline Dashboard](baseline-dashboard-pre-attack.png)
