# CAT-10 – Cloud Security Incident Category

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Incident Category – Cloud Security Incident |
| Document ID | IR-CAT-010 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Category Overview

| Field | Details |
|-------|---------|
| Category ID | CAT-10 |
| Default Severity | P1 – Critical (admin takeover/data breach/service disruption) / P2 – High (confirmed compromise or high-risk misconfiguration) / P3 – Medium (suspicious activity) |
| Escalation Priority | High due to rapid blast radius and credential/token risk |
| Attack Goal | Account takeover, data access, privilege escalation, persistence, resource abuse, disruption |
| Threat Actors | Cybercriminals, APT groups, insiders, compromised vendors |
| Coverage | AWS, Azure, GCP, SaaS (M365/Google Workspace), cloud-native services |
| Playbook Reference | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/` |

---

## 3. What is a Cloud Security Incident?

A cloud security incident is any event that compromises, or is likely to
compromise, the confidentiality, integrity, or availability of cloud
resources, data, or identities.

Cloud incidents commonly involve:

- Compromised identities (users, service principals, access keys)
- Misconfigurations exposing resources publicly
- Unauthorized changes to cloud resources or security controls
- Abuse of cloud services for persistence or resource hijacking
- Data access, exfiltration, or tampering using cloud-native APIs

Cloud incidents can spread quickly due to:

- High-privilege identities controlling multiple services
- Automation and infrastructure-as-code deployment patterns
- Shared or federated authentication with on-prem environments
- Broad access via tokens, API keys, and service principals

---

## 4. Common Cloud Incident Types

| Incident Type | Description |
|--------------|-------------|
| Cloud Account Takeover | Unauthorized access to cloud console or API |
| Privilege Escalation | Unauthorized assignment of admin roles/permissions |
| Public Exposure | Storage bucket/container publicly accessible |
| Data Exfiltration | Large object downloads or exports from cloud services |
| Malicious Resource Changes | Security group changes, route table changes, IAM policy edits |
| Resource Hijacking | Crypto mining, abuse of compute resources, billing spikes |
| Token / Key Compromise | API keys, access tokens, refresh tokens leaked or stolen |
| Service Principal Abuse | Compromise of automation identity in CI/CD |
| SaaS Compromise | Mailbox takeover, OAuth abuse, external forwarding |
| Cloud Logging Tampering | Disabling audit logs or modifying retention settings |

---

## 5. Typical Attack Vectors

| Vector | Description |
|--------|-------------|
| Stolen Credentials | Password reuse, phishing, credential stuffing |
| Token Theft | Session hijacking, token replay, OAuth abuse |
| Exposed Keys | API keys leaked in repos, CI logs, config files |
| Misconfiguration | Public buckets, overly permissive IAM policies |
| Exploited Cloud Workload | Vulnerable web app running in cloud compute |
| Compromised CI/CD | Build pipeline compromise leading to privileged access |
| Third-Party Integration | Abused SaaS integrations with delegated permissions |
| Insider Misuse | Authorized user changes or data access outside role |

---

## 6. Indicators of Cloud Compromise (IoCs and Observables)

### 6.1 Identity and Access Indicators

| Indicator | Details |
|----------|---------|
| Unusual Login | New geography, ASN, device fingerprint |
| Impossible Travel | Rapid location changes for same identity |
| Admin Role Assignment | Privilege escalation events |
| New Access Keys | Keys created unexpectedly (AWS access keys, Azure app secrets) |
| Token Replay | Sign-ins from unusual sources using existing tokens |
| MFA Changes | MFA disabled, new device added, recovery info changed |
| Service Principal Changes | New credentials or permissions granted to automation accounts |

### 6.2 Resource and Configuration Indicators

| Indicator | Details |
|----------|---------|
| Storage ACL Change | Public access enabled on storage bucket/container |
| Security Group Change | Ports opened to the internet unexpectedly |
| IAM Policy Change | Wildcard permissions, admin privileges added |
| Logging Disabled | CloudTrail/Activity Logs disabled or retention reduced |
| New Admin Users | New users created with high privileges |
| Suspicious Compute | New instances/VMs created outside normal pattern |
| Billing Spike | Unexpected spend increase indicating resource hijacking |

### 6.3 Data Access and Exfiltration Indicators

| Indicator | Details |
|----------|---------|
| Mass Download | Large object downloads from storage |
| Export Jobs | Database exports, snapshots shared externally |
| External Sharing | Link sharing enabled broadly or publicly |
| Unusual API Calls | High volume of list/get/download operations |
| Cross-Account Access | Access from accounts not normally interacting |

### 6.4 Key Log Sources

| Source | What to Look For |
|--------|------------------|
| Cloud Audit Logs | Sign-ins, API calls, role assignments, key creation |
| IAM Logs | Permission changes, policy edits, user creation |
| Storage Access Logs | Object downloads, ACL changes, external access |
| Network Flow Logs | Egress patterns, destination IPs/regions |
| CSPM Alerts | Misconfiguration detection findings |
| SIEM | Correlated identity + resource changes |
| SaaS Logs | Mailbox rules, OAuth grants, forwarding, sharing |

---

## 7. Severity Classification

| Scenario | Severity |
|----------|----------|
| Cloud admin account takeover confirmed | P1 – Critical |
| Confirmed exfiltration of sensitive data from cloud storage/SaaS | P1 – Critical |
| Public exposure of sensitive storage with confirmed access | P1 – Critical |
| Logging disabled or security controls tampered in production | P1 – Critical |
| Confirmed unauthorized changes to IAM policies enabling persistence | P1 – Critical |
| Confirmed compromise of service principal with broad access | P2 – High |
| Confirmed compromise of user account with limited access | P2 – High |
| High-risk misconfiguration with no confirmed access yet | P2 – High |
| Suspicious sign-in events requiring validation | P3 – Medium |
| Low-risk CSPM finding or informational alert | P4 – Low |

---

## 8. Immediate Response Actions

### 8.1 First 15 Minutes

- Create incident ticket and assign initial severity
- Notify SOC Lead immediately for P2 and above
- Identify cloud provider/service involved (AWS/Azure/GCP/SaaS)
- Preserve audit logs for the time window (do not delay)
- Identify impacted identity (user/service principal/access key)
- Determine whether unauthorized access is confirmed or suspected
- Initiate containment approval for high-risk access:
  - revoke sessions
  - disable access keys
  - block suspicious IPs via conditional access (where applicable)

### 8.2 First 1 Hour

- Contain identity compromise:
  - reset credentials
  - revoke tokens/sessions
  - rotate access keys/secrets
  - remove unknown MFA methods
- Validate IAM changes:
  - new users, roles, policies
  - privilege assignments
- Validate resource changes:
  - storage permissions
  - security groups
  - firewall rules
  - new instances or services
- Scope all impacted resources and subscriptions/accounts/projects
- Escalate to P1 if admin takeover, logging tampering, or data exfiltration confirmed

### 8.3 First 4 Hours

- Confirm whether data access/exfiltration occurred:
  - storage download logs
  - sharing events
  - database export events
  - egress traffic
- Remove persistence:
  - delete rogue users/keys (after evidence capture)
  - roll back IAM policy changes
  - remove malicious OAuth grants and app registrations
- Implement hardening:
  - enforce MFA
  - apply conditional access
  - restrict public access defaults
  - improve logging retention and immutability
- Provide management status update for P2/P1
- Begin regulatory notification assessment if sensitive data involved

---

## 9. Containment and Recovery Guidance

| Action | Purpose | Notes |
|-------|---------|------|
| Revoke Sessions | Stop active attacker sessions | Fast, low impact |
| Disable/Rotate Keys | Cut off API access | Rotate keys used by automation carefully |
| Roll Back IAM Changes | Remove unauthorized privileges | Preserve evidence prior to rollback |
| Enforce MFA / Conditional Access | Reduce further compromise | Validate user experience impact |
| Restrict Public Access | Close exposure | Capture pre-change configuration for evidence |
| Quarantine Resources | Isolate suspicious instances | Use tags, network policies, or isolation |
| Rebuild Compromised Workloads | Restore integrity | Use golden images and IaC where possible |
| Validate Logging | Ensure audit logs retained | Confirm logs are enabled and immutable |

---

## 10. MITRE ATT&CK Mapping (Cloud-Relevant)

| Tactic | Technique | ID |
|--------|-----------|----|
| Initial Access | Valid Accounts | T1078 |
| Initial Access | Cloud Accounts | T1078.004 |
| Credential Access | Steal Web Session Cookie | T1539 |
| Credential Access | Adversary-in-the-Middle | T1557 |
| Persistence | Account Manipulation | T1098 |
| Persistence | Create Account | T1136 |
| Privilege Escalation | Abuse Elevation Control Mechanism | T1548 |
| Defense Evasion | Modify Cloud Compute Infrastructure | T1578 |
| Defense Evasion | Disable or Modify Tools | T1562 |
| Collection | Data from Cloud Storage Object | T1530 |
| Exfiltration | Exfiltration Over Web Service | T1567 |
| Impact | Resource Hijacking | T1496 |

---

## 11. Key Investigation Questions

1. Which cloud provider/service is affected?
2. Which identity was involved (user, service principal, access key)?
3. Are sign-in anomalies present (geo, ASN, device, impossible travel)?
4. Were access keys/tokens created, rotated, or used unexpectedly?
5. Were IAM roles/policies changed (new admin privileges granted)?
6. Were logging configurations disabled or altered?
7. Were any resources made public (storage, security groups, endpoints)?
8. Was data accessed or downloaded at unusual volume?
9. Were new compute resources created (possible crypto mining)?
10. Is there evidence of persistence (new users, app registrations, OAuth grants)?
11. What is the blast radius (accounts/subscriptions/projects/tenants)?
12. What remediation steps will not disrupt critical services?
13. Are regulatory or contractual notifications required?

---

## 12. Critical Do's and Do Not's

### Do

- Preserve cloud audit logs immediately and verify retention
- Revoke sessions and rotate keys quickly when compromise suspected
- Confirm IAM and logging integrity early (attackers often disable logs)
- Capture pre-change configurations before remediation
- Coordinate with cloud owners and application teams before disruptive changes
- Validate whether automation/service principals will be impacted by key rotations
- Document all actions and approvals

### Do Not

- Disable production resources without business approval unless emergency
- Rotate keys blindly without confirming dependent services
- Assume public exposure means no access occurred (verify access logs)
- Remove malicious identities before capturing audit evidence
- Close incident without verifying persistence removal and logging restoration

---

## 13. Escalation Path

| Stage | Action |
|-------|--------|
| L1 Triage | Identify cloud alert, open ticket, preserve initial logs |
| L2 Investigation | Validate compromise, scope IAM/resource changes |
| SOC Lead | Approve severity and coordinate communications |
| Cloud Security / Cloud Ops | Execute containment (keys, IAM, configs) |
| L3 / IR Team | Engage for admin takeover, breach, or complex persistence |
| GRC / Compliance | Assess breach notification and reporting obligations |
| Legal | Guide disclosure, evidence handling, and external communication |
| Management / CISO | Approve major actions, regulatory strategy, client communications |
| MSSP SDM / Client Owner | Coordinate client actions and required notifications |

---

## 14. Regulatory and Client Reporting Considerations

| Trigger | Action |
|--------|--------|
| Sensitive data exposure in cloud storage | Engage Compliance and Legal immediately |
| Admin takeover or broad IAM compromise | Treat as major incident; assess reporting |
| MSSP multi-client exposure | Notify affected clients per SLA and contract |
| Critical cloud service disruption | Assess customer communication requirements |
| Evidence handling requirement | Ensure audit log preservation is defensible |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 15. Evidence Collection Requirements

| Evidence Type | Priority | Notes |
|--------------|----------|-------|
| Cloud audit logs export | Critical | Sign-ins, API calls, role changes |
| IAM change logs | Critical | Policy edits, role assignments, new identities |
| Storage access logs | High | Object downloads, ACL changes |
| Network flow logs | High | Egress destinations and volumes |
| CSPM findings and snapshots | High | Misconfiguration evidence |
| SaaS mailbox logs (if applicable) | High | Forwarding rules, OAuth grants |
| Resource configuration snapshots | High | Security groups, public endpoints |
| Billing and usage reports | Medium | Identify resource hijacking |
| Change records | Critical | Key rotations, policy rollbacks |
| Chain-of-custody forms | As needed | For legal-grade evidence |

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 16. Related Documents

| Document | Path |
|---------|------|
| Cloud Master Playbook | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Master.md` |
| L1 Triage Playbook | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L1-Triage.md` |
| L2 Investigation Playbook | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L2-Investigation.md` |
| L3 Forensics Playbook | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L3-Forensics.md` |
| AWS Specific | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-AWS-Specific.md` |
| Azure Specific | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Azure-Specific.md` |
| GCP Specific | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-GCP-Specific.md` |
| Containment Playbook | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Containment.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-MITRE-Mapping.md` |
| Data Breach Category | `01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/CAT-06-Data-Breach-Exfiltration.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |

---

## 17. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Manager | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**