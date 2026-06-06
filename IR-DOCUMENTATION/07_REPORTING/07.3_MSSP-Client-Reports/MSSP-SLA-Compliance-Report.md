# MSSP SLA Compliance Report

---

# 1. Document Control

| Field          | Value                                                     |
| -------------- | --------------------------------------------------------- |
| Document Name  | Template – MSSP SLA Compliance Report                     |
| Document ID    | RPT-MSSP-004                                              |
| Version        | 1.0                                                       |
| Effective Date | 30-May-2026                                               |
| Owner          | MSSP Service Delivery Manager (SDM) / SOC Operations Lead |
| Approved By    | SOC Manager                                               |
| Classification | Client Confidential                                       |
| Review Cycle   | Quarterly                                                 |

---

# 2. Purpose

This report template standardizes how the MSSP measures and reports **SLA compliance** to clients, including:

- SLA definitions and scope for the reporting window,
- compliance results by severity and metric,
- exceptions and root causes for breaches,
- corrective and preventive actions (CAPA),
- client dependencies impacting SLA outcomes (e.g., approval delays, access gaps).

SLA compliance reporting is critical because:

- SLAs are contractual obligations that drive trust, renewals, and governance
- consistent SLA metrics prevent disputes and reduce ambiguity
- clear exception handling supports fairness and transparency (MSSP vs client responsibilities)
- breach analysis drives continuous improvement and operational maturity
- audit and assurance reviews often require evidence of SLA governance

This template ensures:

- consistent SLA measurement methodology
- traceable linkage to tickets, timestamps, and notification records
- clear distinction between MSSP-controlled vs client-controlled delays
- action-oriented improvement planning

---

# 3. Scope

This SLA compliance report applies to a single client and covers:

| SLA Area                  | Examples                                                |
| ------------------------- | ------------------------------------------------------- |
| Notification SLAs         | P1/P2 initial notification time                         |
| Response SLAs             | time to acknowledge/triage                              |
| Update cadence            | 30-min P1 updates, 1-hr P2 updates (if contract states) |
| Escalation                | acknowledgment of escalation to L2/L3/IR                |
| Closure/Resolution        | time to resolve/close (if defined)                      |
| Service availability SLAs | MSSP platform uptime (if included in contract)          |

Out of scope:

- technical incident analysis (covered in incident report template)
- SOC operational metrics unrelated to client SLA

References:  
`00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

# 4. Instructions (Mandatory)

- Use UTC timestamps and define reporting window clearly.
- Pull SLA calculations from authoritative sources (ticketing system timestamps).
- Explicitly define:
  - which SLAs are measured,
  - the calculation method, and
  - what constitutes “met” vs “breach”.
- For each breach, document:
  - cause,
  - responsibility (MSSP/client/external),
  - corrective action and due date.
- Keep incident detail minimal; use incident IDs for reference.

---

# 5. Template (Copy/Paste)

## 5.1 Report Metadata (Mandatory)

| Field                         | Value                                               |
| ----------------------------- | --------------------------------------------------- |
| Client Name                   |                                                     |
| Client ID                     |                                                     |
| SLA Tier / Contract Reference |                                                     |
| Reporting Period (UTC)        | `Start: YYYY-MM-DD 00:00` → `End: YYYY-MM-DD 23:59` |
| Prepared By                   | Name / Role                                         |
| Reviewed By                   | Name / Role                                         |
| Approved By                   | Name / Role                                         |
| Delivery Date (UTC)           | `YYYY-MM-DD HH:MM`                                  |
| Version                       | 1.0                                                 |

---

## 5.2 SLA Definitions in Scope (Mandatory)

> List only SLAs applicable to the client contract.

| SLA Metric                | Definition (Client Contract)                              | Target | Applies to (P1/P2/P3/P4) | Data Source                   |
| ------------------------- | --------------------------------------------------------- | ------:| ------------------------ | ----------------------------- |
| Initial notification      | Time from detection/noticing to client notification       |        | P1/P2                    | Ticket timestamps + comms log |
| Acknowledgment            | Time from ticket creation to first analyst acknowledgment |        | P1–P4                    | Ticket timestamps             |
| Initial triage            | Time from ticket creation to triage completion            |        | P1–P4                    | Ticket timestamps             |
| Update cadence            | Frequency of updates during active incident               |        | P1/P2                    | Ticket updates                |
| Escalation acknowledgment | Time from escalation to L2/L3/IR acknowledgment           |        | P1–P3                    | Ticket timestamps             |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

## 5.3 Executive SLA Summary (Mandatory)

### A) Overall SLA Compliance Status

- **Overall SLA posture:** Green / Amber / Red  
- **Summary (3–6 bullets):**
  - `...`

### B) Compliance Scorecard (High Level)

| Severity | Total Applicable Tickets | SLA Met | SLA Breached | Compliance % |
| -------- | ------------------------:| -------:| ------------:| ------------:|
| P1       |                          |         |              |              |
| P2       |                          |         |              |              |
| P3       |                          |         |              |              |
| P4       |                          |         |              |              |
| Total    |                          |         |              |              |

---

## 5.4 SLA Performance by Metric (Mandatory)

> Provide compliance for each SLA metric.

### A) Initial Notification SLA

| Severity | Applicable Cases | Met | Breached | Compliance % | Notes |
| -------- | ----------------:| ---:| --------:| ------------:| ----- |
| P1       |                  |     |          |              |       |
| P2       |                  |     |          |              |       |

### B) Ticket Acknowledgment SLA

| Severity | Applicable Tickets | Met | Breached | Compliance % | Notes |
| -------- | ------------------:| ---:| --------:| ------------:| ----- |
| P1       |                    |     |          |              |       |
| P2       |                    |     |          |              |       |
| P3       |                    |     |          |              |       |
| P4       |                    |     |          |              |       |

### C) Initial Triage SLA

| Severity | Applicable Tickets | Met | Breached | Compliance % | Notes |
| -------- | ------------------:| ---:| --------:| ------------:| ----- |
| P1       |                    |     |          |              |       |
| P2       |                    |     |          |              |       |
| P3       |                    |     |          |              |       |
| P4       |                    |     |          |              |       |

### D) Update Cadence SLA (P1/P2)

| Severity | Applicable Incidents | Met | Breached | Compliance % | Notes |
| -------- | --------------------:| ---:| --------:| ------------:| ----- |
| P1       |                      |     |          |              |       |
| P2       |                      |     |          |              |       |

### E) Escalation Acknowledgment SLA

| Escalation Type | Applicable | Met | Breached | Compliance % | Notes |
| --------------- | ----------:| ---:| --------:| ------------:| ----- |
| L1 → L2         |            |     |          |              |       |
| L2 → L3         |            |     |          |              |       |
| L3 → IR         |            |     |          |              |       |

---

## 5.5 SLA Breach Register (Mandatory if Any Breaches)

> Each breach must have a clear cause and corrective action.

| Breach ID | Incident/Ticket ID | Severity | SLA Metric   | Target | Actual | Breach Duration | Root Cause | Responsibility (MSSP/Client/External) | Corrective Action | Owner | Due (UTC) | Status |
| --------- | ------------------ | -------- | ------------ | ------:| ------:| ---------------:| ---------- | ------------------------------------- | ----------------- | ----- | ---------:| ------ |
| SLA-      | INC-               | P1       | Notification |        |        |                 |            |                                       |                   |       |           |        |

---

## 5.6 Breach Root Cause Themes (Recommended)

| Theme                     | Count | Examples | Notes |
| ------------------------- | -----:| -------- | ----- |
| Client approval delay     |       | INC-     |       |
| Missing access/telemetry  |       | INC-     |       |
| Tool outage               |       | INC-     |       |
| Staffing/coverage         |       | INC-     |       |
| Process/documentation gap |       | INC-     |       |

---

## 5.7 Client Dependencies and Shared Responsibilities (Mandatory)

> Record client-side dependencies that impact SLA outcomes.

| Dependency             | Description                                   | Impacted Incidents | Mitigation Proposal                     | Client Owner |
| ---------------------- | --------------------------------------------- | ------------------ | --------------------------------------- | ------------ |
| Approval delays        | Client response time for containment approval | INC-               | Define pre-approved containment actions |              |
| Log access             | Missing admin access to export logs           | INC-               | Provide read-only access or automation  |              |
| Asset criticality tags | Missing asset criticality mapping             | INC-               | Update asset register                   |              |

Reference:
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`

---

## 5.8 Corrective and Preventive Actions (CAPA) (Mandatory)

| Action                               | Type (Corrective/Preventive) | Owner (MSSP/Client) | Priority | Due (UTC) | Tracking Ref | Status |
| ------------------------------------ | ---------------------------- | ------------------- | -------- | ---------:| ------------ | ------ |
| Improve escalation paging            | Preventive                   | MSSP                | High     |           |              |        |
| Define pre-approved isolation for P1 | Preventive                   | Client              | High     |           |              |        |

---

## 5.9 Methodology and Assumptions (Mandatory)

### A) Time Source and Calculations

- **Time standard:** UTC
- **Primary data source:** Ticketing system timestamps (creation, acknowledgment, escalation, closure)
- **Notification timestamps source:** Ticket communications log + email/phone record (as documented)

### B) Inclusion/Exclusion Rules

- Tickets excluded: `...` (e.g., duplicates, cancelled)
- SLA pause rules (if any): `...` (e.g., awaiting client approval)  
  
  > If SLA pauses are contract-defined, document exact pause conditions.

### C) Data Limitations (If Any)

- `Example: missing comms timestamps for X tickets; corrective action created`

---

# 6. Confidentiality and Distribution (Mandatory)

- This report is **Client Confidential**.
- Distribution must be limited to client-approved recipients.
- Report content must not include any other client information.

---

# 7. Related Documents

| Document                        | Path                                                                                   |
| ------------------------------- | -------------------------------------------------------------------------------------- |
| MSSP Monthly Client Report      | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Monthly-Client-Report.md`                  |
| MSSP Incident Report Template   | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Incident-Report-Template.md`               |
| Internal-to-MSSP Escalation SOP | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md` |
| Ticket Fields Standards         | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`                    |
| Ticket Lifecycle SOP            | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`                       |
| MSSP Responsibility Matrix      | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`   |
| MSSP Client SLA Template        | `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`                           |

---

# 8. Revision History

| Version | Date        | Author                         | Changes         |
| ------- | ----------- | ------------------------------ | --------------- |
| 1.0     | 30-May-2026 | MSSP SDM / SOC Operations Lead | Initial version |

---

# 9. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
