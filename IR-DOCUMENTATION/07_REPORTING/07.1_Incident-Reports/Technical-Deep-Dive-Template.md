# Technical Deep Dive Template (Incident)

---

# 1. Document Control

| Field          | Value                                            |
| -------------- | ------------------------------------------------ |
| Document Name  | Template – Technical Deep Dive (Incident)        |
| Document ID    | RPT-INC-005                                      |
| Version        | 1.0                                              |
| Effective Date | 30-May-2026                                      |
| Owner          | L3 Analyst / Digital Forensics Lead              |
| Approved By    | IR Team Lead                                     |
| Classification | Internal – Confidential / Restricted (as needed) |
| Review Cycle   | Quarterly                                        |

---

# 2. Purpose

This template standardizes the **Technical Deep Dive** section/report used to document detailed technical findings for an incident, including:

- attacker techniques, tools, and indicators,
- entry vector and kill chain reconstruction,
- scope expansion methodology and results,
- forensic artifact analysis and timelines,
- containment/eradication validation evidence,
- detection and control gaps identified for improvement.

A technical deep dive is critical because:

- it provides defensible technical evidence supporting conclusions in final reports
- it supports detection engineering improvements (SIEM/EDR rules, logging gaps)
- it enables future incident response efficiency (repeatable analysis patterns)
- it supports regulator/auditor questions when technical detail is requested (sanitized as needed)
- it supports MSSP clients with a technical appendix (tenant-scoped and sanitized)

This template ensures:

- consistent forensic and investigation documentation
- traceable evidence references and reproducible analysis
- clear “confirmed vs suspected vs unknown” technical statements

---

# 3. Scope

Use this template for:

| Scenario                    | Requirement                                           |
| --------------------------- | ----------------------------------------------------- |
| P1/P2 incidents             | Recommended (often mandatory for major incidents)     |
| P3 incidents (TP)           | Recommended when scope/root cause needs documentation |
| Malware analysis performed  | Recommended                                           |
| Data breach/exfil suspected | Recommended                                           |
| Cloud compromise            | Recommended                                           |

Not intended for:

- short false-positive closures
- executive summaries (use Executive Summary template)

Reference:
`07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`

---

# 4. Instructions (Mandatory)

- Use UTC timestamps.
- Keep evidence references in secure repository; do not embed raw sensitive dumps unless strictly required.
- Document queries and parameters so analysis is reproducible.
- Clearly separate:
  - Confirmed
  - Suspected
  - Unknown
- For MSSP: ensure tenant-scoped artifacts and no cross-client references.

---

# 5. Template (Copy/Paste)

## 5.1 Report Header (Mandatory)

| Field                         | Value               |
| ----------------------------- | ------------------- |
| Incident ID / Ticket ID       | `INC-YYYY-####`     |
| Technical Deep Dive Version   | 1.0                 |
| Incident Category             | `...`               |
| Severity                      | P1 / P2 / P3 / P4   |
| Client/Tenant (if applicable) | `Client ID / Name`  |
| Prepared By                   | `Name / Role`       |
| Reviewed By                   | `Name / Role`       |
| Date (UTC)                    | `YYYY-MM-DD HH:MM`  |
| Evidence Vault Root           | `Path/Reference ID` |

---

## 5.2 Environment Context (Mandatory)

### A) Environment Overview

- **Business unit / client:** `...`
- **Key systems involved:** `...`
- **Network segmentation notes (high level):** `...`
- **Logging coverage:** `SIEM sources, EDR coverage, network telemetry availability`
- **Known constraints:** `Data residency, tool limitations, downtime constraints`

### B) Asset Criticality (If Applicable)

| Asset | Role | Criticality | Notes |
| ----- | ---- | ----------- | ----- |
|       |      |             |       |

Reference:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md` (if MSSP)

---

## 5.3 Incident Hypothesis and Key Questions (Recommended)

### A) Initial Hypothesis (At Time of Detection)

- `Hypothesis and reasoning`

### B) Key Questions to Answer

- Entry vector: `...`
- Persistence: `...`
- Lateral movement: `...`
- Exfiltration: `...`
- Scope: `...`

---

## 5.4 Timeline (UTC) – Technical Timeline (Mandatory)

> Include technical events and evidence references.

| Time (UTC) | Event | Evidence Ref | Confidence (High/Med/Low) | Notes |
| ----------:| ----- | ------------ | ------------------------- | ----- |
|            |       |              |                           |       |
|            |       |              |                           |       |

---

## 5.5 Detection Details (Mandatory)

### A) Alert(s) Triggered

| Source | Rule/Detection | Alert ID | Time (UTC) | Entity | Notes |
| ------ | -------------- | -------- | ----------:| ------ | ----- |
| SIEM   |                |          |            |        |       |
| EDR    |                |          |            |        |       |

### B) Initial Triage Summary (Technical)

- `Key observed signals and why it was suspicious`

---

## 5.6 Entry Vector Analysis (Mandatory)

### A) Confirmed Entry Vector (If Confirmed)

- `...` + evidence references

### B) Suspected Entry Vector (If Not Confirmed)

- `...` + rationale + evidence gaps

### C) Supporting Evidence

| Evidence Type         | Reference | Notes |
| --------------------- | --------- | ----- |
| Email logs            |           |       |
| Proxy/DNS             |           |       |
| Web/WAF               |           |       |
| Vulnerability/exploit |           |       |

---

## 5.7 Adversary Activity Reconstruction (Kill Chain / ATT&CK)

### A) ATT&CK Mapping (Recommended)

| Tactic | Technique ID | Technique | Evidence Ref | Confidence | Notes |
| ------ | ------------ | --------- | ------------ | ---------- | ----- |
|        |              |           |              |            |       |

Reference:
`10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`

### B) Execution and Process Tree Findings (Endpoint)

| Host | Process/Command Summary | Evidence Ref | Notes |
| ---- | ----------------------- | ------------ | ----- |
|      |                         |              |       |

### C) Persistence Findings

- **Persistence confirmed:** Yes/No/Unknown  
- **Mechanisms observed:** `scheduled tasks/services/registry/run keys/cloud persistence/etc.`

| Artifact | Host | Evidence Ref | Notes |
| -------- | ---- | ------------ | ----- |
|          |      |              |       |

### D) Privilege Escalation / Credential Access

- **Credential theft indicators:** `Yes/No/Unknown`
- **Privileged access abuse:** `Yes/No/Unknown`

| Artifact/Event | Evidence Ref | Notes |
| -------------- | ------------ | ----- |
|                |              |       |

### E) Lateral Movement and Internal Recon

| Indicator                  | Evidence Ref | Notes |
| -------------------------- | ------------ | ----- |
| Remote execution artifacts |              |       |
| SMB/WMI/PSRemoting         |              |       |
| Internal scanning          |              |       |

---

## 5.8 Network and Exfiltration Analysis (Mandatory if suspected)

### A) C2 Indicators

| Destination | Protocol/Port | Source Host | First Seen (UTC) | Last Seen (UTC) | Evidence Ref |
| ----------- | ------------- | ----------- | ----------------:| ---------------:| ------------ |
|             |               |             |                  |                 |              |

### B) Exfiltration Assessment

- **Exfiltration confirmed:** Yes/No/Unknown  
- **Exfil method:** `HTTPS/Cloud storage/DNS tunneling/Other`  
- **Data staging observed:** Yes/No/Unknown  

| Evidence             | Reference | Notes |
| -------------------- | --------- | ----- |
| Proxy/firewall bytes |           |       |
| Cloud download logs  |           |       |
| PCAP excerpts        |           |       |

---

## 5.9 Malware Analysis Summary (If Applicable)

> Provide high-level findings here; reference full malware report if separate.

| Sample | Hash (SHA256) | Type | Findings Summary | Evidence Ref |
| ------ | ------------- | ---- | ---------------- | ------------ |
|        |               |      |                  |              |

- **Family / classification:** `...`
- **Capabilities:** `...`
- **Persistence behavior:** `...`
- **Network behavior:** `...`

Reference:
`03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Malware-Analysis-SOP.md`

---

## 5.10 Scope Expansion Methodology (Mandatory)

Document how scope was expanded:

### A) Entities Used for Pivoting

- Hosts: `...`
- Users/accounts: `...`
- IOCs: `...`
- Cloud principals/resources: `...`

### B) Queries and Methods Used (Reproducible)

| Tool  | Query/Method | Time Window (UTC) | Output Ref |
| ----- | ------------ | -----------------:| ---------- |
| SIEM  |              |                   |            |
| EDR   |              |                   |            |
| Cloud |              |                   |            |

### C) Final Scope Result Summary

- `What was included and excluded and why`

---

## 5.11 Containment, Eradication, Recovery – Technical Validation (Mandatory)

### A) Containment Actions (Technical Detail)

| Action | Target | Time (UTC) | Outcome | Evidence Ref |
| ------ | ------ | ----------:| ------- | ------------ |
|        |        |            |         |              |

### B) Eradication Actions

- `Persistence removal steps`
- `Patch applied`
- `Credential reset`

### C) Validation Checks

- `No IOC hits in SIEM for X hours/days`
- `EDR shows no suspicious processes`
- `Network shows no outbound to known C2`

Document validation method and supporting evidence references.

---

## 5.12 Evidence Inventory (Technical Appendix) (Recommended)

| Evidence ID | Artifact | Storage Path/Ref | Hash | Notes |
| ----------- | -------- | ---------------- | ---- | ----- |
|             |          |                  |      |       |

---

## 5.13 Detection and Control Gaps (Mandatory)

### A) Detection Gaps Identified

- `Missing telemetry`
- `Rule coverage gap`
- `High false positive leading to delay`

### B) Control Weaknesses Identified

- `Patch management gap`
- `Excessive privileges`
- `Network segmentation gaps`
- `MFA gaps`

### C) Recommended Improvements (Actionable)

| Improvement | Category | Owner | Priority | Tracking Ref |
| ----------- | -------- | ----- | -------- | ------------ |
|             | Detect   |       |          |              |
|             | Prevent  |       |          |              |
|             | Respond  |       |          |              |

References:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`  
`08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`

---

## 5.14 Open Questions / Remaining Unknowns (If Any)

- `Unknown 1…`
- `Unknown 2…`

---

# 6. Related Documents

| Document                       | Path                                                                                   |
| ------------------------------ | -------------------------------------------------------------------------------------- |
| Final Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`                 |
| Evidence Collection SOP        | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| CoC Digital Evidence SOP       | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`       |
| SIEM Query Library             | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md`                              |
| EDR Investigation Queries      | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Investigation-Queries.md`                        |
| L3 Malware Analysis SOP        | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Malware-Analysis-SOP.md`                 |
| L3 Root Cause Analysis         | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Root-Cause-Analysis.md`                  |

---

# 7. Revision History

| Version | Date        | Author                              | Changes         |
| ------- | ----------- | ----------------------------------- | --------------- |
| 1.0     | 30-May-2026 | L3 Analyst / Digital Forensics Lead | Initial version |

---

# 8. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
