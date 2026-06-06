# Detection Improvement Log

---

# 1. Document Control

| Field          | Value                                    |
| -------------- | ---------------------------------------- |
| Document Name  | Register – Detection Improvement Log     |
| Document ID    | IMP-DET-001                              |
| Version        | 1.0                                      |
| Effective Date | 30-May-2026                              |
| Owner          | Detection Engineering Lead / SOC Manager |
| Approved By    | CISO                                     |
| Classification | Internal – Confidential                  |
| Review Cycle   | Monthly                                  |

---

# 2. Purpose

This document provides the standardized **Detection Improvement Log** register to track all detection engineering improvements arising from incidents, threat intelligence, red/purple team exercises, threat hunting, and continuous improvement initiatives.

A formal detection improvement log is critical because:

- detection gaps are the leading cause of delayed incident detection (high dwell time)
- post-incident lessons must translate into measurable detection enhancements
- NIST CSF Detect (DE) function requires continuous improvement of detection capability
- ISO 27001 Annex A.5.27 mandates learning from incidents
- RBI Cyber Security Framework expects detection capability maturity
- MITRE ATT&CK coverage must be tracked and improved
- audit trail required for detection rule lifecycle (creation, tuning, retirement)
- MSSP clients expect detection enhancement evidence
- repeated incidents indicate uncaptured or unimplemented detection improvements

This register ensures:

- consistent tracking of all detection improvements
- traceability from incident/source to detection rule
- versioning of detection rules
- measurable detection coverage improvements
- MITRE ATT&CK alignment
- linkage to RCA, Lessons Learned, and threat intel
- audit-ready evidence of detection engineering activity

Reference alignment:
`08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md`

---

# 3. Scope

This log covers detection improvements across:

| Source                     | Examples                                     |
| -------------------------- | -------------------------------------------- |
| Incident-driven            | New rules from RCA findings                  |
| Threat intel-driven        | IOC-based detection, TTP detection           |
| Red/Purple team-driven     | Detection gaps identified during exercises   |
| Threat hunting-driven      | Hypothesis-based hunt outcomes               |
| Compliance-driven          | Regulatory required detection (RBI, PCI-DSS) |
| Vendor advisory-driven     | Critical CVE detection                       |
| Continuous improvement     | Tuning, false positive reduction             |
| MITRE ATT&CK gap analysis  | Coverage improvement                         |
| Tabletop exercise findings | Detection scenarios identified               |

Detection platforms covered:

| Platform          | Examples                                        |
| ----------------- | ----------------------------------------------- |
| SIEM              | Splunk, QRadar, Sentinel, Elastic               |
| EDR               | CrowdStrike, SentinelOne, Defender for Endpoint |
| Network Detection | NDR, IDS/IPS, NSM                               |
| Cloud Security    | CSPM, CWPP, CNAPP                               |
| Email Security    | Proofpoint, Mimecast, M365 Defender             |
| Identity          | UEBA, ITDR, IAM analytics                       |
| DLP               | Endpoint DLP, Network DLP                       |

Out of scope:

- routine alert tuning without rule creation/modification (tracked separately in tuning log)
- non-security detection (operational monitoring)

---

# 4. Definitions

| Term                  | Definition                                                        |
| --------------------- | ----------------------------------------------------------------- |
| Detection Rule        | Logic configured in security tool to identify suspicious activity |
| Use Case              | Documented detection scenario with rule, response, and tuning     |
| Detection Gap         | Missing detection capability for a known threat or technique      |
| MITRE ATT&CK Coverage | Percentage of relevant ATT&CK techniques detected                 |
| Rule Lifecycle        | Creation → Testing → Production → Tuning → Retirement             |
| Detection Source      | System/tool where rule is implemented                             |
| False Positive Rate   | Percentage of alerts that are not actual threats                  |
| True Positive Rate    | Percentage of actual threats correctly detected                   |
| Detection Engineer    | Role responsible for developing and maintaining detection rules   |
| Sigma Rule            | Generic open-source detection rule format                         |

---

# 5. Roles and Responsibilities

| Role                       | Responsibilities                                      |
| -------------------------- | ----------------------------------------------------- |
| Detection Engineering Lead | Owns log; prioritizes improvements; assigns engineers |
| Detection Engineer         | Develops, tests, deploys detection rules              |
| L3 Analyst                 | Identifies detection gaps; validates rules            |
| Threat Hunter              | Provides hunt-based detection improvements            |
| Threat Intel Analyst       | Provides intel-driven detection requirements          |
| Red/Purple Team            | Identifies detection gaps via exercises               |
| SOC Lead                   | Validates production deployment readiness             |
| SOC Manager                | Approves rule production; reviews log monthly         |
| CISO                       | Reviews quarterly metrics                             |
| Compliance Lead            | Validates regulatory detection requirements           |
| MSSP SDM (if applicable)   | Coordinates client-specific detection improvements    |

---

# 6. Detection Improvement Lifecycle (Mandatory)

| Phase                 | Activities                                      | Owner                   | Output                    |
| --------------------- | ----------------------------------------------- | ----------------------- | ------------------------- |
| **1. Identification** | Gap identified from incident/intel/hunt         | L3 / Threat Hunter / IR | Improvement entry created |
| **2. Prioritization** | Risk-based prioritization                       | Detection Eng Lead      | Priority assigned         |
| **3. Design**         | Rule logic designed | Detection Engineer      | Detection design doc      |
| **4. Development**    | Rule implemented in tool                        | Detection Engineer      | Draft rule                |
| **5. Testing**        | Tested in non-prod / lab                        | Detection Engineer      | Test results              |
| **6. Validation**     | Validated against test data / red team          | L3 Analyst              | Validation report         |
| **7. Deployment**     | Deployed to production                          | Detection Engineer      | Production rule           |
| **8. Tuning**         | Tuned based on FP/TP feedback                   | Detection Engineer      | Tuned rule                |
| **9. Monitoring**     | Performance monitored                           | SOC Lead                | Performance metrics       |
| **10. Retirement**    | Retired when obsolete                           | Detection Eng Lead      | Retirement record         |

---

# 7. Logging Principles (Mandatory)

| Principle              | Requirement                                                  |
| ---------------------- | ------------------------------------------------------------ |
| Single source of truth | This log is the authoritative detection improvement register |
| Traceable to source    | Every entry links to incident/intel/hunt/exercise            |
| Versioned              | Detection rules have version history                         |
| MITRE-aligned          | Mapped to ATT&CK techniques where applicable                 |
| Measurable             | Performance metrics tracked (FP/TP rates)                    |
| Time-bound             | Target dates with status tracking                            |
| Reviewed               | Monthly review by Detection Eng Lead                         |
| MSSP-segregated        | Client-specific improvements scoped to tenant                |

---

# 8. Detection Improvement Register Template (Copy/Paste)

## 8.1 Register Schema (Mandatory Fields)

| Field                   | Description                                                                                 |
| ----------------------- | ------------------------------------------------------------------------------------------- |
| Improvement ID          | Unique identifier (`DET-IMP-YYYY-####`)                                                     |
| Date Identified (UTC)   | When improvement was identified                                                             |
| Source                  | Incident / Intel / Hunt / Exercise / Compliance / Tuning                                    |
| Source Reference        | INC-####, TI-####, HUNT-####, EX-####                                                       |
| Title                   | Brief title of improvement                                                                  |
| Description             | Detailed description of detection gap and improvement                                       |
| Threat Addressed        | Threat actor / Malware / Technique addressed                                                |
| MITRE Tactic            | Initial Access / Execution / Persistence / etc.                                             |
| MITRE Technique         | T#### (e.g., T1078)                                                                         |
| MITRE Sub-Technique     | T####.### (e.g., T1078.004)                                                                 |
| Detection Platform      | SIEM / EDR / NDR / Email / Cloud / Identity                                                 |
| Specific Tool           | Splunk / Sentinel / CrowdStrike / etc.                                                      |
| Rule Name               | Name of detection rule                                                                      |
| Rule Logic Summary      | Brief description of detection logic                                                        |
| Data Source(s) Required | Logs/telemetry required (Windows Event, sysmon, firewall, etc.)                             |
| Status                  | Identified / In Design / In Development / Testing / Validated / Deployed / Tuning / Retired |
| Priority                | Critical / High / Medium / Low                                                              |
| Owner                   | Assigned Detection Engineer                                                                 |
| Target Deployment Date  | YYYY-MM-DD                                                                                  |
| Actual Deployment Date  | YYYY-MM-DD                                                                                  |
| Rule Version            | v1.0 / v1.1 / etc.                                                                          |
| FP Rate (Initial)       | % at initial deployment                                                                     |
| FP Rate (Current)       | Current %                                                                                   |
| TP Validated            | Yes / No                                                                                    |
| Tuning Iterations       | Count                                                                                       |
| Linked RCA              | RCA-YYYY-####                                                                               |
| Linked LL               | LL-YYYY-####                                                                                |
| Linked CA               | CA-####                                                                                     |
| Test Coverage           | Atomic Red Team / Caldera / Manual                                                          |
| Notes                   | Additional context                                                                          |

---

## 8.2 Register Table (Copy/Paste)

| Improvement ID    | Date Identified | Source       | Source Ref | Title | Description | Threat | MITRE Tactic | MITRE Technique | Platform | Tool | Rule Name | Data Sources | Status     | Priority | Owner | Target Date | Actual Date | Rule Version | FP Rate | TP Validated | Linked RCA | Notes |
| ----------------- | --------------- | ------------ | ---------- | ----- | ----------- | ------ | ------------ | --------------- | -------- | ---- | --------- | ------------ | ---------- | -------- | ----- | ----------- | ----------- | ------------ | ------- | ------------ | ---------- | ----- |
| DET-IMP-YYYY-0001 |                 | Incident     | INC-####   |       |             |        |              | T####           | SIEM     |      |           |              | Identified | High     |       |             |             |              |         |              |            |       |
| DET-IMP-YYYY-0002 |                 | Threat Intel | TI-####    |       |             |        |              |                 |          |      |           |              |            |          |       |             |             |              |         |              |            |       |
| DET-IMP-YYYY-0003 |                 | Purple Team  | EX-####    |       |             |        |              |                 |          |      |           |              |            |          |       |             |             |              |         |              |            |       |

---

## 8.3 Detailed Entry Template (Per Improvement)

> Use this format for each significant detection improvement.

### Improvement: `DET-IMP-YYYY-####`

**Metadata:**

| Field                 | Value                                           |
| --------------------- | ----------------------------------------------- |
| Title                 |                                                 |
| Date Identified (UTC) |                                                 |
| Source                | Incident / Intel / Hunt / Exercise / Compliance |
| Source Reference      |                                                 |
| Priority              | Critical / High / Medium / Low                  |
| Status                | Identified / In Development / Deployed / etc.   |
| Owner                 |                                                 |
| Target Deployment     |                                                 |
| Actual Deployment     |                                                 |

**Threat Context:**

| Field                   | Value                                          |
| ----------------------- | ---------------------------------------------- |
| Threat Actor (if known) |                                                |
| Malware/Tool            |                                                |
| MITRE Tactic            |                                                |
| MITRE Technique         |                                                |
| MITRE Sub-Technique     |                                                |
| Attack Phase            | Pre-Attack / Initial Access / Execution / etc. |

**Detection Gap Description:**

`Describe the detection gap clearly. What was the original incident/finding that exposed the gap? Why was it not detected by existing controls?`

**Proposed Detection Logic:**

```
[Pseudo-code or rule logic description]

Example:
IF (Process = "powershell.exe")
AND (CommandLine CONTAINS "DownloadString")
AND (CommandLine CONTAINS "Invoke-Expression")
AND (ParentProcess NOT IN whitelisted_parents)
THEN Alert
```

**Data Sources Required:**

| Source             | Available? | Coverage       |
| ------------------ | ---------- | -------------- |
| Windows Event Logs |            | % of endpoints |
| Sysmon             |            | % of endpoints |
| EDR Telemetry      |            | % of endpoints |
| Firewall Logs      |            | All / Subset   |
| Cloud Audit Logs   |            | All / Subset   |

**Testing Plan:**

| Test                      | Method | Expected Result | Pass/Fail |
| ------------------------- | ------ | --------------- | --------- |
| Atomic Red Team test      |        |                 |           |
| Manual reproduction       |        |                 |           |
| Historical data backtest  |        |                 |           |
| False positive validation |        |                 |           |

**Deployment Notes:**

- Deployment date: `YYYY-MM-DD`
- Deployment environment: Production / Staging
- Rollback plan: `...`
- Monitoring period: `...`

**Performance Tracking:**

| Metric              | Initial | Week 1 | Week 4 | Current |
| ------------------- | ------- | ------ | ------ | ------- |
| Alert volume        |         |        |        |         |
| False positive rate |         |        |        |         |
| True positive count |         |        |        |         |
| Tuning iterations   |         |        |        |         |

**Tuning History:**

| Version | Date | Change             | Reason | Result |
| ------- | ---- | ------------------ | ------ | ------ |
| v1.0    |      | Initial deployment |        |        |
| v1.1    |      | Added exclusion    |        |        |
| v1.2    |      | Refined threshold  |        |        |

---

# 9. MITRE ATT&CK Coverage Tracking (Mandatory)

## 9.1 Coverage Summary (Update Monthly)

| Tactic               | Total Techniques | Detected | Partial | Not Detected | Coverage % |
| -------------------- | ---------------- | -------- | ------- | ------------ | ---------- |
| Reconnaissance       |                  |          |         |              |            |
| Resource Development |                  |          |         |              |            |
| Initial Access       |                  |          |         |              |            |
| Execution            |                  |          |         |              |            |
| Persistence          |                  |          |         |              |            |
| Privilege Escalation |                  |          |         |              |            |
| Defense Evasion      |                  |          |         |              |            |
| Credential Access    |                  |          |         |              |            |
| Discovery            |                  |          |         |              |            |
| Lateral Movement     |                  |          |         |              |            |
| Collection           |                  |          |         |              |            |
| Command and Control  |                  |          |         |              |            |
| Exfiltration         |                  |          |         |              |            |
| Impact               |                  |          |         |              |            |
| **TOTAL**            |                  |          |         |              |            |

Reference:
`10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`

---

# 10. Status Definitions (Standard)

| Status             | Definition                                       |
| ------------------ | ------------------------------------------------ |
| **Identified**     | Improvement need identified, not yet prioritized |
| **Prioritized**    | Priority assigned, awaiting assignment           |
| **In Design**      | Detection logic being designed                   |
| **In Development** | Rule being implemented                           |
| **Testing**        | Rule under test in non-production                |
| **Validated**      | Tested and validated, awaiting deployment        |
| **Deployed**       | Active in production                             |
| **Tuning**         | Under active tuning to reduce FP rate            |
| **Stable**         | Mature rule with low FP rate                     |
| **Retired**        | Removed from production                          |
| **Blocked**        | Cannot proceed (data gap, tool limitation)       |

---

# 11. Priority Definitions (Standard)

| Priority     | Definition                                                   | Target Deployment SLA |
| ------------ | ------------------------------------------------------------ | --------------------- |
| **Critical** | Detects active threat to organization; regulatory mandate    | 7 days                |
| **High**     | Detects high-impact technique used by relevant threat actors | 30 days               |
| **Medium**   | Improves coverage of known TTPs                              | 60 days               |
| **Low**      | Tuning, optimization, edge cases                             | 90 days               |

---

# 12. Performance Metrics (Mandatory – Monthly Report)

Track these metrics monthly:

| Metric                      | Calculation                      | Target |
| --------------------------- | -------------------------------- | ------ |
| Improvements identified     | Count this month                 |        |
| Improvements deployed       | Count deployed this month        |        |
| Average time-to-deployment  | Days from identified to deployed |        |
| MITRE coverage improvement  | % increase month-over-month      |        |
| Average FP rate (new rules) | % across new rules               |        |
| Rules retired               | Count retired this month         |        |
| Open improvements (backlog) | Count not deployed               |        |
| Overdue improvements        | Count past target date           |        |

---

# 13. Quality Checklist (Per Improvement Entry)

Before marking an improvement as "Deployed":

- [ ] Detection logic documented
- [ ] MITRE ATT&CK mapping completed
- [ ] Data sources validated as available
- [ ] Tested with Atomic Red Team / equivalent
- [ ] Historical data backtest performed
- [ ] False positive rate within acceptable range
- [ ] True positive validation completed
- [ ] Rule peer-reviewed
- [ ] Documentation in SIEM/EDR use case library updated
- [ ] L1/L2 analysts informed of new alert
- [ ] Playbook created/updated for new alert
- [ ] Tuning plan defined
- [ ] Linked to source (incident/intel/hunt)
- [ ] Approved by Detection Engineering Lead
- [ ] MSSP: tenant scoping verified (if applicable)

---

# 14. Review Process (Mandatory)

## 14.1 Weekly Review

Detection Engineer reviews:

- New improvements identified
- Status updates on in-progress items
- Blocked items requiring escalation
- Performance of recently deployed rules

## 14.2 Monthly Review

Detection Engineering Lead + SOC Manager review:

- Backlog and prioritization
- Overdue items
- MITRE ATT&CK coverage trend
- Average FP rate trend
- Rule retirement candidates
- Detection engineering KPIs

## 14.3 Quarterly Review

CISO + Detection Engineering Lead review:

- Strategic detection priorities
- Technology investment needs
- Detection maturity assessment
- Cross-team coordination needs

---

# 15. MSSP Considerations (If Applicable)

For MSSP-managed clients:

- Client-specific detections logged in **tenant-scoped registers**
- Cross-client detection improvements (generic) tracked in master register
- Client-confidential detection logic must not be shared across tenants
- Custom detections for clients require client approval before deployment
- Client receives monthly **detection improvement report** sanitized to their environment
- Common threat-based detections (e.g., new ransomware TTPs) deployed across tenants per SLA
- MITRE coverage reported per client

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`

---

# 16. Integration with Other Processes

| Process            | Integration Point                                 |
| ------------------ | ------------------------------------------------- |
| RCA                | RCA findings create detection improvement entries |
| Lessons Learned    | LL actions for detection create entries           |
| Threat Hunting     | Hunt findings create entries                      |
| Threat Intel       | New IOCs/TTPs create entries                      |
| Red/Purple Team    | Exercise findings create entries                  |
| Vulnerability Mgmt | Critical CVEs may require detection entries       |
| Compliance         | Mandatory detections (RBI, PCI) tracked here      |
| Playbook Updates   | New detections trigger playbook updates           |

---

# 17. Related Documents

| Document                      | Path                                                                            |
| ----------------------------- | ------------------------------------------------------------------------------- |
| Playbook Update Log           | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`             |
| Security Improvement Register | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx` |
| Control Gap Tracker           | `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`           |
| RCA Template                  | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`                     |
| Lessons Learned Template      | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`             |
| SIEM Use Cases Master         | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md`                    |
| SIEM Alert Tuning Guide       | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md`                  |
| EDR Alert Handling Guide      | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Alert-Handling-Guide.md`                  |
| Threat Intel IoC Handling SOP | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md`       |
| L2 Threat Hunting Procedures  | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md`     |
| Purple Team Exercise Guide    | `10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`           |
| MITRE ATT&CK Quick Reference  | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md` |

---

# 18. Revision History

| Version | Date        | Author                                   | Changes         |
| ------- | ----------- | ---------------------------------------- | --------------- |
| 1.0     | 30-May-2026 | Detection Engineering Lead / SOC Manager | Initial version |

---

# 19. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**
