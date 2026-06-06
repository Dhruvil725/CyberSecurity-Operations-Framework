# Daily SOC Report Template

---

# 1. Document Control

| Field          | Value                          |
| -------------- | ------------------------------ |
| Document Name  | Template – Daily SOC Report    |
| Document ID    | RPT-OPS-001                    |
| Version        | 1.0                            |
| Effective Date | 30-May-2026                    |
| Owner          | SOC Lead / SOC Operations Lead |
| Approved By    | SOC Manager                    |
| Classification | Internal – Confidential        |
| Review Cycle   | Quarterly                      |

---

# 2. Purpose

This template standardizes the **Daily SOC Report** used to communicate SOC operational status, notable security activity, incident handling progress, SLA posture, and key risks.

A daily SOC report is critical because it:

- provides consistent management visibility into security operations
- creates an audit-ready record of SOC activity and response posture
- supports shift-to-shift continuity and prioritization
- identifies recurring detection gaps and operational bottlenecks early
- supports MSSP client reporting inputs (when applicable)
- enables trend analysis for weekly/monthly reporting

This template ensures:

- consistent structure and minimum information set
- clear separation between **facts**, **analysis**, and **recommendations**
- repeatable daily reporting aligned to SOC KPIs/SLOs

---

# 3. Scope

Use this report for:

| Scope Area           | Included                                               |
| -------------------- | ------------------------------------------------------ |
| SOC operations       | L1/L2/L3, SOC Lead, IR escalation posture              |
| Security monitoring  | SIEM, EDR, network sensors, cloud logs (as applicable) |
| Incidents and alerts | Open/closed, new incidents, escalations                |
| SLA/SLO performance  | MTTA/MTTR, breaches, backlog                           |
| Tooling health       | Data ingestion, sensor coverage, integrations          |
| MSSP (if applicable) | Client-wise daily highlights (tenant-safe summaries)   |

Out of scope:

- full incident final reports (use incident report templates)
- regulatory report submissions (covered under regulatory SOPs)

---

# 4. Instructions (Mandatory)

- Use **UTC** for all timestamps and reporting windows.
- This report must be prepared and finalized by the SOC Lead (or delegate).
- Do not include sensitive raw evidence (credentials/PII/PCAP/dumps) in the daily report.
- Use incident IDs and evidence references instead of attaching sensitive artifacts.
- For MSSP: ensure client summaries are tenant-scoped and avoid cross-client disclosure.

---

# 5. Template (Copy/Paste)

## 5.1 Report Header (Mandatory)

| Field                              | Value                                               |
| ---------------------------------- | --------------------------------------------------- |
| Report Date (UTC)                  | `YYYY-MM-DD`                                        |
| Reporting Window (UTC)             | `Start: YYYY-MM-DD 00:00` → `End: YYYY-MM-DD 23:59` |
| Prepared By                        | `Name / Role`                                       |
| Reviewed By                        | `Name / Role`                                       |
| SOC Coverage                       | `24x7 / Business hours` + notes                     |
| Major Incident Bridge Call Active? | Yes / No (if yes: incident ID)                      |
| MSSP Scope Included?               | Yes / No (if yes: list tenants included)            |

---

## 5.2 Executive Snapshot (1 Page Summary) (Mandatory)

### A) Overall SOC Status

- **SOC posture:** Green / Amber / Red
- **Reason (1–3 bullets):**
  - `...`
  - `...`

### B) Today’s Top Risks / Priorities (Top 3–5)

1. `...`
2. `...`
3. `...`

### C) Key Outcomes (What Was Achieved)

- `P1 contained and stabilized`
- `High-risk credential attack mitigated`
- `Critical log ingestion restored`

(Replace with actual outcomes.)

---

## 5.3 Incident and Alert Summary (Mandatory)

### A) Incident Summary (By Severity)

| Metric                            | P1  | P2  | P3  | P4  |
| --------------------------------- | ---:| ---:| ---:| ---:|
| New incidents opened              |     |     |     |     |
| Incidents closed                  |     |     |     |     |
| Incidents still open (end of day) |     |     |     |     |
| Escalations (tier changes)        |     |     |     |     |

### B) Notable Incidents (P1/P2 + Significant P3) (Mandatory)

> Add one row per notable case.

| Incident ID | Severity | Category | Tenant/BU (if applicable) | Status | Key Impact | Current Owner | Next Milestone (UTC) |
| ----------- | -------- | -------- | ------------------------- | ------ | ---------- | ------------- | --------------------:|
| INC-        | P1/P2/P3 |          |                           |        |            |               |                      |
| INC-        |          |          |                           |        |            |               |                      |

### C) High-Volume Alert Types (Top 5) (Recommended)

| Rank | Alert / Rule Name | Source (SIEM/EDR/IDS) | Volume | % FP (if known) | Action Taken (tuning/hunt/monitor) |
| ----:| ----------------- | --------------------- | ------:| ---------------:| ---------------------------------- |
| 1    |                   |                       |        |                 |                                    |
| 2    |                   |                       |        |                 |                                    |
| 3    |                   |                       |        |                 |                                    |
| 4    |                   |                       |        |                 |                                    |
| 5    |                   |                       |        |                 |                                    |

---

## 5.4 SLA/SLO and Operational Performance (Mandatory)

### A) SLA Compliance (Daily)

| SLA Metric                    | Target       | Achieved | Notes / Exceptions |
| ----------------------------- | ------------ | -------- | ------------------ |
| Ticket creation SLA           |              | Yes/No   |                    |
| Initial triage SLA            |              | Yes/No   |                    |
| Escalation acknowledgment SLA |              | Yes/No   |                    |
| P1 update cadence met         | Every 30 min | Yes/No   |                    |
| P2 update cadence met         | Every 60 min | Yes/No   |                    |

If any SLA breach occurred:

| Breach ID | Ticket/Incident | Severity | SLA Type | Breach Duration | Root Cause (short) | Corrective Action |
| --------- | --------------- | -------- | -------- | ---------------:| ------------------ | ----------------- |
| SLA-      | INC-            |          |          |                 |                    |                   |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLA-Breach-Escalation-Procedure.md`

### B) Key Metrics (Daily)

| Metric                            | Value | Notes            |
| --------------------------------- | -----:| ---------------- |
| MTTA (Mean Time to Acknowledge)   |       | UTC-based        |
| Mean time to triage               |       |                  |
| MTTR (as defined)                 |       |                  |
| Tickets created                   |       |                  |
| Tickets closed                    |       |                  |
| Backlog (open tickets)            |       | end-of-day count |
| % Tickets with complete fields QA |       | sample size      |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

---

## 5.5 Threat Activity Highlights (Recommended but Strongly Suggested)

### A) Confirmed Threats (TP Summary)

| Threat Type       | Count | Affected Entities (count) | Notes |
| ----------------- | -----:| -------------------------:| ----- |
| Malware           |       |                           |       |
| Phishing/BEC      |       |                           |       |
| Credential attack |       |                           |       |
| Network intrusion |       |                           |       |
| Data exfiltration |       |                           |       |
| DDoS              |       |                           |       |

### B) Emerging Trends (Daily Observations)

- `Example: increased failed logins from ASN X targeting privileged accounts`
- `Example: phishing emails mimicking HR payroll process`

### C) IoC/TI Actions (If Any)

| Action                      | Source | Scope                | Outcome                  |
| --------------------------- | ------ | -------------------- | ------------------------ |
| IOC added to SIEM watchlist | TI     | Internal/MSSP Tenant | Matches observed: Yes/No |
| IOC added to EDR alert list | TI     |                      |                          |
| Block request submitted     | TI/IR  | Firewall/Proxy       | Implemented: Yes/No      |

References:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md`

---

## 5.6 Tooling and Telemetry Health (Mandatory)

### A) SIEM Health (Minimum)

| Check                               | Status (OK/Degraded/Down) | Notes | Owner | ETA (UTC) |
| ----------------------------------- | ------------------------- | ----- | ----- | ---------:|
| Ingestion status (critical sources) |                           |       |       |           |
| Parsing/normalization errors        |                           |       |       |           |
| Correlation rule execution          |                           |       |       |           |
| Storage/retention status            |                           |       |       |           |

### B) EDR Health (Minimum)

| Check                            | Status | Notes | Owner | ETA (UTC) |
| -------------------------------- | ------ | ----- | ----- | ---------:|
| Agent coverage (critical assets) |        |       |       |           |
| Offline endpoints count          |        |       |       |           |
| Policy deployment status         |        |       |       |           |
| Containment capability verified  |        |       |       |           |

### C) Network Sensor Health (If Applicable)

| Sensor           | Status | Notes |
| ---------------- | ------ | ----- |
| Firewall logging |        |       |
| Proxy logging    |        |       |
| IDS/IPS          |        |       |
| DNS logging      |        |       |

### D) Known Visibility Gaps (Mandatory if any)

- `Gap 1 (source not onboarded / retention too low / coverage missing)`
- `Gap 2 ...`

Link to improvement action:

- `DET-IMP / CTRL-GAP ticket reference`

---

## 5.7 Investigation and Hunting Activities (Recommended)

### A) Threat Hunts Conducted

| Hunt ID / Name | Hypothesis | Data Sources | Outcome | Follow-ups |
| -------------- | ---------- | ------------ | ------- | ---------- |
| HUNT-          |            |              |         |            |

### B) Detection Engineering / Tuning Changes (Recommended)

| Change                     | Reason          | Scope           | Status           | Tracking Reference |
| -------------------------- | --------------- | --------------- | ---------------- | ------------------ |
| SIEM rule threshold update | noise reduction | tenant/internal | implemented      | CHG-/TKT-          |
| EDR exclusion update       | FP fix          |                 | pending/approved | TKT-               |

References:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md`  
`04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Exclusion-Management.md`

---

## 5.8 MSSP Client Summary (If Applicable) (Tenant-Safe) (Optional/Recommended)

> Use only if the daily report is intended for MSSP service delivery visibility. Do not mix clients.

### A) Client-wise Daily Snapshot

| Client ID | SLA Tier | New P1/P2 | Open P1/P2 | Key Notes (No sensitive detail) | Client Actions Pending |
| --------- | -------- | ---------:| ----------:| ------------------------------- | ---------------------- |
| CLIENT-   |          |           |            |                                 |                        |
| CLIENT-   |          |           |            |                                 |                        |

### B) Client Pending Approvals (Containment / Evidence)

| Client ID | Approval Needed | Incident ID | Requested At (UTC) | Status | Risk if Delayed |
| --------- | --------------- | ----------- | ------------------:| ------ | --------------- |
|           |                 |             |                    |        |                 |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`

---

## 5.9 Action Items and Next-Day Priorities (Mandatory)

### A) Open Action Items

| #   | Action Item | Owner | Due (UTC) | Tracking Ref | Status |
| ---:| ----------- | ----- | ---------:| ------------ | ------ |
| 1   |             |       |           |              |        |
| 2   |             |       |           |              |        |

### B) Tomorrow’s Priorities (Top 3–5)

1. `...`
2. `...`
3. `...`

---

## 5.10 Appendices (Optional)

- Incident list export (IDs only)
- KPI dashboard snapshot reference
- Maintenance/change windows impacting monitoring
- Evidence package reference IDs (do not embed raw evidence)

---

# 6. Distribution (Fill-In)

| Audience          | Distribution Method          |
| ----------------- | ---------------------------- |
| SOC Leadership    | Email / Portal               |
| CISO / Management | Email (executive snapshot)   |
| Compliance / ISMS | Email (if required)          |
| MSSP SDM          | Portal / Email (tenant-safe) |

---

# 7. Related Documents

| Document                  | Path                                                                 |
| ------------------------- | -------------------------------------------------------------------- |
| Weekly Incident Summary   | `07_REPORTING/07.2_Operational-Reports/Weekly-Incident-Summary.md`   |
| Monthly Metrics Report    | `07_REPORTING/07.2_Operational-Reports/Monthly-Metrics-Report.md`    |
| Quarterly Trend Analysis  | `07_REPORTING/07.2_Operational-Reports/Quarterly-Trend-Analysis.md`  |
| Annual IR Review Template | `07_REPORTING/07.2_Operational-Reports/Annual-IR-Review-Template.md` |
| Ticket Lifecycle SOP      | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`     |
| Internal SLA Definitions  | `00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`         |
| SLO Metrics Definition    | `00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`           |

---

# 8. Revision History

| Version | Date        | Author                         | Changes         |
| ------- | ----------- | ------------------------------ | --------------- |
| 1.0     | 30-May-2026 | SOC Lead / SOC Operations Lead | Initial version |

---

# 9. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
