# Executive Summary Template (Incident)

---

# 1. Document Control

| Field          | Value                                   |
| -------------- | --------------------------------------- |
| Document Name  | Template – Executive Summary (Incident) |
| Document ID    | RPT-INC-001                             |
| Version        | 1.0                                     |
| Effective Date | 30-May-2026                             |
| Owner          | SOC Manager / IR Team Lead              |
| Approved By    | CISO                                    |
| Classification | Internal – Confidential                 |
| Review Cycle   | Quarterly                               |

---

# 2. Purpose

This template standardizes the **Executive Summary** section for security incidents to ensure leadership receives:

- a clear, non-technical overview of what happened,
- business impact and risk exposure,
- actions taken and current status,
- decisions required and next steps,
- consistent, audit-ready reporting language.

This template is critical because:

- executives need concise, decision-oriented information (not raw technical detail)
- post-incident reporting must be consistent across incidents for trend analysis and audits
- regulatory and client communication often begins from executive-level narratives
- MSSP clients require tenant-safe, contract-aligned summaries

---

# 3. Scope

Use this template for:

| Report Type                   | When Used                                            |
| ----------------------------- | ---------------------------------------------------- |
| Initial incident report       | Early confirmed incident (P1–P3)                     |
| Interim status report         | Ongoing P1/P2 incidents requiring leadership updates |
| Final incident report         | Closure documentation and lessons learned            |
| Client incident report (MSSP) | Client-facing executive summary (tenant-scoped)      |

Out of scope:

- technical deep-dive (use Technical Deep Dive template)
- forensic appendices and raw evidence (reference secure evidence package)

References:  
`07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`  
`07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`

---

# 4. Instructions (Mandatory)

- Use **plain language** and avoid tool/vendor jargon.
- Use **UTC** for all timestamps.
- Separate **confirmed facts** from **assumptions/hypotheses**.
- Do not include sensitive raw evidence (credentials/PII/PCAP) in the executive summary.
- For MSSP: verify correct client/tenant and ensure **no cross-client references**.
- Keep the executive summary to **1–2 pages** (recommended), with links to supporting sections.

---

# 5. Template (Copy/Paste)

## 5.1 Report Header (Mandatory)

| Field                         | Value                                                                                                         |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------- |
| Incident ID / Ticket ID       | `INC-YYYY-####`                                                                                               |
| Report Type                   | Initial / Interim / Final                                                                                     |
| Severity                      | P1 / P2 / P3 / P4                                                                                             |
| Incident Category             | Ransomware / Data Breach / Intrusion / Malware / Phishing-BEC / DDoS / Cloud / Insider / Supply Chain / Other |
| Client/Tenant (if applicable) | `Client ID / Client Name`                                                                                     |
| Report Date (UTC)             | `YYYY-MM-DD HH:MM`                                                                                            |
| Incident Commander / Owner    | `Name / Role`                                                                                                 |
| Prepared By                   | `Name / Role`                                                                                                 |
| Reviewed By                   | `Name / Role`                                                                                                 |
| Approved By                   | `Name / Role`                                                                                                 |

---

## 5.2 Executive Summary (Non-Technical) (Mandatory)

### A) What Happened (Confirmed)

Provide 3–6 bullet points:

- `...`
- `...`
- `...`

### B) When It Happened (UTC Timeline)

| Timeline Item                         | Time (UTC)         |
| ------------------------------------- | ------------------:|
| Noticing time (first awareness)       | `YYYY-MM-DD HH:MM` |
| Detection time (alert time)           | `YYYY-MM-DD HH:MM` |
| Incident declared                     | `YYYY-MM-DD HH:MM` |
| Containment started                   | `YYYY-MM-DD HH:MM` |
| Containment completed (if applicable) | `YYYY-MM-DD HH:MM` |
| Service restored (if applicable)      | `YYYY-MM-DD HH:MM` |
| Incident closed (if final)            | `YYYY-MM-DD HH:MM` |

---

## 5.3 Business Impact Summary (Mandatory)

### A) Operational Impact

| Impact Area               | Status                             | Details |
| ------------------------- | ---------------------------------- | ------- |
| Service availability      | Normal / Degraded / Down / Unknown | `...`   |
| Critical systems impacted | Yes / No / Unknown                 | `...`   |
| Customer impact           | Yes / No / Unknown                 | `...`   |
| Financial impact          | Unknown / Estimated                | `...`   |
| Reputational impact       | Low / Medium / High / Unknown      | `...`   |

### B) Data Impact (If Applicable)

| Item                  | Status                                        | Details |
| --------------------- | --------------------------------------------- | ------- |
| Data exposure         | Suspected / Confirmed / No evidence / Unknown | `...`   |
| Data types            | PII / Financial / Credentials / IP / Other    | `...`   |
| Volume / records      | Known / Estimated / Unknown                   | `...`   |
| Exfiltration evidence | Yes / No / Unknown                            | `...`   |

---

## 5.4 Scope Summary (Mandatory)

| Scope Element                           | Current Understanding                           |
| --------------------------------------- | ----------------------------------------------- |
| Affected hosts/systems                  | `Count + key systems`                           |
| Affected users/accounts                 | `Count + privileged?`                           |
| Affected applications/services          | `...`                                           |
| Geographic/tenant scope (if applicable) | `...`                                           |
| Current containment boundary            | `Single host / subnet / multi-system / unknown` |

---

## 5.5 Root Cause (If Known) / Leading Hypothesis (If Not Final)

### A) Root Cause (If Confirmed)

- `Confirmed root cause statement (1–3 lines)`

### B) If Not Confirmed (Interim)

- **Leading hypothesis:** `...`  
- **What is being validated:** `...`  
- **Expected confirmation timeline:** `...`

---

## 5.6 Actions Taken (Mandatory)

### A) Containment (Key Actions)

List major actions only:

| Action | Time (UTC) | Owner | Outcome |
| ------ | ----------:| ----- | ------- |
|        |            |       |         |
|        |            |       |         |

### B) Eradication and Recovery (If Applicable)

- `...`
- `...`

### C) Validation (Why We Believe Risk Is Reduced/Closed)

- `Validation step 1…`
- `Validation step 2…`
- `Validation step 3…`

---

## 5.7 Current Risk and Residual Risk (Mandatory)

| Risk Area                 | Rating                        | Notes |
| ------------------------- | ----------------------------- | ----- |
| Reinfection / persistence | Low / Medium / High / Unknown | `...` |
| Lateral movement          | Low / Medium / High / Unknown | `...` |
| Data exposure             | Low / Medium / High / Unknown | `...` |
| Service stability         | Low / Medium / High / Unknown | `...` |

---

## 5.8 Decisions Required (If Any) (Mandatory If Applicable)

> Make decisions explicit and time-bound.

| Decision Needed | Why | Options | Recommended | Needed By (UTC) | Decision Owner | Status |
| --------------- | --- | ------- | ----------- | ---------------:| -------------- | ------ |
|                 |     |         |             |                 |                |        |

Examples:

- Approve isolation of critical server group
- Approve external IR retainer engagement
- Approve customer communication
- Approve emergency change window exception

---

## 5.9 Notifications and Compliance Status (Mandatory)

| Party                       | Notified?               | Time (UTC) | Notes / Reference |
| --------------------------- | ----------------------- | ----------:| ----------------- |
| SOC Manager / CISO          | Yes/No                  |            |                   |
| Compliance / Legal          | Yes/No                  |            |                   |
| MSSP Client (if applicable) | Yes/No                  |            |                   |
| CERT-In reporting assessed  | Yes/No/Under assessment |            |                   |
| RBI reporting assessed      | Yes/No/Under assessment |            |                   |
| Law enforcement engaged     | Yes/No                  |            |                   |

---

## 5.10 Next Steps (Mandatory)

### A) Next 24–72 Hours Plan

| Action | Owner | Due (UTC) | Notes |
| ------ | ----- | ---------:| ----- |
|        |       |           |       |
|        |       |           |       |

### B) Post-Incident Follow-Ups (If Final or Near Closure)

| Follow-Up Item                | Owner | Due (UTC) | Tracking Reference |
| ----------------------------- | ----- | ---------:| ------------------ |
| RCA completion                |       |           | `RCA-...`          |
| Lessons Learned / PIR meeting |       |           | `PIR-...`          |
| Detection improvement         |       |           | `DET-IMP-...`      |
| Control remediation           |       |           | `CTRL-GAP-...`     |

---

## 5.11 Key Metrics (Recommended)

| Metric                     | Value | Notes       |
| -------------------------- | -----:| ----------- |
| Time to acknowledge (MTTA) |       | `UTC-based` |
| Time to triage             |       |             |
| Time to contain            |       |             |
| Time to recover            |       |             |
| Systems impacted (count)   |       |             |
| Users impacted (count)     |       |             |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

---

# 6. Related Documents

| Document                         | Path                                                                                          |
| -------------------------------- | --------------------------------------------------------------------------------------------- |
| Initial Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Initial-Incident-Report-Template.md`                      |
| Interim Status Report Template   | `07_REPORTING/07.1_Incident-Reports/Interim-Status-Report-Template.md`                        |
| Final Incident Report Template   | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`                        |
| Technical Deep Dive Template     | `07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`                          |
| Ticket Closure Criteria          | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md`                           |
| Evidence Storage Policy          | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`           |
| CERT-In Reporting SOP            | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`      |
| RBI Incident Reporting SOP       | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md` |

---

# 7. Revision History

| Version | Date        | Author                     | Changes         |
| ------- | ----------- | -------------------------- | --------------- |
| 1.0     | 30-May-2026 | SOC Manager / IR Team Lead | Initial version |

---

# 8. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
