# ISO/IEC 27001 Incident Notification (ISMS Requirement)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – ISO/IEC 27001 Incident Notification |
| Document ID | REG-COM-002 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | ISMS Manager / SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines the organization’s internal process to ensure **information security events and incidents** are:

- recorded,
- assessed,
- escalated,
- communicated to appropriate internal stakeholders, and
- logged in a manner consistent with **ISO/IEC 27001:2022** ISMS requirements.

ISO 27001 incident notification is critical because:

- ISO 27001 requires structured handling and documentation of information security incidents
- Audit readiness depends on traceable evidence of detection, response, communication, and improvement
- Timely internal notification enables risk-based decisions and containment actions
- Major incidents often trigger compliance/legal actions and management review
- MSSP operations require tenant-safe incident logs and client notification alignment

This SOP ensures:

- consistent incident notification workflows aligned to ISO clauses and Annex A controls
- a clear internal communication path by severity
- proper evidence logging in the ticketing system and ISMS incident log
- linkage to corrective actions and continual improvement (Clause 10)

---

# 3. ISO Alignment (Reference Summary)

This SOP supports alignment to:

- **ISO/IEC 27001:2022 Clause 8** (Operation) – operational planning and control for incident handling
- **Clause 9** (Performance Evaluation) – monitoring, measurement, internal audit, management review
- **Clause 10** (Improvement) – nonconformity and corrective actions
- **Annex A controls** related to incident management:
  - A.5.24 Incident management planning and preparation
  - A.5.25 Assessment and decision on information security events
  - A.5.26 Response to information security incidents
  - A.5.27 Learning from information security incidents
  - A.5.28 Collection of evidence

Reference:
`00_GOVERNANCE/00.1_Policies/IR-Policy-ISO27001-Alignment.md`

---

# 4. Scope

This SOP applies to:

| Area | Included |
|---|---|
| Information security events | Alerts, suspicious activity, policy violations |
| Information security incidents | Confirmed compromise, malware, breach, ransomware, etc. |
| Notification recipients | SOC Lead, IR Team, ISMS Manager, management, compliance/legal as applicable |
| Records | Ticketing system + ISO incident log + evidence references |
| Environments | Internal operations + MSSP (client scope separately maintained) |

Out of scope:

- Regulatory submissions (handled in CERT-In/RBI SOPs)
- Detailed technical response steps (covered in playbooks and SOC procedures)

---

# 5. Definitions

| Term | Definition |
|---|---|
| Event | Observable occurrence that may impact information security |
| Incident | Confirmed event that compromises confidentiality, integrity, or availability |
| ISMS incident log | Central record maintained for ISO 27001 audit trail |
| Notification | Communication to stakeholders that an event/incident occurred and requires action/awareness |
| Corrective action | Action to eliminate cause of nonconformity and prevent recurrence |
| PIR | Post Incident Review / Lessons Learned session |

---

# 6. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L1 Analyst | Records event in ticket; initial triage; escalates based on severity |
| L2/L3 Analysts | Investigation; evidence references; severity reassessment; technical reporting |
| SOC Lead | Confirms severity; triggers notifications; ensures cadence; ensures ticket quality |
| IR Team Lead | Incident command for P1/P2; containment authority; directs response |
| SOC Manager | Governance oversight; ensures metrics and audit readiness |
| ISMS Manager | Ensures ISO incident logging, classification, corrective action tracking |
| Compliance/Legal | Advises on breach notification obligations and legal hold |
| CISO | Executive approval for major incidents and external communications |
| MSSP SDM | Ensures client communications and tenant segregation (MSSP) |

References:
`07_REPORTING/07.4_Regulatory-Reports/ISO27001-Incident-Log.md`  
`08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`

---

# 7. ISO Incident Notification Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Record everything | Every event/incident must be logged in ticketing system |
| Severity-driven notification | Notifications must follow defined escalation paths |
| Timely communication | Notify stakeholders early; update as facts mature |
| Audit-ready | Communications must be traceable and reproducible |
| Evidence traceability | Evidence references must be captured and retained |
| Continual improvement | Incidents must generate lessons learned and corrective actions where required |
| Confidentiality | Share only what is needed; follow classification rules |

---

# 8. Notification Triggers and Thresholds

## 8.1 Event vs Incident Threshold

| Classification | Trigger | Required Action |
|---|---|---|
| Security Event | Suspicious activity without confirmation | Record ticket; assess; escalate if needed |
| Security Incident | Confirmed compromise, policy breach with impact | Record ticket; notify SOC Lead; IR activation as needed |
| Major Incident | P1/P2 with significant impact | Bridge call; management escalation; ISO incident log update |

Reference:
`01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Master-Triage-Decision-Tree.md`

## 8.2 ISO Notification Triggers (Minimum)

Notify ISMS Manager when:

| Trigger | Severity |
|---|---|
| Any P1 incident | Mandatory |
| Any P2 incident | Mandatory |
| Any incident involving sensitive data | Mandatory |
| Any incident with service disruption | Mandatory |
| Any incident likely to create nonconformity/corrective action | Mandatory |
| Repeated P3 incidents indicating control weakness | As required |

---

# 9. Notification Timelines (Internal Targets)

| Severity | Notify SOC Lead | Notify IR Team | Notify ISMS Manager | Notify Management |
|---|---:|---:|---:|---:|
| P1 | ≤ 15 min | ≤ 30 min | ≤ 60 min | ≤ 30 min |
| P2 | ≤ 30 min | ≤ 60 min (if containment needed) | ≤ 4 hours | ≤ 2 hours (if material risk) |
| P3 | ≤ 2 hours | As needed | Same business day | As needed |
| P4 | ≤ 4 hours | No | Weekly summary (optional) | No |

References:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md`

---

# 10. Notification Workflow (ISO-Aligned)

## 10.1 Step 1 — Record and Classify (SOC)

Owner: L1/L2

Mandatory actions:

1. Create ticket (or confirm existing ticket)
2. Assign:
   - severity (P1–P4)
   - category
   - affected assets/users
   - detection time (UTC)
3. Add initial triage notes and evidence references
4. Escalate per severity

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

## 10.2 Step 2 — Notify Stakeholders (SOC Lead / IR Team Lead)

Owner: SOC Lead

- Trigger bridge call for P1 (mandatory)
- Notify ISMS Manager for P1/P2 and sensitive incidents
- Notify compliance/legal when breach is possible
- Ensure notification and updates are documented in ticket

References:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`

---

## 10.3 Step 3 — Update ISO Incident Log (ISMS Manager)

Owner: ISMS Manager

For P1/P2 incidents, ISMS Manager must:

- Create/update entry in ISO incident log
- Ensure fields are complete and align to audit expectations
- Link the ticket ID and evidence references

Reference:
`07_REPORTING/07.4_Regulatory-Reports/ISO27001-Incident-Log.md`

---

## 10.4 Step 4 — Track Corrective Actions (Clause 10)

Owner: ISMS Manager + SOC Manager

Trigger corrective action when:

- control failure is identified
- process nonconformity is found (e.g., missed SLA)
- repeated incident patterns indicate systemic weakness

Corrective action record must include:

- root cause summary
- corrective action plan
- owner and due date
- validation method
- closure evidence

References:
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`  
`08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`

---

# 11. Required Recordkeeping (Audit Readiness)

## 11.1 Mandatory Records (Minimum)

| Record | Where Stored |
|---|---|
| Incident ticket | Ticketing system |
| Notification records (who/when/how) | Ticket + email/chat logs as permitted |
| Evidence references | Evidence repository + ticket links |
| ISO incident log entry | ISO incident log |
| PIR / Lessons learned | PIR register and meeting notes |
| Corrective actions | Improvement trackers / CAPA system |

References:
`08_POST-INCIDENT/08.1_Lessons-Learned/`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

## 11.2 Ticket Fields Required for ISO Evidence

At minimum, ensure ticket includes:

- detection time and response times (UTC)
- severity classification and changes (with approvals)
- actions taken with timestamps and owners
- evidence references
- closure code and closure summary

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 12. MSSP Considerations (ISO Context)

For MSSP-managed clients:

- Maintain client-specific incident logs where contractually required
- Ensure tenant-safe evidence storage and communications
- Align client notifications to contract SLAs (may differ from internal targets)
- Ensure ISO incident log does not include sensitive client details beyond what is required

References:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`  
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 13. Common Audit Findings and Preventive Controls

| Audit Finding | Risk | Preventive Control |
|---|---|---|
| Missing incident log entries | ISO nonconformity | Mandatory ISMS Manager notification triggers |
| Incomplete timestamps | SLA and audit gaps | UTC required fields and ticket QA |
| No evidence references | Weak defensibility | Evidence handling SOP and checklists |
| No corrective actions from repeated incidents | Lack of continual improvement | CAPA workflow + quarterly review |
| Severity changes without approval | Governance failure | SOC Lead/SOC Manager approval gates |

---

# 14. Related Documents

| Document | Path |
|---|---|
| IR Policy ISO Alignment | `00_GOVERNANCE/00.1_Policies/IR-Policy-ISO27001-Alignment.md` |
| ISO Incident Log | `07_REPORTING/07.4_Regulatory-Reports/ISO27001-Incident-Log.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Ticket Closure Criteria | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md` |
| Escalation Matrix Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| Lessons Learned Register | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Register.xlsx` |
| RCA Template | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md` |
| CERT-In Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md` |

---

# 15. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | ISMS Manager / SOC Manager | Initial version |

---

# 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**