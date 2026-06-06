# Playbook: Insider Threat – L1 Triage

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Insider Threat (L1 Triage) |
| Document ID | IR-PB-INS-002 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | SOC Lead / SOC Manager |
| Approved By | IR Team Lead |
| Classification | Strictly Confidential |
| Review Cycle | Quarterly and after any P1/P2 insider threat incident |

---

## 2. Purpose

This document defines the Level 1 (L1) SOC Analyst procedures for triaging
suspected insider threat activity.

Insider threat incidents require significantly different handling compared to
external attacks because:
- the user may have legitimate access
- activity may initially appear normal
- premature escalation or disclosure can create legal and HR issues
- employee privacy and confidentiality must be protected
- evidence preservation is critical

The objective of L1 triage is to:
- validate suspicious activity
- determine whether escalation is required
- identify business and data impact
- preserve evidence discreetly
- avoid alerting the subject of investigation
- escalate appropriately to L2, HR, Legal, or IR Team

---

## 3. Scope

Applies to:
- suspicious employee activity
- abnormal privileged account activity
- unusual data access patterns
- suspicious USB usage
- mass file access or copying
- unauthorized cloud storage usage
- suspicious email forwarding
- insider sabotage indicators
- data exfiltration concerns
- terminated employee risk monitoring

Includes:
- employees
- contractors
- third-party vendors
- privileged administrators
- MSSP client insider investigations

---

## 4. L1 Safety and Confidentiality Rules

Insider threat investigations are highly sensitive.

Failure to follow confidentiality procedures may:
- compromise investigations
- expose the organization legally
- alert the subject
- result in evidence destruction

---

## 4.1 Mandatory Confidentiality Rules

| Rule | Reason |
|------|--------|
| Do NOT contact the subject directly | Avoid tipping off the individual |
| Do NOT discuss investigation outside approved channels | Maintain confidentiality |
| Do NOT modify user access without approval | Potential HR/legal impact |
| Do NOT confront employees | HR and Legal coordination required |
| Do NOT disclose investigation details in broad SOC channels | Need-to-know principle |

---

## 4.2 Need-to-Know Principle

Investigation details must only be shared with:
- assigned SOC analysts
- SOC Lead
- IR Team
- HR (if approved)
- Legal Counsel
- Executive Management (if approved)

---

# 5. L1 SLA Targets

| Severity | Response Time | Escalation Requirement |
|----------|---------------|------------------------|
| P1 | Immediate | SOC Lead + IR Team |
| P2 | Within 10 minutes | L2 + SOC Lead |
| P3 | Within 30 minutes | L2 review |
| P4 | Same shift | Monitor/document |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

# 6. Inputs Required During Triage

---

## 6.1 Alert Information

| Required Data | Example |
|---------------|---------|
| Alert Source | DLP / UEBA / SIEM |
| Detection Time | UTC timestamp |
| User Identity | Employee username |
| Endpoint | Hostname/IP |
| Activity Type | File copy / USB / cloud upload |
| Severity | Tool-generated severity |

---

## 6.2 User Context Information

| Data Point | Purpose |
|------------|---------|
| Department | Business context |
| Privilege level | Risk assessment |
| Employment status | Termination/resignation risk |
| Remote or onsite | Access context |
| Recent HR flags | Elevated insider risk |

---

## 6.3 Activity Context

| Activity | Example |
|----------|---------|
| Data access | Sensitive file reads |
| File movement | Mass copy activity |
| Cloud uploads | Personal OneDrive/Dropbox |
| USB usage | External storage connected |
| Email forwarding | External forwarding rule |

---

# 7. Step-by-Step L1 Triage Procedure

---

## Step 1 – Validate Alert Authenticity

Determine whether the alert is:
- legitimate suspicious activity
- expected business activity
- false positive
- duplicate alert

---

### Validation Checklist

| Validation Check | Purpose |
|------------------|---------|
| Verify alert source | Confirm tool legitimacy |
| Review user role | Determine expected access |
| Review business context | Identify legitimate work activity |
| Compare with baseline behavior | Detect anomalies |
| Review prior alerts on user | Pattern identification |

---

## Step 2 – Determine Activity Type

Classify the insider activity.

---

### Insider Activity Classification

| Activity Type | Description | Typical Risk |
|---------------|-------------|--------------|
| Data Exfiltration | Large file transfers/uploads | Critical |
| Privileged Abuse | Unauthorized admin activity | Critical |
| Suspicious Downloads | Sensitive file collection | High |
| USB Mass Copy | Removable media exfiltration | High |
| Unauthorized Access | Access outside job role | High |
| Sabotage Indicators | File deletion/config changes | Critical |

---

## Step 3 – Assess Data Sensitivity

Determine what data may be involved.

---

### Data Sensitivity Classification

| Data Type | Risk Level |
|-----------|------------|
| Customer PII | Critical |
| Financial records | Critical |
| Source code/IP | Critical |
| Internal documents | Medium |
| Public information | Low |

---

## Step 4 – Assess User Risk Indicators

Review indicators that increase insider threat risk.

---

### High-Risk User Indicators

| Indicator | Risk |
|-----------|------|
| Employee under termination review | High |
| Privileged administrator | Critical |
| Recent resignation | High |
| Access outside business hours | Medium |
| Large after-hours downloads | High |
| New cloud storage usage | Medium |

---

## Step 5 – Preserve Evidence

Preserve evidence discreetly.

Do NOT:
- modify logs
- disable accounts
- confront the user
- alter endpoint state unnecessarily

---

### Minimum Evidence Collection

| Evidence Type | Source |
|--------------|-------|
| SIEM alert | SIEM |
| File access logs | DLP/File server |
| USB activity logs | Endpoint telemetry |
| Email forwarding logs | Exchange/O365 |
| Cloud upload activity | CASB/Cloud logs |
| Screenshots | SOC evidence package |

---

## Step 6 – Initial Severity Recommendation

Severity must consider:
- privilege level
- data sensitivity
- evidence of malicious intent
- scope of activity
- business impact

---

### Severity Recommendation Matrix

| Scenario | Recommended Severity |
|----------|----------------------|
| Executive or admin data theft | P1 |
| Large sensitive data upload | P1 |
| Privileged abuse confirmed | P1 |
| Unauthorized sensitive access | P2 |
| Suspicious mass file access | P2 |
| Unusual but low-risk behavior | P3 |
| Benign policy violation | P4 |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

## Step 7 – Escalation Decision

---

### Escalate to L2 if:

| Condition | Reason |
|-----------|--------|
| Data access anomaly detected | Requires investigation |
| USB/cloud exfiltration suspected | Scope analysis required |
| Repeated abnormal behavior | Pattern review |
| Privileged access anomaly | Elevated risk |

---

### Escalate to SOC Lead Immediately if:

| Condition | Reason |
|-----------|--------|
| Large-scale data theft suspected | Critical impact |
| Sabotage indicators present | Operational risk |
| Privileged admin involved | Enterprise risk |
| HR termination case involved | Elevated insider threat risk |

---

### Escalate to HR/Legal Through Approved Process if:

| Condition | Reason |
|-----------|--------|
| Employee misconduct suspected | HR/legal coordination |
| Evidence may support disciplinary action | Legal handling required |
| Privacy-sensitive investigation | Compliance requirement |

Reference:
`02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md`

---

# 8. Evidence Handling Requirements

Insider threat evidence is highly sensitive.

---

## 8.1 Handling Requirements

| Requirement | Purpose |
|-------------|---------|
| Encrypt exports | Protect confidentiality |
| Restrict evidence access | Need-to-know control |
| Preserve timestamps | Timeline integrity |
| Maintain chain-of-custody | Legal defensibility |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 9. Common L1 Insider Threat Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Contacting the employee directly | Investigation compromise |
| Discussing incident openly | Confidentiality breach |
| Assuming malicious intent immediately | Incorrect escalation |
| Failing to preserve logs quickly | Evidence loss |
| Ignoring HR context | Missed risk indicators |
| Disabling accounts without approval | Legal and operational impact |

---

# 10. MSSP Handling Notes

For MSSP-managed environments:
- insider threat investigations must remain client-scoped
- do not contact client employees directly unless authorized
- follow client-approved escalation channels
- maintain strict confidentiality
- avoid sharing insider-related intelligence across clients

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 11. Related Documents

| Document | Path |
|---------|------|
| Insider Threat Master | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Master.md` |
| Insider Threat L2 Investigation | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L2-Investigation.md` |
| Insider Threat L3 Forensics | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L3-Forensics.md` |
| Insider Threat Containment | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Containment.md` |
| HR and Legal Coordination | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md` |
| Insider Threat MITRE Mapping | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-MITRE-Mapping.md` |
| Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 12. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | SOC Lead / SOC Manager | Initial version |

---

## 13. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**