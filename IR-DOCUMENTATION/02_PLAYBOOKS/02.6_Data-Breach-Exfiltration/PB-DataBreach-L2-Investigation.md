# Playbook: Data Breach and Data Exfiltration – L2 Investigation

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Data Breach and Data Exfiltration (L2 Investigation) |
| Document ID | IR-PB-DBR-003 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | L2 SOC Lead / IR Team Lead |
| Approved By | CISO |
| Classification | Strictly Confidential |
| Review Cycle | Quarterly and after any P1/P2 data breach incident |

---

## 2. Purpose

This document defines the Level 2 (L2) investigation procedures for
data breach and data exfiltration incidents escalated from L1 triage.

The objectives of L2 investigation are to:
- confirm whether data was accessed or exfiltrated
- determine scope and scale of exposure
- identify impacted systems, users, and datasets
- identify method of exfiltration or exposure
- determine exposure duration
- identify attacker access paths
- support containment decisions
- prepare for legal and regulatory escalation

L2 investigation is focused on technical scoping and validation before
formal legal and regulatory notification actions begin.

---

## 3. Scope

Applies to:
- unauthorized data access
- suspicious outbound transfers
- public cloud exposure
- database export activity
- DLP-triggered exfiltration alerts
- insider data theft investigations
- ransomware-related data staging
- SaaS data exposure

Includes:
- on-premises systems
- databases
- cloud platforms
- collaboration tools
- email systems
- MSSP-managed environments

---

## 4. Preconditions Before Investigation

L2 investigation begins after:
- L1 triage completed
- severity assigned
- evidence preservation initiated
- SOC Lead notified for P1/P2

Required inputs from L1:

| Required Input | Purpose |
|---------------|---------|
| Alert details | Context validation |
| User identity | Access scoping |
| Data type involved | Risk classification |
| Initial exposure indicators | Investigation direction |
| Affected system | Technical scoping |
| Severity recommendation | Escalation context |

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L1-Triage.md`

---

# 5. L2 Investigation Objectives

| Objective | Description |
|-----------|-------------|
| Confirm Data Exposure | Validate unauthorized access |
| Confirm Exfiltration | Determine if data left environment |
| Identify Impacted Records | Quantify affected data |
| Identify Exposure Duration | Determine breach window |
| Identify Root Cause | Determine entry or misconfiguration |
| Support Containment | Provide access restriction guidance |
| Support Legal Review | Prepare technical findings |

---

# 6. Investigation Workflow Overview

| Phase | Focus Area |
|------|-------------|
| Phase 1 | Exposure validation |
| Phase 2 | Data access analysis |
| Phase 3 | Exfiltration pathway analysis |
| Phase 4 | Cloud and SaaS analysis |
| Phase 5 | Database and application review |
| Phase 6 | Timeline reconstruction |
| Phase 7 | Impact assessment |
| Phase 8 | Escalation recommendations |

---

# 7. Phase 1 – Exposure Validation

Confirm whether exposure truly occurred.

---

## 7.1 Exposure Validation Checklist

| Check | Purpose |
|------|---------|
| Confirm unauthorized access | Validate breach |
| Confirm access outside policy | Identify violation |
| Confirm public accessibility | Cloud misconfiguration |
| Confirm abnormal data volume | Detect staging |
| Confirm authentication logs | Identify access identity |

---

## 7.2 Public Cloud Exposure Review

| Exposure Type | Example |
|---------------|---------|
| Public S3 bucket | World-readable object |
| Public Azure Blob | Anonymous access |
| Public SharePoint link | Anyone with link access |
| Misconfigured SaaS sharing | Guest access |

---

### Public Exposure Verification Steps

| Step | Action |
|------|--------|
| Validate bucket/container ACL | Confirm public flag |
| Review access logs | Identify external access |
| Confirm exposure duration | Determine breach window |
| Identify shared links | Remove or restrict |

---

# 8. Phase 2 – Data Access Analysis

Determine what data was accessed and by whom.

---

## 8.1 Data Access Review Areas

| Area | Investigation Focus |
|------|--------------------|
| File server logs | Bulk file access |
| Database logs | Large queries/exports |
| Cloud audit logs | File downloads |
| Application logs | API extraction |
| Email logs | Sensitive attachments |

---

## 8.2 Bulk Access Indicators

| Indicator | Meaning |
|-----------|---------|
| Large sequential file reads | Data collection |
| Database export commands | Structured data extraction |
| High-volume download events | Data theft |
| Access outside business hours | Suspicious activity |

---

## 8.3 Sensitive Data Impact Review

| Data Type | Impact |
|-----------|--------|
| Customer PII | Regulatory risk |
| Financial data | Fraud risk |
| Healthcare data | Compliance risk |
| Intellectual property | Business risk |
| Employee data | HR/legal risk |

---

# 9. Phase 3 – Exfiltration Pathway Analysis

Determine how data may have left the environment.

---

## 9.1 Exfiltration Pathways

| Method | Indicators |
|--------|-----------|
| Cloud upload | CASB logs |
| External email | Mail flow logs |
| API export | API logs |
| Remote session | RDP/VPN logs |
| USB transfer | Endpoint telemetry |

---

## 9.2 Outbound Traffic Analysis

| Review Area | Purpose |
|-------------|---------|
| Proxy logs | External uploads |
| Firewall logs | Large outbound traffic |
| DNS logs | Suspicious domains |
| CDN logs | Data movement patterns |

---

## 9.3 Exfiltration Confirmation Checklist

| Question | Required |
|----------|----------|
| Was data transferred externally? | Yes/No |
| How much data transferred? | Size/volume |
| Was transfer successful? | Confirmed |
| Was encryption used? | Yes/No |
| Was attacker authenticated? | Identity confirmed |

---

# 10. Phase 4 – Cloud and SaaS Analysis

Cloud platforms frequently introduce exposure risks.

---

## 10.1 Cloud Activity Review

| Platform | Investigation Focus |
|----------|--------------------|
| AWS S3 | Bucket permissions |
| Azure Blob | Container access |
| OneDrive | Sharing links |
| SharePoint | External sharing |
| Google Drive | Public links |
| SaaS apps | External exports |

---

## 10.2 Cloud Abuse Indicators

| Indicator | Meaning |
|-----------|---------|
| New public sharing link | Exposure |
| Large upload to personal account | Exfiltration |
| Guest account creation | Data sharing |
| OAuth token abuse | Persistent access |

---

# 11. Phase 5 – Database and Application Review

If structured data involved:

---

## 11.1 Database Activity Indicators

| Indicator | Meaning |
|-----------|---------|
| Large SELECT queries | Data extraction |
| Export commands | Data dump |
| Unusual account usage | Compromise |
| After-hours queries | Suspicious |

---

## 11.2 Application-Level Review

| Application | Focus |
|-------------|------|
| CRM | Customer data access |
| ERP | Financial exports |
| HR systems | Employee data |
| Billing platforms | Payment data |

---

# 12. Phase 6 – Timeline Reconstruction

Build an authoritative timeline.

---

## 12.1 Timeline Components

Include:
- initial access
- first data access
- bulk data access
- staging activity
- exfiltration
- containment actions

---

### Timeline Template

| Time (UTC) | Event | User | System | Source |
|-----------|------|------|--------|--------|
| | Login | | | |
| | Data access | | | |
| | Export command | | | |
| | Upload event | | | |
| | Containment action | | | |

---

# 13. Phase 7 – Impact Assessment

---

## 13.1 Impact Assessment Matrix

| Factor | Assessment |
|--------|------------|
| Data sensitivity | Low/Medium/High/Critical |
| Number of records | Approximate count |
| Regulatory impact | Yes/No |
| Public exposure | Yes/No |
| Legal exposure | Low/Medium/High |
| Customer impact | Low/Medium/High |

---

## 13.2 Exposure Duration Analysis

Determine:
- first exposure timestamp
- last exposure timestamp
- time to detection
- time to containment

---

# 14. Phase 8 – Escalation Recommendations

---

## 14.1 Escalate to IR Team if:

| Condition | Reason |
|-----------|--------|
| Confirmed large-scale exfiltration | Major incident |
| Public exposure confirmed | Reputational risk |
| Multiple systems impacted | Enterprise-wide compromise |
| Regulated data exposed | Compliance risk |

---

## 14.2 Escalate to Legal and Compliance if:

| Condition | Reason |
|-----------|--------|
| PII exposure | Notification requirement |
| Cross-border data | Jurisdictional obligations |
| Customer data involved | Legal review |
| Vendor/third-party impact | Contractual obligations |

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Legal-Notification.md`

---

# 15. Documentation Requirements

| Documentation Item | Required |
|-------------------|----------|
| Exposure confirmation | Yes |
| Exfiltration confirmation | Yes |
| Data type identified | Yes |
| Estimated impacted records | Yes |
| Exposure duration | Yes |
| Root cause | Yes |
| Escalation decision | Yes |
| Containment actions | Yes |

---

# 16. Common L2 Investigation Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Assuming no download means no breach | Exposure still reportable |
| Ignoring cloud audit logs | Missed exposure |
| Failing to quantify records | Inaccurate impact assessment |
| Delayed Legal involvement | Regulatory risk |
| Underestimating insider involvement | Missed malicious activity |
| Not preserving database logs quickly | Log rotation loss |

---

# 17. MSSP Client Handling Notes

For MSSP-managed environments:
- maintain client-specific evidence segregation
- coordinate Legal notifications through client leadership
- follow client SLA timelines
- avoid cross-client data disclosure
- document all escalation actions

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 18. Related Documents

| Document | Path |
|---------|------|
| Data Breach Master | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md` |
| Data Breach L1 Triage | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L1-Triage.md` |
| Data Breach L3 Forensics | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L3-Forensics.md` |
| Legal Notification | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Legal-Notification.md` |
| Regulatory Reporting | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Regulatory-Reporting.md` |
| Data Breach MITRE Mapping | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-MITRE-Mapping.md` |
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