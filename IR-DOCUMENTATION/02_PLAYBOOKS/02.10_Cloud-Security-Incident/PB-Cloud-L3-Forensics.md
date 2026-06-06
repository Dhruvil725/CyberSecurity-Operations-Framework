# Playbook: Cloud Security Incident – L3 Forensics and Advanced Analysis

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Cloud Security Incident (L3 Forensics and Advanced Analysis) |
| Document ID    | IR-PB-CLD-004                                                |
| Version        | 1.0                                                          |
| Effective Date | 20-May-2026                                                  |
| Owner          | L3 Lead / IR Team Lead / Cloud Security Lead                 |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 cloud security incident        |

---

# 2. Purpose

This document defines the Level 3 (L3) forensic and advanced analysis procedures for cloud security incidents.

L3 involvement is required when:

- IAM compromise is confirmed or highly likely
- Data exfiltration or cloud storage exposure occurred
- Kubernetes or container compromise is suspected
- Cloud-native persistence mechanisms are identified
- Cross-account or cross-cloud lateral movement occurred
- Cloud logging was disabled, tampered with, or deleted
- Legal or regulatory evidence requirements exist
- Root/admin account compromise is confirmed
- CI/CD pipelines or automation were abused
- Multi-region or multi-tenant impact exists

L3 objectives:

- Reconstruct the complete cloud attack chain
- Identify patient zero and compromise origin
- Confirm persistence mechanisms
- Validate data access and exfiltration scope
- Produce forensic-grade evidence
- Generate IOC/TTP intelligence packages
- Provide eradication guidance
- Support legal and regulatory reporting
- Define the clean-state validation criteria

This playbook is designed for:

- Enterprise cloud environments
- MSSP-managed cloud tenants
- Hybrid and multi-cloud environments
- High-impact cloud incidents requiring deep technical analysis

---

# 3. Scope

Applies to advanced forensic investigation involving:

## 3.1 Cloud Platforms

- AWS
- Microsoft Azure / Entra ID
- Google Cloud Platform
- Multi-cloud deployments

## 3.2 Cloud Technologies

- Virtual machines and cloud workloads
- Kubernetes and container platforms
- Serverless platforms
- Cloud-native databases
- IAM and federation platforms
- Storage services
- CI/CD pipelines
- Infrastructure-as-Code environments

## 3.3 Incident Types

| Incident Type                     | Example                                                  |
| --------------------------------- | -------------------------------------------------------- |
| IAM compromise                    | Root key theft, OAuth abuse, service account compromise |
| Public storage exposure           | Public S3 bucket with customer data                     |
| Kubernetes compromise             | Privileged pod escape                                   |
| Cryptomining                      | Unauthorized compute abuse                              |
| Cloud malware                     | Runtime backdoor on EC2/Azure VM/GCE                    |
| Cross-account compromise          | AssumeRole abuse across AWS accounts                    |
| Cloud logging tampering           | CloudTrail disabled                                     |
| CI/CD compromise                  | Build pipeline abuse                                    |
| Cloud data exfiltration           | Bulk object downloads                                   |

---

# 4. Preconditions (Inputs from L2)

L3 begins after L2 has completed:

- Resource inventory
- IAM assessment
- Storage exposure assessment
- Initial timeline
- Initial containment actions
- Data breach trigger assessment
- Escalation to IR Team if required

Minimum required inputs:

| Input                              | Required Detail                                      |
| ---------------------------------- | ---------------------------------------------------- |
| Incident summary                   | Cloud provider, attack type, severity                |
| Resource inventory                 | All affected resources                               |
| IAM assessment                     | Affected users/roles/keys                            |
| Data exposure assessment           | Sensitive data involvement                           |
| Containment actions                | Actions already executed                             |
| Timeline                           | Initial UTC timeline                                 |
| Evidence references                | Logs, exports, snapshots                             |

Reference:
`02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L2-Investigation.md`

---

# 5. L3 Required Outputs

L3 must deliver the following:

| Deliverable                              | Description                                      |
| ---------------------------------------- | ------------------------------------------------ |
| Authoritative attack timeline            | Full UTC attack reconstruction                   |
| Patient zero identification              | Initial compromised identity/resource            |
| IAM compromise report                    | Full identity abuse analysis                     |
| Data access and exfiltration assessment  | Confirmed/estimated exposure                     |
| Persistence report                       | All persistence mechanisms identified            |
| Cloud lateral movement map               | Cross-account and cross-service pivoting         |
| IOC package                              | IPs, hashes, domains, API patterns               |
| MITRE ATT&CK mapping                     | Technique mapping                                |
| Eradication guidance                     | Clean-state recommendations                      |
| Detection recommendations                | SIEM/CSPM/EDR improvements                       |
| Forensic evidence package                | Hashed evidence with chain-of-custody            |

---

# 6. Cloud Forensic Principles

Cloud forensics differs significantly from traditional forensic analysis.

Traditional disk-centric investigation is often insufficient because:

- Workloads may be ephemeral
- Containers may disappear automatically
- Serverless functions may leave minimal filesystem artifacts
- Cloud logs may rotate rapidly
- IAM activity may be the primary evidence source

---

## 6.1 Core Principles

| Principle                     | Description                                                  |
| ----------------------------- | ------------------------------------------------------------ |
| Preserve logs first           | Cloud logs are often the most critical evidence source       |
| Snapshot before remediation   | Preserve runtime state before shutdown                       |
| Preserve IAM state            | Identity compromise is central in cloud attacks              |
| Normalize timestamps          | Multi-region events require UTC normalization                |
| Validate logging integrity    | Attackers frequently disable or alter logging                |
| Export before deleting        | Cloud resources may disappear permanently                    |
| Assume lateral movement       | Cross-account and cross-service pivoting is common           |

---

## 6.2 Evidence Integrity Rules

| Rule                          | Requirement                                                  |
| ----------------------------- | ------------------------------------------------------------ |
| Hash all evidence exports     | SHA-256 minimum                                              |
| Preserve chain-of-custody     | Mandatory for P1/P2                                          |
| Record account/project IDs    | Mandatory for every artifact                                 |
| Record cloud region           | Required for all evidence                                    |
| Use UTC timestamps            | Mandatory across all systems                                 |
| Use read-only collection      | Avoid modifying workloads where possible                     |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 7. L3 Investigation Workflow Overview

| Phase    | Focus                                               | Output                          |
| -------- | --------------------------------------------------- | ------------------------------- |
| Phase 1  | Evidence acquisition                                | Evidence inventory              |
| Phase 2  | IAM and identity forensics                          | IAM abuse report                |
| Phase 3  | Cloud workload forensics                            | Runtime compromise report       |
| Phase 4  | Cloud storage and exfiltration analysis             | Data exposure report            |
| Phase 5  | Persistence and lateral movement                    | Persistence map                 |
| Phase 6  | Kubernetes and container analysis                   | Cluster compromise report       |
| Phase 7  | Timeline reconstruction                             | Authoritative timeline          |
| Phase 8  | IOC/TTP extraction                                  | Threat intelligence package     |
| Phase 9  | Eradication validation                              | Clean-state verification        |

---

# 8. Phase 1 – Evidence Acquisition

Cloud evidence must be preserved immediately because resources may be terminated automatically, logs may rotate quickly, and attackers may intentionally destroy evidence.

This is one of the most important phases of cloud forensics.

---

## 8.1 Evidence Collection Priorities

### Priority 1 – Critical Evidence (Immediately)

| Evidence Source                | Why Critical                              |
| ------------------------------ | ----------------------------------------- |
| CloudTrail / Audit Logs        | API activity evidence                     |
| IAM activity logs              | Identity compromise evidence              |
| Kubernetes audit logs          | Cluster activity evidence                 |
| VPC/flow logs                  | Network evidence                          |
| Cloud-native security findings | Native threat detections                  |
| Snapshot references            | Workload preservation                     |

### Priority 2 – High Value

| Evidence Source                | Why Important                             |
| ------------------------------ | ----------------------------------------- |
| VM snapshots                   | Disk evidence                             |
| Memory captures                | Runtime malware and credentials           |
| Container runtime logs         | Runtime activity                          |
| CI/CD logs                     | Automation abuse                          |
| Serverless execution logs      | Function abuse                            |

---

## 8.2 Detailed Evidence Collection Guidance

### 8.2A AWS Evidence Collection

Collect:

- CloudTrail logs
- GuardDuty findings
- VPC Flow Logs
- IAM credential reports
- EC2 snapshots
- Lambda execution logs
- S3 access logs
- Security Group configurations
- Route table configurations
- CloudWatch logs

Important checks:

| Check                                      | Why Important                        |
| ------------------------------------------ | ------------------------------------ |
| CloudTrail disabled?                       | Defense evasion                      |
| New access keys created?                   | Persistence                          |
| S3 public ACL changes?                     | Data exposure                        |
| Unusual AssumeRole activity?               | Lateral movement                     |

---

### 8.2B Azure Evidence Collection

Collect:

- Azure Activity Logs
- Entra sign-in logs
- Audit logs
- NSG Flow Logs
- Defender for Cloud findings
- VM snapshots
- Azure Storage logs
- Key Vault access logs
- Sentinel alerts

Important checks:

| Check                                      | Why Important                        |
| ------------------------------------------ | ------------------------------------ |
| OAuth consent grants                       | Token abuse                          |
| Global Administrator assignment            | Privilege escalation                 |
| Impossible travel events                   | Credential compromise                |
| Storage public access                      | Data exposure                        |

---

### 8.2C GCP Evidence Collection

Collect:

- Cloud Audit Logs
- SCC findings
- VPC Flow Logs
- IAM policy history
- GCS access logs
- VM snapshots
- Cloud Function logs

Important checks:

| Check                                      | Why Important                        |
| ------------------------------------------ | ------------------------------------ |
| Service account key creation               | Persistence                          |
| Logging disabled                           | Defense evasion                      |
| Public bucket ACL changes                  | Data exposure                        |

---

## 8.3 Evidence Acquisition Table

| Evidence Type           | Source                    | Collection Method              | Hash Required |
| ----------------------- | ------------------------- | ------------------------------ | ------------- |
| Cloud audit logs        | CloudTrail/Azure/GCP      | Export via API/console         | Yes           |
| VM snapshot             | EC2/Azure VM/GCE          | Snapshot API                   | Yes           |
| IAM export              | IAM APIs                  | JSON export                    | Yes           |
| Kubernetes logs         | Audit backend             | kubectl/API export             | Yes           |
| Flow logs               | VPC/NSG/Firewall logs     | SIEM/API export                | Yes           |
| Container image         | Registry export           | Save image hash                | Yes           |

---

# 9. Phase 2 – IAM and Identity Forensics

Identity compromise is the most common root cause of cloud incidents.

This phase is mandatory for all cloud incidents.

---

## 9.1 Core IAM Questions

L3 must answer:

| Question                                                      | Required Outcome                        |
| ------------------------------------------------------------- | --------------------------------------- |
| Which identities were compromised?                            | User/role/service account list          |
| Were credentials stolen or reused?                            | Credential abuse assessment             |
| Was privilege escalation performed?                           | IAM escalation map                      |
| Were new accounts, roles, or keys created?                    | Persistence inventory                   |
| Was federation abused?                                        | OAuth/SSO abuse assessment              |
| Did attacker pivot between accounts/projects?                 | Lateral movement confirmation           |

---

## 9.2 Detailed IAM Investigation Workflow

### Step 1 – Identify Initial Identity

Determine:

- Initial compromised user
- Initial compromised role
- Initial compromised access key
- OAuth or SSO abuse

Evidence sources:

- Cloud audit logs
- Sign-in logs
- Access logs
- Threat detection alerts

---

### Step 2 – Review Authentication Patterns

Look for:

| Indicator                                      | Why Important                        |
| ---------------------------------------------- | ------------------------------------ |
| Impossible travel                              | Credential theft                     |
| Access from unusual ASN/country                | External attacker                    |
| Multiple failed logins                         | Brute force                          |
| New MFA registration                           | Persistence                          |
| Session token reuse                            | Token theft                          |

---

### Step 3 – Review Privilege Escalation

Cloud attackers frequently escalate privileges quickly.

Review:

| Action                                         | Risk                                |
| ---------------------------------------------- | ----------------------------------- |
| New admin role assignment                      | Critical                            |
| Inline policy changes                          | Critical                            |
| New trust relationships                        | Persistence/lateral movement        |
| AssumeRole abuse                               | Cross-account movement              |

---

## 9.3 AWS IAM Forensics

### Investigate:

| Check                                      | Why Important                        |
| ------------------------------------------ | ------------------------------------ |
| Root login                                 | Critical compromise                  |
| New IAM user creation                      | Persistence                          |
| New access key creation                    | Persistence                          |
| STS token abuse                            | Temporary credential abuse           |
| CloudTrail disablement                     | Defense evasion                      |
| AssumeRole events                          | Cross-account movement               |

Key logs:

- CloudTrail
- GuardDuty
- IAM credential reports
- STS activity
- Access Advisor

---

## 9.4 Azure IAM / Entra Forensics

### Investigate:

| Check                                      | Why Important                        |
| ------------------------------------------ | ------------------------------------ |
| Impossible travel                          | Credential compromise                |
| OAuth app grants                           | Token abuse                          |
| MFA changes                                | Persistence                          |
| Global Admin assignments                   | Privilege escalation                 |
| Conditional Access policy changes          | Defense evasion                      |

Key logs:

- Entra sign-in logs
- Audit logs
- Defender alerts
- Sentinel analytics

---

## 9.5 GCP IAM Forensics

### Investigate:

| Check                                      | Why Important                        |
| ------------------------------------------ | ------------------------------------ |
| Service account key creation               | Persistence                          |
| IAM policy modifications                   | Privilege escalation                 |
| Logging disablement                        | Defense evasion                      |
| Excessive API activity                     | Automation abuse                     |

Key logs:

- Cloud Audit Logs
- SCC findings
- IAM policy history

---

# 10. Phase 3 – Cloud Workload Forensics

Cloud workloads include:

- Virtual machines
- Containers
- Kubernetes nodes
- Serverless functions

---

## 10.1 VM and Compute Forensics

### Investigation Checklist

| Check                                      | Evidence Source                      |
| ------------------------------------------ | ------------------------------------ |
| New processes                              | EDR/runtime logs                     |
| Outbound connections                       | Flow logs / EDR                      |
| Startup script changes                     | Cloud-init/user-data                 |
| New binaries                               | Disk analysis                        |
| Metadata service access                    | Runtime/network logs                 |
| Cryptomining indicators                    | CPU/network anomalies                |

---

## 10.2 Detailed Runtime Analysis

### Process Analysis

Review:

- Unexpected child processes
- Command interpreters spawned from cloud services
- Encoded PowerShell or shell commands
- Persistence scripts

### Network Analysis

Review:

- Outbound C2 traffic
- Connections to unusual regions
- TOR/VPN/proxy usage
- Large outbound transfers

### File System Analysis

Review:

- Startup scripts
- Scheduled tasks/cron jobs
- SSH authorized_keys
- New binaries
- Temporary staging directories

---

## 10.3 Memory and Snapshot Analysis

Memory analysis is critical because:

- Cloud malware may be fileless
- Tokens and credentials may only exist in memory
- Runtime C2 config may not be written to disk

Focus areas:

| Artifact Type                              | Why Important                        |
| ------------------------------------------ | ------------------------------------ |
| In-memory credentials                      | Token theft                          |
| Runtime malware                            | Fileless persistence                 |
| Process injection                          | Advanced compromise                  |
| Active network sessions                    | C2 confirmation                      |

---

# 11. Phase 4 – Storage and Data Exfiltration Analysis

Cloud storage incidents often become regulatory breaches.

---

## 11.1 Storage Investigation Workflow

### Step 1 – Identify Exposed Resources

Review:

- Public buckets/containers
- IAM access policies
- Object ACLs
- Sharing configurations

### Step 2 – Determine Data Sensitivity

Classify:

| Data Type                  | Risk Level |
| -------------------------- | ---------- |
| Customer PII               | Critical   |
| Financial data             | Critical   |
| Source code                | High       |
| Secrets/API keys           | Critical   |
| Internal docs              | Medium     |

### Step 3 – Review Access Logs

Look for:

- Anonymous access
- Large downloads
- Unusual geographies
- Bulk object reads
- Compression/archive creation

---

## 11.2 Exfiltration Indicators

| Indicator                                      | Why Important                        |
| ---------------------------------------------- | ------------------------------------ |
| Large outbound transfer                        | Data theft                           |
| Multiple object downloads                      | Collection activity                  |
| Public URL scraping                            | Exposure exploitation                |
| Archive creation                               | Staging before exfiltration          |
| Access from TOR/VPN                            | Attacker obfuscation                 |

---

## 11.3 Data Scope Estimation

L3 must estimate:

| Data Type                  | Estimated Volume | Confirmed Access? | Confirmed Exfil? |
| -------------------------- | ---------------- | ----------------- | ---------------- |
| Customer PII               |                  |                   |                  |
| Financial data             |                  |                   |                  |
| Source code                |                  |                   |                  |
| Credentials/secrets        |                  |                   |                  |

---

# 12. Phase 5 – Persistence and Lateral Movement

Cloud persistence frequently relies on IAM abuse instead of malware.

---

## 12.1 Common Cloud Persistence Mechanisms

| Persistence Type                         | Example                              |
| ---------------------------------------- | ------------------------------------ |
| New IAM users                            | Hidden admin                         |
| New API keys                             | Long-term access                     |
| OAuth grants                             | Token persistence                    |
| Lambda/function triggers                 | Hidden execution                     |
| Kubernetes service accounts              | Cluster persistence                  |
| New CI/CD tokens                         | Pipeline persistence                 |
| Cross-account trusts                     | Multi-account persistence            |

---

## 12.2 Lateral Movement Investigation

### Investigate:

| Indicator                                      | Meaning                              |
| ---------------------------------------------- | ------------------------------------ |
| AssumeRole activity                            | Cross-account pivot                  |
| Shared secrets access                          | Credential pivot                     |
| Shared CI/CD credentials                       | Pipeline abuse                       |
| Shared Kubernetes secrets                      | Cluster pivot                        |
| New peering or routes                          | Network pivot                        |

---

## 12.3 Persistence Validation Table

| Persistence Mechanism | Location | Created Time | Removed? | Evidence Ref |
| --------------------- | -------- | ------------ | -------- | ------------ |
|                       |          |              |          |              |

---

# 13. Phase 6 – Kubernetes and Container Analysis

Kubernetes compromise can impact multiple workloads simultaneously.

---

## 13.1 Kubernetes Investigation Priorities

| Check                                      | Why Important                        |
| ------------------------------------------ | ------------------------------------ |
| Cluster-admin role changes                 | Escalation                           |
| Privileged pods                            | Host compromise risk                 |
| Secrets access                             | Credential theft                     |
| kubectl exec activity                      | Interactive attacker access          |
| Node compromise                            | Cluster-wide impact                  |
| Daemonset creation                         | Persistence                          |

---

## 13.2 Container Runtime Analysis

Review:

| Artifact                                   | Why Important                        |
| ------------------------------------------ | ------------------------------------ |
| New container images                       | Supply chain/runtime compromise      |
| Image hash mismatch                        | Integrity failure                    |
| Runtime shell execution                    | Interactive compromise               |
| External network connections               | C2/exfiltration                      |
| Privileged container execution             | Host compromise risk                 |

---

# 14. Phase 7 – Timeline Reconstruction

All timestamps must be normalized to UTC.

---

## 14.1 Timeline Anchors

| Event                                      | Source                               |
| ------------------------------------------ | ------------------------------------ |
| First suspicious login                     | IAM/auth logs                        |
| First privilege escalation                 | IAM audit logs                       |
| First public exposure                      | Config/audit logs                    |
| First exfiltration event                   | Flow/proxy logs                      |
| First persistence action                   | IAM/runtime logs                     |
| First containment action                   | Change management logs               |

---

## 14.2 Timeline Table

| Time (UTC) | Resource | Event | Identity | Evidence Ref |
| ---------- | -------- | ----- | -------- | ------------ |
|            |          |       |          |              |

---

# 15. Phase 8 – IOC and Threat Intelligence Output

L3 must generate IOC packages for detection and hunting.

---

## 15.1 IOC Categories

| IOC Type                  | Examples                              |
| ------------------------- | ------------------------------------- |
| IP addresses              | C2 infrastructure                     |
| Domains                   | Exfiltration endpoints                |
| Access keys               | Compromised credentials               |
| IAM role names            | Persistence                           |
| File hashes               | Malware indicators                    |
| API patterns              | Abnormal cloud activity               |

---

## 15.2 Detection Engineering Recommendations

Examples:

- Hunt for AssumeRole anomalies
- Hunt for public storage changes
- Hunt for metadata service access
- Hunt for unusual API burst activity
- Hunt for cloud logging disablement
- Hunt for suspicious Kubernetes exec events
- Hunt for new IAM key creation spikes
- Hunt for unusual cloud region activity

---

# 16. Phase 9 – Eradication Guidance

---

## 16.1 Eradication Priorities

| Priority | Action                                      |
| -------- | ------------------------------------------- |
| P0       | Disable compromised credentials             |
| P1       | Remove persistence mechanisms               |
| P2       | Restore secure IAM policies                 |
| P3       | Patch vulnerable workloads                  |
| P4       | Re-enable validated logging                 |

---

## 16.2 Clean-State Validation

Before returning systems to production:

| Validation Check                            | Expected Result                    |
| ------------------------------------------- | ---------------------------------- |
| No unauthorized IAM entities                | Verified                           |
| No suspicious workloads running             | Verified                           |
| Logging fully operational                   | Verified                           |
| Public exposure removed                     | Verified                           |
| Persistence removed                         | Verified                           |
| Exfiltration paths blocked                  | Verified                           |
| Cross-account trust validated               | Verified                           |
| Kubernetes secrets rotated                  | Verified if applicable             |

---

# 17. Common L3 Pitfalls to Avoid

| Pitfall                                      | Impact                              | Prevention                         |
| -------------------------------------------- | ----------------------------------- | ---------------------------------- |
| Not exporting logs immediately               | Evidence loss                       | Export first                       |
| Ignoring IAM persistence                     | Attacker retains access             | Review all IAM thoroughly          |
| Failing to snapshot workloads                | Lost runtime evidence               | Snapshot before rebuild            |
| Ignoring cloud-native services               | Missed attack vectors               | Review all cloud services          |
| Not checking cross-account trusts            | Missed lateral movement             | Audit all trust relationships      |
| Assuming cloud provider logs are complete    | Logging gaps                        | Validate logging integrity         |
| Not reviewing Kubernetes audit logs          | Missed cluster compromise           | Always review cluster audit events |

---

# 18. MSSP Client Handling Notes

For MSSP cloud investigations:

- Segregate evidence strictly per client
- Maintain separate timelines per tenant
- Use encrypted evidence transfer methods
- Coordinate all client-facing findings with SDM
- Validate cross-client isolation during investigation
- Avoid sharing cloud account identifiers between clients

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/`

---

# 19. Related Documents

| Document                  | Path                                                         |
| ------------------------- | ------------------------------------------------------------ |
| Cloud Master              | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Master.md` |
| Cloud L1 Triage           | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L1-Triage.md` |
| Cloud L2 Investigation    | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L2-Investigation.md` |
| Cloud Containment         | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Containment.md` |
| AWS Specific              | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-AWS-Specific.md` |
| Azure Specific            | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Azure-Specific.md` |
| GCP Specific              | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-GCP-Specific.md` |
| Cloud MITRE Mapping       | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-MITRE-Mapping.md` |
| Data Breach Playbooks     | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`                |
| Evidence Handling         | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`                          |
| Memory Forensics SOP      | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Memory-Forensics-SOP.md` |

---

## 20. Revision History

| Version | Date        | Author                                   | Changes         |
| ------- | ----------- | ---------------------------------------- | --------------- |
| 1.0     | 20-May-2026 | L3 Lead / IR Team Lead / Cloud Security Lead | Initial version |

---

## 21. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**