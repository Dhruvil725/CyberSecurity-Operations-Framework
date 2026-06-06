# RCA Timeline Builder Template

---

# 1. Document Control

| Field          | Value                           |
| -------------- | ------------------------------- |
| Document Name  | Template – RCA Timeline Builder |
| Document ID    | RCA-TL-001                      |
| Version        | 1.0                             |
| Effective Date | 30-May-2026                     |
| Owner          | IR Team Lead / L3 Analyst       |
| Approved By    | SOC Manager / CISO              |
| Classification | Internal – Confidential         |
| Review Cycle   | Annually                        |

---

# 2. Purpose

This template provides the standardized **RCA Timeline Builder** format used to reconstruct the complete sequence of events during a cyber security incident, from initial compromise through detection, response, and closure.

A structured timeline is critical because:

- root cause analysis depends on accurate, evidence-based event reconstruction
- detection gap analysis requires precise time deltas between events
- regulatory reports (RBI, CERT-In) require chronological incident narratives
- legal and forensic investigations require defensible timelines
- attribution and TTP analysis depend on event sequencing
- MTTR/MTTD metrics require accurate timestamps
- audit evidence requires timeline-based documentation
- MSSP client reports require client-presentable timelines

This template ensures:

- consistent timeline format across all incidents
- UTC-based timestamps with timezone conversion where needed
- evidence references for every timeline entry
- distinction between confirmed, suspected, and inferred events
- linkage to evidence vault, RCA, and final incident reports
- visual representation suitable for executive presentations

Reference alignment:
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`

---

# 3. Scope

This timeline builder is used for:

| Scenario                        | Timeline Required? | Detail Level                                |
| ------------------------------- | ------------------ | ------------------------------------------- |
| P1 incidents                    | **Mandatory**      | Detailed (minute-level where possible)      |
| P2 incidents                    | **Mandatory**      | Detailed (minute-level for key events)      |
| P3 incidents (TP)               | **Recommended**    | Summary (hour-level)                        |
| P4 incidents                    | Optional           | Summary                                     |
| Regulatory reportable incidents | **Mandatory**      | Detailed                                    |
| MSSP client incidents           | Per client SLA     | Per SLA                                     |
| Tabletop / Drill exercises      | **Mandatory**      | Detailed (exercise simulation)              |
| Forensic investigations         | **Mandatory**      | Highly detailed (second-level if available) |

Out of scope:

- false positive closures
- routine BAU alerts without incident declaration

---

# 4. Definitions

| Term            | Definition                                                |
| --------------- | --------------------------------------------------------- |
| Timeline        | Chronological sequence of events related to an incident   |
| Timestamp       | Date and time of an event (UTC mandatory)                 |
| Event           | Discrete action or observation related to the incident    |
| Confirmed Event | Event verified by direct evidence (logs, telemetry)       |
| Suspected Event | Event inferred from evidence but not directly verified    |
| Inferred Event  | Event hypothesized based on patterns or indirect evidence |
| Dwell Time      | Duration from initial compromise to detection             |
| Detection Delay | Time delta between event occurrence and detection         |
| Time Source     | System/tool that provided the timestamp (e.g., SIEM, EDR) |
| Time Skew       | Discrepancy between system clocks                         |

---

# 5. Roles and Responsibilities

| Role                     | Responsibilities                                    |
| ------------------------ | --------------------------------------------------- |
| Timeline Owner           | Builds and maintains timeline; validates timestamps |
| L3 Analyst               | Provides deep technical timeline reconstruction     |
| L2 Analyst               | Contributes investigation timeline entries          |
| IR Team Lead             | Reviews timeline for completeness and accuracy      |
| SOC Lead                 | Validates SOC response timeline                     |
| Forensics Lead           | Provides forensic timeline (disk, memory artifacts) |
| Evidence Custodian       | Provides evidence references for timeline entries   |
| SOC Manager              | Approves final timeline                             |
| MSSP SDM (if applicable) | Reviews client-facing timeline                      |

---

# 6. Timeline Building Principles (Mandatory)

| Principle           | Description                                        |
| ------------------- | -------------------------------------------------- |
| UTC Timestamps      | All times in UTC; local time in brackets if needed |
| Evidence-based      | Every entry must reference evidence source         |
| Confidence Labeling | Mark events as Confirmed / Suspected / Inferred    |
| Chronological       | Strict chronological order                         |
| Granularity         | Minute-level minimum; second-level for forensics   |
| Time Source         | Document source of each timestamp                  |
| Time Skew Awareness | Note any clock discrepancies between sources       |
| Completeness        | Include all relevant events; mark gaps explicitly  |
| Sanitization        | Remove sensitive data; use references              |
| Versioning          | Track timeline updates as investigation progresses |

---

# 7. Timeline Phases (Standard Structure)

A complete timeline should cover these phases:

| Phase                    | Description                                                    |
| ------------------------ | -------------------------------------------------------------- |
| **Pre-Incident**         | Vulnerable conditions, recent changes, threat intel indicators |
| **Initial Access**       | First malicious activity, entry point                          |
| **Execution**            | Malware execution, command execution                           |
| **Persistence**          | Mechanisms established to maintain access                      |
| **Privilege Escalation** | Elevation of permissions (if applicable)                       |
| **Defense Evasion**      | Anti-forensics, log clearing, evasion techniques               |
| **Credential Access**    | Credential harvesting, brute force                             |
| **Discovery**            | Reconnaissance, enumeration                                    |
| **Lateral Movement**     | Movement across systems                                        |
| **Collection**           | Data staging, archive creation                                 |
| **Command & Control**    | C2 communications                                              |
| **Exfiltration**         | Data exfiltration                                              |
| **Impact**               | Encryption, destruction, disruption                            |
| **Detection**            | Alert generation, anomaly observation                          |
| **Response**             | Triage, escalation, containment, eradication, recovery         |
| **Closure**              | Validation, closure, post-incident activities                  |

Reference:
`10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`

---

# 8. Timeline Template (Copy/Paste)

## 8.1 Timeline Metadata (Mandatory)

| Field                          | Value                   |
| ------------------------------ | ----------------------- |
| Timeline ID                    | `TL-YYYY-####`          |
| Incident ID / Ticket ID        | `INC-YYYY-####`         |
| Linked RCA ID                  | `RCA-YYYY-####`         |
| Incident Category              | `...`                   |
| Incident Severity              | P1 / P2 / P3 / P4       |
| Timeline Version               | `1.0 / 1.1 / Final`     |
| Timeline Owner                 | `Name / Role`           |
| Contributors                   | `Name, Name, Name`      |
| Reviewed By                    | `Name / Role`           |
| Approved By                    | `Name / Role`           |
| Date Prepared (UTC)            | `YYYY-MM-DD HH:MM`      |
| Last Updated (UTC)             | `YYYY-MM-DD HH:MM`      |
| Client/Tenant (MSSP only)      | `Client ID / Name`      |
| Classification                 | Internal – Confidential |
| Default Timezone               | UTC                     |
| Secondary Timezone (if needed) | `e.g., IST (UTC+5:30)`  |

---

## 8.2 Key Time Markers (Mandatory Summary)

| Marker                         | Timestamp (UTC) | Local Time (if applicable) | Confidence                       |
| ------------------------------ | --------------- | -------------------------- | -------------------------------- |
| Initial Compromise (estimated) |                 |                            | Confirmed / Suspected / Inferred |
| First Malicious Activity       |                 |                            |                                  |
| First Detection                |                 |                            |                                  |
| Alert Generated                |                 |                            |                                  |
| Triage Initiated               |                 |                            |                                  |
| Incident Declared              |                 |                            |                                  |
| Containment Initiated          |                 |                            |                                  |
| Containment Achieved           |                 |                            |                                  |
| Eradication Completed          |                 |                            |                                  |
| Recovery Completed             |                 |                            |                                  |
| Incident Closed                |                 |                            |                                  |

---

## 8.3 Time Delta Analysis (Mandatory)

Calculate key intervals:

| Metric                              | Calculation                                | Value | Target SLA | Met (Y/N) |
| ----------------------------------- | ------------------------------------------ | ----- | ---------- | --------- |
| **Dwell Time**                      | Initial Compromise → First Detection       |       |            |           |
| **MTTD** (Mean Time to Detect)      | First Malicious Activity → First Detection |       |            |           |
| **MTTA** (Mean Time to Acknowledge) | Alert Generated → Triage Initiated         |       |            |           |
| **Time to Declare**                 | First Detection → Incident Declared        |       |            |           |
| **Time to Contain**                 | Incident Declared → Containment Achieved   |       |            |           |
| **Time to Eradicate**               | Containment → Eradication Completed        |       |            |           |
| **Time to Recover**                 | Eradication → Recovery Completed           |       |            |           |
| **MTTR** (Mean Time to Respond)     | Detection → Recovery Completed             |       |            |           |
| **Total Incident Duration**         | Initial Compromise → Incident Closed       |       |            |           |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

---

## 8.4 Detailed Timeline (Mandatory)

> Use this table to capture every relevant event. Add rows as needed.

| #   | Timestamp (UTC) | Local Time | Phase            | Event Description | Source | Confidence | Evidence Ref | Notes |
| --- | --------------- | ---------- | ---------------- | ----------------- | ------ | ---------- | ------------ | ----- |
| 1   |                 |            | Pre-Incident     |                   |        | Confirmed  |              |       |
| 2   |                 |            | Initial Access   |                   |        | Confirmed  |              |       |
| 3   |                 |            | Execution        |                   |        | Confirmed  |              |       |
| 4   |                 |            | Persistence      |                   |        | Suspected  |              |       |
| 5   |                 |            | Discovery        |                   |        | Inferred   |              |       |
| 6   |                 |            | Lateral Movement |                   |        | Confirmed  |              |       |
| 7   |                 |            | C2 Communication |                   |        | Confirmed  |              |       |
| 8   |                 |            | Exfiltration     |                   |        | Suspected  |              |       |
| 9   |                 |            | Impact           |                   |        | Confirmed  |              |       |
| 10  |                 |            | Detection        |                   |        | Confirmed  |              |       |
| 11  |                 |            | Triage           |                   |        | Confirmed  |              |       |
| 12  |                 |            | Escalation       |                   |        | Confirmed  |              |       |
| 13  |                 |            | Containment      |                   |        | Confirmed  |              |       |
| 14  |                 |            | Eradication      |                   |        | Confirmed  |              |       |
| 15  |                 |            | Recovery         |                   |        | Confirmed  |              |       |
| 16  |                 |            | Closure          |                   |        | Confirmed  |              |       |

---

## 8.5 Visual Timeline (Copy/Paste Format)

### 8.5.1 Linear Visual Timeline

```
[YYYY-MM-DD HH:MM] ── Pre-Incident: Vulnerability disclosed
        |
[YYYY-MM-DD HH:MM] ── Initial Access: Phishing email delivered
        |
        | (Dwell Time: X hours)
        |
[YYYY-MM-DD HH:MM] ── Execution: Malware executed on endpoint
        |
[YYYY-MM-DD HH:MM] ── Persistence: Scheduled task created
        |
[YYYY-MM-DD HH:MM] ── Lateral Movement: SMB exploitation
        |
[YYYY-MM-DD HH:MM] ── C2 Communication: Beacon established
        |
[YYYY-MM-DD HH:MM] ── Exfiltration: Data uploaded to external host
        |
[YYYY-MM-DD HH:MM] ── Impact: Files encrypted (ransomware)
        |
[YYYY-MM-DD HH:MM] ── Detection: EDR alert triggered
        |
        | (MTTA: X minutes)
        |
[YYYY-MM-DD HH:MM] ── Triage: L1 analyst review
        |
[YYYY-MM-DD HH:MM] ── Incident Declared: SOC Lead escalation
        |
[YYYY-MM-DD HH:MM] ── Containment: Network isolation
        |
[YYYY-MM-DD HH:MM] ── Eradication: Malware removal
        |
[YYYY-MM-DD HH:MM] ── Recovery: System restoration
        |
[YYYY-MM-DD HH:MM] ── Closed: Incident closure
```

### 8.5.2 Phase-Grouped Summary

```
┌─────────────────────────────────────────────────────────────┐
│ PRE-INCIDENT PHASE                                          │
│   - [HH:MM] Vulnerability published                         │
│   - [HH:MM] No patch applied                                │
├─────────────────────────────────────────────────────────────┤
│ ATTACK PHASE (Dwell: X hours)                               │
│   - [HH:MM] Initial access                                  │
│   - [HH:MM] Execution                                       │
│   - [HH:MM] Persistence                                     │
│   - [HH:MM] Lateral movement                                │
│   - [HH:MM] Exfiltration                                    │
│   - [HH:MM] Impact                                          │
├─────────────────────────────────────────────────────────────┤
│ DETECTION & RESPONSE PHASE                                  │
│   - [HH:MM] Detection (MTTD: X)                             │
│   - [HH:MM] Triage (MTTA: X)                                │
│   - [HH:MM] Containment                                     │
│   - [HH:MM] Eradication                                     │
│   - [HH:MM] Recovery (MTTR: X)                              │
├─────────────────────────────────────────────────────────────┤
│ POST-INCIDENT PHASE                                         │
│   - [HH:MM] Validation                                      │
│   - [HH:MM] Closure                                         │
│   - [Date] PIR conducted                                    │
│   - [Date] RCA completed                                    │
└─────────────────────────────────────────────────────────────┘
```

---

## 8.6 Evidence-to-Timeline Mapping (Mandatory)

| Evidence Source         | Timeline Entries Supported | Total Entries | Quality             |
| ----------------------- | -------------------------- | ------------- | ------------------- |
| SIEM Logs               |                            |               | High / Medium / Low |
| EDR Telemetry           |                            |               |                     |
| Network Logs / PCAP     |                            |               |                     |
| Firewall Logs           |                            |               |                     |
| Email Logs              |                            |               |                     |
| Authentication Logs     |                            |               |                     |
| Application Logs        |                            |               |                     |
| Disk Forensics          |                            |               |                     |
| Memory Forensics        |                            |               |                     |
| Cloud Audit Logs        |                            |               |                     |
| Threat Intel Reports    |                            |               |                     |
| Witness/User Statements |                            |               |                     |

References:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/`
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`

---

## 8.7 Timeline Gaps and Unknowns (Mandatory)

Document gaps in the timeline:

| #   | Gap / Unknown | Reason                                                         | Impact on Analysis | Mitigation |
| --- | ------------- | -------------------------------------------------------------- | ------------------ | ---------- |
| 1   |               | Log retention exceeded / Telemetry missing / Tool not deployed |                    |            |
| 2   |               |                                                                |                    |            |

---

## 8.8 Time Source and Clock Skew Documentation (Mandatory)

| Source System       | Time Source    | Clock Skew Observed | Adjustment Applied |
| ------------------- | -------------- | ------------------- | ------------------ |
| SIEM                | NTP-synced     |                     |                    |
| EDR                 | Endpoint clock |                     |                    |
| Firewall            | NTP-synced     |                     |                    |
| Application Servers | NTP-synced     |                     |                    |
| Cloud Platform      | Cloud provider |                     |                    |
| Witness Statements  | User reported  |                     |                    |

**Note:** If clock skew detected, document adjustment methodology used to normalize timestamps.

---

## 8.9 Confidence Legend (Mandatory)

| Confidence Level | Definition                                   | Evidence Required                       |
| ---------------- | -------------------------------------------- | --------------------------------------- |
| **Confirmed**    | Direct evidence from authoritative source    | Log entry, telemetry, forensic artifact |
| **Suspected**    | Inferred from evidence with high probability | Multiple correlated indicators          |
| **Inferred**     | Hypothesized based on patterns               | Indirect evidence or known TTPs         |
| **Unknown**      | Cannot be determined from available evidence | N/A – mark gap explicitly               |

---

# 9. Timeline Building Methodology (Mandatory)

## 9.1 Step-by-Step Process

| Step | Action                                          | Owner          |
| ---- | ----------------------------------------------- | -------------- |
| 1    | Collect all relevant evidence sources           | Timeline Owner |
| 2    | Normalize timestamps to UTC                     | Timeline Owner |
| 3    | Identify clock skew across sources              | L3 Analyst     |
| 4    | Extract events from each source                 | L2/L3 Analyst  |
| 5    | Plot events chronologically                     | Timeline Owner |
| 6    | Map events to MITRE ATT&CK phases               | L3 Analyst     |
| 7    | Label confidence (Confirmed/Suspected/Inferred) | Timeline Owner |
| 8    | Identify gaps and unknowns                      | Timeline Owner |
| 9    | Calculate time deltas (MTTD, MTTA, MTTR)        | Timeline Owner |
| 10   | Create visual representation                    | Timeline Owner |
| 11   | Review with IR Team Lead                        | IR Team Lead   |
| 12   | Finalize and version-control                    | SOC Manager    |

## 9.2 Recommended Tools

| Tool Type      | Examples                           | Use Case                      |
| -------------- | ---------------------------------- | ----------------------------- |
| SIEM           | Splunk, QRadar, Sentinel           | Log-based timeline extraction |
| Timeline Tools | Plaso/log2timeline, Timesketch     | Forensic timeline creation    |
| Visualization  | Aeon Timeline, Lucidchart, Draw.io | Visual representation         |
| Spreadsheet    | Excel, Google Sheets               | Timeline table maintenance    |
| Note-taking    | Markdown, Notion, OneNote          | Narrative documentation       |

References:
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Forensics-Toolkit-Reference.md`

---

# 10. Timeline Use Cases

## 10.1 For RCA

- Identify root cause through event sequencing
- Identify detection gaps via time delta analysis
- Validate hypothesis with chronological evidence

## 10.2 For Regulatory Reporting

- RBI requires chronological incident narrative
- CERT-In 6-hour report needs initial timeline
- ISO 27001 audit evidence

## 10.3 For Legal / Forensics

- Defensible timeline for legal proceedings
- Chain of custody alignment
- Attribution analysis

## 10.4 For Executive Reporting

- Simplified visual timeline for executive summary
- Key time markers for board reporting
- MTTR/MTTD trending

## 10.5 For Lessons Learned

- Identify response delays
- Identify communication gaps
- Identify detection blind spots

---

# 11. Timeline Versioning (Mandatory)

| Version | Date (UTC) | Updated By | Changes                   | Reason                  |
| ------- | ---------- | ---------- | ------------------------- | ----------------------- |
| 1.0     |            |            | Initial timeline          | Initial RCA             |
| 1.1     |            |            | Added forensic findings   | Deep forensics complete |
| 1.2     |            |            | Updated dwell time        | New evidence found      |
| Final   |            |            | All evidence incorporated | RCA closure             |

---

# 12. Quality Checklist (Pre-Approval)

Before finalizing the timeline:

- [ ] All timestamps in UTC
- [ ] Local time documented where applicable
- [ ] Every entry has evidence reference
- [ ] Confidence level labeled for each entry
- [ ] Time source documented
- [ ] Clock skew analyzed and documented
- [ ] All incident phases covered (pre-incident → closure)
- [ ] Key time markers extracted
- [ ] Time deltas calculated (MTTD, MTTA, MTTR, dwell time)
- [ ] Visual representation created
- [ ] Gaps and unknowns documented
- [ ] Evidence-to-timeline mapping completed
- [ ] MITRE ATT&CK phase mapping (where applicable)
- [ ] Reviewed by IR Team Lead
- [ ] Approved by SOC Manager
- [ ] Version-controlled
- [ ] MSSP: tenant scoping verified

---

# 13. MSSP Considerations (If Applicable)

For MSSP-managed clients:

- Timeline must be **tenant-scoped**; no cross-client data
- Client-facing version must be **sanitized** of internal MSSP processes
- Evidence references must be **client-accessible** (or replaced with summaries)
- Timeline delivery timeline per client SLA
- Forensic-grade timelines maintain Chain of Custody
- Cross-client trend timelines only in **anonymized aggregate**
- Client may request **joint timeline review** for major incidents

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
`07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Incident-Report-Template.md`

---

# 14. Common Timeline Pitfalls

| Pitfall                           | Mitigation                                    |
| --------------------------------- | --------------------------------------------- |
| Mixing timezones                  | Standardize on UTC                            |
| Ignoring clock skew               | Validate NTP and document adjustments         |
| Missing evidence references       | Reference every entry                         |
| Treating inferred as confirmed    | Use confidence labels                         |
| Skipping pre-incident context     | Include known vulnerabilities, recent changes |
| Skipping post-recovery validation | Include monitoring/validation events          |
| No visual representation          | Always create executive-ready visual          |
| Single source dependency          | Cross-reference multiple sources              |
| Not tracking version updates      | Maintain version log                          |
| Sharing without sanitization      | Always sanitize for external sharing          |

---

# 15. Related Documents

| Document                       | Path                                                                                   |
| ------------------------------ | -------------------------------------------------------------------------------------- |
| RCA Template (Master)          | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`                            |
| RCA 5-Why Template             | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-5-Why-Template.md`                      |
| Lessons Learned Template       | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`                    |
| PIR Meeting Agenda             | `08_POST-INCIDENT/08.1_Lessons-Learned/PIR-Meeting-Agenda.md`                          |
| L3 Root Cause Analysis SOP     | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Root-Cause-Analysis.md`                  |
| L3 Advanced Forensics SOP      | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Advanced-Forensics-SOP.md`               |
| Evidence Collection SOP        | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Forensics Toolkit Reference    | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Forensics-Toolkit-Reference.md`          |
| MITRE ATT&CK Quick Reference   | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`        |
| Final Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`                 |
| RBI Mandatory Report Template  | `07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`                |
| SLO Metrics Definition         | `00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`                             |

---

# 16. Revision History

| Version | Date        | Author                    | Changes         |
| ------- | ----------- | ------------------------- | --------------- |
| 1.0     | 30-May-2026 | IR Team Lead / L3 Analyst | Initial version |

---

# 17. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**
