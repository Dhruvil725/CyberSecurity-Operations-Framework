# Ticket Closure Criteria

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Ticket Closure Criteria |
| Document ID | TOOL-TKT-005 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Manager / SOC Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This document defines the mandatory closure criteria, approval requirements, and closure documentation standards for all SOC security tickets.

Ticket closure is critical because:

- Closed tickets become official incident records for audit and compliance
- Incorrect closure can leave active threats unresolved
- Incomplete closure creates evidence gaps and weakens RCA
- SLA and KPI reporting depends on accurate closure times and reasons
- MSSP client reporting depends on consistent closure codes
- Regulatory inspections may require proof of closure validation steps

This document ensures:

- Consistent closure standards across L1/L2/L3/IR teams
- Accurate recording of outcomes (TP/FP/INFO/DUPLICATE)
- Proper approval authority for closure by severity
- Evidence traceability and audit readiness
- Proper linkage to post-incident actions (RCA, lessons learned)

---

# 3. Scope

This standard applies to closure of:

| Ticket Type | Examples |
|---|---|
| Security alerts | SIEM/EDR detections |
| Confirmed incidents | Malware, ransomware, data breach |
| Change requests | Firewall blocks, containment approvals |
| Service requests | Client communication, evidence requests |
| Operational tasks | Health checks, tuning requests |
| MSSP tickets | Client-specific alerts/incidents |
| Post-incident actions | RCA and lessons learned follow-up tickets |

---

# 4. Closure Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Closure is a formal decision | Not a convenience action |
| Closure must be justified | Written rationale required |
| Evidence must be referenced | Every ticket must point to evidence or reasoning |
| Ownership must be clear | Closed by and approved by must be recorded |
| SLA integrity must remain | Closure time must be accurate |
| No premature closure | Must meet all criteria before closing |

---

# 5. Ticket Status Definitions (Closure Context)

| Status | Meaning | Closure Allowed |
|---|---|---|
| New / Open | Ticket created | No |
| In Triage | Initial analysis ongoing | No |
| Escalated | Ownership transfer in progress | No |
| In Investigation | Active investigation ongoing | No |
| Containment | Containment actions ongoing | No |
| Pending Action | Awaiting external input/approval | No (except with documented cancellation) |
| Resolved | Threat addressed; validation pending | No (must complete closure criteria) |
| Closed | Formally completed | Yes |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

# 6. Closure Authority Matrix

Tickets must be closed only by authorized roles:

| Priority | Closure Authority | Additional Requirement |
|---|---|---|
| P1 | IR Team Lead + SOC Manager | Closure approval mandatory |
| P2 | SOC Lead | SOC Manager review if regulatory impact |
| P3 | L2 Analyst (SOC Lead review) | Review mandatory |
| P4 | L1/L2 Analyst | Spot check by SOC Lead |

---

# 7. Mandatory Closure Criteria (All Must Be Met)

A ticket may be closed only when all applicable criteria are satisfied.

---

## 7.1 Administrative Closure Criteria

| Criterion | Required |
|---|---|
| Ticket title meets standard | Yes |
| Priority and severity confirmed | Yes |
| Ownership history complete | Yes |
| All required timestamps populated (UTC) | Yes |
| Closure reason code selected | Yes |
| Closure summary written | Yes |

---

## 7.2 Investigation Completion Criteria

| Criterion | Required |
|---|---|
| Investigation notes are complete and chronological | Yes |
| FP/TP determination documented with rationale | Yes |
| Scope assessment documented (affected hosts/users) | Yes |
| Related alerts/tickets linked | Yes |
| Evidence references recorded (if applicable) | Yes |
| Validation performed and documented | Yes |

---

## 7.3 Containment / Eradication / Recovery Criteria (If Applicable)

| Criterion | Required |
|---|---|
| Containment actions documented | Yes (if containment performed) |
| Containment authorization documented | Yes (if containment performed) |
| Eradication actions documented | Yes (if eradication performed) |
| Recovery actions documented | Yes (if recovery performed) |
| Post-action validation recorded | Yes |

---

## 7.4 Communication and Notification Criteria (If Applicable)

| Criterion | Required |
|---|---|
| SOC Lead notified for P1/P2 | Yes |
| Management notified (P1/P2 or business impact) | Yes (if applicable) |
| Client notified (MSSP as per SLA) | Yes (if applicable) |
| Regulatory notification assessed | Yes (P1/P2 and data breach indicators) |
| Notification timestamps recorded | Yes (if performed) |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 7.5 Post-Incident Requirements (P1/P2 Mandatory)

| Criterion | Required |
|---|---|
| RCA initiated and referenced | Yes (P1/P2) |
| Lessons learned initiated and referenced | Yes (P1/P2) |
| Detection improvement logged (if needed) | Yes (where applicable) |
| Control gap logged (if applicable) | Yes (where applicable) |

Reference:
`08_POST-INCIDENT/08.1_Lessons-Learned/`
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/`
`08_POST-INCIDENT/08.3_Improvement-Tracking/`

---

# 8. Closure Reason Codes (Mandatory)

Every closed ticket must use one standard closure reason code.

| Code | Meaning | When to Use |
|---|---|---|
| TP-CONTAINED | True positive; threat contained | Confirmed malicious activity contained and validated |
| TP-ERADICATED | True positive; threat eradicated | Malware removed/persistence cleared, validated clean |
| TP-RECOVERED | True positive; recovery completed | Systems restored, validated and monitoring resumed |
| TP-ESCALATED | True positive; transferred to major incident/IR | When moved under separate IR case/ticket |
| FP-IT | False positive; legitimate IT activity | Approved change/activity caused alert |
| FP-TOOL | False positive; tool or rule misfire | Detection error or tuning required |
| INFO | Informational; no action required | Benign alerts with documentation |
| DUPLICATE | Duplicate ticket | Duplicate of existing ticket |
| CANCELLED | Cancelled request | Only with SOC Lead approval and documented reason |

---

# 9. Closure Summary Standard (Mandatory Format)

The closure summary must be written so any analyst/auditor can understand exactly what happened and what was done.

Closure summary must include:

| Item | Required |
|---|---|
| What was detected and when | Yes |
| What investigation steps were performed | Yes |
| What the conclusion was (TP/FP) and why | Yes |
| What actions were taken (containment/eradication/recovery) | If applicable |
| What validation was performed | Yes |
| Any remaining follow-up actions and references | If applicable |

---

## 9.1 Closure Summary Template

Use this template:

**Detection:**  
- [What was detected], [source], [time UTC]

**Triage & Investigation:**  
- [What was checked], [tools used], [key findings]

**Conclusion:**  
- [TP/FP/INFO], [rationale]

**Actions Taken:**  
- [Containment/eradication/recovery], [who executed], [who approved], [time UTC]

**Validation:**  
- [How confirmed clean / resolved]

**Evidence References:**  
- [Links/paths to evidence, queries, screenshots]

**Follow-ups:**  
- [RCA ticket], [Lessons learned], [tuning task]

---

## 9.2 Example Closure Summary (Good)

**Detection:**  
- SIEM alert for encoded PowerShell execution on FIN-WS-12 at 2026-05-25 03:14 UTC.

**Triage & Investigation:**  
- L1 reviewed process tree and user context. L2 decoded command and confirmed malicious download attempt. No lateral movement observed.

**Conclusion:**  
- TP-ERADICATED. Malicious execution confirmed; isolated to single host.

**Actions Taken:**  
- Host FIN-WS-12 isolated via EDR at 04:00 UTC (Executed by IR Team – D.Patel; Authorized by SOC Manager – K.Singh). Malware removed and persistence cleared.

**Validation:**  
- EDR full scan clean; no IOC matches in SIEM for 24 hours post containment.

**Evidence References:**  
- /evidence/INC-2026-0001/process-tree.png  
- /evidence/INC-2026-0001/decoded-command.txt

**Follow-ups:**  
- RCA initiated: RCA-2026-0001. Detection tuning task created: DET-IMP-2026-0012.

---

# 10. Evidence Requirements at Closure

Closure must reference evidence or justify why no evidence exists.

| Scenario | Evidence Required |
|---|---|
| True Positive (TP) | Mandatory evidence references and artifacts |
| False Positive (FP) | Evidence of legitimacy (change ticket, IT confirmation, rule explanation) |
| Informational (INFO) | Supporting context and reasoning |
| Duplicate | Link to primary ticket |
| Cancelled | SOC Lead approval note and reason |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 11. Special Closure Cases

---

## 11.1 Duplicate Ticket Closure

A duplicate ticket may be closed only if:

| Requirement | Standard |
|---|---|
| Primary ticket is identified | Mandatory |
| Duplicate clearly links to primary ticket | Mandatory |
| Notes copied or referenced | Mandatory |
| Duplicate marked as DUPLICATE | Mandatory |

---

## 11.2 Escalated Ticket Closure

When closing a ticket due to escalation:

| Requirement | Standard |
|---|---|
| New incident ticket created and referenced | Mandatory |
| Escalation notes recorded | Mandatory |
| Closure code set to TP-ESCALATED | Mandatory |
| Ownership transfer confirmed | Mandatory |

---

## 11.3 Closure While Pending Action

Tickets in **Pending Action** may only be closed if:

| Condition | Requirement |
|---|---|
| External dependency resolved | Evidence documented |
| Request withdrawn | Written confirmation retained |
| Ticket cancelled | SOC Lead approval required |

---

# 12. Closure Quality Review (QA)

SOC Lead/SOC Manager performs closure QA to ensure:

| QA Item | Check |
|---|---|
| Correct priority used | Yes |
| SLA timestamps correct | Yes |
| Notes complete and chronological | Yes |
| Evidence referenced | Yes |
| Closure code correct | Yes |
| Escalation documentation complete | If applicable |
| MSSP client fields complete | If applicable |

QA sampling requirements:

| Ticket Priority | Minimum QA Sampling |
|---|---|
| P1 | 100% |
| P2 | 50% |
| P3 | 20% |
| P4 | 10% |

---

# 13. SLA and Metrics Impact

Closure time drives:

- Mean Time to Acknowledge (MTTA)
- Mean Time to Triage (MTTT)
- Mean Time to Respond (MTTR)
- SLA compliance tracking
- MSSP reporting accuracy
- Audit evidence integrity

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

---

# 14. Related Documents

| Document | Path |
|---|---|
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Ticket Priority Matrix | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Priority-Matrix.md` |
| Ticket Escalation Workflow | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Escalation-Workflow.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| Internal SLA Definitions | `00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Lessons Learned Template | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md` |
| RCA Template | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md` |
| Management Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md` |

---

# 15. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | SOC Manager / SOC Operations Lead | Initial version |

---

# 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**