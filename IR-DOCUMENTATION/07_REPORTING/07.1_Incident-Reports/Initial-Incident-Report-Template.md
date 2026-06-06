# Initial Incident Report Template

---

# 1. Document Control

| Field          | Value                              |
| -------------- | ---------------------------------- |
| Document Name  | Template – Initial Incident Report |
| Document ID    | RPT-INC-002                        |
| Version        | 1.0                                |
| Effective Date | 30-May-2026                        |
| Owner          | SOC Lead / IR Team Lead            |
| Approved By    | SOC Manager                        |
| Classification | Internal – Confidential            |
| Review Cycle   | Quarterly                          |

---

# 2. Purpose

This template standardizes the **Initial Incident Report** produced shortly after an incident is declared/confirmed (typically P1–P3).

An initial report is critical because:

- it provides a consistent baseline record of what is known at the start
- it supports rapid stakeholder alignment and decision-making
- it reduces confusion by separating confirmed facts from assumptions
- it establishes a time-based narrative for audits and regulatory readiness
- it enables MSSP client reporting with consistent structure and evidence references

This template ensures:

- minimum required fields are captured early
- timelines are documented in UTC
- scope and impact are clearly stated (even if “unknown”)
- early containment plan and decision requests are recorded
- evidence references are traceable without exposing sensitive artifacts

---

# 3. Scope

Use this template when:

- incident is confirmed or strongly suspected (P1–P3)
- P2/P3 requires management or client notification
- incident is likely to require regulatory assessment (CERT-In/RBI)

Not intended for:

- final RCA and lessons learned (use Final Incident Report template)
- deep technical analysis (use Technical Deep Dive template)

---

# 4. Instructions (Mandatory)

- Use UTC timestamps.
- Include only verified facts in “Confirmed” sections.
- Label assumptions as “suspected” or “under investigation”.
- Do not embed sensitive evidence (PII/credentials/PCAP) in report body.
- Provide evidence references (IDs/paths) to secure evidence repository.
- For MSSP: confirm client/tenant; ensure tenant-segregated evidence references.

---

# 5. Template (Copy/Paste)

## 5.1 Report Header (Mandatory)

| Field                         | Value                                  |
| ----------------------------- | -------------------------------------- |
| Incident ID / Ticket ID       | `INC-YYYY-####`                        |
| Report Type                   | Initial                                |
| Severity                      | P1 / P2 / P3 / P4                      |
| Incident Category             | `...`                                  |
| Client/Tenant (if applicable) | `Client ID / Name`                     |
| Report Date/Time (UTC)        | `YYYY-MM-DD HH:MM`                     |
| Prepared By                   | `Name / Role`                          |
| Reviewed By                   | `Name / Role`                          |
| Approved By                   | `Name / Role`                          |
| Bridge Call                   | Active / Not Active + link (if active) |
| War Room Channel              | Link / reference                       |

---

## 5.2 Executive Summary (Mandatory)

> Use the Executive Summary template if needed; keep this section short.

- **What happened (confirmed):** `...`
- **Current status:** `Triage / Investigation / Containment / Recovery`
- **Impact (current):** `...`
- **Immediate next steps:** `...`
- **Decisions required (if any):** `...`

Reference:
`07_REPORTING/07.1_Incident-Reports/Executive-Summary-Template.md`

---

## 5.3 Incident Overview (Mandatory)

### A) Detection and Noticing

| Field                        | Value                           |
| ---------------------------- | ------------------------------- |
| Noticing time (UTC)          | `YYYY-MM-DD HH:MM`              |
| Detection time (UTC)         | `YYYY-MM-DD HH:MM`              |
| Incident declared time (UTC) | `YYYY-MM-DD HH:MM`              |
| Detection source             | SIEM / EDR / User / Client / TI |
| Triggering alert/rule        | Rule name + ID                  |
| Reported by                  | Name/team (if user/client)      |

### B) Incident Category and Classification

- **Category:** `...`
- **Severity:** `P?`
- **Rationale:** `Why severity assigned`

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

## 5.4 Scope (Best Known at This Time) (Mandatory)

### A) Affected Entities

| Entity Type                  | Details                  |
| ---------------------------- | ------------------------ |
| Hosts/systems                | `List + count`           |
| Users/accounts               | `List + count`           |
| Privileged accounts involved | Yes/No/Unknown + details |
| Applications/services        | `...`                    |
| Network segments             | `...`                    |
| Cloud tenants/subscriptions  | `...`                    |

### B) Spread and Persistence Indicators

- **Spread suspected:** Yes/No/Unknown  
- **Persistence suspected:** Yes/No/Unknown  
- **Lateral movement suspected:** Yes/No/Unknown  
- **Exfiltration suspected:** Yes/No/Unknown  

---

## 5.5 Business Impact (Current) (Mandatory)

| Impact Area                   | Status                             | Notes |
| ----------------------------- | ---------------------------------- | ----- |
| Service availability          | Normal / Degraded / Down / Unknown |       |
| Customer impact               | Yes / No / Unknown                 |       |
| Data exposure risk            | High / Medium / Low / Unknown      |       |
| Financial impact              | Unknown / Estimated                |       |
| Compliance/regulatory concern | Yes / No / Under assessment        |       |

---

## 5.6 Confirmed Facts vs Suspected (Mandatory)

### A) Confirmed Facts

- `Fact 1…`
- `Fact 2…`

### B) Suspected / Under Investigation

- `Hypothesis 1…`
- `Hypothesis 2…`

### C) Key Unknowns

- `Unknown 1…`
- `Unknown 2…`

---

## 5.7 Evidence Summary (High-Level) (Mandatory)

> Reference evidence IDs/paths; do not paste raw logs.

| Evidence Type                  | Reference | Notes         |
| ------------------------------ | --------- | ------------- |
| SIEM export/query              | `...`     | Time window   |
| EDR detection/timeline         | `...`     | Hosts         |
| Network logs/PCAP              | `...`     | Destinations  |
| Identity logs                  | `...`     | Accounts      |
| Cloud audit logs               | `...`     | Tenant        |
| Email evidence (if applicable) | `...`     | Message trace |

References:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

## 5.8 Actions Taken (So Far) (Mandatory)

> Include executor, authorizer, time (UTC), and outcome.

| Action | Type (Containment/Investigation) | Executed By | Authorized By | Time (UTC) | Outcome |
| ------ | -------------------------------- | ----------- | ------------- | ----------:| ------- |
|        |                                  |             |               |            |         |
|        |                                  |             |               |            |         |

---

## 5.9 Immediate Response Plan (Next 1–4 Hours) (Mandatory)

### A) Investigation Tasks

| Task | Owner | Due (UTC) | Notes |
| ---- | ----- | ---------:| ----- |
|      |       |           |       |

### B) Containment Candidate Actions (If Needed)

| Action | Scope | Approval Required      | Owner | Needed By (UTC) |
| ------ | ----- | ---------------------- | ----- | ---------------:|
|        |       | Yes/No + approver role |       |                 |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 5.10 Decisions Required (If Any) (Mandatory If Applicable)

| Decision Needed | Why | Options | Recommended | Needed By (UTC) | Decision Owner |
| --------------- | --- | ------- | ----------- | ---------------:| -------------- |
|                 |     |         |             |                 |                |

---

## 5.11 Notifications and Escalations (Mandatory)

| Stakeholder        | Notified?               | Time (UTC) | Method | Notes |
| ------------------ | ----------------------- | ----------:| ------ | ----- |
| SOC Lead           |                         |            |        |       |
| IR Team Lead       |                         |            |        |       |
| SOC Manager / CISO |                         |            |        |       |
| Compliance / Legal |                         |            |        |       |
| Client (MSSP)      |                         |            |        |       |
| CERT-In assessed   | Yes/No/Under assessment |            |        |       |
| RBI assessed       | Yes/No/Under assessment |            |        |       |

References:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 5.12 Next Update Commitment (Mandatory)

- **Next status update by (UTC):** `YYYY-MM-DD HH:MM`
- **Update cadence:**  
  - P1: every 30 minutes minimum  
  - P2: every 60 minutes minimum  
  - P3: milestone updates  

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

---

# 6. Related Documents

| Document                       | Path                                                                                          |
| ------------------------------ | --------------------------------------------------------------------------------------------- |
| Executive Summary Template     | `07_REPORTING/07.1_Incident-Reports/Executive-Summary-Template.md`                            |
| Interim Status Report Template | `07_REPORTING/07.1_Incident-Reports/Interim-Status-Report-Template.md`                        |
| Final Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`                        |
| Technical Deep Dive Template   | `07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`                          |
| Ticket Lifecycle SOP           | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`                              |
| Evidence Collection SOP        | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`        |
| CERT-In Reporting SOP          | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`      |
| RBI Incident Reporting SOP     | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md` |

---

# 7. Revision History

| Version | Date        | Author                  | Changes         |
| ------- | ----------- | ----------------------- | --------------- |
| 1.0     | 30-May-2026 | SOC Lead / IR Team Lead | Initial version |

---

# 8. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
