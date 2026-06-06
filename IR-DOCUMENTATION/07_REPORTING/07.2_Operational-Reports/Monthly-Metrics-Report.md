# Monthly Metrics Report

---

# 1. Document Control

| Field          | Value                             |
| -------------- | --------------------------------- |
| Document Name  | Template – Monthly Metrics Report |
| Document ID    | RPT-OPS-003                       |
| Version        | 1.0                               |
| Effective Date | 30-May-2026                       |
| Owner          | SOC Manager / SOC Operations Lead |
| Approved By    | CISO                              |
| Classification | Internal – Confidential           |
| Review Cycle   | Quarterly                         |

---

# 2. Purpose

This template standardizes the **Monthly Metrics Report** used to evaluate SOC performance, operational health, detection effectiveness, and continual improvement progress.

Monthly reporting is critical because:

- it provides evidence of performance evaluation and improvement (ISO/NIST-aligned)
- it identifies patterns and bottlenecks that daily/weekly reporting may not show
- it supports SLA governance and management reviews
- it supports budgeting and resourcing decisions (staffing, tooling, coverage)
- it drives data-informed detection engineering and control remediation priorities
- it supports MSSP client service delivery metrics (tenant-safe summaries where required)

This template ensures:

- consistent KPI definitions and calculation periods
- comparable month-over-month reporting
- clear linkage between metrics and corrective actions
- audit-ready measurement and management review artifacts

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

---

# 3. Scope

This report covers, for the reporting month:

- incident and alert volumes
- response and escalation performance (MTTA/MTTR)
- SLA compliance
- ticket quality and documentation completeness
- tool coverage/health (SIEM, EDR, network sensors)
- detection engineering improvements and outcomes
- PIR/RCA outcomes and improvement tracking
- MSSP client summaries (if applicable)

Out of scope:

- detailed technical incident reports (covered under incident reporting templates)
- regulator submissions (covered under regulatory SOPs)

---

# 4. Instructions (Mandatory)

- Use UTC for reporting windows.
- Use standard KPI definitions from SLO Metrics Definition doc.
- Clearly state data sources (ticketing, SIEM, EDR, TI platform).
- If metrics are estimated or incomplete, label limitations and remediation plans.
- For MSSP: provide tenant-safe summaries and avoid cross-client exposure.

---

# 5. Template (Copy/Paste)

## 5.1 Report Header (Mandatory)

| Field                  | Value                                                 |
| ---------------------- | ----------------------------------------------------- |
| Reporting Month (UTC)  | `YYYY-MM`                                             |
| Reporting Window (UTC) | `Start: YYYY-MM-01 00:00` → `End: YYYY-MM-last 23:59` |
| Prepared By            | `Name / Role`                                         |
| Reviewed By            | `Name / Role`                                         |
| Approved By            | `Name / Role`                                         |
| SOC Coverage           | 24x7 / Business hours + notes                         |
| Scope                  | Internal / MSSP / Both                                |
| Data Sources           | Ticketing, SIEM, EDR, TI, Network                     |

---

## 5.2 Executive Overview (Mandatory)

### A) Overall Performance Status

- **SOC performance:** Green / Amber / Red  
- **Reason summary (3–8 bullets):**
  - `...`

### B) Month Highlights (What Improved)

- `...`

### C) Month Concerns (What Worsened / Risk Areas)

- `...`

### D) Decisions Required (If Any)

| Decision Needed | Why | Option(s) | Recommendation | Needed By (UTC) |
| --------------- | --- | --------- | -------------- | ---------------:|
|                 |     |           |                |                 |

---

## 5.3 Incident and Alert Volume Metrics (Mandatory)

### A) Incident Volumes by Severity

| Metric            | P1  | P2  | P3  | P4  | Total |
| ----------------- | ---:| ---:| ---:| ---:| -----:|
| Incidents opened  |     |     |     |     |       |
| Incidents closed  |     |     |     |     |       |
| Open at month end |     |     |     |     |       |

### B) Incidents by Category (Top 10)

| Category | Count | %   | Trend vs last month | Notes |
| -------- | -----:| ---:| ------------------- | ----- |
|          |       |     |                     |       |

Reference:
`01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/Category-Master-List.md`

### C) Alert Volumes (If Tracked)

| Source         | Total Alerts | Actionable Alerts | % Actionable | Top Noisy Rule(s) |
| -------------- | ------------:| -----------------:| ------------:| ----------------- |
| SIEM           |              |                   |              |                   |
| EDR            |              |                   |              |                   |
| IDS/IPS        |              |                   |              |                   |
| Email security |              |                   |              |                   |

---

## 5.4 Response Performance Metrics (Mandatory)

> Use standard definitions from SLO Metrics Definition.

### A) Time-to-Action KPIs

| KPI                   | This Month | Last Month | Target | Status (Met/Not Met) | Notes |
| --------------------- | ----------:| ----------:| ------:| -------------------- | ----- |
| MTTA                  |            |            |        |                      |       |
| Mean time to triage   |            |            |        |                      |       |
| Mean time to escalate |            |            |        |                      |       |
| MTTR (as defined)     |            |            |        |                      |       |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

### B) P1/P2 Update Cadence Compliance

| Metric                  | Compliance % | Notes |
| ----------------------- | ------------:| ----- |
| P1 updates every 30 min |              |       |
| P2 updates every 60 min |              |       |

---

## 5.5 SLA Compliance and Breach Analysis (Mandatory)

### A) SLA Compliance Summary

| SLA Metric                                      | Compliance % | Target | Notes |
| ----------------------------------------------- | ------------:| ------:| ----- |
| Ticket creation                                 |              |        |       |
| Initial triage                                  |              |        |       |
| Escalation acknowledgment                       |              |        |       |
| Containment initiation (P1/P2 where applicable) |              |        |       |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

### B) SLA Breaches (If Any) — Root Cause Themes

| Breach Theme                 | Count | Example Ticket(s) | Root Cause Summary | Corrective Action |
| ---------------------------- | -----:| ----------------- | ------------------ | ----------------- |
| Staffing / coverage          |       |                   |                    |                   |
| Tool outage                  |       |                   |                    |                   |
| Client approval delay (MSSP) |       |                   |                    |                   |
| Poor ticket quality          |       |                   |                    |                   |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLA-Breach-Escalation-Procedure.md`

---

## 5.6 Ticket Quality and Documentation QA (Mandatory)

### A) QA Sampling Summary

| Ticket Type/Severity | Sample Size | Pass % | Common Failures |
| -------------------- | -----------:| ------:| --------------- |
| P1                   |             |        |                 |
| P2                   |             |        |                 |
| P3                   |             |        |                 |
| P4                   |             |        |                 |

### B) Common Ticketing Issues (Top 5)

1. `Missing timestamps`
2. `No evidence references`
3. `Vague closure summaries`
4. `Missing owner transfer records`
5. `Severity changes without justification`

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md`

---

## 5.7 Detection Effectiveness and Improvement (Mandatory)

### A) Detection Improvements Implemented

| Improvement | Category    | Scope         | Result/Impact | Tracking Ref |
| ----------- | ----------- | ------------- | ------------- | ------------ |
|             | SIEM/EDR/TI | Internal/MSSP |               | DET-IMP-...  |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

### B) False Positive and Noise Reduction

| Metric                  | This Month | Last Month | Notes |
| ----------------------- | ----------:| ----------:| ----- |
| % FP (overall)          |            |            |       |
| Top noisy rule(s) tuned |            |            |       |
| Allowlist changes       |            |            |       |

### C) Missed Detection Review (If Any)

| Incident ID | Missed Detection? | Why | Corrective Action |
| ----------- | ----------------- | --- | ----------------- |
| INC-        | Yes/No            |     |                   |

---

## 5.8 Tooling Health and Coverage (Mandatory)

### A) SIEM Health Metrics

| Metric                             | Value | Target | Notes |
| ---------------------------------- | -----:| ------:| ----- |
| Critical source ingestion uptime % |       |        |       |
| Parsing error rate                 |       |        |       |
| Unparsed log sources count         |       |        |       |

### B) EDR Coverage

| Metric                                | Value | Target | Notes |
| ------------------------------------- | -----:| ------:| ----- |
| Endpoint coverage % (critical assets) |       |        |       |
| Offline endpoint avg                  |       |        |       |
| Policy deployment success %           |       |        |       |

### C) Network Telemetry (If Applicable)

| Metric                      | Value | Notes |
| --------------------------- | -----:| ----- |
| Firewall log availability % |       |       |
| DNS logging coverage        |       |       |
| IDS/IPS alerting stability  |       |       |

### D) Tool Outages and Impacts

| Tool | Outage/Degradation | Duration | Impact | Corrective Action |
| ---- | ------------------ | --------:| ------ | ----------------- |
|      |                    |          |        |                   |

---

## 5.9 Post-Incident Activities (Mandatory)

### A) PIR / Lessons Learned

| Metric                        | Value | Notes |
| ----------------------------- | -----:| ----- |
| P1/P2 incidents requiring PIR |       |       |
| PIRs completed within target  |       |       |
| Open PIR action items         |       |       |

Reference:
`08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`

### B) RCA Completion

| Metric                       | Value | Notes |
| ---------------------------- | -----:| ----- |
| RCAs required (P1/P2)        |       |       |
| RCAs completed within target |       |       |
| Open RCA items               |       |       |

Reference:
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`

---

## 5.10 MSSP Client Metrics (If Applicable) (Tenant-Safe)

### A) Client Summary Table

| Client ID | SLA Tier | P1/P2 Count | SLA Compliance % | Key Themes | Client Actions Pending |
| --------- | -------- | -----------:| ----------------:| ---------- | ---------------------- |
| CLIENT-   |          |             |                  |            |                        |

### B) Client SLA Exceptions / Risks

| Client ID | Issue | Impact | Mitigation | Owner |
| --------- | ----- | ------ | ---------- | ----- |
|           |       |        |            |       |

Reference:
`07_REPORTING/07.3_MSSP-Client-Reports/MSSP-SLA-Compliance-Report.md` (if available)

---

## 5.11 Key Risks and Recommendations (Mandatory)

### A) Risks (Top 5)

1. `...`
2. `...`

### B) Recommendations (Actionable)

| Recommendation | Owner | Priority | Due (UTC) | Tracking Ref |
| -------------- | ----- | -------- | ---------:| ------------ |
|                |       |          |           |              |

---

## 5.12 Appendix (Optional)

- KPI calculation methodology notes
- Data completeness/limitations
- Key dashboards references

---

# 6. Related Documents

| Document                  | Path                                                                      |
| ------------------------- | ------------------------------------------------------------------------- |
| Daily SOC Report Template | `07_REPORTING/07.2_Operational-Reports/Daily-SOC-Report-Template.md`      |
| Weekly Incident Summary   | `07_REPORTING/07.2_Operational-Reports/Weekly-Incident-Summary.md`        |
| Quarterly Trend Analysis  | `07_REPORTING/07.2_Operational-Reports/Quarterly-Trend-Analysis.md`       |
| Annual IR Review Template | `07_REPORTING/07.2_Operational-Reports/Annual-IR-Review-Template.md`      |
| Internal SLA Definitions  | `00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`              |
| SLO Metrics Definition    | `00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`                |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |
| Control Gap Tracker       | `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`     |

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
