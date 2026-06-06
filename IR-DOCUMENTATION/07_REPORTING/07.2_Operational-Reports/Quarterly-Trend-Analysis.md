# Quarterly Trend Analysis

---

# 1. Document Control

| Field          | Value                                  |
| -------------- | -------------------------------------- |
| Document Name  | Template – Quarterly Trend Analysis    |
| Document ID    | RPT-OPS-004                            |
| Version        | 1.0                                    |
| Effective Date | 30-May-2026                            |
| Owner          | SOC Manager / Threat Intelligence Lead |
| Approved By    | CISO                                   |
| Classification | Internal – Confidential                |
| Review Cycle   | Quarterly                              |

---

# 2. Purpose

This template standardizes the **Quarterly Trend Analysis** report used to evaluate:

- evolving threat landscape affecting the organization (and MSSP clients if applicable),
- incident patterns and root causes,
- performance trends (SLA/SLO/KPIs),
- detection and control maturity changes,
- recurring weaknesses and improvement effectiveness,
- strategic priorities for the next quarter.

Quarterly analysis is critical because:

- it supports management review and security governance (ISO/NIST-aligned)
- it identifies systemic issues not visible in weekly/monthly reporting
- it provides data-driven prioritization for investments and control improvements
- it validates whether improvements delivered measurable impact
- it supports client executive briefings in MSSP operations (tenant-safe versions)

This template ensures:

- consistent quarter-to-quarter comparisons
- evidence-based conclusions with clear recommendations and owners
- linkage to improvement trackers, incident RCAs, and lessons learned

---

# 3. Scope

This report covers the quarter for:

- internal SOC operations
- incidents and alerts across all categories
- tooling/telemetry health and coverage
- detection engineering improvements and outcomes
- post-incident review themes (RCA/PIR)
- MSSP client trends (tenant-safe aggregation, if included)

Out of scope:

- detailed incident technical reports
- regulator submissions (covered separately)

---

# 4. Instructions (Mandatory)

- Use UTC time boundaries for the quarter (start/end).
- Use standard KPI definitions and calculation methodology.
- Clearly state data sources and known limitations.
- Do not include raw sensitive evidence; reference incident IDs and tracker IDs.
- If producing a client version (MSSP), ensure tenant-scoped content and no cross-client disclosure.

---

# 5. Template (Copy/Paste)

## 5.1 Report Header (Mandatory)

| Field                  | Value                                               |
| ---------------------- | --------------------------------------------------- |
| Quarter (UTC)          | `Q# YYYY`                                           |
| Reporting Window (UTC) | `Start: YYYY-MM-DD 00:00` → `End: YYYY-MM-DD 23:59` |
| Prepared By            | `Name / Role`                                       |
| Reviewed By            | `Name / Role`                                       |
| Approved By            | `Name / Role`                                       |
| Scope                  | Internal / MSSP / Both                              |
| Data Sources           | Ticketing, SIEM, EDR, TI, Network, Cloud            |
| Distribution           | SOC leadership / CISO / Management / Compliance     |

---

## 5.2 Executive Summary (Mandatory)

### A) Quarter Snapshot (Non-Technical)

- `Summary of the quarter in 8–12 bullets`
- Focus on: highest impact incidents, trend shifts, improvements, key risks.

### B) Top Strategic Risks (Top 5)

1. `...`
2. `...`
3. `...`
4. `...`
5. `...`

### C) Strategic Recommendations (Top 5)

1. `...`
2. `...`

### D) Decisions Required (If Any)

| Decision Needed | Why | Options | Recommendation | Needed By (UTC) |
| --------------- | --- | ------- | -------------- | ---------------:|
|                 |     |         |                |                 |

---

## 5.3 Incident Trends and Patterns (Mandatory)

### A) Incident Volume Trend (Quarter vs Prior Quarter)

| Metric          | This Quarter | Last Quarter | % Change | Notes |
| --------------- | ------------:| ------------:| --------:| ----- |
| Total incidents |              |              |          |       |
| P1 count        |              |              |          |       |
| P2 count        |              |              |          |       |
| P3 count        |              |              |          |       |
| P4 count        |              |              |          |       |

### B) Category Distribution (Top Categories)

| Category          | This Quarter | Last Quarter | % Change | Comments |
| ----------------- | ------------:| ------------:| --------:| -------- |
| Phishing/BEC      |              |              |          |          |
| Malware           |              |              |          |          |
| Credential attack |              |              |          |          |
| Intrusion         |              |              |          |          |
| Data breach/exfil |              |              |          |          |

Reference:
`01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/Category-Master-List.md`

### C) Notable Incidents (Quarter)

> List all P1 and significant P2.

| Incident ID | Category | Severity | Status | Impact Summary | Root Cause Theme | Follow-ups |
| ----------- | -------- | -------- | ------ | -------------- | ---------------- | ---------- |
| INC-        |          |          |        |                |                  |            |

---

## 5.4 Root Cause and Control Weakness Themes (Mandatory)

### A) Root Cause Themes (Aggregated)

| Theme                   | Count | Example Incident(s) | Primary Control Gap        | Notes |
| ----------------------- | -----:| ------------------- | -------------------------- | ----- |
| Phishing susceptibility |       | INC-                | Awareness / email controls |       |
| Patch delays            |       |                     | Vulnerability mgmt         |       |
| Privilege misuse        |       |                     | IAM governance             |       |
| Logging gaps            |       |                     | SIEM onboarding            |       |
| Misconfiguration        |       |                     | Cloud governance           |       |

Reference:
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/`

### B) Repeat Offenders (Systems/Teams/Patterns) (If Applicable)

- `Repeated issues in system X due to ...`
- `Repeated detection gaps in ...`

> Keep this constructive and action-oriented; avoid blame language.

---

## 5.5 Threat Landscape Analysis (Mandatory)

### A) External Threat Trends (Quarter)

- `Threat 1: ransomware variant trend`
- `Threat 2: credential stuffing increase`
- `Threat 3: cloud IAM abuse trend`

### B) Observed TTP Trends (If Applicable)

| Tactic | Technique | Frequency Trend | Notes |
| ------ | --------- | --------------- | ----- |
|        |           | Up/Down/Stable  |       |

Reference:
`10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`

### C) Top Initial Access Vectors (Estimated)

| Vector                | % of Incidents | Notes |
| --------------------- | --------------:| ----- |
| Phishing              |                |       |
| Credential reuse      |                |       |
| Vulnerability exploit |                |       |
| Third-party           |                |       |
| Unknown               |                |       |

---

## 5.6 Operational Performance Trends (Mandatory)

### A) KPI Trends

| KPI            | This Quarter | Last Quarter | Target | Trend | Notes |
| -------------- | ------------:| ------------:| ------:| ----- | ----- |
| MTTA           |              |              |        |       |       |
| Time to triage |              |              |        |       |       |
| MTTR           |              |              |        |       |       |
| Backlog (avg)  |              |              |        |       |       |
| QA pass rate   |              |              |        |       |       |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

### B) SLA Compliance Trends

| SLA Metric                                            | Compliance % | Last Quarter | Trend | Notes |
| ----------------------------------------------------- | ------------:| ------------:| ----- | ----- |
| Ticket creation                                       |              |              |       |       |
| Initial triage                                        |              |              |       |       |
| Escalation acknowledgment |              |              |       |       |
| P1 update cadence                                     |              |              |       |       |
| P2 update cadence                                     |              |              |       |       |

---

## 5.7 Detection Effectiveness and Engineering (Mandatory)

### A) Detection Improvement Outcomes

| Improvement Theme    | Implemented Count | Measured Impact | Notes | Tracking Ref |
| -------------------- | -----------------:| --------------- | ----- | ------------ |
| Noise reduction      |                   |                 |       | DET-IMP-...  |
| Coverage improvement |                   |                 |       | DET-IMP-...  |
| Faster correlation   |                   |                 |       | DET-IMP-...  |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

### B) False Positive Trend

| Metric            | This Quarter | Last Quarter | Trend | Notes |
| ----------------- | ------------:| ------------:| ----- | ----- |
| % FP overall      |              |              |       |       |
| Top 5 noisy rules | list         | list         |       |       |

### C) Detection Gaps (Open)

| Gap | Risk | Priority | Owner | Due (UTC) | Tracking Ref |
| --- | ---- | -------- | ----- | ---------:| ------------ |
|     |      |          |       |           | CTRL-GAP-... |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`

---

## 5.8 Tooling and Telemetry Maturity (Mandatory)

### A) Coverage and Reliability

| Component          | Availability/Uptime % | Key Issues | Improvement Plan |
| ------------------ | ---------------------:| ---------- | ---------------- |
| SIEM ingestion     |                       |            |                  |
| EDR coverage       |                       |            |                  |
| Threat intel feeds |                       |            |                  |
| Network logging    |                       |            |                  |

### B) High-Impact Outages / Degradation Events

| Date (UTC) | Component | Impact | Duration | Root Cause | Corrective Action |
| ---------- | --------- | ------ | --------:| ---------- | ----------------- |
|            |           |        |          |            |                   |

---

## 5.9 Post-Incident Review (PIR/RCA) Trends (Mandatory)

### A) PIR Completion and Action Closure

| Metric                 | Value | Target | Notes |
| ---------------------- | -----:| ------:| ----- |
| PIRs required          |       |        |       |
| PIRs completed on time |       |        |       |
| Open PIR action items  |       |        |       |

Reference:
`08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`

### B) Improvement Closure Rate

| Improvement Type       | Open at Start | Added | Closed | Open at End |
| ---------------------- | -------------:| -----:| ------:| -----------:|
| Detection improvements |               |       |        |             |
| Control remediation    |               |       |        |             |
| Process improvements   |               |       |        |             |

---

## 5.10 MSSP Client Trends (If Applicable) (Tenant-Safe Aggregation)

> Do not compare clients publicly in shared reports; keep client sections separate if required.

| Client ID | P1/P2 Count | SLA Compliance % | Key Themes | Major Risks | Actions Pending |
| --------- | -----------:| ----------------:| ---------- | ----------- | --------------- |
| CLIENT-   |             |                  |            |             |                 |

---

## 5.11 Next Quarter Plan (Mandatory)

### A) Priority Workstreams (Top 5)

1. `...`
2. `...`

### B) Action Plan (Assigned)

| Workstream | Objective | Owner | Due (UTC) | Tracking Ref |
| ---------- | --------- | ----- | ---------:| ------------ |
|            |           |       |           |              |

---

## 5.12 Appendix (Optional)

- KPI calculation notes
- Data completeness limitations
- Supporting dashboard references

---

# 6. Related Documents

| Document                  | Path                                                                        |
| ------------------------- | --------------------------------------------------------------------------- |
| Monthly Metrics Report    | `07_REPORTING/07.2_Operational-Reports/Monthly-Metrics-Report.md`           |
| Weekly Incident Summary   | `07_REPORTING/07.2_Operational-Reports/Weekly-Incident-Summary.md`          |
| Annual IR Review Template | `07_REPORTING/07.2_Operational-Reports/Annual-IR-Review-Template.md`        |
| SLO Metrics Definition    | `00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`                  |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`   |
| Control Gap Tracker       | `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`       |
| TI Reporting Template     | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Reporting-Template.md` |

---

# 7. Revision History

| Version | Date        | Author                                 | Changes         |
| ------- | ----------- | -------------------------------------- | --------------- |
| 1.0     | 30-May-2026 | SOC Manager / Threat Intelligence Lead | Initial version |

---

# 8. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
