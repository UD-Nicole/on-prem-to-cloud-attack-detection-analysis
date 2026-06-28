# Phase 5 – AWS S3 Exfiltration & Persistence

## Objective

The objective of this phase was to simulate cloud-level impact following identity and credential compromise from previous phases. This included accessing AWS, identifying sensitive data stored in S3, performing data exfiltration, and establishing persistence within the AWS environment.

---

## Attack Summary

Using previously compromised AWS credentials, access to the AWS environment was successfully established.

Once inside AWS, S3 buckets were enumerated and sensitive data was identified and exfiltrated from a target bucket. In addition, persistence was simulated by creating a new IAM user with administrative access, demonstrating the risk of attackers backdoor access to the cloud.

This phase completed the attack chain from on-prem infrastructure to cloud data exposure.

---

## Detection rules

### DR-011 – Suspicious S3 Data Access and Exfiltration Activity

**Objective:** Detect excessive S3 object access that may indicate data enumeration or exfiltration.

```spl
sourcetype=aws:cloudtrail eventSource=s3.amazonaws.com
(eventName=GetObject OR eventName=ListBucket)
| stats count values(requestParameters.bucketName) as buckets
        by userIdentity.arn sourceIPAddress
| bin _time span=5m
| stats count values(requestParameters.bucketName) as buckets by userIdentity.arn sourceIPAddress _time
| where count > 20
```

**Result:** Validated. High-volume S3 access activity was detected, indicating potential data enumeration or exfiltration behavior.

### DR-012 – AWS IAM Persistence Through User and Policy

**Objective:** Detect IAM-related changes that may indicate persistence or privilege escalation in AWS.

```spl
sourcetype=aws:cloudtrail
eventSource=iam.amazonaws.com
(eventName=CreateUser OR
 eventName=CreateAccessKey OR
 eventName=AttachUserPolicy OR
 eventName=PutUserPolicy OR
 eventName=CreateLoginProfile OR
 eventName=AttachRolePolicy)
| stats count
        values(eventName) as actions
        values(requestParameters.userName) as target_user
        by userIdentity.arn sourceIPAddress
```

**Result:** Validated. IAM modification activity was detected, including user creation and policy attachment indicative of persistence attempts.

## Investigation

AWS CloudTrail logs and Splunk ingestion were used to analyze cloud activity.

The investigation confirmed:

- Successful authentication to AWS using compromised credentials.
- Enumeration of available S3 buckets.
- Access to sensitive objects within an S3 bucket.
- Evidence of data retrieval consistent with exfiltration activity.
- Creation of a new IAM user with administrative privileges to maintain persistent access within the AWS environment.

CloudTrail logs provided full visibility into API-level activity, enabling reconstruction of the attacker’s actions in AWS.

---

## MITRE ATT&CK Mapping

|         Technique             | ATT&CK ID | Description |
|-------------------------------|-----------|-------------|
|       Valid Accounts          |   T1078   | Compromised AWS credentials were used to access the environment. |
| Create Account: Cloud Account | T1136.003 | A new IAM user was created within AWS for persistence. |
|      Account Manipulation     |   T1098   | Administrative privileges were assigned to the newly created IAM user. |
| Data from Cloud Storage Object|   T1530   | Data was accessed and exfiltrated from S3 buckets. |

---

## Evidence

- **S3 Data Access & Exfiltration:**
![S3 Data Access & Exfiltration](22-s3-data-access-&-exfiltration.png)

- **IAM Persistence:**
![IAM Persistence](23-iam-persistence.png)

- **AWS Detection:**
![AWS Detection](24-aws-detection.png)

- **AWS Investigation:**
![AWS Investigation](25-aws-investigation.png)

- **AWS Dashboard:**
![AWS Dashboard](26-aws-dashboard.png)
---

## Outcome

## Outcome

The attacker successfully accessed AWS using compromised credentials and performed further actions within the cloud environment.

A new IAM user was created and granted administrative privileges, establishing persistent access within AWS. Additionally, sensitive data was accessed and exfiltrated from S3 storage.

This phase demonstrated the impact of compromised cloud credentials and the risk of improper IAM privilege assignment, which can lead to long-term unauthorized access and data exposure.
