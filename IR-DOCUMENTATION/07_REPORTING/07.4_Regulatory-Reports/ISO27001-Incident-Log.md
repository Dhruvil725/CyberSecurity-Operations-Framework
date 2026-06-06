# ISO/IEC 27001 Incident Log (ISMS Record)

---

# 1. Document Control

| Field          | Value                                 |
| -------------- | ------------------------------------- |
| Document Name  | Register – ISO/IEC 27001 Incident Log |
| Document ID    | RPT-REG-002                           |
| Version        | 1.0                                   |
| Effective Date | 30-May-2026                           |
| Owner          | ISMS Manager / Compliance Lead        |
| Approved By    | CISO                                  |
| Classification | Internal – Confidential               |
| Review Cycle   | Quarterly                             |

---

# 2. Purpose

This document provides the standardized **ISO/IEC 27001 Incident Log** register format to record information security events and incidents in support of ISMS requirements.

Maintaining an incident log is critical because:

- ISO/IEC 27001 requires structured recording and handling of security incidents/events
- audit readiness depends on consistent records with traceable evidence and actions
- incident logs support trend analysis, corrective actions, and continual improvement (Clause 10)
- logs provide evidence of communication, escalation, and decisions taken
- MSSP operations may require client-specific incident logs while maintaining segregation

This register ensures:

- consistent minimum fields across all incidents
- linkage between tickets, evidence packages, PIR/RCA outcomes, and corrective actions
- clear classification and status tracking
- audit-ready evidence of incident management lifecycle

Reference alignment:
`00_GOVERNANCE/00.1_Policies/IR-Policy-ISO27001-Alignment.md`

---

# 3. Scope

This incident log applies to:

| Item                                   | Included                                                                                  |
| -------------------------------------- | ----------------------------------------------------------------------------------------- |
| Information security incidents         | P1–P4 incidents as defined in severity matrix                                             |
| Information security events (optional) | Significant events that require tracking but not declared incidents                       |
| ISMS scope                             | Systems, processes, and operations within ISMS scope                                      |
| MSSP                                   | Client incidents may be logged separately; this log may contain sanitized references only |

Out of scope:

- raw evidence storage (stored in evidence repository)
- detailed incident narratives (stored in incident reports)

References:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

# 4. Definitions

| Term               | Definition                                                        |
| ------------------ | ----------------------------------------------------------------- |
| Incident log entry | Row/record describing an event/incident and its handling outcomes |
| ISMS scope         | Defined scope of ISO 27001 certification/implementation           |
| Corrective action  | CAPA item created to prevent recurrence                           |
| PIR                | Post Incident Review / Lessons Learned                            |
| Evidence reference | Secure link/path/ID pointing to evidence stored in evidence vault |

---

# 5. Roles and Responsibilities

| Role                     | Responsibilities                                                            |
| ------------------------ | --------------------------------------------------------------------------- |
| ISMS Manager             | Owns incident log; ensures completeness; supports audits                    |
| Compliance Lead          | Validates regulatory obligations and reporting records where relevant       |
| SOC Lead                 | Ensures incident tickets exist and are linked; validates classification     |
| IR Team Lead             | Ensures P1/P2 incidents have PIR/RCA and evidence references                |
| SOC Manager              | Oversees quality and governance; ensures KPIs and management review linkage |
| Evidence Custodian       | Provides evidence references and retention details                          |
| MSSP SDM (if applicable) | Ensures client incidents are tenant-scoped and properly referenced          |

---

# 6. Logging Principles (Mandatory)

| Principle                 | Requirement                                                                |
| ------------------------- | -------------------------------------------------------------------------- |
| Single source of truth    | Ticketing system remains operational source; incident log is ISMS register |
| Traceable                 | Every incident log entry must reference ticket ID                          |
| UTC timestamps            | Mandatory for detection, response, closure times                           |
| Consistent classification | Use severity and category definitions from classification folder           |
| No raw sensitive data     | Do not paste credentials/PII; use references                               |
| Continual improvement     | PIR/RCA and corrective actions must be linked for P1/P2                    |
| Reviewable                | Quarterly review and update required                                       |

---

# 7. Minimum Fields (Mandatory)

Each entry must include at minimum:

## 7.1 Identification

- Incident Log ID (unique)
- Incident Ticket ID
- Incident category
- Severity (initial and final)
- ISMS scope flag (in scope/out of scope)

## 7.2 Timing (UTC)

- Noticing time
- Detection time
- Incident declared time
- Containment time (if applicable)
- Resolution time
- Closure time

## 7.3 Impact and Outcome

- CIA impact (Confidentiality/Integrity/Availability)
- Data impact (if applicable)
- Business impact summary
- Root cause summary (or “RCA in progress”)
- Final disposition (TP/FP/INFO/DUPLICATE)

## 7.4 Governance

- Stakeholders notified (management/compliance/legal/client)
- Regulatory reporting assessed/submitted (if applicable)
- Evidence references and CoC reference (if applicable)
- PIR/RCA references
- Corrective action references and status

---

# 8. Incident Log Register Template (Copy/Paste Table)

> Maintain this as a controlled register. Use one row per incident.  
> For large programs, you may store as a spreadsheet; this markdown provides the standard schema.

| Log ID            | Ticket ID     | Date Opened (UTC) | Category | Severity (Initial→Final) | ISMS Scope (Y/N) | Noticing (UTC) | Detection (UTC) | Declared (UTC) | Contained (UTC) | Resolved (UTC) | Closed (UTC) | CIA Impact | Data Impact (Y/N/Unknown) | Business Impact Summary | Root Cause Status | Disposition | Evidence Ref | CoC Ref | PIR Ref | RCA Ref | Corrective Actions Ref | Regulatory (Assessed/Subm.) | Stakeholders Notified | Notes |
| ----------------- | ------------- | -----------------:| -------- | ------------------------ | ---------------- | --------------:| ---------------:| --------------:| ---------------:| --------------:| ------------:| ---------- | ------------------------- | ----------------------- | ----------------- | ----------- | ------------ | ------- | ------- | ------- | ---------------------- | --------------------------- | --------------------- | ----- |
| ISO-INC-YYYY-0001 | INC-YYYY-#### |                   |          |                          |                  |                |                 |                |                 |                |              | C/I/A      |                           |                         |                   |             |              |         |         |         |                        |                             |                       |       |

---

# 9. Field Completion Guidance (Quality Rules)

## 9.1 Severity and Category

- Must match severity matrix and incident category master list.
- If severity changed, reflect final severity and ensure ticket contains justification.

References:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/`  
`01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/`

## 9.2 Root Cause Status

Use one of:

- `RCA not required (P3/P4)`
- `RCA in progress`
- `RCA completed`
- `Root cause unknown (document limitations)`

## 9.3 Evidence References

Evidence references should point to:

- evidence package root path/ID
- key artifact IDs (SIEM export ref, EDR ref)
- CoC references when evidence-grade

Do not paste raw evidence into the register.

## 9.4 Corrective Actions

- Must reference action tracker IDs or improvement registers
- Include closure status if tracked elsewhere

References:
`08_POST-INCIDENT/08.3_Improvement-Tracking/`

---

# 10. Review and Audit Process

## 10.1 Quarterly Review (Mandatory)

ISMS Manager must:

- sample entries for completeness
- validate linkage to tickets and evidence references
- validate PIR/RCA references for P1/P2
- identify missing corrective actions and assign owners
- log review completion and any corrections

## 10.2 Audit Response Usage

For audits:

- provide requested log extract for the audit period
- provide evidence package references (not raw evidence unless requested/approved)
- ensure MSSP client confidentiality is maintained

Reference:
`07_REPORTING/07.4_Regulatory-Reports/Audit-Evidence-Package.md`

---

# 11. MSSP Considerations (If Applicable)

- Client incidents may be logged in client-specific registers.
- This ISO log should contain only:
  - sanitized references,
  - ticket IDs,
  - high-level categories and outcomes,
  - evidence package references (tenant-scoped).
- No cross-client information is permitted.

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 12. Related Documents

| Document                       | Path                                                                                              |
| ------------------------------ | ------------------------------------------------------------------------------------------------- |
| ISO Incident Notification SOP  | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/ISO27001-Incident-Notification.md` |
| IR Policy ISO Alignment        | `00_GOVERNANCE/00.1_Policies/IR-Policy-ISO27001-Alignment.md`                                     |
| Audit Evidence Package         | `07_REPORTING/07.4_Regulatory-Reports/Audit-Evidence-Package.md`                                  |
| Final Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`                            |
| Lessons Learned Template       | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`                               |
| RCA Template                   | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`                                       |
| Evidence Storage Policy        | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`               |

---

# 13. Revision History

| Version | Date        | Author                         | Changes         |
| ------- | ----------- | ------------------------------ | --------------- |
| 1.0     | 30-May-2026 | ISMS Manager / Compliance Lead | Initial version |

---

# 14. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
