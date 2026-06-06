# Playbook: Data Breach – Regulatory Reporting

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Data Breach (Regulatory Reporting) |
| Document ID | IR-PB-DBR-006 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | IR Team Lead / Compliance Lead |
| Approved By | CISO and Legal Counsel |
| Classification | Strictly Confidential |
| Review Cycle | Quarterly and after any P1/P2 data breach incident |

---

## 2. Purpose

This document defines the regulatory reporting procedures for data breach
incidents where regulatory obligations are triggered.

The objectives are to:
- identify applicable regulatory frameworks
- determine reporting obligations and timelines
- prepare accurate and complete regulatory reports
- coordinate internal approvals before submission
- maintain documentation of all regulatory communications
- minimize regulatory penalty risk
- demonstrate organizational accountability and transparency

Regulatory reporting is a formal legal obligation.

All regulatory reports must be:
- reviewed and approved by Legal Counsel
- approved by CISO and Executive Management
- submitted through authorized communication channels
- documented with delivery confirmation

---

## 3. Scope

Applies to:
- incidents involving regulated data
- customer PII breaches
- financial data breaches
- healthcare data exposure
- cross-border data incidents
- incidents meeting regulatory notification thresholds
- MSSP-managed client regulatory obligations

Includes:
- RBI regulatory reporting
- CERT-In reporting
- GDPR supervisory authority reporting
- PCI-DSS reporting
- HIPAA reporting
- industry-specific regulatory frameworks

---

## 4. Regulatory Reporting Principles

| Principle | Description |
|-----------|-------------|
| Timeliness | Submit within regulatory deadlines |
| Accuracy | Report based on confirmed facts |
| Completeness | Include all required elements |
| Legal Review | All reports reviewed by Legal Counsel |
| Documentation | Maintain full submission records |
| Consistency | Align with internal incident records |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|------|------------------|
| Compliance Lead | Identify obligations and coordinate reporting |
| Legal Counsel | Review and approve all submissions |
| IR Team | Technical findings and evidence |
| CISO | Final security sign-off |
| Executive Management | Approval for major disclosures |
| SOC Team | Technical investigation support |
| MSSP SDM | Client regulatory coordination |

---

# 6. Regulatory Framework Identification

Determine which regulations apply to the incident.

---

## 6.1 Regulatory Applicability Matrix

| Framework | Applies When |
|-----------|-------------|
| RBI Cyber Security Framework | Incident impacts RBI-regulated entity |
| CERT-In Guidelines | Incident in India |
| GDPR | EU/EEA citizens data involved |
| PDPB India | Indian citizen data involved |
| PCI-DSS | Payment card data involved |
| HIPAA | US healthcare data involved |
| ISO 27001 | ISMS incident notification |
| Sector-specific regulations | As applicable |

---

## 6.2 Multi-Jurisdiction Considerations

When multiple regulations apply:
- identify the strictest deadline
- coordinate with Legal for jurisdiction-specific requirements
- prepare separate reports if required
- maintain separate documentation per regulation

---

# 7. RBI Regulatory Reporting Procedure

---

## 7.1 RBI Reporting Triggers

| Trigger | Reporting Required |
|---------|-------------------|
| Cyber attack on banking infrastructure | Yes |
| Customer financial data breach | Yes |
| Payment system compromise | Yes |
| Service disruption above threshold | Yes |

---

## 7.2 RBI Reporting Timeline

| Milestone | Timeline |
|-----------|---------|
| Initial notification | As per RBI circular |
| Preliminary report | Within defined hours |
| Detailed report | Within defined days |
| Final report | Upon incident closure |

---

## 7.3 RBI Report Content Requirements

| Required Element | Description |
|------------------|-------------|
| Incident description | Nature of breach |
| Systems impacted | Affected infrastructure |
| Data involved | Categories and volume |
| Timeline | Detection to containment |
| Impact assessment | Business and customer impact |
| Containment actions | Steps taken |
| Recovery status | Current operational status |
| Preventive measures | Future controls |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`
`07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`

---

# 8. CERT-In Reporting Procedure

---

## 8.1 CERT-In Reporting Triggers

| Trigger | Reporting Required |
|---------|-------------------|
| Cybersecurity incident | Yes |
| Data breach | Yes |
| Ransomware | Yes |
| Unauthorized access | Yes |

---

## 8.2 CERT-In Reporting Timeline

| Milestone | Timeline |
|-----------|---------|
| Initial report | Within 6 hours of detection |
| Follow-up report | As required |
| Final report | Upon closure |

---

## 8.3 CERT-In Report Content Requirements

| Required Element | Description |
|------------------|-------------|
| Incident type | Classification |
| Date and time | UTC timestamps |
| Systems affected | Infrastructure details |
| Nature of data | Categories involved |
| Actions taken | Response steps |
| Current status | Active/contained/resolved |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`

---

# 9. GDPR Reporting Procedure

---

## 9.1 GDPR Reporting Triggers

| Trigger | Reporting Required |
|---------|-------------------|
| EU/EEA citizen data breach | Yes |
| Risk to individual rights | Supervisory authority |
| High risk to individuals | Individual notification |

---

## 9.2 GDPR Reporting Timeline

| Milestone | Timeline |
|-----------|---------|
| Supervisory authority notification | Within 72 hours |
| Individual notification | Without undue delay |

---

## 9.3 GDPR Report Content Requirements

| Required Element | Description |
|------------------|-------------|
| Nature of breach | Incident description |
| Data categories | Types of data involved |
| Approximate individuals | Record count estimate |
| Likely consequences | Risk assessment |
| Measures taken | Response and prevention |
| DPO contact | Data Protection Officer details |

---

## 9.4 GDPR Derogation Handling

If 72-hour deadline cannot be met:
- notify supervisory authority with reason for delay
- provide preliminary information available
- document the derogation rationale
- submit complete report as soon as possible

---

# 10. PCI-DSS Reporting Procedure

---

## 10.1 PCI-DSS Reporting Triggers

| Trigger | Reporting Required |
|---------|-------------------|
| Cardholder data compromise | Yes |
| Suspected payment card fraud | Yes |
| POS or payment system breach | Yes |

---

## 10.2 PCI-DSS Reporting Timeline

| Milestone | Timeline |
|-----------|---------|
| Card scheme notification | Immediately upon confirmation |
| Acquiring bank notification | Immediate |
| Forensic investigation | Within defined PCI timelines |

---

## 10.3 PCI-DSS Report Content Requirements

| Required Element | Description |
|------------------|-------------|
| Compromised data types | Card data categories |
| Number of cards | Estimated volume |
| Time of compromise | Exposure window |
| Systems affected | Infrastructure |
| Containment actions | Steps taken |

---

# 11. ISO 27001 Incident Notification

---

## 11.1 ISO 27001 Reporting Requirements

| Requirement | Purpose |
|-------------|---------|
| Incident log updated | ISMS record |
| Corrective action tracked | Improvement evidence |
| Management review notified | Governance |
| Audit evidence maintained | Certification compliance |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/ISO27001-Incident-Notification.md`
`07_REPORTING/07.4_Regulatory-Reports/ISO27001-Incident-Log.md`

---

# 12. Regulatory Report Preparation Workflow

---

## 12.1 Report Preparation Steps

| Step | Action |
|------|--------|
| 1 | Confirm regulatory applicability |
| 2 | Identify reporting deadline |
| 3 | Gather technical findings from IR Team |
| 4 | Draft report content |
| 5 | Legal Counsel review |
| 6 | CISO review and approval |
| 7 | Executive Management approval |
| 8 | Submit through authorized channel |
| 9 | Obtain delivery confirmation |
| 10 | Document submission in evidence package |

---

## 12.2 Report Review Checklist

| Checklist Item | Required |
|----------------|----------|
| All required elements present | Yes |
| Technical findings verified | Yes |
| Legal review completed | Yes |
| Timeline accuracy confirmed | Yes |
| Record count validated | Yes |
| Approval documented | Yes |

---

# 13. Post-Submission Requirements

After regulatory submission:

| Requirement | Purpose |
|-------------|---------|
| Monitor for regulator response | Ongoing coordination |
| Respond to follow-up inquiries | Cooperation |
| Provide additional evidence if requested | Compliance |
| Update report if new facts emerge | Accuracy |
| Maintain submission records | Audit |

---

## 13.1 Regulator Follow-Up Management

| Action | Owner |
|--------|-------|
| Acknowledge regulator response | Compliance Team |
| Coordinate technical responses | IR Team + Legal |
| Provide requested evidence | IR Team |
| Track outstanding requirements | Compliance Team |

---

# 14. Documentation Requirements

| Documentation Item | Required |
|-------------------|----------|
| Regulatory applicability assessment | Yes |
| Report draft versions | Yes |
| Legal approval record | Yes |
| Submission confirmation | Yes |
| Regulator correspondence | Yes |
| Follow-up tracking | Yes |

---

# 15. Common Regulatory Reporting Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Missing regulatory deadline | Penalty risk |
| Inaccurate record count | Regulatory issues |
| Submitting without Legal review | Legal exposure |
| Inconsistent information | Regulatory scrutiny |
| Failing to document submissions | Audit failure |
| Not monitoring regulator responses | Compliance gaps |

---

# 16. MSSP Client Handling Notes

For MSSP-managed environments:
- regulatory reporting obligation rests with the client
- MSSP provides technical findings and evidence support
- do not submit regulatory reports on client behalf without written authorization
- coordinate through client Compliance and Legal contacts
- maintain documentation of all coordination
- follow client-specific regulatory timelines

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`
`09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-ISO27001-Controls.md`

---

# 17. Related Documents

| Document | Path |
|---------|------|
| Data Breach Master | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md` |
| Data Breach L1 Triage | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L1-Triage.md` |
| Data Breach L2 Investigation | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L2-Investigation.md` |
| Data Breach L3 Forensics | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L3-Forensics.md` |
| Legal Notification | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Legal-Notification.md` |
| Data Breach MITRE Mapping | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-MITRE-Mapping.md` |
| RBI Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md` |
| CERT-In Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md` |
| ISO 27001 Notification | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/ISO27001-Incident-Notification.md` |
| RBI Report Template | `07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md` |

---

## 18. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | IR Team Lead / Compliance Lead | Initial version |

---

## 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**