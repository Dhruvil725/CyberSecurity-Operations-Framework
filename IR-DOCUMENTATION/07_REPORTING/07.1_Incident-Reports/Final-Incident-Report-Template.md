# Final Incident Report Template

---

# 1. Document Control

| Field          | Value                                                     |
| -------------- | --------------------------------------------------------- |
| Document Name  | Template – Final Incident Report                          |
| Document ID    | RPT-INC-004                                               |
| Version        | 1.0                                                       |
| Effective Date | 30-May-2026                                               |
| Owner          | IR Team Lead / SOC Manager                                |
| Approved By    | CISO                                                      |
| Classification | Internal – Confidential (Client version: as per contract) |
| Review Cycle   | Quarterly                                                 |

---

# 2. Purpose

This template standardizes the **Final Incident Report** produced at incident closure to document:

- what happened and why (root cause),
- the full scope and impact,
- response actions (containment → eradication → recovery),
- evidence references and validation steps,
- regulatory/client notifications,
- lessons learned and improvement actions.

Final incident reports are critical because:

- they serve as the official incident record for audits, inspections, and internal governance
- they support regulatory reporting and client contractual reporting obligations
- they capture learning and drive corrective actions and detection improvements
- they provide an accountable timeline of decisions and actions
- they support insurance, legal, and third-party assessments when required

This template ensures:

- consistent structure across incidents
- audit-ready traceability to tickets and evidence packages
- clear separation of facts, assumptions, and conclusions
- actionable remediation and improvement tracking

---

# 3. Scope

Use this template for:

| Scenario              | Requirement                                                 |
| --------------------- | ----------------------------------------------------------- |
| P1 incidents          | Mandatory                                                   |
| P2 incidents          | Mandatory                                                   |
| P3 incidents          | Required when confirmed TP or client/regulatory needs       |
| P4 incidents          | Optional (unless client requires)                           |
| MSSP client incidents | Required per client contract/SLA and reporting expectations |

Not intended for:

- purely informational tickets with no incident declaration (use ticket closure summary)

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md`

---

# 4. Instructions (Mandatory)

- Use UTC timestamps for all times.
- Provide evidence references (IDs/paths), not raw sensitive data.
- Clearly label:
  - **Confirmed**
  - **Suspected**
  - **Unknown (not determined)**
- If a “client report” is required, produce a sanitized tenant-scoped version.
- Ensure all post-incident actions are tracked with owners and due dates.

---

# 5. Template (Copy/Paste)

## 5.1 Report Header (Mandatory)

| Field                         | Value                         |
| ----------------------------- | ----------------------------- |
| Incident ID / Ticket ID       | `INC-YYYY-####`               |
| Incident Category             | `...`                         |
| Severity (Final)              | P1 / P2 / P3 / P4             |
| Client/Tenant (if applicable) | `Client ID / Name`            |
| Report Date (UTC)             | `YYYY-MM-DD HH:MM`            |
| Incident Commander            | `Name / Role`                 |
| Report Owner                  | `Name / Role`                 |
| Reviewed By                   | `Name / Role`                 |
| Approved By                   | `Name / Role`                 |
| Classification                | Internal – Confidential       |
| Related Tickets               | `CHG-... / PIR-... / RCA-...` |

---

## 5.2 Executive Summary (Mandatory)

> Use Executive Summary template; include high-level outcomes and impact.

Reference:
`07_REPORTING/07.1_Incident-Reports/Executive-Summary-Template.md`

---

## 5.3 Incident Overview (Mandatory)

### A) What Happened (Narrative)

- `1–2 paragraphs describing incident in plain language`

### B) Detection and Declaration

| Field                   | Value                           |
| ----------------------- | ------------------------------- |
| Noticing time (UTC)     |                                 |
| Detection time (UTC)    |                                 |
| Incident declared (UTC) |                                 |
| Initial severity        |                                 |
| Final severity          |                                 |
| Detection sources       | SIEM / EDR / User / Client / TI |

### C) Incident Category and Type

- `Category: ...`
- `Type: ... (e.g., ransomware variant, phishing/BEC, intrusion)`

---

## 5.4 Timeline of Events (UTC) (Mandatory)

> Provide a chronological timeline of key events and actions.

| Time (UTC) | Event | Source / Evidence Ref | Notes |
| ----------:| ----- | --------------------- | ----- |
|            |       |                       |       |
|            |       |                       |       |

Include, at minimum:

- first observed suspicious activity (if known)
- detection and escalation events
- containment actions and approvals
- eradication actions
- recovery milestones
- key communications (management/client/regulator)
- incident closure

---

## 5.5 Scope and Impact (Final) (Mandatory)

### A) Affected Scope

| Scope Element                | Final Determination |
| ---------------------------- | ------------------- |
| Hosts/systems impacted       |                     |
| Users/accounts impacted      |                     |
| Privileged accounts impacted | Yes/No + details    |
| Services impacted            |                     |
| Network segments impacted    |                     |
| Cloud resources impacted     |                     |

### B) CIA Impact Assessment

| Dimension       | Impact                       | Details |
| --------------- | ---------------------------- | ------- |
| Confidentiality | None / Suspected / Confirmed |         |
| Integrity       | None / Suspected / Confirmed |         |
| Availability    | None / Degraded / Outage     |         |

### C) Data Impact (If Applicable)

| Item                           | Status                                        | Details |
| ------------------------------ | --------------------------------------------- | ------- |
| Data exposure                  | Suspected / Confirmed / No evidence / Unknown |         |
| Data types                     | PII / Financial / Credentials / IP / Other    |         |
| Volume/records                 | Known / Estimated / Unknown                   |         |
| Exfiltration method            | Known / Suspected / Unknown                   |         |
| Evidence supporting conclusion | Evidence IDs/paths                            |         |

### D) Business Impact Summary

- `Customer impact details`
- `Operational impact details`
- `Financial/reputational impact assessment`

---

## 5.6 Root Cause Analysis (Mandatory)

### A) Root Cause (Final)

- `Root cause statement`

### B) Contributing Factors

- `Contributing factor 1`
- `Contributing factor 2`

### C) Entry Vector (Initial Access)

- **Confirmed:** `...`  
- **If not confirmed:** `Best hypothesis + rationale`

### D) Kill Chain Summary (High Level)

- `Initial access → execution → persistence → lateral movement → exfiltration/impact`

Reference:
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`

---

## 5.7 Technical Summary (High Level) (Mandatory)

> Link to Technical Deep Dive if detailed technical analysis exists.

- **Key TTPs observed:** `...`
- **Key IOCs (sanitized list or reference):** `...`
- **Malware/tools used (if confirmed):** `...`
- **Systems used for lateral movement (if confirmed):** `...`
- **Detection gaps encountered:** `...`

Reference:
`07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`

---

## 5.8 Response Actions (Mandatory)

### A) Containment Actions

| Action | Scope | Executed By | Authorized By | Time (UTC) | Outcome |
| ------ | ----- | ----------- | ------------- | ----------:| ------- |
|        |       |             |               |            |         |

### B) Eradication Actions

| Action | Scope | Owner | Time (UTC) | Outcome |
| ------ | ----- | -----:| ----------:| ------- |
|        |       |       |            |         |

### C) Recovery Actions

| Action | Scope | Owner | Time (UTC) | Outcome |
| ------ | ----- | -----:| ----------:| ------- |
|        |       |       |            |         |

### D) Validation Performed (Why We Closed)

- `Validation step 1`
- `Validation step 2`
- `Validation step 3`

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md`

---

## 5.9 Evidence Summary and References (Mandatory)

> Provide references only; no raw evidence embedded.

| Evidence Type     | Evidence ID / Path | Hash (SHA256 if applicable) | Notes |
| ----------------- | ------------------ | --------------------------- | ----- |
| SIEM exports      |                    |                             |       |
| EDR telemetry     |                    |                             |       |
| Network logs/PCAP |                    |                             |       |
| Disk image        |                    |                             |       |
| Memory dump       |                    |                             |       |
| CoC forms         |                    |                             |       |

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`

---

## 5.10 Communications and Escalations (Mandatory)

| Communication              | Completed?             | Time (UTC) | Owner | Notes/Reference |
| -------------------------- | ---------------------- | ----------:| ----- | --------------- |
| P1/P2 bridge call          |                        |            |       |                 |
| Management notification    |                        |            |       |                 |
| Client notification (MSSP) |                        |            |       |                 |
| Legal counsel engaged      |                        |            |       |                 |
| CERT-In reporting          | Submitted/Not required |            |       |                 |
| RBI reporting              | Submitted/Not required |            |       |                 |
| Law enforcement            | Yes/No                 |            |       |                 |
| Vendor engagement          | Yes/No                 |            |       |                 |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`  
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

---

## 5.11 Lessons Learned (Mandatory for P1/P2)

### A) What Went Well

- `...`

### B) What Did Not Go Well

- `...`

### C) Improvements Identified

- `...`

Reference:
`08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`

---

## 5.12 Corrective and Preventive Actions (CAPA) / Improvement Plan (Mandatory)

> All actions must be assigned, time-bound, and tracked.

| Action Item | Category (Prevent/Detect/Respond/Recover) | Owner | Due Date (UTC) | Tracking Ref | Status |
| ----------- | ----------------------------------------- | ----- | --------------:| ------------ | ------ |
|             |                                           |       |                |              |        |
|             |                                           |       |                |              |        |

References:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`  
`08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`

---

## 5.13 Appendix (Optional)

- IoC appendix (sanitized)
- Screenshots (sanitized)
- Query appendix (SIEM queries used)
- External correspondence references

---

# 6. Related Documents

| Document                         | Path                                                                                |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| Executive Summary Template       | `07_REPORTING/07.1_Incident-Reports/Executive-Summary-Template.md`                  |
| Initial Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Initial-Incident-Report-Template.md`            |
| Interim Status Report Template   | `07_REPORTING/07.1_Incident-Reports/Interim-Status-Report-Template.md`              |
| Technical Deep Dive Template     | `07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`                |
| Lessons Learned Template         | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`                 |
| RCA Template                     | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`                         |
| Evidence Storage Policy          | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| CoC Master Form                  | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`         |
| Ticket Closure Criteria          | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md`                 |

---

# 7. Revision History

| Version | Date        | Author                     | Changes         |
| ------- | ----------- | -------------------------- | --------------- |
| 1.0     | 30-May-2026 | IR Team Lead / SOC Manager | Initial version |

---

# 8. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
