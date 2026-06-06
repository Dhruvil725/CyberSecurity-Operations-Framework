# TEMPLATE: L2 Shift Handover Procedures and Template

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Template – L2 Shift Handover Procedures and Template |
| Document ID | SOC-L2-TMP-009 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / SOC Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This document defines the operational procedures, communication standards, and documentation requirements for Level 2 (L2) SOC shift handovers.

Shift handover is one of the most operationally critical activities in a 24x7 SOC environment because incomplete or inaccurate handovers can result in:

- Missed attacker activity
- Delayed incident response
- Investigation gaps
- Duplicate investigative effort
- SLA violations
- Missed escalations
- Containment delays
- Loss of operational continuity

The purpose of this procedure is to ensure:

- Continuous investigative coverage
- Accurate transfer of operational context
- Consistent communication between shifts
- Proper escalation awareness
- Preservation of investigation continuity
- Effective prioritization of ongoing incidents

This SOP applies to:

- Internal SOC operations
- MSSP multi-tenant operations
- P1/P2 active incidents
- Ongoing investigations
- Threat hunting activities
- Escalated incidents
- Regulatory-impacting incidents

---

# 3. Scope

Applies to all L2 shift transitions involving:

| Operational Area | Example |
|---|---|
| Active investigations | Malware analysis |
| Escalated incidents | IR escalation |
| Ongoing containment | Endpoint isolation |
| Threat hunting operations | IOC hunting |
| SLA-sensitive tickets | Client escalation |
| MSSP tenant incidents | Multi-client operations |
| Pending evidence collection | Forensic support |
| Regulatory-impacting incidents | Data exposure |

---

# 4. Shift Handover Philosophy (IMPORTANT)

A shift handover is not simply a status update.

The objective is to ensure the incoming analyst can immediately continue operations without loss of:

- Context
- Timeline understanding
- Investigation continuity
- Escalation awareness
- Threat visibility
- Containment status

The outgoing analyst must assume:

“If I leave incomplete information, the next analyst may miss a critical threat.”

The incoming analyst must assume:

“If I do not validate the handover, I may inherit operational risk.”

---

## 4.1 Common Handover Failures

| Poor Practice | Operational Risk |
|---|---|
| Incomplete ticket notes | Investigation delays |
| No timeline summary | Context loss |
| Missing escalation details | Missed response |
| No pending actions listed | Operational gaps |
| Weak prioritization | SLA breaches |
| No ownership assignment | Accountability gaps |

---

# 5. L2 Shift Handover Responsibilities

---

## 5.1 Outgoing Analyst Responsibilities

| Responsibility | Description |
|---|---|
| Update tickets | Ensure current status |
| Summarize investigations | Provide operational context |
| Document pending actions | Maintain continuity |
| Identify escalation status | Ensure awareness |
| Transfer evidence references | Preserve investigation integrity |
| Communicate priorities | Guide incoming analyst |

---

## 5.2 Incoming Analyst Responsibilities

| Responsibility | Description |
|---|---|
| Review handover notes | Understand context |
| Validate priorities | Confirm urgency |
| Confirm ownership | Maintain accountability |
| Review escalations | Ensure continuity |
| Verify pending actions | Continue investigation |
| Clarify uncertainties | Reduce operational risk |

---

# 6. Shift Handover Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Review Active Work | Operational overview |
| Phase 2 | Update Tickets | Accurate documentation |
| Phase 3 | Prioritize Incidents | Operational focus |
| Phase 4 | Conduct Verbal Handover | Context transfer |
| Phase 5 | Confirm Ownership | Accountability transfer |
| Phase 6 | Validate Handover | Operational continuity |

---

# 7. Phase 1 – Review Active Work

Before handover, the outgoing analyst must review all active operational items.

---

## 7.1 Active Work Categories

| Category | Example |
|---|---|
| Active incidents | Ransomware investigation |
| Escalated tickets | IR Team engagement |
| Threat hunting activities | IOC searches |
| Pending containment | Endpoint isolation |
| Evidence collection | PCAP exports |
| SLA-sensitive investigations | P1/P2 incidents |

---

## 7.2 Active Work Validation Checklist

| Validation Item | Completed |
|---|---|
| All active tickets reviewed | ☐ |
| Ticket priorities validated | ☐ |
| Escalations documented | ☐ |
| Pending actions identified | ☐ |
| SLA risks reviewed | ☐ |
| Evidence references updated | ☐ |

---

# 8. Phase 2 – Ticket Update Requirements

All tickets must be updated before shift handover.

---

## 8.1 Required Ticket Updates

| Requirement | Purpose |
|---|---|
| Current status | Operational awareness |
| Timeline summary | Investigation continuity |
| Actions completed | Context preservation |
| Pending actions | Next-step guidance |
| Escalation status | Response awareness |
| Evidence references | Investigation integrity |

---

## 8.2 Ticket Documentation Standards

GOOD:
“EDR telemetry confirmed encoded PowerShell execution on FIN-WS-12 at 02:14 UTC. Host isolated at 02:22 UTC. DNS beaconing to malicious domain blocked at firewall. Pending memory acquisition by L3 team.”

BAD:
“Host suspicious. Needs review.”

---

## 8.3 Ticket Prioritization Matrix

| Priority | Response Focus |
|---|---|
| P1 | Immediate response |
| P2 | High urgency |
| P3 | Standard investigation |
| P4 | Routine review |

---

# 9. Phase 3 – Prioritize Incidents

The outgoing analyst must clearly identify operational priorities.

---

## 9.1 Priority Incident Categories

| Category | Priority Level |
|---|---|
| Active ransomware | Critical |
| Active exfiltration | Critical |
| Domain compromise | Critical |
| Cloud admin compromise | Critical |
| Ongoing beaconing | High |
| Credential abuse | High |
| Suspicious anomalies | Medium |

---

## 9.2 SLA Risk Identification

| Risk Type | Example |
|---|---|
| Escalation delay | P1 not acknowledged |
| Investigation backlog | Multiple unresolved P2 |
| Evidence collection delay | Volatile logs pending |
| Client notification pending | MSSP SLA risk |

---

# 10. Phase 4 – Verbal Handover Procedures

A verbal handover must occur for all critical investigations.

---

## 10.1 Mandatory Verbal Handover Conditions

Verbal handover is mandatory for:

| Condition | Reason |
|---|---|
| Active P1 incident | Operational urgency |
| IR Team engagement | Coordination continuity |
| Ongoing exfiltration | Immediate risk |
| SLA breach risk | Escalation awareness |
| Multi-client MSSP impact | Business risk |

---

## 10.2 Verbal Handover Requirements

The outgoing analyst must explain:

- Current incident status
- Timeline summary
- Threat severity
- Actions completed
- Pending actions
- Escalation status
- Containment status
- Evidence preservation status
- Client communication status
- SLA concerns

---

## 10.3 Handover Communication Channels

| Channel | Usage |
|---|---|
| SOC bridge call | Critical incidents |
| Secure messaging | Operational updates |
| Ticketing system | Documentation |
| Shift briefing | Team-wide awareness |

---

# 11. Phase 5 – Ownership Transfer

Ownership transfer must be explicit and documented.

---

## 11.1 Ownership Transfer Rules

| Rule | Requirement |
|---|---|
| Ticket ownership updated | Mandatory |
| Incoming analyst acknowledged | Required |
| Escalation ownership clarified | Mandatory |
| Pending tasks assigned | Required |

---

## 11.2 Ownership Tracking Table

| Ticket ID | Current Owner | New Owner | Priority | Confirmed |
|---|---|---|---|---|
| | | | | |

---

# 12. Phase 6 – Handover Validation

The incoming analyst must validate the handover.

---

## 12.1 Incoming Analyst Validation Checklist

| Validation Item | Completed |
|---|---|
| Active incidents reviewed | ☐ |
| Ticket notes reviewed | ☐ |
| Escalations understood | ☐ |
| Pending actions identified | ☐ |
| SLA risks understood | ☐ |
| Ownership confirmed | ☐ |

---

## 12.2 Clarification Requirements

The incoming analyst must seek clarification if:

- Timeline is unclear
- Severity appears inaccurate
- Escalation status uncertain
- Evidence references missing
- Containment status unclear
- SLA deadlines not documented

---

# 13. Critical Incident Handover Procedures

Critical incidents require enhanced handover controls.

---

## 13.1 Critical Incident Requirements

| Requirement | Mandatory |
|---|---|
| Verbal handover | Yes |
| SOC Lead awareness | Yes |
| Bridge call continuity | Yes |
| Escalation status review | Yes |
| Evidence tracking validation | Yes |
| SLA review | Yes |

---

## 13.2 Critical Incident Tracking Table

| Incident ID | Severity | Current Status | Escalated To | SLA Risk |
|---|---|---|---|---|
| | | | | |

---

# 14. MSSP Shift Handover Requirements

MSSP environments require additional controls.

---

## 14.1 MSSP Operational Requirements

| Requirement | Purpose |
|---|---|
| Client segregation maintained | Prevent data leakage |
| Client SLA reviewed | Contract compliance |
| Cross-client impact identified | Operational awareness |
| Client communication status updated | Escalation continuity |
| Tenant visibility restrictions followed | Compliance |

---

## 14.2 Client-Specific Handover Table

| Client | Active Incidents | Priority | SLA Risk | Escalated |
|---|---|---|---|---|
| | | | | |

---

# 15. Escalation Awareness During Handover

The outgoing analyst must identify all active escalations.

---

## 15.1 Escalation Categories

| Escalation Type | Example |
|---|---|
| L2 to L3 | Memory forensics |
| L2 to IR Team | Ransomware |
| Legal escalation | Data breach |
| Executive escalation | Business impact |
| Client escalation | MSSP notification |

---

## 15.2 Escalation Tracking Table

| Incident | Escalation Target | Status | Awaiting Response? |
|---|---|---|---|
| | | | |

---

# 16. Evidence Awareness During Handover

The outgoing analyst must identify evidence-related operational risks.

---

## 16.1 Evidence Status Review

| Evidence Activity | Status |
|---|---|
| Log exports completed | ☐ |
| PCAP collection completed | ☐ |
| Hash verification completed | ☐ |
| Chain-of-custody updated | ☐ |
| Volatile evidence pending | ☐ |

---

## 16.2 Volatile Evidence Risk Conditions

Immediate attention required if:

- Memory capture pending
- Logs approaching rotation
- Active network sessions ongoing
- Cloud logs nearing expiration
- Endpoint scheduled for reboot

---

# 17. Shift Handover Documentation Template

---

## 17.1 Shift Summary

| Field | Information |
|---|---|
| Shift Date | |
| Outgoing Analyst | |
| Incoming Analyst | |
| Shift Timing | |
| SOC Lead | |

---

## 17.2 Active Incidents Summary

| Incident ID | Severity | Status | Current Owner | Next Action |
|---|---|---|---|---|
| | | | | |

---

## 17.3 Pending Actions

| Action | Assigned To | Deadline | Priority |
|---|---|---|---|
| | | | |

---

## 17.4 Escalation Summary

| Incident | Escalated To | Status | Follow-Up Required |
|---|---|---|---|
| | | | |

---

## 17.5 SLA Risk Summary

| Ticket/Incident | SLA Risk | Required Action |
|---|---|---|
| | | |

---

# 18. Common Shift Handover Mistakes

| Mistake | Operational Risk |
|---|---|
| Incomplete ticket updates | Investigation delays |
| No verbal handover | Context loss |
| Missing escalation details | Missed response |
| Weak prioritization | SLA violations |
| No ownership confirmation | Accountability gaps |
| No pending action tracking | Operational confusion |

---

# 19. Related Documents

| Document | Path |
|---|---|
| L2 Investigation SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md` |
| L2 Escalation Criteria | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Escalation-Criteria.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Ticket Escalation Workflow | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Escalation-Workflow.md` |
| SOC Lead Shift Management | `03_SOC-TIER-PROCEDURES/03.4_SOC-Lead-Procedures/SOCLead-Shift-Management.md` |
| Emergency P1 Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md` |

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