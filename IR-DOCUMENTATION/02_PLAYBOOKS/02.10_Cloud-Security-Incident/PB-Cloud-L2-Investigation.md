# Playbook: Cloud Security Incident – L2 Investigation

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Cloud Security Incident (L2 Investigation)        |
| Document ID    | IR-PB-CLD-003                                                |
| Version        | 1.0                                                          |
| Effective Date | 20-May-2026                                                  |
| Owner          | L2 SOC Lead / Cloud Security Lead                            |
| Approved By    | IR Team Lead                                                 |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 cloud security incident        |

---

## 2. Purpose

This document defines the Level 2 (L2) investigation procedures for cloud security incidents escalated from L1 triage.

Cloud investigations at L2 are different from traditional infrastructure investigations because:

- Identity, API usage, and cloud-native automation are central to the attack chain
- Attackers frequently use legitimate cloud APIs instead of malware
- Compromise may span multiple regions, subscriptions, projects, or accounts
- Persistence often relies on IAM abuse rather than traditional malware persistence
- Cloud workloads can be ephemeral and disappear quickly
- Logging and telemetry are distributed across many cloud-native services

L2 objectives:

- Confirm whether compromise or exposure actually occurred
- Determine attack scope across cloud resources
- Identify affected accounts, IAM entities, workloads, storage, and regions
- Assess data exposure and breach indicators
- Identify persistence and lateral movement indicators
- Build actionable containment recommendations
- Escalate to L3 or IR Team when required

L2 must produce:

- A technically defensible investigation summary
- Clear impact assessment
- Structured timeline
- Prioritized containment actions
- Evidence references for every major finding

---

## 3. Scope

Applies to investigation of:

- AWS incidents
- Azure/Entra incidents
- GCP incidents
- Multi-cloud incidents
- IAM compromise
- Cloud storage exposure
- Kubernetes compromise
- Container runtime compromise
- Serverless abuse
- Cloud API abuse
- Cloud malware/cryptomining
- Cloud lateral movement
- Cloud-native persistence
- Cross-account compromise

Includes:

- Production cloud environments
- Development and staging cloud environments
- MSSP-managed cloud tenants
- Hybrid cloud/on-prem integrated environments

---

## 4. Preconditions (Inputs from L1)

Before L2 begins, confirm the ticket includes:

| Required Input                    | Minimum Content                                      |
| --------------------------------- | ---------------------------------------------------- |
| Cloud provider                    | AWS / Azure / GCP                                    |
| Account/subscription/project ID   | Yes                                                  |
| Region                            | Yes                                                  |
| Resource identifiers              | Instance/bucket/VM/cluster IDs                       |
| Alert source and finding          | SIEM/GuardDuty/Defender/SCC/etc.                     |
| Initial severity recommendation   | P1–P4 with rationale                                 |
| IAM context                       | User/role/service account details                    |
| Evidence references               | Logs exported or preserved                           |
| Data exposure context             | Public resource / sensitive data indicators          |

Reference:
`02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L1-Triage.md`

---

## 5. L2 Required Outputs

L2 must provide the following:

| Output                              | Required Detail                                      |
| ----------------------------------- | ---------------------------------------------------- |
| Confirmed incident status           | Confirmed / Likely / Not confirmed                   |
| Affected resource inventory         | Cloud resources impacted                             |
| IAM impact assessment               | Compromised users, roles, keys, sessions             |
| Data exposure assessment            | Scope and sensitivity                                |
| Persistence assessment              | New users/roles/keys/jobs/functions                  |
| Lateral movement assessment         | Cross-account or workload pivoting                   |
| Timeline                            | UTC timeline with evidence references                |
| Containment recommendations         | Prioritized actions with owners                      |
| Escalation decision                 | L3 / IR Team requirement                             |
| Evidence references                 | All findings linked to evidence                      |

---

## 6. Investigation Workflow Overview

| Phase   | Goal                                                  | Key Output                     |
| ------- | ----------------------------------------------------- | ------------------------------ |
| Phase 1 | Validate compromise or exposure                       | Confirmed impact status        |
| Phase 2 | Scope affected cloud resources                        | Resource inventory             |
| Phase 3 | IAM and authentication investigation                  | IAM impact assessment          |
| Phase 4 | Storage and data exposure assessment                  | Data exposure status           |
| Phase 5 | Workload and runtime investigation                    | Runtime compromise status      |
| Phase 6 | Persistence and lateral movement investigation        | Persistence assessment         |
| Phase 7 | Timeline reconstruction                               | UTC timeline                   |
| Phase 8 | Containment recommendations                           | Action plan                    |
| Phase 9 | Escalation decision                                   | L3 / IR Team activation        |

---

# 7. Phase 1 – Confirm Compromise or Exposure

Cloud alerts frequently represent suspicious activity but not always confirmed compromise.

L2 must determine:

- Was the activity malicious?
- Was there unauthorized access?
- Was data exposed?
- Did attacker actions succeed?

---

## 7.1 Cloud Incident Confidence Levels

| Level            | Meaning                                                  | Evidence Required                                  |
| ---------------- | -------------------------------------------------------- | -------------------------------------------------- |
| Confirmed        | Unauthorized access or malicious action confirmed        | Log/API evidence or confirmed exposure             |
| Highly Likely    | Strong indicators but incomplete visibility              | Multiple correlated indicators                     |
| Possible         | Some indicators present but uncertain                    | Single weak indicator                              |
| Not Confirmed    | Alert appears benign or false positive                   | Supporting evidence disproves compromise           |

---

## 7.2 Immediate High-Risk Indicators

If any of the following are confirmed, escalate severity immediately:

| Indicator                                                | Risk Level |
| -------------------------------------------------------- | ---------- |
| Root/admin account compromise                            | Critical   |
| CloudTrail/Audit logging disabled                        | Critical   |
| Public storage with sensitive data                       | Critical   |
| Access key created unexpectedly                          | High       |
| Cross-account role assumption from unusual source        | High       |
| Kubernetes cluster-admin abuse                           | High       |
| Large outbound data transfer                             | Critical   |
| IAM policy granting full admin                           | Critical   |
| MFA disabled for privileged account                      | High       |
| Multiple regions/accounts affected                       | Critical   |

---

# 8. Phase 2 – Scope Affected Resources

L2 must identify every affected cloud resource.

---

## 8.1 Resource Inventory Collection

| Resource Type          | Examples                                          |
| ---------------------- | ------------------------------------------------- |
| Compute                | EC2, Azure VM, GCE, Lambda, Functions             |
| Storage                | S3, Blob, GCS                                     |
| Identity               | IAM users, roles, Entra users, service accounts   |
| Networking             | VPC, NSG, security groups, routes                 |
| Kubernetes             | EKS, AKS, GKE clusters                            |
| Databases              | RDS, Azure SQL, Cloud SQL                         |
| CI/CD                  | CodeBuild, Azure DevOps, Cloud Build              |

---

## 8.2 Required Scope Table

| Resource Name | Type | Region | Account/Project | Public? | Sensitive? | Evidence Ref |
| ------------- | ---- | ------ | --------------- | ------- | ----------- | ------------ |
|               |      |        |                 |         |             |              |

---

## 8.3 Multi-Region and Multi-Account Scope

Cloud attackers frequently pivot across:

- Multiple AWS accounts
- Azure subscriptions
- GCP projects
- Multiple cloud regions
- Shared Kubernetes clusters
- Shared IAM trust relationships

L2 must:

- Enumerate all linked accounts/projects
- Check organization-level IAM trusts
- Review cross-account role assumptions
- Review federation relationships

---

# 9. Phase 3 – IAM and Authentication Investigation

Identity is the primary attack surface in cloud incidents.

This phase is mandatory for every cloud investigation.

---

## 9.1 IAM Investigation Checklist

| Check Item                                         | Why Important                           |
| -------------------------------------------------- | --------------------------------------- |
| New access keys created                            | Persistence or credential abuse         |
| New IAM users or roles                             | Persistence                             |
| Privileged role assignments                        | Privilege escalation                    |
| MFA disabled                                       | Account weakening                       |
| Impossible travel                                  | Credential compromise                   |
| Excessive failed logins                            | Brute force or password spraying        |
| OAuth app grants                                   | Token abuse                             |
| Cross-account AssumeRole activity                  | Lateral movement                        |
| Service account key creation                       | Persistence                             |

---

## 9.2 Key Questions L2 Must Answer

| Question                                                      | Required Output                         |
| ------------------------------------------------------------- | --------------------------------------- |
| Which identity was used?                                      | User/role/service account               |
| Was MFA enabled?                                              | Yes/No                                  |
| What APIs were called?                                        | API activity summary                    |
| Were privileges escalated?                                    | Yes/No + details                        |
| Were new credentials created?                                 | Yes/No + details                        |
| Were sessions/token reused?                                   | Yes/No                                  |
| Was cross-account access used?                                | Yes/No                                  |

---

## 9.3 Cloud-Specific IAM Indicators

### AWS

| Indicator                              | Meaning                             |
| -------------------------------------- | ----------------------------------- |
| AssumeRole from unusual IP             | Cross-account abuse                 |
| New access key creation                | Persistence                         |
| Root login without MFA                 | Critical compromise                 |
| CloudTrail disabled                    | Defense evasion                     |

### Azure

| Indicator                              | Meaning                             |
| -------------------------------------- | ----------------------------------- |
| New Global Administrator assignment    | Privilege escalation                |
| OAuth consent grant                    | Token abuse                         |
| Impossible travel                      | Credential theft                    |

### GCP

| Indicator                              | Meaning                             |
| -------------------------------------- | ----------------------------------- |
| Service account key creation           | Persistence                         |
| IAM policy changes                     | Privilege escalation                |
| Logging disabled                       | Defense evasion                     |

---

# 10. Phase 4 – Storage and Data Exposure Assessment

Cloud storage exposure is one of the highest-risk cloud incident categories.

---

## 10.1 Storage Investigation Checklist

| Check                                          | Purpose                              |
| ---------------------------------------------- | ------------------------------------ |
| Public access enabled?                         | Exposure risk                        |
| Sensitive data stored?                         | Breach assessment                    |
| Object access logs enabled?                    | Determine access evidence            |
| Versioning enabled?                            | Recovery support                     |
| Encryption enabled?                            | Data protection review               |
| Anonymous access detected?                     | Confirm exploitation                 |
| Large download activity?                       | Potential exfiltration               |

---

## 10.2 Storage Exposure Assessment Table

| Storage Resource | Public? | Sensitive Data | Access Confirmed? | Logging Enabled? | Exfil Indicators? |
| ---------------- | ------- | -------------- | ----------------- | ---------------- | ----------------- |
|                  |         |                |                   |                  |                   |

---

## 10.3 Data Breach Trigger Assessment

L2 must formally answer:

| Question                                                      | Answer (Yes/No/Unknown) |
| ------------------------------------------------------------- | ----------------------- |
| Was sensitive data publicly accessible?                       |                         |
| Were unauthorized downloads detected?                         |                         |
| Were access logs available?                                   |                         |
| Was regulated data involved?                                  |                         |
| Was exfiltration confirmed or highly likely?                  |                         |

If any answer indicates likely breach:
- Activate Data Breach playbooks immediately
- Notify SOC Lead and Legal/Compliance

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`

---

# 11. Phase 5 – Workload and Runtime Investigation

Cloud workloads include VMs, containers, and serverless services.

---

## 11.1 Workload Compromise Indicators

| Indicator                                      | Meaning                             |
| ---------------------------------------------- | ----------------------------------- |
| Cryptomining process                           | Unauthorized compute usage          |
| Unexpected outbound connections                | C2 or exfiltration                  |
| New startup scripts                            | Persistence                         |
| Container exec activity                        | Interactive attacker access         |
| Suspicious child processes                     | Malware execution                   |
| New binaries or scripts                        | Backdoor deployment                 |
| Metadata service access                        | Credential theft                    |

---

## 11.2 Kubernetes Investigation Priorities

If Kubernetes is involved:

| Check                                      | Why Important                        |
| ------------------------------------------ | ------------------------------------ |
| Cluster-admin role creation                | Privilege escalation                 |
| Privileged pods                            | Host compromise risk                 |
| Secrets access                             | Credential theft                     |
| kubectl exec activity                      | Interactive attacker access          |
| Node compromise                            | Cluster-wide impact                  |
| New service accounts                       | Persistence                          |

---

## 11.3 Serverless Investigation Priorities

| Check                                      | Why Important                        |
| ------------------------------------------ | ------------------------------------ |
| Function code changes                      | Backdoor injection                   |
| Environment variable access                | Secret exposure                      |
| Unusual invocation spikes                  | Abuse or cryptomining                |
| New external network calls                 | C2/exfiltration                      |

---

# 12. Phase 6 – Persistence and Lateral Movement

Cloud persistence frequently relies on IAM abuse instead of malware.

---

## 12.1 Cloud Persistence Mechanisms

| Persistence Type                         | Example                              |
| ---------------------------------------- | ------------------------------------ |
| New IAM users                            | Hidden admin user                    |
| New access keys                          | Long-term credential access          |
| OAuth grants                             | Persistent delegated access          |
| New Lambda/Function triggers             | Hidden execution                     |
| Kubernetes service accounts              | Cluster persistence                  |
| Cross-account trust relationships        | Lateral movement                     |
| New API tokens                           | Automation persistence               |

---

## 12.2 Lateral Movement Indicators

| Indicator                                | Meaning                              |
| ---------------------------------------- | ------------------------------------ |
| Cross-account role assumptions           | Multi-account movement               |
| New peering or routing                   | Network pivot                        |
| Shared secrets accessed                  | Credential pivot                     |
| CI/CD abuse                              | Deployment pipeline compromise       |
| Shared Kubernetes secrets                | Cluster pivot                        |

---

# 13. Phase 7 – Timeline Reconstruction

All cloud investigations require a UTC timeline.

---

## 13.1 Timeline Anchors

| Anchor Event                              | Source                               |
| ----------------------------------------- | ------------------------------------ |
| First suspicious login                    | IAM/auth logs                        |
| First malicious API call                  | Audit logs                           |
| First privilege escalation                | IAM logs                             |
| First storage exposure                    | Config logs                          |
| First outbound transfer                   | Flow/proxy logs                      |
| First containment action                  | Change logs                          |

---

## 13.2 Timeline Table (Required)

| Time (UTC) | Resource | Event | User/Role | Evidence Ref |
| ---------- | -------- | ----- | --------- | ------------ |
|            |          |       |           |              |

---

# 14. Phase 8 – Containment Recommendations

L2 must provide a prioritized containment plan.

---

## 14.1 Cloud Containment Recommendation Matrix

| Finding                                      | Recommended Action                     | Owner           | Approval |
| -------------------------------------------- | -------------------------------------- | ---------------- | -------- |
| IAM compromise                               | Disable keys/sessions                  | IAM Team         | SOC Lead |
| Public storage exposure                      | Remove public access                   | Cloud Team       | SOC Lead |
| Kubernetes compromise                        | Isolate cluster/node                   | Platform Team    | IR Team  |
| Active exfiltration                          | Block egress immediately               | Network Team     | IR Team  |
| Cross-account compromise                     | Disable trust relationships            | IAM Team         | CISO     |
| CloudTrail disabled                          | Re-enable immediately                  | Cloud Team       | SOC Lead |
| Cryptomining                                 | Isolate workload                       | Cloud Team       | SOC Lead |

---

## 14.2 High-Risk Containment Actions

The following require elevated approval:

| Action                                      | Why High Risk                         |
| ------------------------------------------- | ------------------------------------- |
| Disable root/admin account                  | Potential production impact           |
| Shut down Kubernetes cluster                | Large-scale outage                    |
| Remove cloud peering                        | Connectivity disruption               |
| Revoke all OAuth grants                     | Broad user impact                     |
| Disable CI/CD pipeline                      | Deployment interruption               |

---

# 15. Phase 9 – Escalation Decision

---

## 15.1 Escalate to L3 if:

| Condition                                      | Reason                               |
| ---------------------------------------------- | ------------------------------------ |
| Persistence confirmed                          | Deep forensic analysis required      |
| Multi-account compromise                       | Advanced scoping required            |
| Kubernetes compromise                          | Runtime forensics required           |
| Logging tampering detected                     | Evidence reconstruction needed       |
| Data exfiltration likely                       | Forensic validation required         |

---

## 15.2 Escalate to IR Team if:

| Condition                                      | Reason                               |
| ---------------------------------------------- | ------------------------------------ |
| Root/admin compromise                          | Crisis-level incident                |
| Sensitive data breach                          | Legal/regulatory impact              |
| Multi-client cloud impact                      | MSSP crisis coordination             |
| Cross-cloud compromise                         | Enterprise-wide impact               |
| Active attacker in environment                 | Major incident response              |

---

# 16. Documentation Requirements

Before handoff or closure, complete:

| Requirement                                      | Status |
| ------------------------------------------------ | ------ |
| Affected resources inventory completed           | ☐      |
| IAM assessment completed                         | ☐      |
| Storage exposure assessment completed            | ☐      |
| Timeline completed                               | ☐      |
| Data breach trigger documented                   | ☐      |
| Containment recommendations documented           | ☐      |
| Escalation decision documented                   | ☐      |
| Evidence references attached                     | ☐      |

---

## 17. Common L2 Mistakes to Avoid

| Mistake                                              | Risk                                      | Correct Approach                              |
| ---------------------------------------------------- | ----------------------------------------- | --------------------------------------------- |
| Investigating only one region/account                | Missed attacker movement                  | Check all linked environments                 |
| Ignoring IAM activity                                | Missed persistence                        | Always review IAM thoroughly                  |
| Failing to export logs quickly                       | Evidence loss                             | Export immediately                            |
| Assuming public storage means confirmed breach       | Inaccurate reporting                      | Verify access evidence                        |
| Not checking cloud-native logging                    | Missing key evidence                      | Review provider-native logs first             |
| Ignoring serverless or containers                    | Missed runtime compromise                 | Review all compute models                     |

---

## 18. MSSP Client Handling Notes

For MSSP-managed cloud environments:

- Maintain strict tenant segregation
- Document all client-specific actions
- Obtain client approvals for high-impact containment
- Store evidence separately per client
- Notify SDM for all P1/P2 incidents

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/`

---

## 19. Related Documents

| Document                  | Path                                                         |
| ------------------------- | ------------------------------------------------------------ |
| Cloud Master              | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Master.md` |
| Cloud L1 Triage           | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L1-Triage.md` |
| Cloud L3 Forensics        | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L3-Forensics.md` |
| Cloud Containment         | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Containment.md` |
| Cloud AWS Specific        | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-AWS-Specific.md` |
| Cloud Azure Specific      | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Azure-Specific.md` |
| Cloud GCP Specific        | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-GCP-Specific.md` |
| Cloud MITRE Mapping       | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-MITRE-Mapping.md` |
| Data Breach Playbooks     | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`                |
| Evidence Handling         | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`                          |

---

## 20. Revision History

| Version | Date        | Author                                 | Changes         |
| ------- | ----------- | -------------------------------------- | --------------- |
| 1.0     | 20-May-2026 | L2 SOC Lead / Cloud Security Lead      | Initial version |

---

## 21. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**