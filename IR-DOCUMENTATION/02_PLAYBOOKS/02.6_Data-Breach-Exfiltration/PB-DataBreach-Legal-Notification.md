# Playbook: Data Breach – Legal Notification

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Data Breach (Legal Notification) |
| Document ID | IR-PB-DBR-005 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | IR Team Lead / Legal Counsel |
| Approved By | CISO and Legal Counsel |
| Classification | Strictly Confidential |
| Review Cycle | Quarterly and after any P1/P2 data breach incident |

---

## 2. Purpose

This document defines the legal notification procedures for data breach
incidents where:
- customer or employee data was exposed
- regulated data was compromised
- legal obligations may require notification
- litigation risk exists
- law enforcement involvement is possible

The objectives are to:
- determine legal notification obligations
- coordinate internal approvals
- prepare accurate notification content
- meet regulatory and contractual timelines
- minimize legal and reputational risk
- maintain documentation for legal defensibility

Legal notifications are among the most sensitive and consequential
actions in any data breach response.

All legal notification decisions must be approved by:
- Legal Counsel
- CISO
- Executive Management

---

## 3. Scope

Applies to:
- customer personal data breaches
- employee personal data exposure
- regulated data compromise
- third-party vendor data exposure
- cross-border data incidents
- incidents with litigation risk
- incidents requiring law enforcement referral
- MSSP-managed client breach notifications

---

## 4. Notification Principles

| Principle | Description |
|-----------|-------------|
| Accuracy | Notify based on confirmed facts |
| Timeliness | Meet regulatory and contractual deadlines |
| Confidentiality | Restrict internal knowledge |
| Legal Guidance | All notifications reviewed by Legal |
| Completeness | Include required information |
| Consistency | Align messaging across channels |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|------|------------------|
| Legal Counsel | Legal notification decisions and review |
| CISO | Security findings and approvals |
| IR Team | Technical findings and evidence |
| Compliance Team | Regulatory obligations review |
| Executive Management | Final approval for disclosures |
| Communications/PR | Public statements where required |
| MSSP SDM | Client notification coordination |

---

# 6. Legal Notification Triggers

Legal Counsel must be engaged immediately when:

| Trigger | Action |
|---------|--------|
| Customer PII confirmed exposed | Immediate Legal escalation |
| Regulated data confirmed compromised | Immediate Legal escalation |
| Cross-border data involved | Jurisdiction review |
| Employee data exposed | HR + Legal engagement |
| Litigation risk identified | Legal protective action |
| Law enforcement referral possible | Legal direction required |
| Contractual notification required | Contract review |

---

# 7. Legal Hold Requirements

When litigation or regulatory action is possible:
- all relevant evidence must be preserved
- retention policies must be suspended for impacted data
- destruction schedules must be paused

---

## 7.1 Legal Hold Triggers

| Trigger | Action |
|---------|--------|
| Litigation risk | Immediate legal hold |
| Regulatory investigation | Preserve all relevant evidence |
| Law enforcement referral | Evidence preservation order |
| Customer dispute | Hold relevant communications |

---

## 7.2 Legal Hold Coverage

Preserve:
- system logs
- database records
- email communications
- cloud audit logs
- forensic evidence
- incident documentation
- communications with regulators

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 8. Notification Determination Workflow

The following workflow guides the notification decision process.

---

## 8.1 Notification Decision Matrix

| Question | Yes Path | No Path |
|----------|----------|---------|
| Was personal data accessed or exposed? | Proceed to Step 2 | Monitor and document |
| Is the data regulated? | Legal review mandatory | Risk assessment |
| Was access unauthorized? | Notification likely required | Review circumstances |
| Is the exposure significant? | Prepare notification | Monitor |
| Does regulation require notification? | Initiate notification process | Legal discretion |

---

## 8.2 Notification Obligation Assessment

| Data Type | Likely Notification Required |
|-----------|------------------------------|
| Customer PII | Yes |
| Financial data | Yes |
| Healthcare data | Yes |
| Employee records | Context-dependent |
| Source code/IP | Not typically |
| Non-sensitive data | Unlikely |

---

# 9. Notification Categories

---

## 9.1 Regulatory Notification

Required when data breach meets regulatory thresholds.

| Regulation | Requirement |
|------------|-------------|
| GDPR | 72-hour notification to supervisory authority |
| RBI Framework | Per circular requirements |
| CERT-In | As per advisory timelines |
| PDPB India | As per applicable regulations |
| HIPAA | 60-day notification |
| PCI-DSS | Card scheme notification |

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Regulatory-Reporting.md`

---

## 9.2 Individual Notification

Required when individuals are at risk from exposure.

---

### Individual Notification Checklist

| Checklist Item | Required |
|----------------|----------|
| Identify impacted individuals | Yes |
| Confirm notification obligation | Legal review |
| Prepare notification content | Legal review |
| Determine notification channel | Legal direction |
| Document notifications sent | Yes |

---

### Individual Notification Content Requirements

| Content Item | Purpose |
|--------------|---------|
| Description of incident | Transparency |
| Data types exposed | Individual awareness |
| Likely impact | Risk communication |
| Protective actions recommended | Individual protection |
| Contact information | Support channel |
| Organization response actions | Accountability |

---

## 9.3 Third-Party and Contractual Notification

When third-party data is involved:
- review contracts for notification obligations
- coordinate with Legal and procurement teams
- follow contractual timelines
- document all notifications

---

### Third-Party Notification Matrix

| Scenario | Notification Required |
|----------|-----------------------|
| Customer data processed by vendor | Notify customer |
| Vendor breach impacts your data | Legal review |
| Partner data involved | Contract review |
| Supply chain compromise | Coordination required |

---

## 9.4 Law Enforcement Notification

Law enforcement engagement requires:
- Legal Counsel approval
- Executive Management approval
- careful timing to avoid compromising investigation

---

### Law Enforcement Engagement Triggers

| Trigger | Consideration |
|---------|---------------|
| Criminal data theft | Legal decision |
| Nation-state attack | Legal + Executive decision |
| Financial fraud | Legal direction |
| Major infrastructure impact | Legal + Government relations |

---

# 10. Notification Content Requirements

---

## 10.1 Regulatory Notification Content

| Required Element | Description |
|------------------|-------------|
| Incident description | Nature of breach |
| Data categories | Types of data involved |
| Approximate records | Number of individuals affected |
| Exposure window | Timeline |
| Likely consequences | Risk assessment |
| Containment measures | Actions taken |
| Preventive measures | Future controls |
| Contact point | DPO or responsible person |

---

## 10.2 Customer Notification Content

| Required Element | Description |
|------------------|-------------|
| What happened | Plain language description |
| What was involved | Data types exposed |
| What we are doing | Response actions |
| What you should do | Protective steps for individual |
| Contact information | Support channel |
| Date of incident | Transparency |

---

# 11. Notification Timing Requirements

---

## 11.1 Internal Notification Timeline

| Action | Timing |
|--------|--------|
| Legal Counsel notification | Immediate on P1/P2 confirmation |
| CISO notification | Immediate |
| Executive notification | Within 1 hour of P1 confirmation |
| Compliance notification | Within 2 hours |

---

## 11.2 External Notification Timeline

| Notification Type | Timing |
|-------------------|--------|
| CERT-In | Per advisory |
| RBI | Per circular |
| GDPR supervisory authority | Within 72 hours |
| Individuals | As per regulation |
| Third parties | Per contract |

---

# 12. Notification Documentation Requirements

All notifications must be documented.

| Documentation Item | Required |
|-------------------|----------|
| Notification decision rationale | Yes |
| Legal approval record | Yes |
| Notification content copy | Yes |
| Delivery confirmation | Yes |
| Recipient list | Yes |
| Timestamp of each notification | Yes |

---

# 13. Notification Risks and Controls

| Risk | Impact | Control |
|------|--------|---------|
| Premature disclosure | Legal/business risk | Legal approval required |
| Inaccurate content | Legal liability | Legal review mandatory |
| Missed deadline | Regulatory penalty | Compliance monitoring |
| Inadequate content | Regulatory issues | Template review |
| Unauthorized disclosure | Confidentiality breach | Need-to-know enforced |

---

# 14. Common Legal Notification Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Notifying without Legal review | Legal exposure |
| Missing regulatory deadlines | Regulatory penalty |
| Inaccurate record count | Regulatory issues |
| Inconsistent messaging | Legal/reputational risk |
| Not documenting notifications | Audit failure |
| Premature public disclosure | Reputational/legal risk |

---

# 15. MSSP Client Handling Notes

For MSSP-managed environments:
- all notification decisions rest with the client organization
- MSSP provides technical findings and timeline support
- do not issue notifications on client behalf without written authorization
- coordinate through client Legal and Compliance contacts
- maintain documentation of all coordination activities
- follow client contractual notification timelines strictly

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 16. Related Documents

| Document | Path |
|---------|------|
| Data Breach Master | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md` |
| Data Breach L1 Triage | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L1-Triage.md` |
| Data Breach L2 Investigation | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L2-Investigation.md` |
| Data Breach L3 Forensics | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L3-Forensics.md` |
| Regulatory Reporting | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Regulatory-Reporting.md` |
| Data Breach MITRE Mapping | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-MITRE-Mapping.md` |
| Legal Counsel Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| RBI Incident Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md` |
| Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 17. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | IR Team Lead / Legal Counsel | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**