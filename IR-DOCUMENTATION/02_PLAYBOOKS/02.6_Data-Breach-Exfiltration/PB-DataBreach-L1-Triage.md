# Playbook: Data Breach and Data Exfiltration – L1 Triage

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Data Breach and Data Exfiltration (L1 Triage) |
| Document ID | IR-PB-DBR-002 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | SOC Lead / SOC Manager |
| Approved By | IR Team Lead |
| Classification | Strictly Confidential |
| Review Cycle | Quarterly and after any P1/P2 data breach incident |

---

## 2. Purpose

This document defines the Level 1 (L1) SOC Analyst procedures for triaging
data breach and data exfiltration alerts.

The objectives of L1 triage are to:
- validate potential data exposure indicators
- determine whether unauthorized access or exfiltration occurred
- identify impacted systems, users, and data sources
- assess data sensitivity and business impact
- preserve critical evidence quickly
- escalate appropriately to L2, Legal, Compliance, and IR Teams

Data breach incidents are highly sensitive because they may:
- trigger legal obligations
- require regulatory reporting
- expose customer or employee data
- create reputational damage
- result in financial penalties

L1 analysts must prioritize:
- confidentiality
- evidence preservation
- rapid escalation
- accurate severity classification

---

## 3. Scope

Applies to:
- DLP alerts
- cloud storage exposure alerts
- suspicious outbound transfers
- unauthorized file sharing
- public cloud bucket exposure
- suspicious database exports
- ransomware-related exfiltration alerts
- insider data theft indicators
- unauthorized external sharing

Includes:
- endpoints
- cloud platforms
- databases
- SaaS applications
- collaboration platforms
- MSSP-managed environments

---

## 4. L1 Safety and Confidentiality Rules

Data breach investigations require strict confidentiality.

---

## 4.1 Mandatory Confidentiality Rules

| Rule | Reason |
|------|--------|
| Do NOT publicly discuss breach details | Prevent reputational/legal impact |
| Do NOT notify impacted users directly | Legal and executive coordination required |
| Do NOT alter exposed systems immediately | Preserve evidence |
| Do NOT disable accounts without approval | Business/legal impact |
| Do NOT download exposed sensitive data unnecessarily | Reduce exposure risk |

---

## 4.2 Need-to-Know Principle

Investigation details must only be shared with:
- assigned SOC personnel
- SOC Lead
- IR Team
- Legal Counsel
- Compliance Team
- approved executive management

---

# 5. L1 SLA Targets

| Severity | Response Time | Escalation Requirement |
|----------|---------------|------------------------|
| P1 | Immediate | SOC Lead + IR Team immediately |
| P2 | Within 10 minutes | L2 within 15 minutes |
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
| Alert source | DLP / CASB / SIEM |
| Detection timestamp | UTC time |
| Affected system | Database, cloud storage, endpoint |
| User account | Employee/service account |
| Data type | PII, financial, source code |
| Transfer method | Upload, email, USB |

---

## 6.2 Exposure Context

| Data Point | Purpose |
|------------|---------|
| Public or internal exposure | Risk classification |
| Number of records | Impact assessment |
| Exposure duration | Severity determination |
| External access confirmed | Escalation requirement |
| Encryption status | Exposure severity |

---

## 6.3 Cloud and Sharing Context

| Data Point | Example |
|------------|---------|
| Public cloud bucket | S3/Azure Blob |
| Shared link | OneDrive/SharePoint |
| External email | Unauthorized forwarding |
| Collaboration platform | Slack/Teams |

---

# 7. Step-by-Step L1 Triage Procedure

---

## Step 1 – Validate Alert Authenticity

Determine whether the alert is:
- confirmed suspicious activity
- legitimate business transfer
- misconfiguration
- false positive

---

### Validation Checklist

| Validation Check | Purpose |
|------------------|---------|
| Verify alert source | Confirm detection legitimacy |
| Review user role | Determine expected behavior |
| Review transfer size | Identify abnormal volume |
| Review destination | Detect external exposure |
| Review timing | Detect after-hours activity |

---

## Step 2 – Identify Exposure Type

Classify the data exposure scenario.

---

### Exposure Classification Matrix

| Exposure Type | Example | Risk |
|----------------|---------|------|
| Public cloud exposure | Public S3 bucket | Critical |
| Unauthorized external sharing | Public SharePoint link | High |
| Large outbound transfer | Bulk upload | High |
| Email exfiltration | Sensitive attachment sent externally | High |
| USB transfer | Sensitive files copied | High |
| Internal-only accidental exposure | Incorrect internal permissions | Medium |

---

## Step 3 – Assess Data Sensitivity

Determine the sensitivity of the potentially exposed data.

---

### Sensitive Data Classification

| Data Type | Risk Level |
|-----------|------------|
| Customer PII | Critical |
| Payment data | Critical |
| Healthcare data | Critical |
| Source code/IP | Critical |
| Employee records | High |
| Internal business data | Medium |

---

## Step 4 – Determine Exposure Status

Determine whether:
- data was exposed
- data was accessed
- data was downloaded
- exfiltration completed

---

### Exposure Status Matrix

| Status | Meaning |
|--------|---------|
| Potential Exposure | Data accessible but no access evidence |
| Confirmed Exposure | Unauthorized access confirmed |
| Confirmed Exfiltration | Data transferred externally |
| Public Exposure | Data accessible publicly |

---

## Step 5 – Preserve Evidence

Evidence preservation is critical for:
- legal review
- regulatory reporting
- forensic investigation

---

### Minimum Evidence Collection

| Evidence Type | Source |
|--------------|-------|
| Alert export | SIEM/DLP |
| Access logs | Cloud or server logs |
| Sharing configuration | Cloud storage settings |
| File access records | DLP/file server logs |
| Screenshots | SOC evidence package |
| User activity logs | Endpoint/cloud telemetry |

---

## Step 6 – Initial Severity Recommendation

Severity depends on:
- data sensitivity
- exposure scope
- public accessibility
- confirmed access or exfiltration

---

### Severity Recommendation Matrix

| Scenario | Recommended Severity |
|----------|----------------------|
| Confirmed public exposure of regulated data | P1 |
| Confirmed customer data exfiltration | P1 |
| Large unauthorized outbound transfer | P1 |
| Unauthorized sensitive sharing | P2 |
| Internal accidental exposure | P3 |
| Low-risk exposure with no access evidence | P4 |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

## Step 7 – Escalation Decision

---

### Escalate to L2 if:

| Condition | Reason |
|-----------|--------|
| Sensitive data involved | Scope analysis required |
| Unauthorized sharing detected | Investigation required |
| Large transfers observed | Exfiltration review required |
| Public cloud exposure | Cloud review required |

---

### Escalate to SOC Lead Immediately if:

| Condition | Reason |
|-----------|--------|
| Regulated data exposed | Legal/regulatory risk |
| Publicly accessible sensitive data | Critical exposure |
| Confirmed exfiltration | Major incident |
| Multiple systems involved | Enterprise-wide risk |

---

### Escalate to Legal and Compliance Through Approved Process if:

| Condition | Reason |
|-----------|--------|
| Customer data involved | Notification obligations |
| Regulated data exposed | Compliance review |
| Cross-border data involved | Jurisdictional review |
| Third-party/customer impact | Legal review |

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Legal-Notification.md`

---

# 8. Evidence Handling Requirements

Data breach evidence may become:
- legal evidence
- regulatory evidence
- audit evidence

---

## 8.1 Handling Requirements

| Requirement | Purpose |
|-------------|---------|
| Encrypt evidence exports | Protect sensitive data |
| Restrict access | Need-to-know principle |
| Preserve timestamps | Timeline integrity |
| Maintain chain-of-custody | Legal defensibility |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 9. Common L1 Data Breach Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Delaying escalation | Continued exposure |
| Publicly discussing breach | Reputational/legal impact |
| Failing to preserve logs quickly | Evidence loss |
| Underestimating cloud exposure | Large-scale impact missed |
| Assuming no download means no breach | Exposure may still be reportable |
| Ignoring insider involvement indicators | Missed malicious activity |

---

# 10. MSSP Handling Notes

For MSSP-managed environments:
- maintain strict client confidentiality
- follow client-specific notification timelines
- preserve client evidence separately
- avoid cross-client disclosure
- coordinate Legal and Compliance actions through approved client contacts

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 11. Related Documents

| Document | Path |
|---------|------|
| Data Breach Master | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md` |
| Data Breach L2 Investigation | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L2-Investigation.md` |
| Data Breach L3 Forensics | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L3-Forensics.md` |
| Legal Notification | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Legal-Notification.md` |
| Regulatory Reporting | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Regulatory-Reporting.md` |
| Data Breach MITRE Mapping | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-MITRE-Mapping.md` |
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