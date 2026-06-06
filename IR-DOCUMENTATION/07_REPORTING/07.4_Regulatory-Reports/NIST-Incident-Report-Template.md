# NIST Incident Report Template

---

# 1. Document Control

| Field          | Value                                            |
| -------------- | ------------------------------------------------ |
| Document Name  | Template – NIST Incident Report                  |
| Document ID    | RPT-REG-003                                      |
| Version        | 1.0                                              |
| Effective Date | 30-May-2026                                      |
| Owner          | IR Team Lead / SOC Manager                       |
| Approved By    | CISO                                             |
| Classification | Internal – Confidential / Restricted (as needed) |
| Review Cycle   | Quarterly                                        |

---

# 2. Purpose

This template provides a structured incident report format aligned to:

- **NIST SP 800-61 Rev.2** (Computer Security Incident Handling Guide) lifecycle, and
- **NIST Cybersecurity Framework (CSF)** Respond/Recover functions.

It is used to produce a report that is:

- operationally useful for responders,
- audit-ready for NIST assessments and client assurance,
- consistent across incidents for trend analysis and improvement.

This template is critical because:

- NIST emphasizes structured incident handling, documentation, and post-incident improvement
- consistent reporting improves response repeatability and reduces future dwell time
- evidence-backed reporting supports regulatory obligations and internal governance
- MSSP operations require tenant-safe reporting and consistent deliverables

Reference alignment:
`00_GOVERNANCE/00.1_Policies/IR-Policy-NIST-Alignment.md`

---

# 3. Scope

Use this template for:

| Scenario                        | Requirement                                       |
| ------------------------------- | ------------------------------------------------- |
| P1/P2 incidents                 | Recommended (often mandatory for major incidents) |
| P3 incidents (TP)               | Recommended when deep documentation is needed     |
| Client assurance reports        | When clients request NIST-structured reports      |
| Internal NIST maturity evidence | For assessments/audits                            |

Not intended for:

- short false positive closures
- daily/weekly operational reporting

---

# 4. Instructions (Mandatory)

- Use UTC timestamps for all events.
- Provide evidence references (IDs/paths) instead of embedding sensitive data.
- Clearly label **Confirmed / Suspected / Unknown**.
- Document decisions and approvals for containment actions.
- If any sections are not applicable, mark them “N/A” with rationale.
- For MSSP: ensure client/tenant scoping and no cross-client references.

---

# 5. Template (Copy/Paste)

## 5.1 Report Metadata (Mandatory)

| Field                         | Value                 |
| ----------------------------- | --------------------- |
| Incident ID / Ticket ID       | `INC-YYYY-####`       |
| Incident Category             | `...`                 |
| Severity                      | P1 / P2 / P3 / P4     |
| Report Type                   | Interim / Final       |
| Client/Tenant (if applicable) | `Client ID / Name`    |
| Prepared By                   | `Name / Role`         |
| Reviewed By                   | `Name / Role`         |
| Approved By                   | `Name / Role`         |
| Report Date (UTC)             | `YYYY-MM-DD HH:MM`    |
| Evidence Vault Root           | `Reference ID / path` |

---

## 5.2 Executive Summary (Mandatory)

- **What happened (confirmed):** `...`
- **Impact summary:** `...`
- **Status:** `Contained/Eradicated/Recovered/Monitoring`
- **Key decisions made:** `...`
- **Next steps / follow-ups:** `...`

---

## 5.3 NIST SP 800-61 Lifecycle Documentation (Mandatory)

### Phase 1 — Preparation (Environment and Readiness Context)

> Document what preparedness controls existed and whether they functioned.

- Tools in use (SIEM/EDR/TI/ticketing): `...`
- Logging coverage relevant to incident: `...`
- Incident contacts and escalation path used: `...`
- Known constraints (e.g., missing telemetry): `...`

Evidence references:

- `Policies/SOPs used`
- `Tool health evidence`

---

### Phase 2 — Detection & Analysis

#### A) Detection Details

| Item                      | Details                         |
| ------------------------- | ------------------------------- |
| Noticing time (UTC)       |                                 |
| Detection time (UTC)      |                                 |
| Detection source          | SIEM / EDR / User / Client / TI |
| Triggering rule/alert IDs |                                 |
| Initial affected entities |                                 |

#### B) Incident Classification and Severity

- Category: `...`
- Initial severity and rationale: `...`
- Severity changes (if any): `...` + approvals

#### C) Analysis Summary (Confirmed vs Suspected)

**Confirmed:**

- `...`

**Suspected / under validation:**

- `...`

**Key unknowns:**

- `...`

#### D) Scope Assessment (Best Known)

| Scope Element       | Findings |
| ------------------- | -------- |
| Hosts/systems       |          |
| Users/accounts      |          |
| Privileged accounts |          |
| Services            |          |
| Network segments    |          |
| Cloud resources     |          |

#### E) Indicators and TTPs (Sanitized)

- IOCs: `IPs/domains/hashes (reference list or appendix)`
- TTPs/MITRE mapping (optional): `...`

Evidence references:

- SIEM export ref: `...`
- EDR timeline ref: `...`
- Network logs ref: `...`
- Cloud audit logs ref: `...`

---

### Phase 3 — Containment, Eradication & Recovery

#### A) Containment Strategy

- Containment objectives: `stop spread / stop exfil / isolate hosts / protect critical assets`
- Containment scope: `...`
- Containment constraints (business impact): `...`

#### B) Containment Actions Log

| Action | Scope/Target | Authorized By | Executed By | Time (UTC) | Outcome |
| ------ | ------------ | ------------- | ----------- | ----------:| ------- |
|        |              |               |             |            |         |

#### C) Eradication Actions

| Action | Scope | Owner | Time (UTC) | Outcome |
| ------ | ----- | -----:| ----------:| ------- |
|        |       |       |            |         |

#### D) Recovery Actions

| Action | Scope | Owner | Time (UTC) | Outcome |
| ------ | ----- | -----:| ----------:| ------- |
|        |       |       |            |         |

#### E) Validation (Required)

- Validation steps performed: `...`
- Monitoring plan post-recovery: `...`
- Criteria used to declare “resolved”: `...`

Evidence references:

- `EDR clean scan results`
- `SIEM “no IOC hits” query outputs`
- `Change records (firewall/IAM changes)`

---

### Phase 4 — Post-Incident Activity

#### A) Root Cause Summary

- Root cause (confirmed): `...`
- Contributing factors: `...`
- Root cause status: `RCA completed / in progress`

Reference:
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`

#### B) Lessons Learned

- What went well: `...`
- What did not go well: `...`
- Key improvements: `...`

Reference:
`08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`

#### C) Corrective Actions (CAPA)

| Action | Category (Prevent/Detect/Respond/Recover) | Owner | Due (UTC) | Tracking Ref | Status |
| ------ | ----------------------------------------- | ----- | ---------:| ------------ | ------ |
|        |                                           |       |           |              |        |

#### D) Metrics

| Metric           | Value | Notes |
| ---------------- | -----:| ----- |
| MTTA             |       |       |
| Time to contain  |       |       |
| Time to recover  |       |       |
| Systems impacted |       |       |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

---

## 5.4 NIST CSF Mapping (Optional but Recommended)

Map incident activities to CSF functions:

| CSF Function | Evidence / What Was Done                   |
| ------------ | ------------------------------------------ |
| Identify     | Asset context used, risk decisions         |
| Protect      | Controls used (MFA, segmentation, backups) |
| Detect       | How detected and correlated                |
| Respond      | Containment/communications/analysis        |
| Recover      | Recovery actions and verification          |

Reference:
`00_GOVERNANCE/00.1_Policies/IR-Policy-NIST-Alignment.md`

---

## 5.5 Communications and Notifications (Mandatory)

| Target              | Notified? | Time (UTC) | Notes/Reference |
| ------------------- | --------- | ----------:| --------------- |
| Management/CISO     |           |            |                 |
| Compliance/Legal    |           |            |                 |
| Client (MSSP)       |           |            |                 |
| CERT-In             |           |            |                 |
| RBI                 |           |            |                 |
| Vendors/IR retainer |           |            |                 |

---

## 5.6 Evidence Inventory (Mandatory)

| Evidence Type     | Evidence ID/Path | Hash (SHA256 if applicable) | Notes |
| ----------------- | ---------------- | --------------------------- | ----- |
| SIEM exports      |                  |                             |       |
| EDR telemetry     |                  |                             |       |
| Network logs/PCAP |                  |                             |       |
| Disk/memory       |                  |                             |       |
| CoC records       |                  |                             |       |

References:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/`

---

## 5.7 Appendix (Optional)

- IOC appendix (sanitized)
- SIEM query appendix
- Timeline builder output reference
- Malware analysis summary reference

---

# 6. Related Documents

| Document                       | Path                                                                                   |
| ------------------------------ | -------------------------------------------------------------------------------------- |
| IR Policy – NIST Alignment     | `00_GOVERNANCE/00.1_Policies/IR-Policy-NIST-Alignment.md`                              |
| Final Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`                 |
| Technical Deep Dive Template   | `07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`                   |
| Evidence Collection SOP        | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Lessons Learned Template       | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`                    |
| RCA Template                   | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`                            |

---

# 7. Revision History

| Version | Date        | Author                     | Changes         |
| ------- | ----------- | -------------------------- | --------------- |
| 1.0     | 30-May-2026 | IR Team Lead / SOC Manager | Initial version |

---

# 8. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
