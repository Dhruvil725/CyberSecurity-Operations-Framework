# Playbook: Insider Threat – L2 Investigation

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Insider Threat (L2 Investigation) |
| Document ID | IR-PB-INS-003 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | L2 SOC Lead / IR Team Lead |
| Approved By | CISO |
| Classification | Strictly Confidential |
| Review Cycle | Quarterly and after any P1/P2 insider threat incident |

---

## 2. Purpose

This document defines the Level 2 (L2) investigation procedures for
insider threat incidents escalated from L1 triage.

The objective of L2 investigation is to:
- determine the scope and intent of insider activity
- identify impacted systems, users, and data
- confirm whether activity violates policy or law
- determine whether exfiltration or sabotage occurred
- identify persistence or privilege misuse
- coordinate discreetly with HR and Legal
- support containment decisions without alerting the subject

Unlike external attacker investigations, insider threat investigations require:
- enhanced confidentiality
- legal defensibility
- careful evidence handling
- HR and Legal coordination
- minimal operational disruption

---

## 3. Scope

Applies to:
- malicious insider investigations
- privileged misuse investigations
- data theft investigations
- sabotage investigations
- insider-assisted breaches
- suspicious cloud storage uploads
- removable media exfiltration
- unauthorized access investigations
- MSSP-managed insider investigations

Includes:
- endpoint activity analysis
- DLP review
- IAM review
- cloud activity analysis
- email and collaboration review
- access pattern analysis

---

## 4. Preconditions Before Investigation

L2 investigation begins after:
- L1 triage completed
- confidentiality controls established
- initial evidence preserved
- escalation approved by SOC Lead

Required inputs from L1:

| Required Input | Purpose |
|---------------|---------|
| Alert details | Initial context |
| User identity | Investigation scoping |
| Data sensitivity indicators | Risk assessment |
| Initial evidence | Timeline review |
| Severity recommendation | Escalation context |
| HR/termination flags | Insider risk analysis |

Reference:
`02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L1-Triage.md`

---

# 5. L2 Investigation Objectives

| Objective | Description |
|-----------|-------------|
| Determine Intent | Malicious vs negligent behavior |
| Scope Data Access | Identify impacted information |
| Confirm Exfiltration | Validate unauthorized transfer |
| Review Privileged Activity | Detect admin misuse |
| Build Timeline | Reconstruct events |
| Assess Business Impact | Operational and legal impact |
| Support Containment | Recommend access restrictions |
| Preserve Legal Integrity | Ensure defensible investigation |

---

# 6. Investigation Workflow Overview

| Phase | Focus Area |
|------|-------------|
| Phase 1 | User and activity validation |
| Phase 2 | Data access analysis |
| Phase 3 | Exfiltration analysis |
| Phase 4 | Privileged activity review |
| Phase 5 | Cloud and collaboration review |
| Phase 6 | Timeline reconstruction |
| Phase 7 | Risk and intent assessment |
| Phase 8 | Escalation and containment recommendations |

---

# 7. Phase 1 – User and Activity Validation

The first objective is validating:
- who performed the activity
- whether the activity is unusual
- whether the activity aligns with job responsibilities

---

## 7.1 User Context Review

Review:
- department
- job role
- privilege level
- manager
- recent HR status
- remote work patterns

---

### High-Risk User Indicators

| Indicator | Risk |
|-----------|------|
| Recent resignation | Elevated exfiltration risk |
| Termination pending | High insider risk |
| Privileged administrator | Critical |
| Repeated policy violations | Escalation concern |
| Access outside role | Suspicious |

---

## 7.2 Activity Validation

Determine whether activity:
- aligns with business role
- exceeds normal behavior
- occurred during unusual hours
- targeted sensitive data

---

### Suspicious Activity Indicators

| Activity | Investigation Concern |
|----------|----------------------|
| Mass file access | Data staging |
| USB device insertion | Potential exfiltration |
| Personal cloud storage usage | Data transfer |
| Bulk email forwarding | Data theft |
| Access outside business hours | Suspicious behavior |
| Access to unrelated departments | Privilege misuse |

---

# 8. Phase 2 – Data Access Analysis

This phase identifies:
- what data was accessed
- whether access was authorized
- whether sensitive information was involved

---

## 8.1 Data Access Review Areas

| Area | Purpose |
|------|---------|
| File server access | Sensitive file review |
| SharePoint/OneDrive access | Cloud data review |
| Database access | Structured data exposure |
| Email access | Internal information review |
| Collaboration platforms | Information sharing review |

---

## 8.2 Sensitive Data Categories

| Data Type | Risk Level |
|-----------|------------|
| Customer PII | Critical |
| Financial data | Critical |
| HR records | Critical |
| Source code/IP | Critical |
| Legal documents | High |
| Internal business plans | High |

---

## 8.3 Mass Access Indicators

| Indicator | Meaning |
|-----------|---------|
| Large number of file opens | Data collection |
| Rapid directory traversal | Bulk discovery |
| Compression/archive creation | Data staging |
| Sequential downloads | Exfiltration preparation |

---

# 9. Phase 3 – Exfiltration Analysis

This phase determines whether data left the environment.

---

## 9.1 Exfiltration Review Areas

| Area | Purpose |
|------|---------|
| USB activity | Removable media transfer |
| Cloud uploads | External sharing |
| Email attachments | Unauthorized sending |
| Browser uploads | Cloud storage abuse |
| Remote sessions | External transfer |

---

## 9.2 Common Exfiltration Methods

| Method | Indicators |
|--------|-----------|
| USB storage | File copy events |
| Personal cloud drives | Dropbox/Google Drive uploads |
| Personal email | External attachments |
| Encrypted archives | ZIP/RAR staging |
| Remote access tools | Data movement |

---

## 9.3 Exfiltration Evidence Checklist

| Evidence | Source |
|----------|-------|
| USB insertion logs | Endpoint telemetry |
| File copy events | DLP |
| Upload logs | Proxy/CASB |
| Email attachments | Email logs |
| Compression utility execution | Endpoint logs |

---

# 10. Phase 4 – Privileged Activity Review

Privileged misuse carries elevated risk.

---

## 10.1 Privileged Review Areas

| Review Area | Purpose |
|-------------|---------|
| Admin account usage | Detect abuse |
| Permission changes | Unauthorized escalation |
| Access to sensitive systems | Abuse detection |
| Log tampering attempts | Cover-up indicators |
| Security control changes | Defense evasion |

---

## 10.2 High-Risk Privileged Indicators

| Indicator | Risk |
|-----------|------|
| New admin accounts | Persistence |
| Privilege escalation | Unauthorized access |
| Log deletion | Evidence tampering |
| Security control disablement | Defense evasion |
| Unauthorized data exports | Data theft |

---

# 11. Phase 5 – Cloud and Collaboration Review

Modern insider threats frequently use:
- cloud collaboration
- SaaS platforms
- messaging tools
- external sharing links

---

## 11.1 Cloud Activity Review

Review:
- OneDrive activity
- SharePoint sharing
- Google Drive uploads
- SaaS access logs
- external sharing links

---

## 11.2 Collaboration Platform Review

| Platform | Review Focus |
|----------|--------------|
| Teams | File sharing |
| Slack | External sharing |
| Email | Forwarding and attachments |
| SharePoint | Public links |
| Zoom/Meeting tools | Shared files |

---

## 11.3 Cloud Risk Indicators

| Indicator | Meaning |
|-----------|---------|
| New external sharing links | Potential exfiltration |
| Large uploads | Data movement |
| Access from unusual locations | Suspicious behavior |
| External guest access added | Data sharing risk |

---

# 12. Phase 6 – Timeline Reconstruction

Build a complete timeline of insider activity.

---

## 12.1 Timeline Requirements

Include:
- login activity
- file access
- USB insertion
- cloud uploads
- privilege changes
- email forwarding
- suspicious downloads

---

### Timeline Template

| Time (UTC) | Event | User | System | Source |
|-----------|------|------|--------|--------|
| | Login | | | |
| | File access | | | |
| | USB insertion | | | |
| | Cloud upload | | | |
| | Privilege change | | | |

---

# 13. Phase 7 – Risk and Intent Assessment

Intent determination is sensitive and must be handled carefully.

SOC should document indicators, NOT make HR disciplinary conclusions.

---

## 13.1 Intent Indicators

| Indicator | Possible Interpretation |
|-----------|------------------------|
| Access outside role | Unauthorized curiosity or theft |
| Large after-hours transfers | Potential exfiltration |
| Deletion of logs/files | Cover-up behavior |
| Compression and encryption | Data staging |
| Attempts to bypass DLP | Malicious intent |

---

## 13.2 Risk Assessment Matrix

| Risk Area | Assessment |
|-----------|-----------|
| Data sensitivity | Low/Medium/High/Critical |
| Business impact | Low/Medium/High/Critical |
| Legal exposure | Low/Medium/High/Critical |
| Privilege misuse | Low/Medium/High/Critical |

---

# 14. Phase 8 – Escalation and Containment Recommendations

---

## 14.1 Escalate to HR and Legal if:

| Condition | Reason |
|-----------|--------|
| Confirmed policy violation | HR involvement required |
| Data theft suspected | Legal exposure |
| Employee sabotage indicators | Executive/legal involvement |
| Disciplinary action likely | Legal defensibility required |

---

## 14.2 Escalate to IR Team if:

| Condition | Reason |
|-----------|--------|
| Large-scale data theft | Major incident |
| Privileged abuse confirmed | Enterprise risk |
| Sabotage affecting operations | Critical business impact |
| Multiple insiders involved | Coordinated activity |

---

## 14.3 Containment Recommendations

| Finding | Recommended Action |
|---------|-------------------|
| Active exfiltration | Restrict account access |
| USB abuse | Disable removable media |
| Unauthorized sharing | Revoke links and permissions |
| Privileged misuse | Suspend elevated access |
| Cloud abuse | Disable external sharing |

Reference:
`02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Containment.md`

---

# 15. Documentation Requirements

The following must be documented:

| Documentation Item | Required |
|-------------------|----------|
| User activity timeline | Yes |
| Data accessed | Yes |
| Exfiltration indicators | Yes |
| Cloud activity reviewed | Yes |
| Privileged actions reviewed | Yes |
| HR/legal escalation status | Yes |
| Containment recommendations | Yes |

---

# 16. Common L2 Investigation Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Assuming malicious intent immediately | Incorrect escalation |
| Broadly sharing investigation details | Confidentiality breach |
| Failing to preserve evidence quickly | Evidence loss |
| Ignoring cloud collaboration activity | Missed exfiltration |
| Not involving Legal early | Compliance/legal exposure |
| Alerting the user through account changes | Investigation compromise |

---

# 17. MSSP Client Handling Notes

For MSSP-managed environments:
- maintain strict client confidentiality
- insider investigations must remain client-scoped
- obtain client approval before employee-impacting actions
- avoid sharing insider intelligence between clients
- document all communications carefully

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 18. Related Documents

| Document | Path |
|---------|------|
| Insider Threat Master | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Master.md` |
| Insider Threat L1 Triage | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L1-Triage.md` |
| Insider Threat L3 Forensics | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L3-Forensics.md` |
| Insider Threat Containment | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Containment.md` |
| HR and Legal Coordination | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md` |
| Insider Threat MITRE Mapping | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-MITRE-Mapping.md` |
| Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 19. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | L2 SOC Lead / IR Team Lead | Initial version |

---

## 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**