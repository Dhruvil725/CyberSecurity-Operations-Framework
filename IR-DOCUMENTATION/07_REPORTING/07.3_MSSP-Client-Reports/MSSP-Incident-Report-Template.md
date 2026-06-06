# MSSP Incident Report Template (Client-Facing)

---

# 1. Document Control

| Field          | Value                                              |
| -------------- | -------------------------------------------------- |
| Document Name  | Template – MSSP Incident Report                    |
| Document ID    | RPT-MSSP-002                                       |
| Version        | 1.0                                                |
| Effective Date | 30-May-2026                                        |
| Owner          | MSSP Service Delivery Manager (SDM) / IR Team Lead |
| Approved By    | SOC Manager                                        |
| Classification | Client Confidential                                |
| Review Cycle   | Quarterly                                          |

---

# 2. Purpose

This template standardizes the **client-facing incident report** provided by the MSSP to a client following a security incident.

This report is critical because:

- it is the client’s primary written record of what happened and how it was handled
- client audit and regulatory requests often require a structured incident report
- it documents evidence references, actions taken, and validation steps in a consumable format
- it helps the client understand root cause, impact, and required remediation
- it supports contractual requirements and SLA transparency

This template ensures:

- tenant-safe, client-specific reporting with no cross-client disclosure
- consistent structure and completeness across incidents
- clear distinction between confirmed facts and assumptions
- linkage to evidence references (without exposing raw sensitive artifacts)
- actionable recommendations and follow-up tracking

---

# 3. Scope

Use this template for:

| Incident Severity | When to Use                                 |
| ----------------- | ------------------------------------------- |
| P1                | Mandatory                                   |
| P2                | Mandatory                                   |
| P3                | Required for confirmed TP or client request |
| P4                | Optional (unless contract requires)         |

Applicable for all incident categories (ransomware, phishing/BEC, malware, intrusion, cloud, etc.).

Not intended for:

- daily status updates (use notification templates)
- internal-only technical deep dives (separate internal report)

---

# 4. Instructions (Mandatory)

- Use UTC timestamps for all events/timelines.
- Do not include sensitive raw evidence (PCAP/memory/disk images) directly in the report body.
- Provide evidence references and summaries; provide raw evidence only through approved secure transfer and with approvals.
- Clearly label:
  - Confirmed
  - Suspected
  - Unknown
- Ensure the report is reviewed for confidentiality and tenant scoping prior to delivery.

---

# 5. Template (Copy/Paste)

## 5.1 Report Header (Mandatory)

| Field                         | Value                                               |
| ----------------------------- | --------------------------------------------------- |
| Client Name                   |                                                     |
| Client ID                     |                                                     |
| Incident ID (MSSP)            | `MSSP-INC-YYYY-####` (or `INC-YYYY-####`)           |
| Incident Category             | `...`                                               |
| Severity (Final)              | P1 / P2 / P3 / P4                                   |
| Report Type                   | Initial / Interim / Final (Client)                  |
| Reporting Window (UTC)        | `Start: YYYY-MM-DD HH:MM` → `End: YYYY-MM-DD HH:MM` |
| Detected At (UTC)             | `YYYY-MM-DD HH:MM`                                  |
| Notified At (UTC)             | `YYYY-MM-DD HH:MM`                                  |
| Report Date (UTC)             | `YYYY-MM-DD HH:MM`                                  |
| MSSP Incident Owner           | Name / Role                                         |
| MSSP Service Delivery Contact | Name / Role                                         |
| Prepared By                   | Name / Role                                         |
| Reviewed By                   | Name / Role                                         |
| Approved By                   | Name / Role                                         |

---

## 5.2 Executive Summary (Client-Friendly) (Mandatory)

### A) What Happened (Confirmed)

- `3–6 bullets`

### B) Impact Summary

- **Service impact:** `None/Limited/Outage/Unknown`
- **Data exposure:** `No evidence / Suspected / Confirmed / Unknown`
- **Business risk:** `Low/Medium/High` + rationale

### C) Current Status

- `Contained / Eradicated / Recovered / Monitoring`

### D) Key Actions Taken

- `Containment actions`
- `Recovery actions`

### E) Client Actions Required

- `...`

---

## 5.3 Incident Overview (Mandatory)

### A) Detection Details

| Field                   | Value                           |
| ----------------------- | ------------------------------- |
| Detection source        | SIEM / EDR / Client report / TI |
| Trigger description     |                                 |
| Initial indicator(s)    | IP/Domain/Hash/Account          |
| Initial affected entity | Host/User/App                   |

### B) Incident Classification

- Category: `...`
- Severity: `P?`
- Rationale: `...`

---

## 5.4 Timeline of Events (UTC) (Mandatory)

| Time (UTC) | Event                 | Notes |
| ----------:| --------------------- | ----- |
|            | Noticing time         |       |
|            | Detection time        |       |
|            | Client notified       |       |
|            | Investigation started |       |
|            | Containment executed  |       |
|            | Containment validated |       |
|            | Eradication executed  |       |
|            | Recovery executed     |       |
|            | Closure               |       |

---

## 5.5 Scope and Impact (Final/Best Known) (Mandatory)

### A) Affected Scope

| Scope Element                | Details                  |
| ---------------------------- | ------------------------ |
| Hosts/systems impacted       | list/count               |
| Users/accounts impacted      | list/count               |
| Privileged accounts involved | Yes/No/Unknown + details |
| Services impacted            |                          |
| Cloud resources impacted     |                          |

### B) Impact (CIA)

| Dimension       | Status                                 | Details |
| --------------- | -------------------------------------- | ------- |
| Confidentiality | None / Suspected / Confirmed / Unknown |         |
| Integrity       | None / Suspected / Confirmed / Unknown |         |
| Availability    | Normal / Degraded / Outage / Unknown   |         |

### C) Data Impact (If Applicable)

- **Data types:** `PII/financial/credentials/other`
- **Exfiltration:** `Confirmed/Suspected/No evidence/Unknown`
- **Evidence summary:** `...`

---

## 5.6 Investigation Summary (Client-Safe Technical Summary) (Mandatory)

### A) Confirmed Findings

- `...`

### B) Suspected / Under Investigation (If Any)

- `...`

### C) IOCs and TTPs (Sanitized)

> Provide minimal necessary list or reference an IOC appendix.

- IPs: `...`
- Domains/URLs: `...`
- Hashes (SHA256): `...`
- Observed behaviors: `...`

---

## 5.7 Actions Taken by MSSP (Mandatory)

### A) Containment Actions

| Action | Scope | Time (UTC) | Outcome | Client Approval Required? |
| ------ | ----- | ----------:| ------- | ------------------------- |
|        |       |            |         | Yes/No                    |

### B) Eradication Actions

| Action | Scope | Time (UTC) | Outcome |
| ------ | ----- | ----------:| ------- |
|        |       |            |         |

### C) Recovery Actions

| Action | Scope | Time (UTC) | Outcome |
| ------ | ----- | ----------:| ------- |
|        |       |            |         |

### D) Validation Performed

- `What was checked and why it supports closure/containment success`

---

## 5.8 Client Communications and SLA (Mandatory)

### A) Notification Summary

| Communication        | Time (UTC) | Method | Recipient | Notes |
| -------------------- | ----------:| ------ | --------- | ----- |
| Initial notification |            |        |           |       |
| Status updates       |            |        |           |       |
| Closure notification |            |        |           |       |

### B) SLA Performance Summary

| SLA Metric                       | Target | Achieved | Notes |
| -------------------------------- | ------:| --------:| ----- |
| Acknowledgment time              |        |          |       |
| Notification time                |        |          |       |
| Update cadence                   |        |          |       |
| Resolution time (if contractual) |        |          |       |

---

## 5.9 Evidence Summary (Client-Safe References) (Mandatory)

> Provide references, not raw evidence in report body.

| Evidence Type  | Reference ID/Path | Notes |
| -------------- | ----------------- | ----- |
| SIEM exports   |                   |       |
| EDR telemetry  |                   |       |
| Network logs   |                   |       |
| Email evidence |                   |       |

If client requests raw evidence:

- ensure secure transfer method
- document approval and transfer record
- include hash manifest if evidence-grade

References:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md`

---

## 5.10 Root Cause (If Known) and Contributing Factors (Recommended)

### A) Root Cause

- `Confirmed root cause` OR `RCA in progress`

### B) Contributing Factors

- `...`

---

## 5.11 Recommendations and Client Required Remediation (Mandatory)

> Must be actionable, owned, and time-bound.

| Recommendation | Priority     | Owner (Client/MSSP) | Due (UTC) | Notes |
| -------------- | ------------ | ------------------- | ---------:| ----- |
|                | High/Med/Low |                     |           |       |
|                |              |                     |           |       |

---

## 5.12 Follow-Up Tracking (Mandatory for P1/P2)

| Follow-Up Item          | Owner | Due (UTC) | Tracking Ref |
| ----------------------- | ----- | ---------:| ------------ |
| RCA completion          |       |           |              |
| Lessons learned meeting |       |           |              |
| Detection improvement   |       |           |              |
| Control remediation     |       |           |              |

---

## 5.13 Closure Statement (Mandatory for Final Report)

This incident is considered **closed** as of **[UTC time]** based on the validation performed above.  
Any future related activity should reference **Incident ID: [MSSP-INC/INC]**.

---

# 6. Distribution and Confidentiality (Mandatory)

- Distribution list must be client-approved.
- This report is Client Confidential.
- Do not forward outside approved recipients.

---

# 7. Related Documents

| Document                         | Path                                                                                      |
| -------------------------------- | ----------------------------------------------------------------------------------------- |
| MSSP Executive Briefing Template | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Executive-Briefing-Template.md`               |
| MSSP Monthly Client Report       | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Monthly-Client-Report.md`                     |
| MSSP SLA Compliance Report       | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-SLA-Compliance-Report.md`                     |
| MSSP Client Evidence Handling    | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md` |
| Internal-to-MSSP Escalation      | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`    |

---

# 8. Revision History

| Version | Date        | Author                  | Changes         |
| ------- | ----------- | ----------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP SDM / IR Team Lead | Initial version |

---

# 9. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
