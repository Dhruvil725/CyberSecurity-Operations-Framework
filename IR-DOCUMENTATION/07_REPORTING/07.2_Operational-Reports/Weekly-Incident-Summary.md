# Weekly Incident Summary

---

# 1. Document Control

| Field          | Value                              |
| -------------- | ---------------------------------- |
| Document Name  | Template – Weekly Incident Summary |
| Document ID    | RPT-OPS-002                        |
| Version        | 1.0                                |
| Effective Date | 30-May-2026                        |
| Owner          | SOC Manager / SOC Operations Lead  |
| Approved By    | CISO (or SOC Manager – delegated)  |
| Classification | Internal – Confidential            |
| Review Cycle   | Quarterly                          |

---

# 2. Purpose

This template standardizes the **Weekly Incident Summary** report used to provide leadership with a concise, decision-oriented view of:

- incident volumes and severity distribution,
- notable incidents and outcomes,
- SLA/SLO performance,
- recurring attack patterns and trends,
- detection/control gaps and improvement actions,
- MSSP client highlights (tenant-safe, when applicable).

Weekly summaries are critical because:

- they connect daily SOC operations to management oversight and risk decisions
- they provide consistent evidence for governance, audit, and ISMS review
- they enable trend-based prioritization of improvements
- they highlight chronic issues (tooling health, backlog, SLA breaches)
- they support client service delivery reviews in MSSP contexts

This template ensures:

- consistent structure and key metrics tracked week-to-week
- actionable management insights (risks, blockers, required decisions)
- traceability to tickets and improvement trackers

---

# 3. Scope

This report covers activity for:

- internal SOC operations and/or MSSP operations (as defined in distribution)
- all incident categories and severities P1–P4
- operational and performance metrics relevant to SOC governance

Out of scope:

- detailed technical incident deep dives (handled in incident reports)
- regulatory reporting content (covered by regulatory SOPs)

---

# 4. Instructions (Mandatory)

- Use UTC for week boundaries and key timestamps.
- Include only tenant-safe summaries for MSSP clients (no cross-client data).
- Report should be concise (recommended 3–6 pages).
- Use incident IDs as references (do not paste raw evidence).
- Ensure action items have owners and due dates.

---

# 5. Template (Copy/Paste)

## 5.1 Report Header (Mandatory)

| Field                     | Value                                           |
| ------------------------- | ----------------------------------------------- |
| Week Number / Range (UTC) | `Week ## – YYYY-MM-DD to YYYY-MM-DD`            |
| Prepared By               | `Name / Role`                                   |
| Reviewed By               | `Name / Role`                                   |
| SOC Coverage              | `24x7 / Business hours`                         |
| MSSP Scope Included       | Yes/No (if yes: list tenants included)          |
| Report Distribution       | `SOC leadership / CISO / Compliance / MSSP SDM` |

---

## 5.2 Executive Highlights (Mandatory)

### A) Summary (Non-Technical, 5–10 bullets)

- `...`
- `...`

### B) Top Risks Identified (Top 3–5)

1. `...`
2. `...`
3. `...`

### C) Decisions Needed from Leadership (If Any)

| Decision Needed | Why | Needed By (UTC) | Owner | Status |
| --------------- | --- | ---------------:| ----- | ------ |
|                 |     |                 |       |        |

---

## 5.3 Incident Volume and Severity Distribution (Mandatory)

### A) Incident Counts (Week)

| Metric                             | P1  | P2  | P3  | P4  | Total |
| ---------------------------------- | ---:| ---:| ---:| ---:| -----:|
| New incidents opened               |     |     |     |     |       |
| Incidents closed                   |     |     |     |     |       |
| Incidents still open (end of week) |     |     |     |     |       |
| Escalations (tier changes)         |     |     |     |     |       |

### B) Incidents by Category (Top 10)

| Category          | Count | % of Total | Notable Notes |
| ----------------- | -----:| ----------:| ------------- |
| Phishing/BEC      |       |            |               |
| Malware           |       |            |               |
| Credential attack |       |            |               |
| Web attack        |       |            |               |
| Cloud incident    |       |            |               |
| Other             |       |            |               |

Reference:
`01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/Category-Master-List.md`

---

## 5.4 Notable Incidents (Mandatory)

> Include all P1/P2 and any significant P3s.

| Incident ID | Severity | Category | Tenant/BU | Status/Outcome           | Impact Summary | Root Cause (if known) | Lessons / Follow-ups |
| ----------- | -------- | -------- | --------- | ------------------------ | -------------- | --------------------- | -------------------- |
| INC-        | P1       |          |           | Closed/Contained/Ongoing |                |                       |                      |
| INC-        | P2       |          |           |                          |                |                       |                      |

For each P1, ensure the final report exists or is scheduled.

Reference:
`07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`

---

## 5.5 SLA/SLO Performance (Mandatory)

### A) SLA Compliance Summary (Week)

| Metric                        | Target | Achieved | Trend vs Last Week | Notes |
| ----------------------------- | ------ | -------- | ------------------ | ----- |
| Ticket creation SLA           |        | Yes/No   | Up/Down/Stable     |       |
| Initial triage SLA            |        | Yes/No   |                    |       |
| Escalation acknowledgment SLA |        | Yes/No   |                    |       |
| P1 update cadence compliance  | 30 min | Yes/No   |                    |       |
| P2 update cadence compliance  | 1 hr   | Yes/No   |                    |       |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

### B) SLA Breaches (If Any) (Mandatory)

| Breach ID | Incident/Ticket | Severity | SLA Type | Breach Duration | Root Cause | Corrective Action |
| --------- | --------------- | -------- | -------- | ---------------:| ---------- | ----------------- |
| SLA-      | INC-            |          |          |                 |            |                   |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLA-Breach-Escalation-Procedure.md`

### C) KPI Summary (Week)

| KPI                  | Value | Target | Trend | Notes |
| -------------------- | -----:| ------:| ----- | ----- |
| MTTA                 |       |        |       |       |
| Mean time to triage  |       |        |       |       |
| MTTR (definition)    |       |        |       |       |
| Backlog (avg)        |       |        |       |       |
| % tickets passing QA |       |        |       |       |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

---

## 5.6 Threat Trends and Attack Patterns (Recommended)

### A) Observed Trends (Week)

- `Trend 1 (e.g., targeted phishing to finance group)`
- `Trend 2 (e.g., credential stuffing against VPN)`
- `Trend 3 (e.g., increased scanning from specific geo/ASN)`

### B) Common TTPs Observed (If Applicable)

| Tactic | Technique | Frequency | Notes |
| ------ | --------- | ---------:| ----- |
|        |           |           |       |

Reference:
`10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`

### C) IOC/TI Highlights (If Applicable)

| Item                   | Source | Action Taken          | Outcome    |
| ---------------------- | ------ | --------------------- | ---------- |
| IOC list updated       | TI     | SIEM watchlist update | Matches:   |
| Threat advisory issued | TI     | Client comms          | Completed: |

References:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Reporting-Template.md`

---

## 5.7 Operational Health (Tooling and Coverage) (Mandatory)

### A) Telemetry and Tool Health Summary

| Component          | Status (OK/Degraded/Down) | Incidents/Impact | Remediation Owner | ETA (UTC) |
| ------------------ | ------------------------- | ---------------- | ----------------- | ---------:|
| SIEM ingestion     |                           |                  |                   |           |
| EDR coverage       |                           |                  |                   |           |
| Ticketing system   |                           |                  |                   |           |
| Threat Intel feeds |                           |                  |                   |           |
| Network sensors    |                           |                  |                   |           |

### B) Visibility Gaps (Mandatory if any)

- `Gap 1 (source not onboarded / low retention / missing endpoint coverage)`
- `Gap 2 ...`

Link to tracker:

- `CTRL-GAP-... / DET-IMP-...`

References:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`  
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

## 5.8 Improvement Activities (Mandatory)

### A) Detection Engineering and Tuning Changes

| Change | Reason | Scope | Status | Tracking Ref |
| ------ | ------ | ----- | ------ | ------------ |
|        |        |       |        |              |

### B) Playbook/Process Improvements

| Improvement | Trigger | Owner | Due (UTC) | Tracking Ref |
| ----------- | ------- | ----- | ---------:| ------------ |
|             |         |       |           |              |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`

---

## 5.9 MSSP Client Highlights (If Applicable) (Tenant-Safe)

### A) Client Incident Highlights (No sensitive detail)

| Client ID | New P1/P2 | Open P1/P2 | Key Themes | Client Actions Pending |
| --------- | ---------:| ----------:| ---------- | ---------------------- |
| CLIENT-   |           |            |            |                        |
| CLIENT-   |           |            |            |                        |

### B) SLA/Communication Exceptions (If Any)

| Client ID | Incident ID | SLA Risk/Breach | Reason | Mitigation |
| --------- | ----------- | --------------- | ------ | ---------- |
|           |             |                 |        |            |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`

---

## 5.10 Next Week Priorities (Mandatory)

1. `...`
2. `...`
3. `...`

### Action Items (Assigned)

| #   | Action Item | Owner | Due (UTC) | Tracking Ref | Status |
| ---:| ----------- | ----- | ---------:| ------------ | ------ |
| 1   |             |       |           |              |        |
| 2   |             |       |           |              |        |

---

# 6. Related Documents

| Document                  | Path                                                                      |
| ------------------------- | ------------------------------------------------------------------------- |
| Daily SOC Report Template | `07_REPORTING/07.2_Operational-Reports/Daily-SOC-Report-Template.md`      |
| Monthly Metrics Report    | `07_REPORTING/07.2_Operational-Reports/Monthly-Metrics-Report.md`         |
| Quarterly Trend Analysis  | `07_REPORTING/07.2_Operational-Reports/Quarterly-Trend-Analysis.md`       |
| Annual IR Review Template | `07_REPORTING/07.2_Operational-Reports/Annual-IR-Review-Template.md`      |
| Ticket Lifecycle SOP      | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`          |
| SLO Metrics Definition    | `00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`                |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |

---

# 7. Revision History

| Version | Date        | Author                            | Changes         |
| ------- | ----------- | --------------------------------- | --------------- |
| 1.0     | 30-May-2026 | SOC Manager / SOC Operations Lead | Initial version |

---

# 8. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
