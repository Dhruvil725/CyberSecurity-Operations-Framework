# Playbook: Insider Threat – L3 Forensics and Advanced Analysis

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Insider Threat (L3 Forensics and Advanced Analysis) |
| Document ID | IR-PB-INS-004 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | L3 Lead / IR Team Lead |
| Approved By | CISO |
| Classification | Strictly Confidential |
| Review Cycle | Quarterly and after any P1/P2 insider threat incident |

---

## 2. Purpose

This document defines the Level 3 (L3) forensic and advanced analysis
procedures for insider threat investigations.

L3 involvement is required when:
- privileged misuse is suspected
- data theft is confirmed or likely
- legal action may occur
- endpoint forensic analysis is required
- cloud and identity correlation is needed
- evidence must be preserved to forensic standards
- sabotage or destructive actions occurred

The objectives of L3 analysis are to:
- reconstruct the full activity timeline
- determine the exact scope of data access or exfiltration
- identify persistence or concealment attempts
- preserve legally defensible evidence
- support HR and Legal decision-making
- provide advanced technical findings to the IR Team and executives

---

## 3. Scope

Applies to:
- malicious insider investigations
- privileged account abuse
- employee data theft
- intellectual property theft
- sabotage incidents
- insider-assisted breaches
- cloud collaboration misuse
- unauthorized data staging
- evidence tampering

Includes:
- endpoint forensics
- cloud forensics
- email and collaboration analysis
- timeline reconstruction
- advanced log correlation
- evidence integrity validation

---

## 4. Preconditions Before L3 Investigation

L3 engagement begins after:
- L2 investigation completed
- HR and Legal coordination initiated where required
- evidence preservation approved
- confidentiality controls established

Required inputs from L2:

| Required Input | Purpose |
|---------------|---------|
| Investigation timeline | Initial reconstruction |
| User activity findings | Scope review |
| DLP evidence | Exfiltration review |
| Endpoint telemetry | Behavioral analysis |
| Cloud audit logs | SaaS review |
| Privileged access logs | Admin activity review |

Reference:
`02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L2-Investigation.md`

---

# 5. L3 Investigation Objectives

| Objective | Description |
|-----------|-------------|
| Reconstruct Timeline | Build authoritative event timeline |
| Confirm Exfiltration | Validate exact data movement |
| Analyze Endpoints | Identify local staging or tampering |
| Review Cloud Activity | Analyze SaaS collaboration and sharing |
| Validate Privileged Abuse | Confirm unauthorized elevated activity |
| Preserve Evidence | Ensure legal defensibility |
| Support Legal Review | Provide technical findings |
| Improve Monitoring | Generate future detection improvements |

---

# 6. Investigation Workflow Overview

| Phase | Focus Area |
|------|-------------|
| Phase 1 | Evidence acquisition |
| Phase 2 | Endpoint forensic analysis |
| Phase 3 | Data staging and exfiltration analysis |
| Phase 4 | Cloud and collaboration analysis |
| Phase 5 | Privileged activity analysis |
| Phase 6 | Timeline reconstruction |
| Phase 7 | Legal evidence preparation |
| Phase 8 | Detection engineering outputs |

---

# 7. Phase 1 – Evidence Acquisition

Evidence collection must preserve:
- integrity
- confidentiality
- legal defensibility

---

## 7.1 Evidence Collection Priorities

| Priority | Evidence Type |
|----------|--------------|
| Critical | Endpoint forensic image |
| Critical | Cloud audit logs |
| High | DLP events |
| High | Email records |
| High | USB activity |
| Medium | Screenshots |
| Medium | Browser history |

---

## 7.2 Chain-of-Custody Requirements

Every evidence item must include:
- evidence ID
- collector
- collection timestamp
- source system
- integrity hash
- storage location

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`

---

## 7.3 Forensic Imaging Guidance

Forensic imaging required when:
- sabotage suspected
- large-scale exfiltration suspected
- legal escalation likely
- endpoint tampering suspected

---

### Imaging Requirements

| Requirement | Purpose |
|-------------|---------|
| Full disk image | Preserve complete evidence |
| Memory acquisition | Capture volatile artifacts |
| Hash validation | Integrity verification |
| Secure storage | Evidence protection |

---

# 8. Phase 2 – Endpoint Forensic Analysis

Endpoint analysis focuses on:
- local staging
- file access
- evidence tampering
- unauthorized tooling
- removable media usage

---

## 8.1 File System Analysis

Review:
- recently accessed files
- staged archives
- deleted files
- hidden directories
- compressed archives

---

### High-Risk File Indicators

| Indicator | Meaning |
|-----------|---------|
| Large ZIP/RAR archives | Data staging |
| Hidden directories | Concealment |
| Recently deleted files | Evidence tampering |
| Bulk file copies | Exfiltration preparation |
| Portable encryption tools | Concealment |

---

## 8.2 USB and Removable Media Analysis

Review:
- inserted USB devices
- file copy events
- serial numbers
- transfer timestamps

---

### USB Investigation Indicators

| Indicator | Meaning |
|-----------|---------|
| Large transfers to USB | Potential exfiltration |
| Multiple USB devices used | Data movement |
| Unknown removable media | Unauthorized device |

---

## 8.3 Browser and Application Analysis

Review:
- cloud uploads
- browser downloads
- external sharing
- browser extensions
- clipboard history (where available)

---

### Cloud Upload Indicators

| Indicator | Meaning |
|-----------|---------|
| Dropbox/Drive uploads | External transfer |
| Personal email access | Unauthorized sharing |
| Temporary file staging | Data preparation |
| Browser-based uploads | Web exfiltration |

---

# 9. Phase 3 – Data Staging and Exfiltration Analysis

This phase determines:
- what data was staged
- how data was moved
- whether exfiltration succeeded

---

## 9.1 Exfiltration Path Review

| Exfiltration Method | Investigation Focus |
|---------------------|--------------------|
| USB transfer | File copy analysis |
| Cloud storage | Upload logs |
| Email forwarding | Mail flow review |
| Collaboration sharing | External link analysis |
| Remote sessions | Data movement review |

---

## 9.2 Data Staging Indicators

| Indicator | Meaning |
|-----------|---------|
| Temporary archive creation | Packaging data |
| Compression utilities | Staging |
| Encryption before upload | Concealment |
| Large temporary directories | Collection activity |

---

## 9.3 Data Volume Assessment

Key questions:
- how much data was accessed?
- how much data was transferred?
- was sensitive data involved?
- did transfer complete successfully?

---

### Data Exposure Assessment Matrix

| Data Type | Exposure Impact |
|-----------|----------------|
| Customer PII | Critical |
| Financial records | Critical |
| Source code | Critical |
| Internal documentation | Medium |
| Public data | Low |

---

# 10. Phase 4 – Cloud and Collaboration Analysis

Modern insider threats frequently abuse:
- OneDrive
- SharePoint
- Teams
- Slack
- Google Drive
- personal cloud storage

---

## 10.1 Cloud Activity Review

Review:
- external sharing links
- upload/download activity
- guest access creation
- sync client activity
- OAuth grants

---

### Cloud Abuse Indicators

| Indicator | Meaning |
|-----------|---------|
| New external sharing links | Potential exfiltration |
| Large outbound transfers | Data movement |
| Guest accounts added | Unauthorized sharing |
| Sync activity spikes | Bulk movement |

---

## 10.2 Collaboration Platform Analysis

| Platform | Investigation Focus |
|----------|--------------------|
| Teams | Shared files/chats |
| Slack | External workspaces |
| SharePoint | External links |
| Email | Forwarding and attachments |

---

# 11. Phase 5 – Privileged Activity Analysis

Privileged misuse is one of the highest-risk insider threat scenarios.

---

## 11.1 Privileged Review Areas

| Area | Purpose |
|------|---------|
| Admin login activity | Abuse detection |
| Privilege escalation | Unauthorized elevation |
| Security control changes | Defense evasion |
| Log access/deletion | Evidence tampering |
| Access to restricted systems | Unauthorized activity |

---

## 11.2 High-Risk Privileged Indicators

| Indicator | Meaning |
|-----------|---------|
| New admin account creation | Persistence |
| Security tool disablement | Concealment |
| Log clearing | Anti-forensics |
| Access outside change window | Suspicious behavior |
| Unauthorized exports | Data theft |

---

# 12. Phase 6 – Timeline Reconstruction

L3 must produce the authoritative investigation timeline.

---

## 12.1 Timeline Components

Include:
- initial access
- file access
- privilege changes
- data staging
- exfiltration
- USB activity
- cloud sharing
- containment actions

---

### Timeline Template

| Time (UTC) | Event | User | System | Evidence Source |
|-----------|------|------|--------|-----------------|
| | Login | | | |
| | File access | | | |
| | USB insertion | | | |
| | Archive creation | | | |
| | Cloud upload | | | |
| | Privilege escalation | | | |

---

# 13. Phase 7 – Legal Evidence Preparation

Insider threat investigations frequently involve:
- disciplinary action
- litigation
- regulatory review
- law enforcement coordination

Evidence must be legally defensible.

---

## 13.1 Legal Evidence Requirements

| Requirement | Purpose |
|-------------|---------|
| Chain-of-custody maintained | Evidence integrity |
| Evidence hashed | Tamper detection |
| Timestamps normalized to UTC | Timeline consistency |
| Access restricted | Confidentiality |
| Secure storage | Legal preservation |

---

## 13.2 Sensitive Evidence Handling

Sensitive evidence includes:
- HR records
- employee communications
- compensation data
- legal correspondence
- executive communications

Access must be strictly controlled.

---

# 14. Phase 8 – Detection Engineering Outputs

Every insider threat investigation should improve visibility.

---

## 14.1 Detection Improvement Areas

| Improvement | Purpose |
|-------------|---------|
| USB monitoring alerts | Detect removable media abuse |
| DLP tuning | Detect exfiltration |
| Cloud sharing alerts | Detect external sharing |
| Privileged activity monitoring | Detect abuse |
| UEBA tuning | Behavioral anomaly detection |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 15. Escalation Guidance

---

## 15.1 Escalate to IR Team if:

| Condition | Reason |
|-----------|--------|
| Large-scale data theft | Major incident |
| Privileged abuse confirmed | Enterprise risk |
| Sabotage confirmed | Operational impact |
| Multiple insiders involved | Coordinated activity |

---

## 15.2 Escalate to Executive Management if:

| Condition | Reason |
|-----------|--------|
| Regulatory impact | Compliance risk |
| Executive involvement | High sensitivity |
| Legal exposure | Organizational liability |
| Public disclosure risk | Reputation impact |

---

# 16. Common L3 Investigation Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Modifying endpoint before imaging | Evidence contamination |
| Failing to preserve cloud logs quickly | Log expiration |
| Ignoring collaboration tools | Missed exfiltration |
| Broadly sharing evidence | Confidentiality breach |
| Assuming intent without evidence | Legal risk |
| Incomplete timeline reconstruction | Weak legal case |

---

# 17. MSSP Client Handling Notes

For MSSP-managed environments:
- insider investigations must remain client-scoped
- evidence access must be tightly restricted
- coordinate all employee-impacting actions with client HR/legal
- maintain encrypted evidence transfer procedures
- avoid cross-client intelligence sharing

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 18. Related Documents

| Document | Path |
|---------|------|
| Insider Threat Master | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Master.md` |
| Insider Threat L1 Triage | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L1-Triage.md` |
| Insider Threat L2 Investigation | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L2-Investigation.md` |
| Insider Threat Containment | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Containment.md` |
| HR and Legal Coordination | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md` |
| Insider Threat MITRE Mapping | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-MITRE-Mapping.md` |
| Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 19. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | L3 Lead / IR Team Lead | Initial version |

---

## 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**