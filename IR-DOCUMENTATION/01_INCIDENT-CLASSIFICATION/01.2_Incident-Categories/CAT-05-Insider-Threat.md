# CAT-05 – Insider Threat Incident Category

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Incident Category – Insider Threat |
| Document ID | IR-CAT-005 |
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
| Category ID | CAT-05 |
| Default Severity | P2 – High (confirmed malicious or sensitive data exposure) / P3 – Medium (suspicious behavior) |
| Escalation Priority | High due to legal, HR, and reputational implications |
| Attack Goal | Unauthorized data access, theft, sabotage, policy violation, fraud |
| Threat Actors | Employees, contractors, third-party support staff, former employees |
| Playbook Reference | `02_PLAYBOOKS/02.5_Insider-Threat/` |

---

## 3. What is an Insider Threat?

An insider threat is a security incident where a person with authorized
access (or a person who previously had access) misuses that access to
harm the organization or its clients.

Insider threats may be:

- Malicious (intentional harm, data theft, sabotage)
- Negligent (unsafe behavior, policy violations, accidental exposure)
- Compromised insider (legitimate user account controlled by an attacker)

Insider investigations typically require coordination across multiple
functions because they may involve employment actions, disciplinary
processes, privacy obligations, and legal evidence handling.

---

## 4. Insider Threat Types

| Type | Description |
|------|-------------|
| Malicious Insider | Intentional actions to steal data, sabotage systems, or commit fraud |
| Negligent Insider | Unintentional actions leading to exposure (misdelivery, weak passwords, unsafe handling) |
| Compromised Insider | Legitimate account taken over by external attacker |
| Privileged Insider | Insider with elevated access (admin, database, cloud admin) posing higher risk |
| Third-Party Insider | Vendor or contractor with access misusing or mishandling access |
| Departing Employee Risk | Increased risk during resignation/termination windows |

---

## 5. Common Insider Threat Scenarios

| Scenario | Description |
|---------|-------------|
| Data Exfiltration | Copying sensitive files to USB, personal cloud storage, email forwarding |
| Unauthorized Access | Accessing systems or files outside job role, after-hours access to sensitive systems |
| Sabotage | Deleting files, altering configurations, disabling security controls |
| Fraud | Manipulating financial systems, invoices, payroll, procurement, or customer records |
| Policy Violations | Sharing credentials, bypassing controls, shadow IT usage |
| Account Abuse | Creating backdoor accounts, privilege escalation without approval |
| Intellectual Property Theft | Copying source code, product designs, customer lists |
| Excessive Downloading | Large downloads from file shares or repositories by one user |

---

## 6. Indicators of Insider Threat (IoCs and Observables)

### 6.1 User Behavior Indicators

| Indicator | Details |
|----------|---------|
| Unusual Access Times | After-hours access inconsistent with role |
| Unusual Access Volume | Large number of files accessed in short period |
| Access Outside Role | Access to HR, finance, or sensitive data not required for duties |
| Privilege Misuse | Privileged commands executed without change request |
| Attempts to Disable Logging | Clearing logs, disabling agents, modifying audit settings |
| Multiple Failed Logins | Repeated failures followed by success across systems |
| Geographical Anomalies | Remote logins from unusual locations or IP ranges |

### 6.2 Data Handling Indicators

| Indicator | Details |
|----------|---------|
| External Transfers | Upload to personal cloud drives or file-sharing services |
| USB Activity | Copying large datasets to removable media |
| Email Forwarding | External forwarding rules created; sensitive attachments sent externally |
| Printing Activity | Large print jobs of confidential documents |
| Compression and Archiving | Large archives created (zip/rar/7z) in short time window |

### 6.3 System and Log Indicators

| Log Source | Indicator |
|-----------|-----------|
| IAM / AD Logs | Privilege changes, group membership modifications |
| Endpoint Logs / EDR | Unusual process execution, compression tools, file copy operations |
| File Share Logs | Mass reads, downloads, or deletions |
| DLP Logs | Sensitive data transfers to external destinations |
| Email Logs | Forwarding rules, unusual sending patterns |
| Cloud Audit Logs | Unusual object downloads, permission changes, token creation |
| VPN Logs | After-hours sessions, anomalous device posture |
| Database Logs | Large query volumes, export operations, schema access anomalies |

---

## 7. Severity Classification

| Scenario | Severity |
|----------|----------|
| Confirmed exfiltration of regulated or sensitive data by insider | P1 – Critical |
| Confirmed sabotage of business-critical systems | P1 – Critical |
| Privileged insider compromise affecting core identity systems | P1 – Critical |
| Confirmed unauthorized access to sensitive systems or data | P2 – High |
| Confirmed external sharing of internal confidential data | P2 – High |
| Insider activity suggests fraud or financial manipulation | P2 – High |
| Suspicious but unconfirmed abnormal access or behavior | P3 – Medium |
| Policy violation with no sensitive data and no malicious indicators | P4 – Low |

Note: Insider incidents frequently require reclassification as evidence is confirmed.

---

## 8. Immediate Response Actions

### 8.1 First 15 Minutes

- Create incident ticket and classify initial severity
- Notify SOC Lead immediately for P2 and above
- Preserve logs relevant to user activity (do not modify user system)
- Identify the user account, department, role, and access level
- Identify affected systems, data repositories, and time window
- Engage IR Team if P1 or confirmed sensitive data exposure is suspected
- Initiate evidence preservation procedures (chain-of-custody readiness)

### 8.2 First 1 Hour

- Engage HR and Legal for suspected malicious insider cases (P2/P1)
- Engage GRC/Compliance if sensitive or regulated data is involved
- Confirm whether activity is authorized (role-based access and approved tasks)
- Review recent privilege changes and access grants
- Review DLP alerts and file access logs for data movement patterns
- Review email logs for forwarding, external sharing, or unusual sending patterns
- Consider immediate access restriction only with proper approval and HR/Legal coordination

### 8.3 First 4 Hours (P2/P1 Cases)

- Determine whether account compromise by external actor is possible
- Identify exfiltration paths (USB, cloud drive, email, VPN, web upload)
- Collect evidence suitable for HR/legal actions (logs, audit trails, screenshots)
- Implement containment actions per authority matrix and legal guidance
- Maintain strict confidentiality and need-to-know access controls
- Prepare management updates and coordinate client communication if MSSP client data is impacted

---

## 9. Containment Guidance (High Sensitivity)

Containment actions in insider cases must be controlled and documented.

| Action | When to Perform | Notes |
|-------|------------------|------|
| Disable account | Confirmed malicious insider or immediate risk | Requires HR/Legal approval for employee cases |
| Session revocation | Suspected compromise or active exfiltration | Often lower impact than full disable |
| Restrict access | Limit to minimal role access | Coordinate with IAM and HR |
| Device seizure | For forensic acquisition | Must follow legal/HR procedures |
| Preserve mailbox | BEC/insider email misuse | Preserve before modifying rules or deleting content |
| Network isolation | Suspected data exfiltration from endpoint | Coordinate with IT and HR |

Reference: `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 10. MITRE ATT&CK Mapping (Common in Insider / Compromised Insider)

| Tactic | Technique | ID |
|--------|-----------|----|
| Credential Access | Valid Accounts | T1078 |
| Credential Access | Account Manipulation | T1098 |
| Collection | Data from Information Repositories | T1213 |
| Collection | Data from Local System | T1005 |
| Exfiltration | Exfiltration Over Web Service | T1567 |
| Exfiltration | Exfiltration Over Alternative Protocol | T1048 |
| Exfiltration | Exfiltration to Cloud Storage | T1567.002 |
| Defense Evasion | Clear Windows Event Logs | T1070.001 |
| Impact | Data Destruction | T1485 |
| Impact | Service Stop | T1489 |

Note: If the “insider” is actually an external attacker using a valid account, additional techniques (phishing, malware, lateral movement) may apply.

---

## 11. Key Investigation Questions

1. Who is the user (employee/contractor/vendor) and what is their role?
2. Is the activity within the user’s job function and approved tasks?
3. Is the account privileged or does it have elevated access?
4. What systems and data repositories were accessed?
5. What is the time window and pattern of access (volume, timing, location)?
6. Is there evidence of data movement (USB, cloud upload, email forwarding, printing)?
7. Are there indicators of account compromise (impossible travel, new device, MFA anomalies)?
8. Were any new permissions, groups, tokens, or access grants created?
9. Is there evidence of log tampering or attempted cover-up?
10. Is there a relationship to resignation, termination, or disciplinary events?
11. Does the incident involve regulated client data (MSSP scenario)?
12. What containment action is required, and who must approve it (HR/Legal/Management)?

---

## 12. Critical Do's and Do Not's

### Do

- Follow strict need-to-know handling and confidentiality
- Preserve evidence before taking corrective action
- Engage HR and Legal early for suspected malicious insider activity
- Use chain-of-custody for evidence intended for disciplinary/legal use
- Assess whether the account is compromised by an external attacker
- Document decision-making and approvals for containment actions

### Do Not

- Confront the suspected individual without HR/Legal guidance
- Disable accounts or seize devices without approval in employee cases
- Share investigation details broadly; restrict to authorized stakeholders
- Modify or delete key logs without preservation
- Delay containment if active exfiltration is confirmed (escalate for approval quickly)

---

## 13. Escalation Path

| Stage | Action |
|-------|--------|
| L1 Triage | Identify suspicious insider indicators, create ticket |
| L2 Investigation | Validate authorization, scope, and data movement indicators |
| SOC Lead | Approve severity changes, coordinate internal communications |
| IR Team | Lead evidence handling, forensic collection, and containment strategy |
| HR | Manage employee relations, disciplinary process, and interviews |
| Legal | Guide evidence handling, privacy constraints, legal exposure |
| GRC / Compliance | Assess regulatory and contractual reporting obligations |
| Management | Approve high-impact actions; oversee business impact decisions |
| MSSP SDM / Client Owner | Engage when client data or client user is involved |

---

## 14. Regulatory and Client Reporting Considerations

| Trigger | Action |
|--------|--------|
| Confirmed exfiltration of regulated data | Engage Compliance and Legal; assess reporting obligations |
| Confirmed client data exposure (MSSP) | Notify client as per SLA; follow contractual reporting |
| Financial fraud or theft | Engage Legal and finance leadership immediately |
| Significant sabotage affecting availability | Treat as major incident and escalate to P1 |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 15. Evidence Collection Requirements

| Evidence Type | Priority | Notes |
|--------------|----------|-------|
| IAM / AD audit logs | Critical | Group membership, privilege changes, login history |
| File server access logs | Critical | Access volumes and file paths |
| DLP logs | Critical | Data movement to external destinations |
| Email logs and mailbox audit logs | High | Forwarding rules, external sharing, unusual sends |
| Cloud audit logs | High | Downloads, token creation, permission changes |
| Endpoint EDR telemetry | High | File operations, compression tools, uploads |
| VPN logs | Medium | Connection timing, source IP, device |
| Forensic image (disk/memory) | As needed | Only with approval and CoC |
| Chain-of-custody forms | Critical | Required for disciplinary/legal evidence packages |

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 16. Related Documents

| Document | Path |
|---------|------|
| Insider Threat Master Playbook | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Master.md` |
| L1 Triage Playbook | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L1-Triage.md` |
| L2 Investigation Playbook | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L2-Investigation.md` |
| L3 Forensics Playbook | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L3-Forensics.md` |
| HR and Legal Coordination | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md` |
| Containment Playbook | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Containment.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-MITRE-Mapping.md` |
| Evidence and Chain of Custody | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |
| P1 Critical Definition | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md` |
| P2 High Definition | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P2-High-Definition.md` |

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