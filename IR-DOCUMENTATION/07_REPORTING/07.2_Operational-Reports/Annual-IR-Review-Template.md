# Annual IR Review Template (Incident Response Program Review)

---

# 1. Document Control

| Field          | Value                          |
| -------------- | ------------------------------ |
| Document Name  | Template – Annual IR Review    |
| Document ID    | RPT-OPS-005                    |
| Version        | 1.0                            |
| Effective Date | 30-May-2026                    |
| Owner          | SOC Manager / IR Program Owner |
| Approved By    | CISO                           |
| Classification | Internal – Confidential        |
| Review Cycle   | Annual                         |

---

# 2. Purpose

This template defines the annual review structure for the organization’s **Incident Response (IR) Program** to ensure the program remains:

- operationally effective,
- compliant with relevant frameworks and regulatory expectations (ISO 27001, NIST, RBI, CERT-In as applicable),
- audit-ready, and
- continuously improving based on incident learnings and evolving threats.

The annual IR review is critical because:

- it provides formal governance evidence for audits and management review
- it validates whether the IR program is meeting SLA/SLO and business requirements
- it confirms that playbooks, escalation paths, and evidence handling remain fit-for-purpose
- it identifies systemic gaps and prioritizes investments and improvements for the next year
- it supports MSSP service maturity and client assurance where applicable

This template ensures:

- consistent annual review structure year-over-year
- clear ownership and accountability for improvement actions
- linkage to evidence (incident reports, KPIs, PIRs, audits, training, drills)
- measurable outcomes and maturity tracking

---

# 3. Scope

This annual review covers:

| Review Area                   | Included                                                                       |
| ----------------------------- | ------------------------------------------------------------------------------ |
| Governance and policy         | IR policy, roles/RACI, SLAs/SLOs, exceptions                                   |
| Operational performance       | incident volumes, MTTA/MTTR, SLA compliance, backlog, QA                       |
| Incident quality              | accuracy of severity classification, documentation quality, evidence practices |
| Detection and tooling         | SIEM/EDR effectiveness, logging coverage, TI integration, tuning maturity      |
| Response capability           | containment authority, recovery coordination, bridge call effectiveness        |
| Post-incident improvement     | PIR/RCA completion, improvement closure rate, trend management                 |
| Training and exercises        | onboarding, tabletop, drills, red/purple engagements                           |
| Compliance and audit          | ISO audits, RBI inspections, client audits, evidence packages                  |
| MSSP delivery (if applicable) | client SLAs, tenant segregation controls, client reporting maturity            |

Out of scope:

- enterprise risk assessment (unless specifically requested)
- non-security IT operational reviews not related to IR

---

# 4. Instructions (Mandatory)

- Reporting window must be explicitly stated in UTC.
- Use supporting evidence references (reports, tickets, KPI exports, audit outcomes) rather than anecdotal statements.
- Clearly distinguish:
  - what is **measured**
  - what is **observed**
  - what is **assumed**
- Provide an action plan with owners, due dates, and tracking references.
- If this report will be used for external assurance (client/audit), create a sanitized external version.

---

# 5. Template (Copy/Paste)

## 5.1 Review Metadata (Mandatory)

| Field                                | Value                                                           |
| ------------------------------------ | --------------------------------------------------------------- |
| Review Year                          | `YYYY`                                                          |
| Review Window (UTC)                  | `Start: YYYY-01-01 00:00` → `End: YYYY-12-31 23:59`             |
| Prepared By                          | `Name / Role`                                                   |
| Contributors                         | `SOC Lead, IR Lead, TI Lead, SIEM/EDR owners, Compliance, etc.` |
| Reviewed By                          | `Name / Role`                                                   |
| Approved By                          | `CISO`                                                          |
| Scope                                | Internal / MSSP / Both                                          |
| Document Location                    | `Link/path`                                                     |
| Supporting Evidence Package Location | `Link/path`                                                     |

---

## 5.2 Executive Summary (Mandatory)

### A) Program Health Statement

- **Overall IR maturity posture:** Green / Amber / Red  
- **Summary rationale (5–10 bullets):**
  - `...`

### B) Major Achievements (Year)

- `Achievement 1`
- `Achievement 2`

### C) Key Risks and Gaps (Year)

1. `...`
2. `...`

### D) Strategic Priorities (Next Year)

1. `...`
2. `...`

### E) Decisions Required from Leadership

| Decision | Why | Options | Recommendation | Needed By (UTC) |
| -------- | --- | ------- | -------------- | ---------------:|
|          |     |         |                |                 |

---

## 5.3 IR Program Governance Review (Mandatory)

### A) Policy and Standard Review

| Document                   | Current Version | Last Review Date | Changes Needed? | Notes |
| -------------------------- | ---------------:| ----------------:| --------------- | ----- |
| IR Policy Master           |                 |                  | Yes/No          |       |
| NIST Alignment             |                 |                  |                 |       |
| ISO 27001 Alignment        |                 |                  |                 |       |
| RBI Alignment              |                 |                  |                 |       |
| Evidence Handling Policies |                 |                  |                 |       |
| Ticketing SOPs             |                 |                  |                 |       |

References:
`00_GOVERNANCE/00.1_Policies/`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

### B) Roles, RACI, and Authority Review

- Are roles and responsibilities current? `Yes/No`
- Are containment authorities clear and used correctly? `Yes/No`
- Any conflicts/gaps identified? `...`

Reference:
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx`  
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

### C) SLA/SLO Review

| SLA/SLO           | Target | Achieved (Year Avg) | Trend | Notes |
| ----------------- | ------:| -------------------:| ----- | ----- |
| MTTA              |        |                     |       |       |
| MTTR              |        |                     |       |       |
| P1 update cadence |        |                     |       |       |
| P2 update cadence |        |                     |       |       |

References:
`00_GOVERNANCE/00.4_SLA-and-SLO/`

### D) Policy Exceptions Review

| Metric                        | Value | Notes |
| ----------------------------- | -----:| ----- |
| Total exceptions requested    |       |       |
| Active exceptions end-of-year |       |       |
| High/Critical risk exceptions |       |       |
| Exceptions overdue for review |       |       |

Reference:
`00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`

---

## 5.4 Incident Statistics and Operational Performance (Mandatory)

### A) Incident Volumes (Year)

| Metric                   | P1  | P2  | P3  | P4  | Total |
| ------------------------ | ---:| ---:| ---:| ---:| -----:|
| Incidents opened         |     |     |     |     |       |
| Incidents closed         |     |     |     |     |       |
| Still open (end-of-year) |     |     |     |     |       |
| Reopened incidents       |     |     |     |     |       |

### B) Incident Categories (Top 10)

| Category | Count | %   | YoY Trend | Notes |
| -------- | -----:| ---:| --------- | ----- |
|          |       |     |           |       |

### C) Performance and Throughput

| KPI                 | Value | Target | Notes |
| ------------------- | -----:| ------:| ----- |
| MTTA                |       |        |       |
| Mean time to triage |       |        |       |
| MTTR                |       |        |       |
| Tickets created     |       |        |       |
| Tickets closed      |       |        |       |
| Backlog (avg)       |       |        |       |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

### D) SLA Breach Review (Mandatory)

| Breach Theme                  | Count | Root Cause | Corrective Actions Completed? | Notes |
| ----------------------------- | -----:| ---------- | ----------------------------- | ----- |
| Staffing/coverage             |       |            | Yes/No                        |       |
| Tool outages                  |       |            |                               |       |
| Client approval delays (MSSP) |       |            |                               |       |
| Process gaps                  |       |            |                               |       |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLA-Breach-Escalation-Procedure.md`

### E) Ticket Quality Review (Mandatory)

| QA Metric                           | Result | Target | Notes |
| ----------------------------------- | ------:| ------:| ----- |
| % tickets with complete fields      |        |        |       |
| % tickets with evidence references  |        |        |       |
| % tickets with correct closure code |        |        |       |
| Severity reassessment compliance    |        |        |       |

References:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/`

---

## 5.5 Incident Lifecycle Effectiveness Review (Mandatory)

Review each lifecycle stage and document what worked and what did not.

### A) Detection & Declaration

- Were incidents detected in time? `Yes/No`
- Were severity assignments accurate? `...`
- Key recurring issues:
  - `...`

### B) Containment

- Average time to containment (P1/P2): `...`
- Containment actions executed under authority matrix? `Yes/No`
- Issues (approvals, tooling, scope errors):
  - `...`

### C) Eradication

- Common eradication challenges:
  - `patching delays`
  - `persistence missed`
  - `re-infection risk`

### D) Recovery

- Recovery quality and stability issues:
  - `restore failures`
  - `verification gaps`
  - `DR coordination issues`

### E) Post-Incident Activity

- PIR completion rate and action closure:
  - `...`

References:
`02_PLAYBOOKS/`  
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Closure-Criteria.md`  
`08_POST-INCIDENT/`

---

## 5.6 Threat Landscape and Intelligence Review (Mandatory)

### A) Top Threat Themes (Year)

- `Theme 1 (phishing/BEC patterns)`
- `Theme 2 (credential stuffing)`
- `Theme 3 (ransomware trends)`
- `Theme 4 (cloud IAM abuse)`

### B) MITRE ATT&CK Trend (Optional but Recommended)

| Technique | Frequency | Trend | Notes |
| --------- | ---------:| ----- | ----- |
|           |           |       |       |

Reference:
`10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`

### C) TI Program Effectiveness

| Metric                          | Value | Notes |
| ------------------------------- | -----:| ----- |
| # of actionable TI alerts       |       |       |
| IOC match rate leading to TP    |       |       |
| Feed outages                    |       |       |
| Time to operationalize new IOCs |       |       |

References:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/`

---

## 5.7 Tooling and Telemetry Review (Mandatory)

### A) SIEM Program Review

- Coverage: critical log sources onboarded? `Yes/No`
- Parsing/normalization quality issues: `...`
- Use-case library maturity: `...`
- Significant outages and impact: `...`

References:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/`

### B) EDR Program Review

- Coverage of critical assets: `%`
- Policy hygiene and exclusions: `...`
- Response capability (isolation/kill): validated? `Yes/No`
- Gaps: `...`

References:
`04_TOOLS-AND-TECHNOLOGY/04.2_EDR/`

### C) Network Telemetry Review

- Firewall/proxy logging stability: `...`
- IDS/IPS tuning maturity: `...`
- Capture capability readiness: `...`

References:
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/`

### D) Ticketing and Workflow Review

- Ticket field completeness and workflow adherence: `...`
- Automation/templating opportunities: `...`

References:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/`

---

## 5.8 Evidence Handling and CoC Review (Mandatory)

### A) Evidence Storage and Integrity

- Evidence vault access control and logging: `OK/Needs improvement`
- Hashing compliance (P1/P2 evidence-grade): `%`
- Evidence retrieval and audit readiness: `...`

### B) Chain-of-Custody Compliance

| Metric                     | Value | Notes |
| -------------------------- | -----:| ----- |
| # incidents requiring CoC  |       |       |
| CoC completed correctly    |       |       |
| Transfer form completeness |       |       |

References:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 5.9 Training, Exercises, and Readiness Review (Mandatory)

### A) Staffing and Competency

- Staffing model changes needed? `Yes/No`
- Skills gaps identified: `...`
- Training plan execution status: `...`

### B) Tabletop Exercises (TTX)

| Exercise       | Date | Attendance | Score/Outcome | Actions |
| -------------- | --------------------------------:| ----------:| ------------- | ------- |
| Ransomware TTX |                                  |            |               |         |
| APT TTX        |                                  |            |               |         |

References:
`10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/`

### C) Drills and Red/Purple Engagements

| Drill | Date | Result | Improvements Logged |
| ----- | ----:| ------ | ------------------- |
|       |      |        |                     |

Reference:
`10_TRAINING-AND-EXERCISES/10.3_Drills/`

---

## 5.10 Compliance and Audit Review (Mandatory)

### A) Audit Activities and Findings

| Audit/Assessment      | Date | Findings Count | Severity | Closure Status |
| --------------------- | ----:| --------------:| -------- | -------------- |
| ISO 27001 audit       |      |                |          |                |
| RBI compliance review |      |                |          |                |
| Client audit (MSSP)   |      |                |          |                |

### B) Regulatory Reporting Performance (If Applicable)

| Regulator | # Reports | On-time % | Issues/Delays | Improvements |
| --------- | ---------:| ---------:| ------------- | ------------ |
| CERT-In   |           |           |               |              |
| RBI       |           |           |               |              |

References:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`  
`11_ARCHIVE/11.3_Audit-Records/`

---

## 5.11 MSSP Program Review (If Applicable) (Mandatory for MSSP)

### A) Client SLA Performance

| Client SLA Tier | Compliance % | Notes |
| --------------- | ------------:| ----- |
| Gold            |              |       |
| Silver          |              |       |
| Bronze          |              |       |

### B) Tenant Segregation and Cross-Client Risk

- Any segregation incidents? `Yes/No`
- Evidence segregation audits performed? `Yes/No`
- Actions taken: `...`

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

## 5.12 Improvement Roadmap (Next Year) (Mandatory)

### A) Improvement Themes (Top 6–10)

1. `...`
2. `...`

### B) Detailed Roadmap Table

| Initiative                       | Objective                  | Benefit          | Owner    | Priority | Target Quarter | Tracking Ref |
| -------------------------------- | -------------------------- | ---------------- | -------- | -------- | -------------- | ------------ |
| Improve SIEM onboarding coverage | Add critical sources       | Better detection | SIEM Eng | High     | Q1             | CTRL-GAP-... |
| Reduce FP rate for top rules     | Improve analyst efficiency | Reduced backlog  | SOC Lead | Med      | Q2             | DET-IMP-...  |

### C) Resource/Investment Requirements

- Headcount: `...`
- Tooling: `...`
- Training: `...`

---

## 5.13 Appendices (Optional but Recommended)

- KPI calculation definitions
- list of all P1/P2 incident IDs for the year
- list of open improvement actions and status
- maturity assessment results (if performed)

---

# 6. Related Documents

| Document                  | Path                                                                      |
| ------------------------- | ------------------------------------------------------------------------- |
| Daily SOC Report Template | `07_REPORTING/07.2_Operational-Reports/Daily-SOC-Report-Template.md`      |
| Monthly Metrics Report    | `07_REPORTING/07.2_Operational-Reports/Monthly-Metrics-Report.md`         |
| Quarterly Trend Analysis  | `07_REPORTING/07.2_Operational-Reports/Quarterly-Trend-Analysis.md`       |
| Lessons Learned Register  | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Register.xlsx`     |
| RCA Template              | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`               |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |
| Control Gap Tracker       | `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`     |
| Policy Exception Register | `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`                |
| IR Policy Master          | `00_GOVERNANCE/00.1_Policies/IR-Policy-Master.md`                         |
| Audit Records             | `11_ARCHIVE/11.3_Audit-Records/`                                          |

---

# 7. Revision History

| Version | Date        | Author                         | Changes         |
| ------- | ----------- | ------------------------------ | --------------- |
| 1.0     | 30-May-2026 | SOC Manager / IR Program Owner | Initial version |

---

# 8. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
