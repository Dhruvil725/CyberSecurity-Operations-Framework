# MSSP Executive Briefing Template

---

# 1. Document Control

| Field          | Value                                             |
| -------------- | ------------------------------------------------- |
| Document Name  | Template – MSSP Executive Briefing                |
| Document ID    | RPT-MSSP-001                                      |
| Version        | 1.0                                               |
| Effective Date | 30-May-2026                                       |
| Owner          | MSSP Service Delivery Manager (SDM) / SOC Manager |
| Approved By    | CISO (or MSSP Program Head – delegated)           |
| Classification | Client Confidential                               |
| Review Cycle   | Quarterly                                         |

---

# 2. Purpose

This template standardizes the **MSSP Executive Briefing** delivered to client leadership (CISO/CIO/CTO/IT Head) to communicate:

- security posture and risk themes (non-technical),
- key incidents and outcomes (tenant-scoped),
- SLA and service performance,
- improvements delivered and roadmap,
- decisions required from the client (approvals, investments, access).

This briefing is critical because:

- executive audiences need clear risk and impact, not raw SOC details
- it supports contractual transparency and strengthens governance
- it provides traceable service evidence for audits and client assurance
- it aligns operational outcomes (SOC activity) with business priorities
- it improves decision-making by identifying client blockers and required actions

This template ensures:

- consistent structure and messaging across clients
- tenant-safe summaries without cross-client disclosure
- measurable, evidence-backed claims and KPIs
- clear next steps and ownership for client-side actions

---

# 3. Scope

Use this template for:

| Scenario                                   | Frequency                                          |
| ------------------------------------------ | -------------------------------------------------- |
| Executive monthly/quarterly service review | Monthly or Quarterly (contract-driven)             |
| After major incident                       | Within 5–10 business days of closure (recommended) |
| Renewal / QBR (quarterly business review)  | Quarterly                                          |
| Audit support briefing                     | As requested                                       |

Out of scope:

- detailed forensic findings (use MSSP incident report template or technical annex)
- daily/weekly operational reporting (covered elsewhere)

---

# 4. Instructions (Mandatory)

- Ensure all content is **client-specific** and **tenant-scoped**.
- Use UTC timestamps for incident timelines.
- Do not include:
  - raw logs/PCAP/memory dumps,
  - other clients’ data,
  - sensitive internal MSSP tooling details beyond what is needed.
- Use references:
  - incident IDs,
  - high-level evidence references,
  - action tracker IDs.
- Include “limitations” section for visibility gaps or client constraints.

---

# 5. Template (Copy/Paste)

## 5.1 Briefing Metadata (Mandatory)

| Field                  | Value                                               |
| ---------------------- | --------------------------------------------------- |
| Client Name            |                                                     |
| Client ID              |                                                     |
| SLA Tier               | Gold / Silver / Bronze (or contract label)          |
| Briefing Type          | Monthly / Quarterly / Post-Incident / Renewal       |
| Reporting Window (UTC) | `Start: YYYY-MM-DD 00:00` → `End: YYYY-MM-DD 23:59` |
| Prepared By (MSSP)     | Name / Role                                         |
| Presented By (MSSP)    | Name / Role                                         |
| Client Attendees       | Names / Roles                                       |
| Delivery Method        | Call / Onsite / Slide deck / Document               |
| Version                | 1.0                                                 |
| Date (UTC)             | `YYYY-MM-DD HH:MM`                                  |

---

## 5.2 Executive Summary (Mandatory)

### A) Current Security Posture (Client Environment)

- **Overall posture:** Green / Amber / Red  
- **Rationale (3–6 bullets):**
  - `...`

### B) Top Risk Themes (Client-Specific)

1. `...`
2. `...`
3. `...`

### C) Outcomes Delivered (MSSP Value)

- `Key outcomes delivered during this period`
- Examples:
  - `Reduced response time by X%`
  - `Improved detection coverage for Y`
  - `Resolved Z recurring false positives`

---

## 5.3 Key Incidents and Outcomes (Tenant-Scoped) (Mandatory)

> Include all P1/P2 and major P3 incidents.

| Incident ID | Severity | Category | Date(s) (UTC) | Outcome          | Impact Summary | Client Actions Required (Completed?) |
| ----------- | -------- | -------- | ------------- | ---------------- | -------------- | ------------------------------------ |
| INC-        | P1       |          |               | Closed/Contained |                | Yes/No                               |
| INC-        | P2       |          |               |                  |                |                                      |

For each P1, add 3–5 bullets:

- `What happened (confirmed)`
- `What was impacted`
- `What was done (containment → recovery)`
- `Validation performed`
- `Residual risk and monitoring`

---

## 5.4 Threat Landscape Highlights (Relevant to Client) (Recommended)

### A) Threat Trends (Period)

- `Phishing/BEC targeting pattern`
- `Credential stuffing against VPN/SSO`
- `Ransomware campaigns in sector`

### B) Top TTPs Observed (If Applicable)

| Technique/Pattern        | Observed? | Notes |
| ------------------------ | --------- | ----- |
| Privileged account abuse | Yes/No    |       |
| Suspicious PowerShell    | Yes/No    |       |
| Cloud IAM misuse         | Yes/No    |       |

---

## 5.5 Service Performance and SLA Summary (Mandatory)

### A) SLA Performance Snapshot

| SLA Metric                    | Target | Achieved | Notes |
| ----------------------------- | ------:| --------:| ----- |
| Time to acknowledge (MTTA)    |        |          |       |
| Time to triage                |        |          |       |
| Update cadence (P1/P2)        |        |          |       |
| Incident reporting timeliness |        |          |       |

### B) SLA Exceptions (If Any)

| Period | Incident ID | SLA Type | Reason | Mitigation | Preventive Action |
| ------ | ----------- | -------- | ------ | ---------- | ----------------- |
|        |             |          |        |            |                   |

Reference:
`07_REPORTING/07.3_MSSP-Client-Reports/MSSP-SLA-Compliance-Report.md`

---

## 5.6 Operational Health and Visibility (Mandatory)

### A) Monitoring Coverage Status (Client-Specific)

| Control/Telemetry                    | Status (OK/Gap) | Details | Risk | Recommended Action | Owner |
| ------------------------------------ | --------------- | ------- | ---- | ------------------ | ----- |
| SIEM log coverage (critical sources) |                 |         |      |                    |       |
| EDR coverage (critical assets)       |                 |         |      |                    |       |
| DNS/Proxy/Firewall logging           |                 |         |      |                    |       |
| Cloud audit logs                     |                 |         |      |                    |       |

### B) Constraints and Limitations (Mandatory)

- `Example: EDR not deployed on X due to vendor restriction`
- `Example: log retention limited to Y days`
- `Example: client approval delays impacted containment`

---

## 5.7 Improvements Delivered (MSSP Actions) (Mandatory)

### A) Detection/Use-Case Improvements

| Improvement | Benefit | Date (UTC) | Status | Notes |
| ----------- | ------- | ----------:| ------ | ----- |
|             |         |            |        |       |

### B) Tuning / False Positive Reduction

| Tuning Item | Impact | Status | Notes |
| ----------- | ------ | ------ | ----- |
|             |        |        |       |

### C) Process Improvements

- `Improvement 1`
- `Improvement 2`

---

## 5.8 Client Required Actions and Decisions (Mandatory)

> These must be clear, time-bound, and assigned.

### A) Actions Required from Client

| Action | Why | Priority     | Due (UTC) | Client Owner | Status |
| ------ | --- | ------------ | ---------:| ------------ | ------ |
|        |     | High/Med/Low |           |              |        |

### B) Decisions Required from Client Leadership

| Decision Needed | Options | Recommendation | Needed By (UTC) | Decision Owner | Status |
| --------------- | ------- | -------------- | ---------------:| -------------- | ------ |
|                 |         |                |                 |                |        |

Examples:

- Approve EDR rollout to remaining assets
- Approve increased log retention
- Approve new alerting/response automation
- Approve incident containment authorities for P1

---

## 5.9 Roadmap (Next Period) (Recommended)

| Initiative | Objective | Expected Benefit | Owner (MSSP/Client) | Target Date (UTC) |
| ---------- | --------- | ---------------- | ------------------- | -----------------:|
|            |           |                  |                     |                   |

---

## 5.10 Appendix (Optional)

- Incident list (IDs only)
- KPI definitions
- Top noisy detections and tuning status
- Client-specific improvement tracker snapshot

---

# 6. Quality and Compliance Notes (Mandatory)

- This document is **Client Confidential** and must not be shared outside authorized recipients.
- All incident summaries must be tenant-scoped and validated for confidentiality.
- Where metrics are estimated or incomplete, explicitly state limitations.

---

# 7. Related Documents

| Document                        | Path                                                                                   |
| ------------------------------- | -------------------------------------------------------------------------------------- |
| MSSP Monthly Client Report      | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Monthly-Client-Report.md`                  |
| MSSP Incident Report Template   | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Incident-Report-Template.md`               |
| MSSP SLA Compliance Report      | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-SLA-Compliance-Report.md`                  |
| Internal-to-MSSP Escalation SOP | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md` |
| Client Data Segregation Policy  | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`      |

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
