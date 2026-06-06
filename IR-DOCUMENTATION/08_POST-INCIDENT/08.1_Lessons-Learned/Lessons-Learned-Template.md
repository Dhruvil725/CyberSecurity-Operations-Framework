# Lessons Learned Template (Post-Incident Review)

---

# 1. Document Control

| Field          | Value                                             |
| -------------- | ------------------------------------------------- |
| Document Name  | Template – Lessons Learned (Post-Incident Review) |
| Document ID    | PIR-LL-001                                        |
| Version        | 1.0                                               |
| Effective Date | 30-May-2026                                       |
| Owner          | IR Team Lead / SOC Manager                        |
| Approved By    | CISO                                              |
| Classification | Internal – Confidential                           |
| Review Cycle   | Annually              |

---

# 2. Purpose

This template provides the standardized **Lessons Learned (LL)** format used during **Post-Incident Reviews (PIR)** to capture insights, identify improvement opportunities, and drive continual improvement of the incident response program.

Lessons Learned are critical because:

- NIST SP 800-61 mandates post-incident review as the final phase of the IR lifecycle
- ISO 27001 Annex A.5.27 requires learning from incidents
- RBI Cyber Security Framework expects RCA and improvement tracking
- repeated incidents indicate uncaptured or unimplemented lessons
- audits expect documented LL with traceable corrective actions
- MSSP operations require client-facing LL reports for transparency
- LL feeds into playbook updates, detection engineering, and training

This template ensures:

- consistent structure across all PIR sessions
- clear identification of what went well and what didn't
- traceable corrective actions with owners and due dates
- linkage to RCA, playbook updates, and detection improvements
- evidence-ready documentation for audits and management reviews

Reference alignment:
`00_GOVERNANCE/00.1_Policies/IR-Policy-Master.md`
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`

---

# 3. Scope

This template is used for:

| Scenario                  | Requirement                                     |
| ------------------------- | ----------------------------------------------- |
| P1 incidents              | **Mandatory** within 5 working days of closure  |
| P2 incidents              | **Mandatory** within 10 working days of closure |
| P3 incidents (TP)         | **Recommended** if significant learnings exist  |
| P4 incidents              | Optional (only if pattern observed)             |
| Near-miss events          | **Recommended** to capture preventive learnings |
| MSSP client incidents     | Per client SLA and contractual requirement      |
| Tabletop exercises        | **Mandatory** post-exercise                     |
| Red/Purple team exercises | **Mandatory** post-exercise                     |

Out of scope:

- false positive closures with no learning value
- routine operational issues handled in BAU

References:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

# 4. Definitions

| Term                   | Definition                                                             |
| ---------------------- | ---------------------------------------------------------------------- |
| PIR                    | Post-Incident Review – structured meeting to discuss incident handling |
| Lessons Learned (LL)   | Documented insights from incident handling for improvement             |
| Corrective Action (CA) | Action taken to address identified gap or weakness                     |
| Preventive Action (PA) | Action taken to prevent recurrence                                     |
| Root Cause             | Underlying cause identified through RCA                                |
| Action Owner           | Person accountable for completing corrective/preventive action         |
| Blameless Review       | Review focused on process/system improvement, not individual blame     |

---

# 5. Roles and Responsibilities

| Role                     | Responsibilities                                                    |
| ------------------------ | ------------------------------------------------------------------- |
| PIR Facilitator          | Conducts PIR session; ensures blameless culture; documents findings |
| IR Team Lead             | Owns LL document; presents incident timeline and analysis           |
| SOC Lead                 | Provides SOC perspective; identifies process/tooling gaps           |
| L1/L2/L3 Analysts        | Share frontline observations and constraints faced                  |
| SOC Manager              | Approves LL; ensures actions are tracked; reports to management     |
| CISO                     | Reviews LL for major incidents; approves strategic actions          |
| Action Owners            | Execute assigned corrective/preventive actions within timelines     |
| Compliance Lead          | Ensures LL aligns with audit/regulatory requirements                |
| MSSP SDM (if applicable) | Coordinates client-facing LL share-out                              |

---

# 6. PIR Principles (Mandatory)

| Principle       | Description                                                    |
| --------------- | -------------------------------------------------------------- |
| Blameless       | Focus on systems/processes, not individuals                    |
| Timely          | Conduct within defined timelines post-closure                  |
| Inclusive       | Include all stakeholders involved in response                  |
| Evidence-based  | Use ticket data, timestamps, and evidence references           |
| Action-oriented | Every finding must have a corresponding action or rationale    |
| Traceable       | Actions linked to improvement registers and tracked to closure |
| Honest          | Document what didn't go well candidly                          |
| Confidential    | LL is internal; sanitized version may be shared externally     |

---

# 7. Template (Copy/Paste)

## 7.1 PIR Metadata (Mandatory)

| Field                       | Value                        |
| --------------------------- | ---------------------------- |
| PIR ID                      | `PIR-YYYY-####`              |
| Incident ID / Ticket ID     | `INC-YYYY-####`              |
| Incident Category           | `...`                        |
| Incident Severity (Final)   | P1 / P2 / P3 / P4            |
| Incident Closure Date (UTC) | `YYYY-MM-DD HH:MM`           |
| PIR Date (UTC)              | `YYYY-MM-DD HH:MM`           |
| PIR Facilitator             | `Name / Role`                |
| PIR Duration                | `e.g., 60 mins`              |
| PIR Mode                    | In-Person / Virtual / Hybrid |
| Document Prepared By        | `Name / Role`                |
| Reviewed By                 | `Name / Role`                |
| Approved By                 | `Name / Role`                |
| Client/Tenant (MSSP only)   | `Client ID / Name`           |
| Classification              | Internal – Confidential      |

---

## 7.2 Attendees (Mandatory)

| Name | Role                     | Team                | Attended (Y/N) |
| ---- | ------------------------ | ------------------- | -------------- |
|      | IR Team Lead             | IR                  |                |
|      | SOC Lead                 | SOC                 |                |
|      | L2 Analyst               | SOC                 |                |
|      | L3 Analyst               | SOC                 |                |
|      | SOC Manager              | SOC                 |                |
|      | CISO                     | Security Leadership |                |
|      | Compliance Lead          | Compliance          |                |
|      | IT Operations Rep        | IT Ops              |                |
|      | Business Stakeholder     | Business            |                |
|      | MSSP SDM (if applicable) | MSSP                |                |

---

## 7.3 Incident Summary (Mandatory)

- **Brief Description:** `1–2 line summary of incident`
- **Detection Source:** `SIEM / EDR / User / Threat Intel / Client / Other`
- **Detection Time (UTC):** `...`
- **Containment Time (UTC):** `...`
- **Resolution Time (UTC):** `...`
- **Total Duration:** `...`
- **Scope:** `Systems / Users / Data affected`
- **Business Impact:** `...`
- **Root Cause (Summary):** `...` (full RCA in separate document)

Reference:
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`

---

## 7.4 Timeline Review (Mandatory)

| Phase                       | Time Taken | SLA/Target | Met (Y/N) | Notes |
| --------------------------- | ---------- | ---------- | --------- | ----- |
| Detection to Triage         |            |            |           |       |
| Triage to Declaration       |            |            |           |       |
| Declaration to Containment  |            |            |           |       |
| Containment to Eradication  |            |            |           |       |
| Eradication to Recovery     |            |            |           |       |
| Recovery to Closure         |            |            |           |       |
| **Total Incident Duration** |            |            |           |       |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

---

## 7.5 What Went Well (Mandatory)

> Document strengths to reinforce and replicate.

| #   | Observation | Category                      | Reinforce How? |
| --- | ----------- | ----------------------------- | -------------- |
| 1   |             | People / Process / Technology |                |
| 2   |             |                               |                |
| 3   |             |                               |                |

**Examples to consider:**

- Detection was timely (within SLA)
- Escalation worked smoothly
- Containment decision was well-coordinated
- Communication to stakeholders was effective
- Evidence collection was complete
- Playbook was clear and followed
- Tool functioned as expected

---

## 7.6 What Did Not Go Well (Mandatory)

> Document gaps candidly without blame.

| #   | Observation | Category                      | Impact | Root Cause Link |
| --- | ----------- | ----------------------------- | ------ | --------------- |
| 1   |             | People / Process / Technology |        |                 |
| 2   |             |                               |        |                 |
| 3   |             |                               |        |                 |

**Examples to consider:**

- Detection delayed due to tuning gap
- Escalation matrix was unclear
- Playbook was outdated
- Evidence was missing/incomplete
- Tool/log source was unavailable
- Communication breakdown with stakeholders
- Containment took longer than expected
- Recovery validation was insufficient

---

## 7.7 Gaps Identified (Mandatory)

### 7.7.1 People Gaps

| Gap | Impact | Recommendation |
| --- | ------ | -------------- |
|     |        |                |

### 7.7.2 Process Gaps

| Gap | Impact | Recommendation |
| --- | ------ | -------------- |
|     |        |                |

### 7.7.3 Technology Gaps

| Gap | Impact | Recommendation |
| --- | ------ | -------------- |
|     |        |                |

### 7.7.4 Detection Gaps

| Gap | Impact | Recommendation |
| --- | ------ | -------------- |
|     |        |                |

### 7.7.5 Documentation Gaps

| Gap | Impact | Recommendation |
| --- | ------ | -------------- |
|     |        |                |

---

## 7.8 Corrective and Preventive Actions (Mandatory)

| Action ID | Action Description | Category                                         | Type (CA/PA) | Owner | Due Date (UTC) | Priority         | Status | Tracking Ref |
| --------- | ------------------ | ------------------------------------------------ | ------------ | ----- | -------------- | ---------------- | ------ | ------------ |
| CA-001    |                    | Playbook / Detection / Tool / Training / Process | CA / PA      |       |                | High / Med / Low | Open   |              |
| CA-002    |                    |                                                  |              |       |                |                  |        |              |
| CA-003    |                    |                                                  |              |       |                |                  |        |              |

References:
`08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`
`08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`

---

## 7.9 Playbook / Documentation Updates (Mandatory)

| Document        | Current Version | Update Required | Owner | Target Date |
| --------------- | --------------- | --------------- | ----- | ----------- |
| `Playbook name` |                 |                 |       |             |
| `SOP name`      |                 |                 |       |             |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`

---

## 7.10 Detection Engineering Improvements (Mandatory)

| Detection Gap | New Rule/Use Case Required | Tool               | Owner | Target Date |
| ------------- | -------------------------- | ------------------ | ----- | ----------- |
|               |                            | SIEM / EDR / Other |       |             |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

## 7.11 Training Needs Identified (Optional)

| Training Topic | Target Audience         | Mode                           | Owner | Target Date |
| -------------- | ----------------------- | ------------------------------ | ----- | ----------- |
|                | L1 / L2 / L3 / IR / All | Classroom / Self-paced / Drill |       |             |

---

## 7.12 Threat Intelligence Output (If Applicable)

| Item                  | Value | Shared With             | Reference |
| --------------------- | ----- | ----------------------- | --------- |
| IOCs extracted        |       | TI Platform / Internal  |           |
| TTPs documented       |       | Internal Knowledge Base |           |
| Threat actor insights |       |                         |           |

Reference:
`08_POST-INCIDENT/08.4_Threat-Intel-Output/`

---

## 7.13 Key Metrics (Mandatory)

| Metric                               | Value | Target | Met (Y/N) |
| ------------------------------------ | ----- | ------ | --------- |
| MTTD (Mean Time to Detect)           |       |        |           |
| MTTA (Mean Time to Acknowledge)      |       |        |           |
| MTTR (Mean Time to Respond)          |       |        |           |
| Time to Contain                      |       |        |           |
| Time to Eradicate                    |       |        |           |
| Time to Recover                      |       |        |           |
| False Positive Rate (related alerts) |       |        |           |

---

## 7.14 Risk Assessment Update (If Applicable)

- **Did this incident reveal new risks?** Yes / No
- **Are existing risks materialized?** Yes / No
- **Risk register update required?** Yes / No
- **Risk owner notified:** Yes / No

| Risk Description | Likelihood | Impact | Treatment Plan | Owner |
| ---------------- | ---------- | ------ | -------------- | ----- |
|                  |            |        |                |       |

---

## 7.15 Management Reporting (Mandatory for P1/P2)

- **Reported to CISO:** Yes / No (Date: `...`)
- **Reported to Executive Management:** Yes / No (Date: `...`)
- **Reported to Board / Audit Committee:** Yes / No (Date: `...`)
- **Client briefing completed (MSSP):** Yes / No (Date: `...`)

---

# 8. Action Tracking and Closure

## 8.1 Action Tracking Rules

- All actions must be entered into `Action-Items-Tracker.xlsx`
- Each action must have a single accountable owner
- Due dates must be realistic and tracked
- Status updates required bi-weekly until closure
- Overdue actions escalated to SOC Manager
- Closed actions require evidence of completion

## 8.2 LL Closure Criteria

LL document is considered "Closed" when:

- [ ] All sections completed
- [ ] All actions assigned with owners and due dates
- [ ] Actions logged in tracker
- [ ] Document approved by SOC Manager
- [ ] Document distributed to stakeholders
- [ ] Filed in incident archive

---

# 9. MSSP Considerations (If Applicable)

For MSSP-managed clients:

- LL must be **tenant-scoped**; no cross-client information
- **Sanitized client-facing version** prepared separately if shared
- Client review/approval may be required per SLA
- Client-specific corrective actions tracked separately
- LL filed in **client-specific evidence folder**
- MSSP-internal LL maintained for service improvement
- Cross-client trends analyzed only in aggregated, anonymized form

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
`07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Incident-Report-Template.md`

---

# 10. Quality Checklist (Pre-Approval)

Before finalizing the LL document:

- [ ] All mandatory sections completed
- [ ] Blameless language used throughout
- [ ] Timeline review completed with SLA comparison
- [ ] What went well documented (minimum 3 items)
- [ ] What didn't go well documented (minimum 3 items)
- [ ] Gaps identified across People/Process/Technology
- [ ] Every gap has corresponding action or rationale for no action
- [ ] All actions have owners and due dates
- [ ] Actions logged in Action-Items-Tracker
- [ ] Playbook/Detection updates identified
- [ ] Metrics captured with target comparison
- [ ] Document reviewed by IR Team Lead
- [ ] Document approved by SOC Manager
- [ ] MSSP: tenant scoping verified

---

# 11. Related Documents

| Document                       | Path                                                                            |
| ------------------------------ | ------------------------------------------------------------------------------- |
| PIR Meeting Agenda             | `08_POST-INCIDENT/08.1_Lessons-Learned/PIR-Meeting-Agenda.md`                   |
| Lessons Learned Register       | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Register.xlsx`           |
| Action Items Tracker           | `08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`               |
| RCA Template                   | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`                     |
| Security Improvement Register  | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx` |
| Playbook Update Log            | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`             |
| Detection Improvement Log      | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`       |
| Final Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`          |
| SLO Metrics Definition         | `00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`                      |

---

# 12. Revision History

| Version | Date        | Author                     | Changes         |
| ------- | ----------- | -------------------------- | --------------- |
| 1.0     | 30-May-2026 | IR Team Lead / SOC Manager | Initial version |

---

# 13. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**
