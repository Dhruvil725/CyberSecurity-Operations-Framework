# SOP: Ticket Lifecycle Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Ticket Lifecycle Procedures |
| Document ID | TOOL-TKT-001 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / SOC Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the complete lifecycle of a security incident ticket from creation through closure within the SOC ticketing system.

The ticket lifecycle is foundational to SOC operations because:

- Every alert, incident, or task must be tracked in a ticket
- Ticket quality directly impacts investigation quality
- Audit and compliance evidence depends on accurate ticket records
- SLA management is driven by ticket timings
- Escalation workflows depend on proper ticket status management
- MSSP client reporting depends on ticket data accuracy

This SOP ensures:

- Consistent ticket creation standards
- Accurate status management throughout incident lifecycle
- Proper evidence references documented in tickets
- Clear ownership and accountability at each stage
- Audit-ready ticket records
- SLA-compliant handling
- Multi-tier escalation alignment (L1/L2/L3/IR)

---

# 3. Scope

This SOP applies to all ticketing activities for:

| Ticket Type | Examples |
|---|---|
| Security alerts | SIEM/EDR alerts requiring investigation |
| Confirmed incidents | Malware, ransomware, breach |
| Change requests | Firewall blocks, containment approvals |
| Service requests | Client notification, evidence requests |
| Operational tasks | Coverage checks, health checks |
| MSSP client incidents | Client-specific incidents |
| Post-incident actions | RCA, lessons learned tracking |

---

# 4. Ticketing Principles (IMPORTANT)

| Principle | Requirement |
|---|---|
| One ticket per incident | Avoid duplicate tracking |
| Real-time updates | Ticket must reflect current status always |
| UTC timestamps | All entries must use UTC |
| Reproducible notes | Notes must be readable by any analyst |
| Evidence linked | Evidence references documented in ticket |
| Ownership is explicit | Owner must be named at every stage |
| Closure is validated | Closure requires documented rationale |

---

# 5. Roles and Responsibilities

| Role | Ticketing Responsibilities |
|---|---|
| L1 Analyst | Create tickets, initial triage notes, escalation handoff |
| L2 Analyst | Update tickets during investigation, evidence references, severity updates |
| L3 Analyst | Update tickets with forensic findings, escalation packages |
| SOC Lead | Validate severity, monitor SLA, escalation oversight |
| IR Team | Update tickets during major incident, closure recommendation |
| SOC Manager | Quality review, KPI tracking |
| MSSP Service Delivery | Client-specific ticket reporting and SLA tracking |

---

# 6. Ticket Lifecycle Stages

| Stage | Status | Description |
|---|---|---|
| Stage 1 | New / Open | Ticket created from alert or report |
| Stage 2 | In Triage | L1 initial investigation underway |
| Stage 3 | Escalated | Handed to L2/L3 or IR Team |
| Stage 4 | In Investigation | Active analysis underway |
| Stage 5 | Containment | Containment actions in progress |
| Stage 6 | Pending Action | Awaiting approval/external input |
| Stage 7 | Resolved | Threat addressed; awaiting final validation |
| Stage 8 | Closed | All criteria met; formally closed |

---

# 7. Ticket Lifecycle Workflow

| Phase | Objective | Owner |
|---|---|---|
| Phase 1 | Ticket Creation | L1 Analyst |
| Phase 2 | Initial Triage | L1 Analyst |
| Phase 3 | Severity Assignment | L1 / SOC Lead |
| Phase 4 | Escalation (if required) | L1/L2/SOC Lead |
| Phase 5 | Investigation | L2/L3 Analyst |
| Phase 6 | Containment | IR Team / SOC Lead |
| Phase 7 | Resolution | L2/L3/IR Team |
| Phase 8 | Closure | SOC Lead / IR Team Lead |

---

# 8. Phase 1 — Ticket Creation (Mandatory Standards)

Every alert or incident must have a ticket created within SLA timelines.

---

## 8.1 Ticket Creation Triggers

| Trigger | Source |
|---|---|
| SIEM alert | Automated or manual |
| EDR alert | Automated or manual |
| User-reported incident | Helpdesk/direct report |
| Client-reported incident | MSSP client |
| Threat intel match | TI platform IOC hit |
| Manual discovery | Analyst during hunting |

---

## 8.2 Mandatory Ticket Creation Fields (Minimum)

| Field | Requirement |
|---|---|
| Ticket ID | Auto-generated |
| Title | Descriptive (not "Alert #1234") |
| Severity | P1/P2/P3/P4 |
| Detection source | SIEM/EDR/Manual/Client |
| Affected host(s) | Hostname/IP |
| Affected user(s) | Username/Account |
| Detection time (UTC) | From alert or report |
| Ticket creation time (UTC) | Mandatory |
| Assigned to | Named owner |
| Initial description | What was detected |
| Status | New/Open |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

## 8.3 Title Standards (Mandatory)

Good ticket titles must include the key context:

| Format | Example |
|---|---|
| `[Severity] – [Alert Type] – [Host/User]` | `P2 – Encoded PowerShell – FIN-WS-12` |
| `[Severity] – [Incident Type] – [Client]` | `P1 – Ransomware – ClientABC` |
| `[Severity] – [Threat Category]` | `P3 – Suspicious LOLBin Execution` |

---

# 9. Phase 2 — Initial Triage

---

## 9.1 L1 Triage Requirements

L1 analysts must complete within SLA:

| Task | Purpose |
|---|---|
| Review alert source/type | Context |
| Check host criticality | Severity validation |
| Check user privilege level | Risk assessment |
| Review parent process / alert details | Initial investigation |
| Search for related alerts | Pattern detection |
| Confirm false positive or escalate | Decision point |

---

## 9.2 Triage Notes Standard (Ticket Update)

| Field | Requirement |
|---|---|
| Actions taken | What was reviewed |
| Findings | What was observed |
| FP/TP decision | Documented rationale |
| Evidence | Alert IDs / screenshots / queries |
| Next action | Escalate / monitor / close |

---

## 9.3 Documentation Quality Example

GOOD:
"Reviewed alert: PowerShell encoded command observed on FIN-WS-12 at 03:14 UTC. Parent process: WINWORD.EXE. User: jsmith (standard user). Related alerts: none. Assessed as TP - escalating to L2."

BAD:
"Looks suspicious. Escalated."

---

# 10. Phase 3 — Severity Assignment

---

## 10.1 Severity Assignment Criteria

| Severity | Criteria Summary |
|---|---|
| P1 | Active compromise, ransomware, domain-wide risk, data breach |
| P2 | Likely compromise, privileged accounts, lateral movement |
| P3 | Suspicious activity requiring investigation |
| P4 | Low-risk, informational |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Priority-Matrix.md`

---

## 10.2 Severity Validation Requirements

| Requirement | Standard |
|---|---|
| Severity must be reviewed at each major update | Mandatory |
| Severity upgrades must be documented with reason | Mandatory |
| Severity downgrades require SOC Lead approval | Mandatory |

---

# 11. Phase 4 — Escalation

---

## 11.1 Escalation Documentation Requirements

All escalations must be recorded in the ticket:

| Field | Requirement |
|---|---|
| Escalation time (UTC) | Mandatory |
| Escalated to | Named person/team |
| Escalation reason | Technical justification |
| Evidence package reference | Links to evidence |
| New owner | Updated in ticket |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Escalation-Workflow.md`

---

# 12. Phase 5 — Investigation

---

## 12.1 Investigation Update Standards

Tickets must be updated at regular intervals:

| Severity | Minimum Update Frequency |
|---|---|
| P1 | Every 30 minutes |
| P2 | Every 60 minutes |
| P3 | At key milestones |
| P4 | At completion |

---

## 12.2 Investigation Notes Must Include

| Item | Requirement |
|---|---|
| Analyst name | Who performed action |
| Timestamp (UTC) | When |
| Action performed | What |
| Tools/queries used | How |
| Findings | What was discovered |
| Evidence references | Linked artifacts |

---

# 13. Phase 6 — Containment

---

## 13.1 Containment Documentation Requirements

| Field | Requirement |
|---|---|
| Action taken | Specific containment |
| System/user targeted | Scope |
| Time of action (UTC) | Mandatory |
| Executed by | Named person |
| Authorized by | Named approver |
| Outcome | Result of action |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 14. Phase 7 — Resolution

---

## 14.1 Resolution Criteria

Ticket may move to "Resolved" when:

| Criterion | Required |
|---|---|
| Threat activity stopped | Yes |
| Persistence removed | Yes |
| Affected systems identified | Yes |
| Evidence preserved | Yes |
| Stakeholders notified | Yes |
| RCA initiated (P1/P2) | Mandatory |

---

## 14.2 Resolution Notes Standard

| Item | Requirement |
|---|---|
| Resolution summary | What was done |
| Eradication steps | Actions taken |
| Validation performed | How confirmed clean |
| Outstanding actions | If any |
| Post-incident tracking | RCA/Lessons learned ticket |

---

# 15. Phase 8 — Closure

---

## 15.1 Closure Criteria (All Must Be Met)

| Criterion | Required |
|---|---|
| Severity confirmed | Yes |
| Investigation completed | Yes |
| Evidence documented | Yes |
| Containment confirmed | Yes |
| Stakeholders notified | Yes |
| Closure reason documented | Yes |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md`

---

## 15.2 Closure Approval Requirements

| Severity | Closure Authority |
|---|---|
| P1 | IR Team Lead + SOC Manager |
| P2 | SOC Lead |
| P3 | L2 Analyst (SOC Lead review) |
| P4 | L1/L2 Analyst |

---

## 15.3 Standard Closure Reason Codes

| Code | Meaning |
|---|---|
| TP-CONTAINED | True positive; threat contained |
| TP-ESCALATED | True positive; escalated to IR |
| FP-IT | False positive; IT activity |
| FP-TOOL | False positive; known tool |
| INFO | Informational; no action required |
| DUPLICATE | Duplicate of another ticket |

---

# 16. SLA Requirements (Ticket-Level)

| SLA Metric | P1 | P2 | P3 | P4 |
|---|---|---|---|---|
| Ticket creation | Immediate | 15 min | 30 min | 1 hour |
| Initial triage | 15 min | 30 min | 2 hours | 4 hours |
| Escalation acknowledgment | 15 min | 30 min | 2 hours | 4 hours |
| Status update frequency | 30 min | 1 hour | Milestones | Completion |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

# 17. MSSP-Specific Ticket Requirements

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Client ID tagged in ticket | Tenant tracking |
| Client-specific SLA applied | Contract compliance |
| Evidence segregated per client | Compliance |
| Client communication documented | Audit trail |
| Client reporting extracted from ticket | Monthly reports |

---

# 18. Common Ticketing Mistakes

| Mistake | Operational Risk |
|---|---|
| Vague ticket titles | Investigation confusion |
| Missing timestamps | SLA and audit failures |
| No evidence references | Investigation gaps |
| Not updating during investigation | Management visibility loss |
| Premature closure | Residual threat risk |
| Missing ownership | Accountability gaps |

---

# 19. Related Documents

| Document | Path |
|---|---|
| Ticket Priority Matrix | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Priority-Matrix.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| Ticket Escalation Workflow | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Escalation-Workflow.md` |
| Ticket Closure Criteria | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md` |
| Internal SLA Definitions | `00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md` |
| Severity Classification Guide | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md` |

---

# 20. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / SOC Operations Lead | Initial version |

---

# 21. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**