# Phase 1 - Initial Access (SSH Brute Force)

## Objective
The objective of this phase was to simulate an external attacker gaining initial access to the WebHost through SSH brute force techniques.

## Attack Summary
Kali Linux was used to perform a brute force attack against the SSH service on the WebHost. After multiple failed login attempts, valid credentials were successfully discovered and an SSH session was established.

## Detection 
Splunk identified repeated failed SSH authentication attempts followed by a successful login from the same source IP, indicating potential brute force activity.

## Investigation
The activity was investigated using Splunk search queries across Linux authentication logs. The logs confirmed:

- High volume of failed SSH login attempts
- A successful authentication following the failures
- Session initiation from the same source IP

This pattern is consistent with brute force credential guessing.

## MITRE ATT&CK Mapping

| Technique | ID | Description |
|------------|-----|-------------|
| Brute Force | T1110 | Repeated login attempts against SSH |

## Evidence
Screenshots in this folder show:

- **Hydra Terminal Success:**
![Hydra Terminal Success](01-hydra-terminal-success.png)

- **Hydra Successful Credentials:**
![Hydra Successful Credentials](02-hydra-successful-credentials....)

- **DR-003 Alert Trigger History:**
![DR-003 Alert Trigger History](03-dr003-alert-trigger-history.png)

- **DR-003 Investigation Result:**
![DR-003 Investigation Result](04-dr003-investigation-result.png)

- **Dashboard Update:**
![Dashboard Update](06-dashboard-update.png)


## Outcome
Initial access to the WebHost was successfully achieved and confirmed through log analysis in Splunk.
