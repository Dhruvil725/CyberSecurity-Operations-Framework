# Interim Status Report Template (Incident SITREP)

---

# 1. Document Control

| Field          | Value                                     |
| -------------- | ----------------------------------------- |
| Document Name  | Template – Interim Status Report (SITREP) |
| Document ID    | RPT-INC-003                               |
| Version        | 1.0                                       |
| Effective Date | 30-May-2026                               |
| Owner          | SOC Lead / IR Team Lead                   |
| Approved By    | SOC Manager                               |
| Classification | Internal – Confidential                   |
| Review Cycle   | Quarterly                                 |

---

# 2. Purpose

This template standardizes interim **Situation Reports (SITREPs)** used during ongoing incidents (typically P1/P2) to communicate:

- what changed since last report,
- current scope and impact,
- actions completed and planned,
- risks, blockers, and decisions required,
- regulatory/client communication status.

Interim SITREPs are critical because:

- leadership and stakeholders need predictable, consistent updates during crises
- repeated updates form an audit-ready timeline for incident governance
- structured updates reduce confusion and ensure accountability
- MSSP incidents require client-safe, tenant-scoped communications
- incident response effectiveness depends on timely decision-making and approvals

This template ensures:

- consistent update structure across authors and shifts
- clear differentiation of confirmed facts vs suspected items
- alignment to escalation, SLA, and communication cadence requirements

---

# 3. Scope

Use this template for:

| Severity | When Used                                                      |
| -------- | -------------------------------------------------------------- |
| P1       | Mandatory (aligned to 30-minute or hourly cadence as directed) |
| P2       | Mandatory (hourly minimum or as directed)                      |
| P3       | Optional when management/client requires frequent updates      |

Recipients may include:

- SOC/IR and IT operations
- management/CISO
- compliance/legal (as applicable)
- MSSP client contacts (if applicable)

References:  
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-30min.md`  
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-1hr.md`

---

# 4. Instructions (Mandatory)

- Use UTC timestamps.
- Start with “since last update” changes.
- Keep the report factual and decision-oriented.
- Do not paste raw sensitive evidence; reference evidence IDs/paths.
- Ensure SITREP is posted/attached in the incident ticket or linked bridge notes.

---

# 5. Template (Copy/Paste)

## 5.1 SITREP Header (Mandatory)

| Field                         | Value                      |
| ----------------------------- | -------------------------- |
| Incident ID / Ticket ID       | `INC-YYYY-####`            |
| SITREP Number                 | `#N`                       |
| Severity                      | P1 / P2 / P3               |
| Incident Category             | `...`                      |
| Client/Tenant (if applicable) | `Client ID / Name`         |
| SITREP Time (UTC)             | `YYYY-MM-DD HH:MM`         |
| Incident Commander / Owner    | `Name / Role`              |
| Bridge Call                   | Active / Not Active + link |
| War Room Channel              | Link / reference           |
| Prepared By                   | `Name / Role`              |

---

## 5.2 Since Last SITREP (What Changed) (Mandatory)

- `Change 1…`
- `Change 2…`
- `Change 3…`

---

## 5.3 Current Status (Phase) (Mandatory)

- `Triage / Investigation / Containment / Eradication / Recovery / Monitoring`

---

## 5.4 Scope (Best Known at This Time) (Mandatory)

| Scope Element                | Current Understanding    |
| ---------------------------- | ------------------------ |
| Hosts/systems impacted       | `...`                    |
| Users/accounts impacted      | `...`                    |
| Privileged accounts involved | Yes/No/Unknown + details |
| Services impacted            | `...`                    |
| Network segments impacted    | `...`                    |
| Cloud resources impacted     | `...`                    |

Indicators:

- **Spread:** Yes/No/Unknown  
- **Persistence:** Yes/No/Unknown  
- **Exfiltration:** Yes/No/Unknown  

---

## 5.5 Impact (Current) (Mandatory)

| Impact Area                   | Status                             | Notes |
| ----------------------------- | ---------------------------------- | ----- |
| Service availability          | Normal / Degraded / Down / Unknown |       |
| Customer impact               | Yes / No / Unknown                 |       |
| Data exposure risk            | High / Medium / Low / Unknown      |       |
| Financial impact              | Unknown / Estimated                |       |
| Compliance/regulatory concern | Yes / No / Under assessment        |       |

---

## 5.6 Actions Completed (Since Last SITREP) (Mandatory)

> Include time (UTC), executor, authorizer for major actions.

| Action | Type | Executed By | Authorized By | Time (UTC) | Outcome |
| ------ | ---- | ----------- | ------------- | ----------:| ------- |
|        |      |             |               |            |         |
|        |      |             |               |            |         |

---

## 5.7 Investigation Findings (Key Points) (Mandatory)

### A) Confirmed Findings

- `...`
- `...`

### B) Suspected / Under Validation

- `...`
- `...`

### C) Key IOCs/TTPs (As Known)

- `IOCs: ...`
- `TTPs: ...`

---

## 5.8 Evidence References (High-Level) (Mandatory)

| Evidence Type           | Reference | Notes        |
| ----------------------- | --------- | ------------ |
| SIEM exports/queries    | `...`     | Window       |
| EDR detections/timeline | `...`     | Hosts        |
| Network logs/PCAP       | `...`     | Destinations |
| Identity logs           | `...`     | Accounts     |
| Cloud audit logs        | `...`     | Tenant       |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

## 5.9 Current Risks and Blockers (Mandatory)

### A) Risks

- `...`

### B) Blockers

- `...` (e.g., approvals pending, access constraints, missing logs)

---

## 5.10 Decisions Required (Mandatory If Applicable)

| Decision Needed | Why | Needed By (UTC) | Decision Owner | Status |
| --------------- | --- | ---------------:| -------------- | ------ |
|                 |     |                 |                |        |

---

## 5.11 Plan for Next Period (Next 30–60 Minutes / Next Hour) (Mandatory)

| Next Action | Owner | Due (UTC) | Notes |
| ----------- | ----- | ---------:| ----- |
|             |       |           |       |
|             |       |           |       |

---

## 5.12 Communications / Notifications (Mandatory)

| Party                       | Notified? | Time (UTC) | Notes |
| --------------------------- | --------- | ----------:| ----- |
| Management / CISO           |           |            |       |
| Compliance / Legal          |           |            |       |
| MSSP Client (if applicable) |           |            |       |
| CERT-In assessed/submitted  |           |            |       |
| RBI assessed/submitted      |           |            |       |
| Vendor/IR retainer engaged  |           |            |       |

---

## 5.13 Next SITREP Commitment (Mandatory)

- **Next SITREP due (UTC):** `YYYY-MM-DD HH:MM`
- **Cadence:** 30 min (P1) / 60 min (P2) / as directed

---

# 6. Related Documents

| Document                         | Path                                                                                           |
| -------------------------------- | ---------------------------------------------------------------------------------------------- |
| Executive Summary Template       | `07_REPORTING/07.1_Incident-Reports/Executive-Summary-Template.md`                             |
| Initial Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Initial-Incident-Report-Template.md`                       |
| Final Incident Report Template   | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`                         |
| Status Update Template (30 min)  | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-30min.md` |
| Status Update Template (1 hr)    | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-1hr.md`   |
| Evidence Collection SOP          | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`         |
| Ticket Lifecycle SOP             | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`                               |

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
