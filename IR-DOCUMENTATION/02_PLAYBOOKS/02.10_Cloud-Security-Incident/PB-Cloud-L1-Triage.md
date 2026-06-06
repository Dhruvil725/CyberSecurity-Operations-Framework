# Playbook: Cloud Security Incident – L1 Triage

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Cloud Security Incident (L1 Triage)               |
| Document ID    | IR-PB-CLD-002                                                |
| Version        | 1.0                                                          |
| Effective Date | 20-May-2026                                                  |
| Owner          | SOC Lead / Cloud Security Lead                               |
| Approved By    | IR Team Lead                                                 |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 cloud security incident        |

---

## 2. Purpose

This document defines the Level 1 (L1) SOC Analyst triage procedures for cloud security incidents.

Cloud incidents require specialized triage because:

- Cloud environments are highly dynamic and rapidly changing
- Identity is often the primary attack surface
- A single compromised IAM credential can expose multiple services simultaneously
- Cloud logs are distributed across services and regions
- Cloud misconfigurations can expose sensitive data directly to the internet
- Attackers frequently abuse automation, APIs, and cloud-native tooling
- Containment actions can unintentionally disrupt production at large scale

L1 triage objectives:

- Validate whether the alert represents a real cloud security incident
- Identify the affected cloud provider, account/subscription/project, and services
- Determine if there is active compromise, data exposure, or IAM abuse
- Preserve critical cloud evidence before automated changes occur
- Recommend severity (P1–P4)
- Escalate to L2/SOC Lead appropriately with all required context

L1 must prioritize:

- Fast validation
- Identity compromise assessment
- Evidence preservation
- Scope identification
- Early escalation for IAM or data exposure incidents

---

## 3. Scope

Applies to alerts and incidents involving:

- AWS
- Microsoft Azure / Entra ID
- Google Cloud Platform (GCP)
- Multi-cloud environments
- Kubernetes and container platforms
- Serverless services
- Cloud storage exposure
- Cloud IAM compromise
- Cloud-native malware or cryptomining
- Public cloud misconfigurations
- Cloud API abuse

Detection sources include:

- Cloud-native security services
- SIEM alerts
- CSPM findings
- EDR telemetry from cloud workloads
- Cloud audit logs
- DLP alerts
- Threat intelligence feeds
- IAM anomaly alerts
- Kubernetes security alerts

---

## 4. L1 Safety Rules (Cloud Incidents)

| Rule                                                          | Why it Matters                                               |
| ------------------------------------------------------------- | ------------------------------------------------------------ |
| Do NOT delete cloud resources immediately                     | Evidence may be permanently lost                             |
| Do NOT rotate keys before preserving logs if possible         | Attribution evidence may be destroyed                        |
| Do NOT shut down cloud workloads without approval             | May cause large production outage                            |
| Preserve audit logs immediately                               | Some cloud logs have short retention                         |
| Record account IDs, regions, and timestamps accurately        | Cloud investigations depend heavily on metadata              |
| Assume IAM compromise can affect multiple services            | Cloud identity often has broad privileges                    |
| Use UTC timestamps only                                       | Multi-region cloud timelines require normalization           |
| Validate cloud provider account context before action         | Wrong account actions can impact unrelated environments      |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 5. L1 SLA Targets (Cloud Incidents)

| Severity (likely) | L1 Triage Target | Escalation Target                          |
| ----------------- | ---------------- | ------------------------------------------ |
| P1                | 5 minutes        | SOC Lead + L2 immediately                  |
| P2                | 10 minutes       | SOC Lead immediately; L2 within 15 minutes |
| P3                | 20 minutes       | L2 within 30 minutes if required           |
| P4                | 30 minutes       | Monitor and close per SOP                  |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 6. Inputs to Collect at L1 (Mandatory)

### 6.1 Cloud Environment Context

| Data Point                  | Required Detail                                      |
| --------------------------- | ---------------------------------------------------- |
| Cloud provider              | AWS / Azure / GCP / Multi-cloud                      |
| Account/subscription/project| Account ID, tenant ID, project ID                    |
| Region                      | Cloud region or availability zone                    |
| Environment                 | Production / DR / Staging / Development              |
| Affected service            | EC2, S3, IAM, Azure VM, Blob, Kubernetes, etc.       |
| Resource identifier         | Instance ID, bucket name, VM name, cluster name      |

### 6.2 Alert Context

| Data Point                  | Required Detail                                      |
| --------------------------- | ---------------------------------------------------- |
| Alert source                | GuardDuty / Defender / SCC / SIEM / CSPM             |
| Detection timestamp         | UTC                                                   |
| Alert type                  | IAM abuse / exposed storage / malware / API abuse    |
| Alert severity              | Native cloud severity if available                   |
| Detection rule name         | Exact rule or finding title                          |

### 6.3 Identity Context (Critical)

Cloud incidents frequently involve IAM compromise.

| Data Point                  | Required Detail                                      |
| --------------------------- | ---------------------------------------------------- |
| User / role / service account | Name and identifier                                |
| Authentication method       | Access key / OAuth / SSO / federation / console      |
| MFA enabled?                | Yes / No / Unknown                                  |
| Source IP                   | External IP or cloud service                         |
| Geo-location                | Country / ASN                                       |
| Last successful login       | Timestamp if available                              |

### 6.4 Data Exposure Context

| Data Point                  | Required Detail                                      |
| --------------------------- | ---------------------------------------------------- |
| Public resource?            | Yes / No                                             |
| Sensitive data involved?    | PII / Financial / Health / Internal                  |
| Storage type                | S3 / Blob / GCS / Database                           |
| Access confirmed?           | Yes / No / Unknown                                   |
| Logging enabled?            | Yes / No                                             |

---

## 7. L1 Triage Decision Flow

| Step | Question                                                          | If YES                                      | If NO              |
| ---- | ----------------------------------------------------------------- | ------------------------------------------- | ------------------ |
| 1    | Is root/admin IAM compromise suspected?                           | P1 → SOC Lead + L2 immediately              | Step 2             |
| 2    | Is sensitive cloud storage publicly exposed?                      | P1/P2 → escalate immediately                | Step 3             |
| 3    | Is active data exfiltration suspected?                            | P1 → IR Team escalation                     | Step 4             |
| 4    | Are there suspicious API calls or unusual IAM behavior?           | P2 → L2 investigation                       | Step 5             |
| 5    | Is this only a misconfiguration with no exploitation evidence?    | P3 → monitor and escalate if needed         | Step 6             |
| 6    | Is this informational or expected cloud activity?                 | P4 or close                                 | Escalate if unsure |

---

## 8. Step-by-Step L1 Triage Procedure

### Step 1 – Validate Alert Source and Type

Classify the alert:

| Alert Category             | Examples                                                |
| -------------------------- | ------------------------------------------------------- |
| IAM compromise             | Impossible travel, unusual API usage, root login        |
| Storage exposure           | Public S3 bucket, public Blob container                 |
| Cloud workload compromise  | EC2 malware, Azure VM cryptomining                      |
| Kubernetes compromise      | Privileged pod creation, suspicious exec into pod       |
| Cloud API abuse            | Excessive API calls, suspicious role assumptions        |
| Data exfiltration          | Large outbound transfer from storage or workload        |
| Misconfiguration           | Open security group, disabled logging                   |

### Step 2 – Preserve Critical Evidence Immediately

Cloud evidence can disappear quickly due to automation, scaling, or retention limits.

#### 8.2A Minimum Evidence Set

| Evidence Item                 | Source                                  | Priority |
| ----------------------------- | --------------------------------------- | -------- |
| Cloud audit logs              | CloudTrail / Azure Activity / GCP Audit | P0       |
| IAM event logs                | Identity provider logs                 | P0       |
| Alert export                  | SIEM/CSPM/cloud-native service         | P0       |
| Resource metadata             | Cloud console/API                      | P1       |
| Security group/firewall state | Cloud networking config                | P1       |
| Snapshot references           | Existing snapshots/backups             | P2       |

### Step 3 – Determine Identity Impact

This is one of the most important L1 cloud tasks.

#### 8.3A IAM Compromise Indicators

| Indicator                                           | Risk Level |
| --------------------------------------------------- | ---------- |
| Root account login                                  | Critical   |
| Access key used from unusual geo-location           | High       |
| MFA disabled                                        | High       |
| New IAM user or role created unexpectedly           | High       |
| Privilege escalation API calls                      | Critical   |
| OAuth app consent granted unexpectedly              | High       |
| Multiple failed console logins                      | Medium     |

### Step 4 – Assess Data Exposure Risk

#### 8.4A Public Storage Exposure Checks

| Check                                      | Why Important                              |
| ------------------------------------------ | ------------------------------------------ |
| Is bucket/container public?                | Internet exposure risk                     |
| Is sensitive data stored?                  | Regulatory impact                          |
| Are access logs enabled?                   | Determine whether data was accessed        |
| Is versioning enabled?                     | Recovery and rollback support              |
| Is encryption enabled?                     | Data protection assessment                 |

#### 8.4B Data Exposure Severity Guidance

| Condition                                             | Severity |
| ----------------------------------------------------- | -------- |
| Public bucket with confirmed sensitive data exposure  | P1       |
| Public bucket with unknown contents                   | P2       |
| Public bucket with no sensitive data                  | P3       |
| Internal-only storage with no exposure                | P4       |

---

## 9. Cloud-Specific Indicators of Compromise (Quick Reference)

### 9.1 AWS Indicators

| Indicator                                | Why Suspicious                            |
| ---------------------------------------- | ----------------------------------------- |
| Root login without MFA                   | High-risk compromise                      |
| Unusual AssumeRole activity              | Cross-account movement                    |
| CloudTrail disabled                      | Defense evasion                           |
| S3 bucket policy changed to public       | Data exposure                             |
| GuardDuty finding for crypto activity    | Cloud cryptomining                        |
| EC2 instance making unusual outbound connections | Possible malware/C2                |

### 9.2 Azure Indicators

| Indicator                                | Why Suspicious                            |
| ---------------------------------------- | ----------------------------------------- |
| Impossible travel alert                  | Credential compromise                     |
| Privileged role assignment               | Privilege escalation                      |
| New OAuth app consent                    | Token abuse                               |
| Blob storage public access enabled       | Data exposure                             |
| Defender for Cloud malware alert         | Workload compromise                       |

### 9.3 GCP Indicators

| Indicator                                | Why Suspicious                            |
| ---------------------------------------- | ----------------------------------------- |
| Service account key creation             | Persistence or credential abuse           |
| Public storage ACL changes               | Data exposure                             |
| Excessive IAM policy changes             | Privilege escalation                      |
| SCC malware findings                     | Workload compromise                       |

---

## 10. Severity Recommendation (Cloud-Specific)

| Condition                                                     | Recommended Severity |
| ------------------------------------------------------------- | -------------------- |
| Root/admin account compromise                                 | P1                   |
| Active cloud data exfiltration                                | P1                   |
| Public storage exposure with sensitive data                   | P1                   |
| Cross-account compromise                                      | P1                   |
| IAM abuse without confirmed data access                       | P2                   |
| Kubernetes compromise suspected                               | P2                   |
| Cloud cryptomining in production                              | P2                   |
| Misconfiguration without exploitation                         | P3                   |
| Informational finding                                         | P4                   |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

## 11. Ticket Creation Requirements

The incident ticket must contain:

| Field                                   | Required |
| --------------------------------------- | -------- |
| Incident category                       | Yes      |
| Cloud provider                          | Yes      |
| Account/subscription/project ID         | Yes      |
| Region                                  | Yes      |
| Resource identifiers                    | Yes      |
| IAM user/role involved                  | Yes if applicable |
| Alert source and rule                   | Yes      |
| Severity recommendation                 | Yes      |
| Evidence references                     | Yes      |
| Escalations performed                   | Yes      |
| Data exposure assessment                | Yes      |
| Immediate actions taken                 | Yes      |

---

## 12. Escalation Rules

| Trigger                                      | Escalate To                  | Timing      |
| -------------------------------------------- | ---------------------------- | ----------- |
| Root/admin compromise                        | SOC Lead + IR Team           | Immediately |
| Sensitive data exposure                      | SOC Lead + Legal/Compliance  | Immediately |
| Active data exfiltration                     | IR Team                      | Immediately |
| Kubernetes compromise                        | L2 + Cloud Security Team     | Immediately |
| Multiple cloud accounts affected             | IR Team + Management         | Immediately |
| MSSP client cloud environment affected       | SOC Lead + SDM              | Per SLA     |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/`

---

## 13. L1 Allowed Actions

L1 may:

- Preserve logs and alerts
- Export cloud findings
- Identify affected resources
- Notify SOC Lead and cloud teams
- Request temporary log retention increase
- Recommend containment actions

L1 must NOT:

- Disable production cloud services
- Rotate credentials without approval
- Delete cloud resources
- Remove storage access policies directly
- Modify IAM policies without authorization
- Shut down Kubernetes clusters
- Publicly communicate incident details

---

## 14. Common L1 Mistakes to Avoid

| Mistake                                              | Risk                                      | Correct Approach                              |
| ---------------------------------------------------- | ----------------------------------------- | --------------------------------------------- |
| Deleting exposed cloud resources                     | Evidence destruction                      | Preserve first                                |
| Assuming no breach because logs are missing          | Logs may have been disabled               | Escalate immediately                          |
| Ignoring IAM anomalies                               | Identity compromise is primary cloud risk | Always review IAM events                      |
| Looking only at one region                           | Attacker may pivot regions                | Check all regions/accounts                    |
| Not checking cloud storage exposure                  | Missed data breach                        | Always review public access settings          |
| Rotating credentials before preserving evidence      | Attribution loss                          | Export logs before changes if feasible        |

---

## 15. MSSP Client Handling Notes

For MSSP-managed cloud environments:

- Confirm correct client cloud account before evidence collection
- Maintain strict evidence segregation
- Follow client-specific approval workflows for containment
- Do not expose one client's cloud identifiers to another client
- Notify SDM immediately for all P1/P2 cloud incidents

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/`

---

## 16. Related Documents

| Document                  | Path                                                         |
| ------------------------- | ------------------------------------------------------------ |
| Cloud Master              | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Master.md` |
| Cloud L2 Investigation    | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L2-Investigation.md` |
| Cloud L3 Forensics        | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L3-Forensics.md` |
| Cloud Containment         | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Containment.md` |
| Cloud AWS Specific        | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-AWS-Specific.md` |
| Cloud Azure Specific      | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Azure-Specific.md` |
| Cloud GCP Specific        | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-GCP-Specific.md` |
| Cloud MITRE Mapping       | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-MITRE-Mapping.md` |
| Evidence Handling         | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`                          |
| Severity Matrix           | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/`           |

---

## 17. Revision History

| Version | Date        | Author                          | Changes         |
| ------- | ----------- | ------------------------------- | --------------- |
| 1.0     | 20-May-2026 | SOC Lead / Cloud Security Lead  | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**