# Playbook: Cloud Security Incident Response (Master)

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Cloud Security Incident Response (Master)         |
| Document ID    | IR-PB-CLD-001                                                |
| Version        | 1.0                                                          |
| Effective Date | 20-May-2026                                                  |
| Owner          | SOC Manager / Cloud Security Lead / IR Team Lead             |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 cloud security incident        |

---

## 2. Purpose

This master playbook defines the end-to-end response procedures for cloud security incidents across enterprise and MSSP-managed environments.

Cloud incidents are fundamentally different from traditional on-prem incidents because:

- Infrastructure is highly dynamic and ephemeral
- Identity is the primary security boundary
- Misconfigurations can expose internet-facing resources instantly
- Logging and telemetry are provider-specific
- Attackers can scale rapidly across cloud services
- Persistence often relies on IAM, API keys, OAuth grants, and automation
- Cloud compromise frequently leads to large-scale data exposure and cross-account impact

This playbook standardizes:

- Cloud incident detection and triage
- Investigation across AWS, Azure, and GCP
- IAM compromise analysis
- Cloud-native containment procedures
- Forensic evidence collection
- Regulatory and breach assessment
- Cross-cloud investigation workflow
- MSSP multi-tenant cloud response coordination

---

## 3. Scope

### 3.1 In Scope

Applies to cloud incidents involving:

- AWS, Azure, GCP environments
- Multi-cloud deployments
- IaaS, PaaS, SaaS, serverless, and container platforms
- Cloud IAM compromise
- Cloud storage exposure
- API key/token compromise
- Misconfigured cloud resources
- Cloud workload compromise
- Cloud-native malware or cryptomining
- Kubernetes and container compromise
- Cloud lateral movement
- Cloud data exfiltration
- OAuth abuse and identity federation attacks

### 3.2 Cloud Service Coverage

| Cloud Layer          | Examples                                                  |
| -------------------- | --------------------------------------------------------- |
| Compute              | EC2, Azure VM, GCE, Lambda, Azure Functions, Cloud Functions |
| Storage              | S3, Azure Blob, GCS, EBS, EFS                             |
| Identity             | IAM, Azure AD/Entra ID, GCP IAM                           |
| Containers           | EKS, AKS, GKE, Docker, Kubernetes                         |
| Networking           | VPC, NSG, Security Groups, Cloud Firewall                 |
| Databases            | RDS, Azure SQL, Cloud SQL, DynamoDB                       |
| Logging/Monitoring   | CloudTrail, GuardDuty, Sentinel, Security Command Center  |
| DevOps               | CodeBuild, Azure DevOps, Cloud Build                      |

### 3.3 Out of Scope

| Scenario                                      | Use Playbook                                  |
| --------------------------------------------- | --------------------------------------------- |
| Pure web application attack                   | 02.8_Web-Application-Attack/                  |
| Traditional on-prem network intrusion only    | 02.11_Network-Intrusion/                      |
| Phishing/BEC without cloud compromise         | 02.2_Phishing-BEC/                            |
| Supply chain compromise affecting cloud later | 02.9_Supply-Chain-Attack/                     |

---

## 4. Cloud Incident Categories

| Category                     | Description                                              | Typical Impact                         |
| ---------------------------- | -------------------------------------------------------- | -------------------------------------- |
| IAM Compromise               | Stolen keys, tokens, OAuth abuse, role hijacking         | Full cloud account compromise          |
| Storage Exposure             | Public bucket/container exposure                         | Data breach                            |
| Cloud Workload Compromise    | VM/container/serverless compromise                       | Lateral movement, persistence          |
| Kubernetes Compromise        | Cluster compromise, pod escape, secrets theft            | Multi-service compromise               |
| Cryptomining                 | Unauthorized cloud compute usage                         | Financial impact                       |
| Misconfiguration             | Public services, weak security groups, open admin access | Exposure and unauthorized access       |
| Cloud API Abuse              | Excessive or malicious API calls                         | Data manipulation, persistence         |
| OAuth / Federation Abuse     | SSO token theft or misuse                                | Account takeover                       |
| Cross-Account Compromise     | Attacker pivots between cloud accounts                   | Enterprise-wide compromise             |
| Cloud Data Exfiltration      | Data stolen from storage/services                        | Regulatory breach                      |

---

## 5. Severity Classification (Cloud-Specific)

| Scenario                                                     | Default Severity |
| ------------------------------------------------------------ | ---------------- |
| Root/admin cloud account compromise                          | P1               |
| Active cloud data exfiltration                               | P1               |
| Public storage bucket with sensitive data exposed            | P1               |
| Cross-account compromise confirmed                           | P1               |
| Kubernetes cluster compromise                                | P1/P2            |
| Production cloud workload compromise                         | P1/P2            |
| IAM key exposure without confirmed misuse                    | P2               |
| Cryptomining in isolated environment                         | P2/P3            |
| Misconfiguration without exploitation evidence               | P3               |
| Informational cloud security finding                         | P4               |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

## 6. Cloud Shared Responsibility Model (Critical)

Cloud incidents must always consider responsibility boundaries.

| Area                          | Customer Responsibility | Cloud Provider Responsibility |
| ----------------------------- | ----------------------- | ----------------------------- |
| IAM users and roles           | Yes                     | No                            |
| Data encryption configuration | Yes                     | Partial                       |
| Operating system patching     | Yes (IaaS)              | No                            |
| Physical datacenter security  | No                      | Yes                           |
| Hypervisor security           | No                      | Yes                           |
| Cloud-native service security | Partial                 | Partial                       |
| Application security          | Yes                     | No                            |
| Cloud logging configuration   | Yes                     | No                            |

---

## 7. Cloud Incident Response Lifecycle

| Phase                   | Description                                           | Primary Owner             |
| ----------------------- | ----------------------------------------------------- | ------------------------- |
| Detection & Triage      | Validate alert, identify affected cloud assets        | L1/L2                     |
| Investigation           | Scope cloud resources, IAM, storage, workloads        | L2                        |
| Containment             | Revoke keys, isolate workloads, block API abuse       | IR Team / Cloud Team      |
| Forensics               | Collect cloud logs, snapshots, IAM evidence           | L3 / IR Team              |
| Eradication             | Remove persistence, rotate credentials, patch configs | Cloud Team / IR           |
| Recovery                | Restore secure state and validate integrity           | Cloud Team                |
| Post-Incident           | PIR, detection engineering, cloud hardening           | IR / Cloud Security       |

---

## 8. Cloud Incident Detection Sources

### 8.1 Native Cloud Security Services

| Cloud Provider | Service                            | Purpose                          |
| -------------- | ---------------------------------- | -------------------------------- |
| AWS            | GuardDuty                          | Threat detection                 |
| AWS            | CloudTrail                         | API activity logging             |
| AWS            | Security Hub                       | Security findings aggregation    |
| Azure          | Microsoft Defender for Cloud       | Threat detection                 |
| Azure          | Azure Activity Logs                | Administrative activity logging  |
| Azure          | Microsoft Sentinel                 | SIEM and analytics               |
| GCP            | Security Command Center            | Security findings                |
| GCP            | Cloud Audit Logs                   | API and admin activity           |

### 8.2 Third-Party Detection Sources

- SIEM correlation
- CSPM tools
- CWPP tools
- EDR agents on cloud workloads
- DLP systems
- Threat intelligence feeds
- Kubernetes runtime security tools
- Identity protection platforms

---

## 9. Cloud-Specific Investigation Priorities

Cloud investigations must prioritize:

### 9.1 Identity and Access

Cloud incidents frequently begin with identity compromise.

Always investigate:

- IAM users
- Access keys
- OAuth grants
- Federation trust relationships
- MFA bypass attempts
- Service accounts
- Role assumptions

### 9.2 Logging Preservation

Cloud logs are critical evidence.

Immediately preserve:

| Log Type                | Why Important                          |
| ----------------------- | -------------------------------------- |
| CloudTrail              | API actions and IAM changes            |
| Azure Activity Logs     | Administrative operations              |
| GCP Audit Logs          | API activity and access                |
| VPC Flow Logs           | Network communications                 |
| Kubernetes Audit Logs   | Cluster activity                       |
| Storage Access Logs     | Data access evidence                   |
| Authentication Logs     | Login and federation events            |

### 9.3 Time Synchronization

Cloud environments span regions and providers.

All investigations must:

- Normalize timestamps to UTC
- Document cloud region
- Record account/subscription/project identifiers
- Correlate across providers carefully

---

## 10. Core Cloud Investigation Areas

Every cloud incident investigation must assess the following areas:

| Investigation Area         | Key Questions                                              |
| -------------------------- | ---------------------------------------------------------- |
| IAM                        | Were credentials compromised or abused?                    |
| Storage                    | Was data exposed, accessed, or exfiltrated?                |
| Compute                    | Were workloads compromised or modified?                    |
| Networking                 | Were malicious connections established?                    |
| Logging                    | Were logs disabled, modified, or deleted?                  |
| Persistence                | Did attacker create new roles/users/keys?                  |
| Lateral Movement           | Did attacker pivot across accounts/projects/subscriptions? |
| Automation                 | Were CI/CD pipelines or IaC templates abused?              |
| Kubernetes                 | Were clusters or secrets compromised?                      |
| Serverless                 | Were functions modified or abused?                         |

---

## 11. Cloud Containment Principles

Cloud containment differs from traditional containment because actions can be immediate and large-scale.

### 11.1 Core Principles

| Principle                     | Description                                                  |
| ----------------------------- | ------------------------------------------------------------ |
| Revoke first                  | Revoke exposed credentials immediately                       |
| Preserve evidence             | Export logs before deleting resources                        |
| Minimize disruption           | Isolate affected resources instead of broad shutdowns        |
| Assume automation abuse       | Check CI/CD, Terraform, CloudFormation, ARM, Deployment Manager |
| Check cross-account trust     | Attackers often pivot between accounts                       |
| Verify persistence            | Review IAM roles, keys, startup scripts, functions           |
| Validate logging integrity    | Ensure logging was not disabled                              |

### 11.2 Common Immediate Containment Actions

| Action                          | Purpose                              |
| ------------------------------- | ------------------------------------ |
| Disable IAM keys                | Stop attacker API access             |
| Revoke OAuth sessions           | Remove active attacker sessions      |
| Isolate cloud workloads         | Prevent lateral movement             |
| Block malicious IPs             | Stop active C2 or exfiltration       |
| Remove public access            | Prevent further exposure             |
| Enable additional logging       | Increase visibility                  |
| Rotate secrets                  | Invalidate compromised credentials   |
| Snapshot compromised workloads  | Preserve forensic evidence           |

---

## 12. Escalation Criteria

### 12.1 Escalate to L3 if:

- IAM compromise is confirmed
- Cross-account access detected
- Cloud workload persistence identified
- Kubernetes compromise suspected
- Logging disabled or tampered with
- Data exfiltration indicators present

### 12.2 Escalate to IR Team if:

- Root/admin compromise confirmed
- Production data exposed
- Multi-cloud compromise suspected
- Multiple cloud accounts affected
- MSSP multi-client cloud impact exists
- Regulatory reporting likely required

### 12.3 Escalate to Legal/Compliance if:

- Sensitive data exposure confirmed
- Customer/employee data involved
- Public cloud storage exposure occurred
- Regulatory notification timelines triggered

---

## 13. Data Breach Trigger Assessment

Cloud incidents frequently result in data exposure.

Mandatory breach trigger questions:

| Question                                                      | If YES → Action                          |
| ------------------------------------------------------------- | ---------------------------------------- |
| Was cloud storage publicly accessible?                        | Activate Data Breach playbook            |
| Were sensitive objects/files accessed?                        | Activate Data Breach playbook            |
| Were IAM credentials stolen or abused?                        | Assess downstream impact immediately     |
| Was customer or regulated data accessible?                    | Engage Legal/Compliance immediately      |
| Did attacker access backup or archive storage?                | Assess full historical exposure          |

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`

---

## 14. MSSP-Specific Cloud Considerations

For MSSP-managed cloud environments:

- Multiple clients may share cloud management infrastructure
- Cross-tenant evidence segregation is mandatory
- Shared IAM or management tooling increases blast radius
- Cloud provider APIs may expose metadata across tenants if misconfigured
- Client notification timing must follow contractual SLA obligations

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`

---

## 15. Cloud Forensics Overview

### 15.1 Evidence Types

| Evidence Type              | Examples                                      |
| -------------------------- | --------------------------------------------- |
| API logs                   | CloudTrail, Azure Activity Logs               |
| Snapshots                  | EBS snapshots, VM snapshots                   |
| Memory captures            | Cloud workload memory dumps                   |
| IAM records                | Access key creation, role assumptions         |
| Kubernetes audit logs      | Pod exec, secret access                       |
| Storage access logs        | S3 access logs, Blob access logs              |
| Container runtime logs     | Docker/containerd/K8s runtime telemetry       |

### 15.2 Evidence Preservation Rules

- Export logs before account cleanup
- Snapshot workloads before rebuild
- Hash forensic exports
- Preserve IAM state
- Maintain chain-of-custody for all artifacts

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 16. Cloud Incident Common Mistakes to Avoid

| Mistake                                              | Risk                                      | Correct Approach                              |
| ---------------------------------------------------- | ----------------------------------------- | --------------------------------------------- |
| Deleting cloud resources before snapshots            | Evidence destruction                      | Snapshot first                                |
| Rotating credentials before preserving logs          | Loss of attribution evidence              | Export logs before key rotation if possible   |
| Ignoring cross-account trust                         | Missed attacker persistence               | Review all trust relationships                |
| Disabling workloads broadly                          | Major outage                              | Isolate targeted systems first                |
| Not checking storage access logs                     | Missed exfiltration evidence              | Review all object access                      |
| Failing to review cloud IAM thoroughly               | Persistence remains active                | Audit all users, roles, policies, sessions    |
| Assuming cloud provider handles security automatically | Shared responsibility misunderstanding | Investigate customer-controlled configs       |

---

## 17. Related Documents

| Document                     | Path                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| Cloud L1 Triage              | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L1-Triage.md` |
| Cloud L2 Investigation       | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L2-Investigation.md` |
| Cloud L3 Forensics           | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L3-Forensics.md` |
| Cloud Containment            | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Containment.md` |
| Cloud AWS Specific           | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-AWS-Specific.md` |
| Cloud Azure Specific         | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Azure-Specific.md` |
| Cloud GCP Specific           | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-GCP-Specific.md` |
| Cloud MITRE Mapping          | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-MITRE-Mapping.md` |
| Data Breach Playbooks        | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`                |
| Network Intrusion Playbooks  | `02_PLAYBOOKS/02.11_Network-Intrusion/`                      |
| Evidence Handling            | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`                          |

---

## 18. Revision History

| Version | Date        | Author                                      | Changes         |
| ------- | ----------- | ------------------------------------------- | --------------- |
| 1.0     | 20-May-2026 | SOC Manager / Cloud Security Lead / IR Team Lead | Initial version |

---

## 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**