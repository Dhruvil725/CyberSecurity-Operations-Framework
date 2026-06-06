# MSSP Monthly Client Report

---

# 1. Document Control

| Field          | Value                                             |
| -------------- | ------------------------------------------------- |
| Document Name  | Template – MSSP Monthly Client Report             |
| Document ID    | RPT-MSSP-003                                      |
| Version        | 1.0                                               |
| Effective Date | 30-May-2026                                       |
| Owner          | MSSP Service Delivery Manager (SDM) / SOC Manager |
| Approved By    | MSSP Program Head / CISO (delegated)              |
| Classification | Client Confidential                               |
| Review Cycle   | Quarterly                                         |

---

# 2. Purpose

This template standardizes the **Monthly Client Report** delivered by the MSSP to provide each client with:

- a measurable view of SOC service performance and outcomes,
- incident and alert summaries (tenant-scoped),
- SLA compliance results and exceptions,
- operational health and visibility gaps,
- improvements delivered and recommendations,
- action items requiring client ownership.

Monthly reporting is critical because:

- it provides contractual service transparency and supports renewals/QBRs
- it helps clients understand their risk posture and prioritize remediation
- it creates audit-ready service evidence for client compliance programs
- it drives continuous improvement with measurable results
- it aligns MSSP operations with client expectations, constraints, and governance

This report ensures:

- consistent reporting structure month-to-month
- tenant-safe client-specific data with no cross-client disclosure
- clear linkage between metrics, incidents, and improvement actions
- actionable recommendations with ownership and timelines

---

# 3. Scope

This report covers the monthly reporting window for a single client:

| Area            | Included                                                               |
| --------------- | ---------------------------------------------------------------------- |
| Incidents       | P1–P4 incidents handled for the client                                 |
| Alerts          | High-level alert volumes and top drivers (if contract includes)        |
| SLA performance | notification and response timelines per SLA tier                       |
| SOC operations  | update cadence, escalation performance, ticket quality (as applicable) |
| Visibility      | logging and EDR coverage posture, telemetry gaps                       |
| Improvements    | tuning, detections, playbook/process improvements related to client    |
| Client actions  | pending approvals, remediation actions, hardening work                 |

Out of scope:

- detailed forensic evidence dumps (delivered only via secure evidence sharing process)
- internal MSSP cross-tenant metrics (no other client comparisons)

---

# 4. Instructions (Mandatory)

- Ensure the report is **client-specific** and **tenant-scoped**.
- Use UTC timestamps for incident timelines and reporting windows.
- Do not include sensitive evidence in the report body (raw logs/PCAP/dumps).
- Use incident IDs and evidence reference IDs/paths for traceability.
- Clearly note any data limitations (missing log sources, partial coverage).
- If client requires, provide report via client portal and track delivery.

---

# 5. Template (Copy/Paste)

## 5.1 Report Metadata (Mandatory)

| Field                  | Value                                                 |
| ---------------------- | ----------------------------------------------------- |
| Client Name            |                                                       |
| Client ID              |                                                       |
| SLA Tier               | Gold / Silver / Bronze (or contract label)            |
| Reporting Month (UTC)  | `YYYY-MM`                                             |
| Reporting Window (UTC) | `Start: YYYY-MM-01 00:00` → `End: YYYY-MM-last 23:59` |
| Prepared By (MSSP)     | Name / Role                                           |
| Reviewed By (MSSP)     | Name / Role                                           |
| Delivered To (Client)  | Names / Roles                                         |
| Delivery Date (UTC)    | `YYYY-MM-DD HH:MM`                                    |
| Delivery Method        | Email / Portal / Onsite                               |
| Version                | 1.0                                                   |

---

## 5.2 Executive Summary (Client-Friendly) (Mandatory)

### A) Monthly Snapshot (Non-Technical)

- `3–8 bullets summarizing key security outcomes and risks`

### B) Overall Posture

- **Client posture:** Green / Amber / Red  
- **Rationale:** `...`

### C) Top 3 Client Risks (Month)

1. `...`
2. `...`
3. `...`

### D) Key MSSP Outcomes (Value Delivered)

- `...`

---

## 5.3 Incident Summary (Tenant-Scoped) (Mandatory)

### A) Incident Volumes by Severity

| Metric            | P1  | P2  | P3  | P4  | Total |
| ----------------- | ---:| ---:| ---:| ---:| -----:|
| Incidents opened  |     |     |     |     |       |
| Incidents closed  |     |     |     |     |       |
| Open at month end |     |     |     |     |       |

### B) Incidents by Category

| Category          | Count | %   | Notes |
| ----------------- | -----:| ---:| ----- |
| Phishing/BEC      |       |     |       |
| Malware           |       |     |       |
| Credential attack |       |     |       |
| Cloud incident    |       |     |       |
| Intrusion         |       |     |       |
| Other             |       |     |       |

### C) Notable Incidents (P1/P2 + Significant P3)

| Incident ID | Severity | Category | Dates (UTC) | Outcome | Impact Summary | Client Action Required |
| ----------- | -------- | -------- | ----------- | ------- | -------------- | ---------------------- |
|             |          |          |             |         |                |                        |

For each P1/P2, include a short summary:

- `What happened (confirmed)`
- `What was impacted`
- `Actions taken`
- `Validation performed`
- `Residual risk`

---

## 5.4 Alerting Summary (If Included in Contract) (Recommended)

> Keep high-level. Avoid listing every alert.

### A) Alert Volumes by Source

| Source          | Total Alerts | Actionable | % Actionable | Notes |
| --------------- | ------------:| ----------:| ------------:| ----- |
| SIEM            |              |            |              |       |
| EDR             |              |            |              |       |
| Email security  |              |            |              |       |
| Network sensors |              |            |              |       |

### B) Top Alert Drivers (Top 5)

| Rank | Alert/Rule | Volume | FP Trend (Up/Down/Stable) | Action Taken |
| ----:| ---------- | ------:| ------------------------- | ------------ |
| 1    |            |        |                           |              |
| 2    |            |        |                           |              |

---

## 5.5 SLA and Service Performance (Mandatory)

### A) SLA KPI Summary

| SLA Metric                   | Target | Achieved | Notes |
| ---------------------------- | ------:| --------:| ----- |
| Initial notification (P1)    |        |          |       |
| Initial notification (P2)    |        |          |       |
| Update cadence (P1)          |        |          |       |
| Update cadence (P2)          |        |          |       |
| Acknowledgment time          |        |          |       |
| Resolution time (if defined) |        |          |       |

### B) SLA Exceptions (If Any)

| Incident ID | SLA Metric | Exception Reason | Client Impact | Corrective Action |
| ----------- | ---------- | ---------------- | ------------- | ----------------- |
|             |            |                  |               |                   |

---

## 5.6 Visibility and Coverage Review (Mandatory)

### A) Telemetry Coverage Snapshot (Client-Specific)

| Control/Telemetry                    | Status (OK/Gap) | Details | Risk | Recommendation | Owner |
| ------------------------------------ | --------------- | ------- | ---- | -------------- | ----- |
| EDR coverage (critical assets)       |                 |         |      |                |       |
| SIEM log coverage (critical sources) |                 |         |      |                |       |
| Firewall/Proxy/DNS logging           |                 |         |      |                |       |
| Cloud audit logs                     |                 |         |      |                |       |
| MFA/SSO telemetry                    |                 |         |      |                |       |

### B) Data Limitations (Mandatory if any)

- `Missing logs from X source`
- `Retention insufficient for Y investigation`
- `Asset inventory not updated`

---

## 5.7 Security Improvement Activities (Mandatory)

### A) Improvements Delivered by MSSP (Month)

| Improvement | Category (Detect/Respond) | Benefit | Status | Date (UTC) | Notes |
| ----------- | ------------------------- | ------- | ------ | ----------:| ----- |
|             |                           |         |        |            |       |

### B) Recommendations for Client Hardening (Month) (Mandatory)

| Recommendation | Priority     | Client Owner | Due (UTC) | Notes |
| -------------- | ------------ | ------------ | ---------:| ----- |
|                | High/Med/Low |              |           |       |

Examples:

- enforce MFA for admin accounts
- close exposed services
- patch critical vulnerabilities
- deploy EDR to remaining critical servers
- increase log retention for key sources

---

## 5.8 Client Action Items and Pending Approvals (Mandatory)

### A) Pending Approvals (Containment / Evidence / Changes)

| Approval Needed | Incident ID | Requested At (UTC) | Status | Risk if Delayed |
| --------------- | ----------- | ------------------:| ------ | --------------- |
|                 |             |                    |        |                 |

### B) Action Items Tracker

| #   | Action Item | Owner (Client/MSSP) | Priority | Due (UTC) | Status |
| ---:| ----------- | ------------------- | -------- | ---------:| ------ |
| 1   |             |                     |          |           |        |
| 2   |             |                     |          |           |        |

---

## 5.9 Roadmap (Next Month) (Recommended)

| Initiative | Objective | Owner | Target Date (UTC) | Notes |
| ---------- | --------- | ----- | -----------------:| ----- |
|            |           |       |                   |       |

---

## 5.10 Appendix (Optional)

- Incident list (IDs only)
- KPI definitions
- Client-approved IoC appendix reference
- Evidence package references (IDs only)

---

# 6. Confidentiality and Distribution (Mandatory)

- This report is **Client Confidential**.
- Distribution must be limited to client-approved recipients.
- Report must not include any other client information or MSSP internal sensitive details beyond what is necessary.

---

# 7. Related Documents

| Document                         | Path                                                                                      |
| -------------------------------- | ----------------------------------------------------------------------------------------- |
| MSSP Executive Briefing Template | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Executive-Briefing-Template.md`               |
| MSSP Incident Report Template    | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Incident-Report-Template.md`                  |
| MSSP SLA Compliance Report       | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-SLA-Compliance-Report.md`                     |
| MSSP Client Evidence Handling    | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md` |
| Internal-to-MSSP Escalation      | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`    |
| Client Data Segregation Policy   | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`         |

---

# 8. Revision History

| Version | Date        | Author                 | Changes         |
| ------- | ----------- | ---------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP SDM / SOC Manager | Initial version |

---

# 9. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**# MSSP Monthly Client Report

---

# 1. Document Control

| Field          | Value                                             |
| -------------- | ------------------------------------------------- |
| Document Name  | Template – MSSP Monthly Client Report             |
| Document ID    | RPT-MSSP-003                                      |
| Version        | 1.0                                               |
| Effective Date | 30-May-2026                                       |
| Owner          | MSSP Service Delivery Manager (SDM) / SOC Manager |
| Approved By    | MSSP Program Head / CISO (delegated)              |
| Classification | Client Confidential                               |
| Review Cycle   | Quarterly                                         |

---

# 2. Purpose

This template standardizes the **Monthly Client Report** delivered by the MSSP to provide each client with:

- a measurable view of SOC service performance and outcomes,
- incident and alert summaries (tenant-scoped),
- SLA compliance results and exceptions,
- operational health and visibility gaps,
- improvements delivered and recommendations,
- action items requiring client ownership.

Monthly reporting is critical because:

- it provides contractual service transparency and supports renewals/QBRs
- it helps clients understand their risk posture and prioritize remediation
- it creates audit-ready service evidence for client compliance programs
- it drives continuous improvement with measurable results
- it aligns MSSP operations with client expectations, constraints, and governance

This report ensures:

- consistent reporting structure month-to-month
- tenant-safe client-specific data with no cross-client disclosure
- clear linkage between metrics, incidents, and improvement actions
- actionable recommendations with ownership and timelines

---

# 3. Scope

This report covers the monthly reporting window for a single client:

| Area            | Included                                                               |
| --------------- | ---------------------------------------------------------------------- |
| Incidents       | P1–P4 incidents handled for the client                                 |
| Alerts          | High-level alert volumes and top drivers (if contract includes)        |
| SLA performance | notification and response timelines per SLA tier                       |
| SOC operations  | update cadence, escalation performance, ticket quality (as applicable) |
| Visibility      | logging and EDR coverage posture, telemetry gaps                       |
| Improvements    | tuning, detections, playbook/process improvements related to client    |
| Client actions  | pending approvals, remediation actions, hardening work                 |

Out of scope:

- detailed forensic evidence dumps (delivered only via secure evidence sharing process)
- internal MSSP cross-tenant metrics (no other client comparisons)

---

# 4. Instructions (Mandatory)

- Ensure the report is **client-specific** and **tenant-scoped**.
- Use UTC timestamps for incident timelines and reporting windows.
- Do not include sensitive evidence in the report body (raw logs/PCAP/dumps).
- Use incident IDs and evidence reference IDs/paths for traceability.
- Clearly note any data limitations (missing log sources, partial coverage).
- If client requires, provide report via client portal and track delivery.

---

# 5. Template (Copy/Paste)

## 5.1 Report Metadata (Mandatory)

| Field                  | Value                                                                  |
| ---------------------- | ---------------------------------------------------------------------- |
| Client Name            |                                                                        |
| Client ID              |                                                                        |
| SLA Tier               | Gold / Silver / Bronze (or contract label) |
| Reporting Month (UTC)  | `YYYY-MM`                                                              |
| Reporting Window (UTC) | `Start: YYYY-MM-01 00:00` → `End: YYYY-MM-last 23:59`                  |
| Prepared By (MSSP)     | Name / Role                                                            |
| Reviewed By (MSSP)     | Name / Role                                                            |
| Delivered To (Client)  | Names / Roles                                                          |
| Delivery Date (UTC)    | `YYYY-MM-DD HH:MM`                                                     |
| Delivery Method        | Email / Portal / Onsite                                                |
| Version                | 1.0                                                                    |

---

## 5.2 Executive Summary (Client-Friendly) (Mandatory)

### A) Monthly Snapshot (Non-Technical)

- `3–8 bullets summarizing key security outcomes and risks`

### B) Overall Posture

- **Client posture:** Green / Amber / Red  
- **Rationale:** `...`

### C) Top 3 Client Risks (Month)

1. `...`
2. `...`
3. `...`

### D) Key MSSP Outcomes (Value Delivered)

- `...`

---

## 5.3 Incident Summary (Tenant-Scoped) (Mandatory)

### A) Incident Volumes by Severity

| Metric            | P1  | P2  | P3  | P4  | Total |
| ----------------- | ---:| ---:| ---:| ---:| -----:|
| Incidents opened  |     |     |     |     |       |
| Incidents closed  |     |     |     |     |       |
| Open at month end |     |     |     |     |       |

### B) Incidents by Category

| Category          | Count | %   | Notes |
| ----------------- | -----:| ---:| ----- |
| Phishing/BEC      |       |     |       |
| Malware           |       |     |       |
| Credential attack |       |     |       |
| Cloud incident    |       |     |       |
| Intrusion         |       |     |       |
| Other             |       |     |       |

### C) Notable Incidents (P1/P2 + Significant P3)

| Incident ID | Severity | Category | Dates (UTC) | Outcome | Impact Summary | Client Action Required |
| ----------- | -------- | -------- | ----------- | ------- | -------------- | ---------------------- |
|             |          |          |             |         |                |                        |

For each P1/P2, include a short summary:

- `What happened (confirmed)`
- `What was impacted`
- `Actions taken`
- `Validation performed`
- `Residual risk`

---

## 5.4 Alerting Summary (If Included in Contract) (Recommended)

> Keep high-level. Avoid listing every alert.

### A) Alert Volumes by Source

| Source          | Total Alerts | Actionable | % Actionable | Notes |
| --------------- | ------------:| ----------:| ------------:| ----- |
| SIEM            |              |            |              |       |
| EDR             |              |            |              |       |
| Email security  |              |            |              |       |
| Network sensors |              |            |              |       |

### B) Top Alert Drivers (Top 5)

| Rank | Alert/Rule | Volume | FP Trend (Up/Down/Stable) | Action Taken |
| ----:| ---------- | ------:| ------------------------- | ------------ |
| 1    |            |        |                           |              |
| 2    |            |        |                           |              |

---

## 5.5 SLA and Service Performance (Mandatory)

### A) SLA KPI Summary

| SLA Metric                   | Target | Achieved | Notes |
| ---------------------------- | ------:| --------:| ----- |
| Initial notification (P1)    |        |          |       |
| Initial notification (P2)    |        |          |       |
| Update cadence (P1)          |        |          |       |
| Update cadence (P2)          |        |          |       |
| Acknowledgment time          |        |          |       |
| Resolution time (if defined) |        |          |       |

### B) SLA Exceptions (If Any)

| Incident ID | SLA Metric | Exception Reason | Client Impact | Corrective Action |
| ----------- | ---------- | ---------------- | ------------- | ----------------- |
|             |            |                  |               |                   |

---

## 5.6 Visibility and Coverage Review (Mandatory)

### A) Telemetry Coverage Snapshot (Client-Specific)

| Control/Telemetry                    | Status (OK/Gap) | Details | Risk | Recommendation | Owner |
| ------------------------------------ | --------------- | ------- | ---- | -------------- | ----- |
| EDR coverage (critical assets)       |                 |         |      |                |       |
| SIEM log coverage (critical sources) |                 |         |      |                |       |
| Firewall/Proxy/DNS logging           |                 |         |      |                |       |
| Cloud audit logs                     |                 |         |      |                |       |
| MFA/SSO telemetry                    |                 |         |      |                |       |

### B) Data Limitations (Mandatory if any)

- `Missing logs from X source`
- `Retention insufficient for Y investigation`
- `Asset inventory not updated`

---

## 5.7 Security Improvement Activities (Mandatory)

### A) Improvements Delivered by MSSP (Month)

| Improvement | Category (Detect/Respond) | Benefit | Status | Date (UTC) | Notes |
| ----------- | ------------------------- | ------- | ------ | ----------:| ----- |
|             |                           |         |        |            |       |

### B) Recommendations for Client Hardening (Month) (Mandatory)

| Recommendation | Priority     | Client Owner | Due (UTC) | Notes |
| -------------- | ------------ | ------------ | ---------:| ----- |
|                | High/Med/Low |              |           |       |

Examples:

- enforce MFA for admin accounts
- close exposed services
- patch critical vulnerabilities
- deploy EDR to remaining critical servers
- increase log retention for key sources

---

## 5.8 Client Action Items and Pending Approvals (Mandatory)

### A) Pending Approvals (Containment / Evidence / Changes)

| Approval Needed | Incident ID | Requested At (UTC) | Status | Risk if Delayed |
| --------------- | ----------- | ------------------:| ------ | --------------- |
|                 |             |                    |        |                 |

### B) Action Items Tracker

| #   | Action Item | Owner (Client/MSSP) | Priority | Due (UTC) | Status |
| ---:| ----------- | ------------------- | -------- | ---------:| ------ |
| 1   |             |                     |          |           |        |
| 2   |             |                     |          |           |        |

---

## 5.9 Roadmap (Next Month) (Recommended)

| Initiative | Objective | Owner | Target Date (UTC) | Notes |
| ---------- | --------- | ----- | -----------------:| ----- |
|            |           |       |                   |       |

---

## 5.10 Appendix (Optional)

- Incident list (IDs only)
- KPI definitions
- Client-approved IoC appendix reference
- Evidence package references (IDs only)

---

# 6. Confidentiality and Distribution (Mandatory)

- This report is **Client Confidential**.
- Distribution must be limited to client-approved recipients.
- Report must not include any other client information or MSSP internal sensitive details beyond what is necessary.

---

# 7. Related Documents

| Document                         | Path                                                                                      |
| -------------------------------- | ----------------------------------------------------------------------------------------- |
| MSSP Executive Briefing Template | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Executive-Briefing-Template.md`               |
| MSSP Incident Report Template    | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Incident-Report-Template.md`                  |
| MSSP SLA Compliance Report       | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-SLA-Compliance-Report.md`                     |
| MSSP Client Evidence Handling    | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md` |
| Internal-to-MSSP Escalation      | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`    |
| Client Data Segregation Policy   | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`         |

---

# 8. Revision History

| Version | Date        | Author                 | Changes         |
| ------- | ----------- | ---------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP SDM / SOC Manager | Initial version |

---

# 9. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
