# SOP: L1 Ticket Creation Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L1 Ticket Creation Procedures |
| Document ID | SOC-L1-SOP-005 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / SOC Operations Lead |
| Approved By | SOC Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the standardized process for creating, updating, and managing incident tickets at the Level 1 (L1) SOC tier.

Ticketing is one of the most operationally critical functions in a SOC because the incident ticket becomes:

- The official investigation record
- The primary communication mechanism between analysts
- The operational timeline of the incident
- Audit evidence during compliance review
- A legal and forensic reference during major incidents
- The basis for metrics, reporting, and lessons learned

Poor ticket quality creates serious operational problems including:

- Investigation delays
- Escalation confusion
- Incomplete evidence tracking
- SLA violations
- Audit failures
- Incident duplication
- Loss of historical context

This SOP ensures tickets are:

- Accurate
- Consistent
- Traceable
- Action-oriented
- Audit-ready
- Useful to L2/L3 and IR teams

---

# 3. Scope

Applies to ticket creation for:

- SIEM alerts
- EDR alerts
- IDS/IPS detections
- Malware incidents
- Phishing alerts
- Cloud security incidents
- Identity compromise
- Threat intelligence matches
- MSSP client incidents
- Escalated operational issues

Applicable systems include:

- ITSM platforms
- SOC ticketing systems
- MSSP case management platforms
- Integrated SIEM ticketing modules

---

# 4. Ticketing Philosophy (IMPORTANT)

The ticket is not just administrative documentation.

A properly written ticket must allow:

- Another analyst to continue investigation immediately
- IR teams to understand incident state quickly
- Auditors to reconstruct analyst actions
- Management to assess operational impact
- Legal teams to review evidence chain

The ticket should answer:

- What happened?
- When did it happen?
- Who was involved?
- Which systems were affected?
- What actions were taken?
- What evidence exists?
- What remains unresolved?

---

# 5. Ticket Lifecycle Overview

| Phase | Description |
|---|---|
| Phase 1 | Alert triggers ticket |
| Phase 2 | Initial triage and enrichment |
| Phase 3 | Severity assignment |
| Phase 4 | Escalation or investigation |
| Phase 5 | Resolution or closure |
| Phase 6 | Documentation retention |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

# 6. When a Ticket Must Be Created

A ticket must be created when:

| Condition | Ticket Required? |
|---|---|
| Confirmed malicious activity | Yes |
| Suspicious activity requiring investigation | Yes |
| Escalation to L2/L3 required | Yes |
| Potential SLA impact exists | Yes |
| Monitoring outage detected | Yes |
| False positive validated | Usually Yes |
| Duplicate alert of active incident | Link to existing ticket |

---

# 7. Ticket Creation Workflow

| Phase | Objective |
|---|---|
| Phase 1 | Create initial ticket |
| Phase 2 | Populate mandatory fields |
| Phase 3 | Add enrichment and evidence |
| Phase 4 | Assign severity |
| Phase 5 | Escalate if required |
| Phase 6 | Maintain updates |

---

# 8. Phase 1 – Initial Ticket Creation

Tickets should be created immediately after initial triage confirms the alert requires investigation or escalation.

---

## 8.1 Initial Ticket Timing

| Severity | Ticket Creation Requirement |
|---|---|
| P1 | Immediate |
| P2 | Within SLA |
| P3 | During triage workflow |
| P4 | As required |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 8.2 Initial Ticket Naming Convention

Use clear and structured naming.

### Format

`[Severity] – [Incident Type] – [Affected Asset/User] – [Primary Indicator]`

### Examples

GOOD:
- P1 – Ransomware – FIN-SRV-01 – Mass Encryption Activity
- P2 – Credential Attack – VPN User Admin01 – Impossible Travel
- P2 – Cloud Incident – AWS Root Account – Unauthorized API Activity

BAD:
- Weird Alert
- Possible Attack
- Malware Maybe

---

# 9. Phase 2 – Mandatory Ticket Fields

Every ticket must include mandatory information.

---

## 9.1 Core Ticket Fields

| Field | Requirement |
|---|---|
| Ticket ID | Auto-generated |
| Severity | Mandatory |
| Alert source | Mandatory |
| Timestamp (UTC) | Mandatory |
| Analyst name | Mandatory |
| Affected host/user | Mandatory |
| Incident summary | Mandatory |
| Current status | Mandatory |

---

## 9.2 Technical Fields

| Field | Example |
|---|---|
| Source IP | 10.10.20.15 |
| Destination IP | 185.x.x.x |
| Username | admin01 |
| Process name | powershell.exe |
| File hash | SHA256 |
| Domain | suspicious-domain.com |

---

## 9.3 Business Context Fields (IMPORTANT)

Many SOCs ignore business context, which reduces operational effectiveness.

Always document:

| Business Context | Why Important |
|---|---|
| Asset criticality | Prioritization |
| Business owner | Escalation |
| Production or test system | Impact assessment |
| Sensitive data involved | Regulatory impact |
| Client environment | MSSP handling |

---

# 10. Phase 3 – Enrichment and Evidence Documentation

---

## 10.1 Required Enrichment

The ticket must contain:

- Threat intelligence results
- Asset context
- Authentication context
- Historical activity
- Correlated alerts
- Related incident references

---

## 10.2 Evidence Documentation Standards

Every important observation must reference evidence.

Examples:

GOOD:
- “EDR alert ID 48392 shows LSASS access by powershell.exe at 14:22 UTC.”

BAD:
- “Looks like credential dumping.”

---

## 10.3 Evidence Reference Table

| Evidence Type | Reference |
|---|---|
| SIEM Alert ID | |
| EDR Detection ID | |
| Firewall Event | |
| PCAP Reference | |
| Ticket Attachment | |

---

# 11. Phase 4 – Severity Assignment

Severity must be documented clearly.

---

## 11.1 Severity Justification (IMPORTANT)

Always explain WHY severity assigned.

GOOD:
“Assigned P1 due to confirmed ransomware encryption activity affecting production finance server.”

BAD:
“P1 because looks critical.”

---

## 11.2 Severity Upgrade Rules

Upgrade severity immediately if:

| Condition | Upgrade |
|---|---|
| Multiple systems affected | Increase severity |
| Privileged accounts involved | Increase severity |
| Data exfiltration suspected | Increase severity |
| Cloud admin compromise | Increase severity |
| Domain controller impacted | Increase severity |

---

# 12. Phase 5 – Escalation Documentation

When escalating:

- Record escalation timestamp
- Record recipient/team
- Record escalation reason
- Attach supporting evidence
- Update ticket status

---

## 12.1 Escalation Note Example

“Escalated to L2 at 14:31 UTC due to confirmed beaconing behavior from critical finance server communicating with known malicious infrastructure.”

---

# 13. Phase 6 – Ticket Maintenance (IMPORTANT)

A ticket must remain operationally useful throughout the incident lifecycle.

---

## 13.1 Update Frequency Requirements

| Severity | Update Frequency |
|---|---|
| P1 | Every 30 minutes minimum |
| P2 | As investigation progresses |
| P3 | During major changes |
| P4 | As required |

---

## 13.2 Ticket Hygiene Requirements

The analyst must ensure:

- Notes are chronological
- UTC timestamps used consistently
- Duplicate notes avoided
- Technical language clear
- Assumptions avoided

---

# 14. Ticket Closure Requirements

Before closure:

| Requirement | Status |
|---|---|
| Investigation completed | ☐ |
| Severity finalized | ☐ |
| Escalation documented | ☐ |
| False positive rationale documented | ☐ |
| Evidence references attached | ☐ |
| Final summary added | ☐ |

---

# 15. Ticket Writing Best Practices

---

## 15.1 Good Ticket Writing Principles

Tickets should be:

- Concise
- Technical
- Clear
- Timestamped
- Evidence-based

---

## 15.2 Avoid These Practices

| Bad Practice | Risk |
|---|---|
| Vague notes | Investigation confusion |
| Missing timestamps | Timeline gaps |
| Missing evidence references | Audit failure |
| Emotional language | Professional risk |
| Unsupported assumptions | Incorrect escalation |

---

# 16. Ticketing During Major Incidents (IMPORTANT)

During P1 incidents:

- Ticket updates become operational command history
- Every containment action must be documented
- Every escalation must be timestamped
- Every communication affecting response must be logged

During bridge calls:
Assign one analyst for ticket documentation if possible.

---

# 17. MSSP Ticketing Requirements

For MSSP operations:

- Maintain tenant separation
- Use client-specific categorization
- Follow client naming conventions
- Apply client SLA tracking
- Avoid cross-client references

---

# 18. Metrics and Quality Monitoring

SOC management should track:

| Metric | Purpose |
|---|---|
| Ticket quality score | Documentation quality |
| Missing fields | Operational compliance |
| SLA compliance | Response efficiency |
| Ticket update frequency | Incident visibility |
| Duplicate tickets | Operational maturity |

---

# 19. Common Ticketing Mistakes

| Mistake | Operational Risk |
|---|---|
| Poor summaries | Escalation confusion |
| Missing timestamps | Timeline gaps |
| No severity rationale | Audit issues |
| Weak evidence references | Investigation delays |
| Delayed updates | Loss of operational visibility |

---

## 20. Related Documents

| Document | Path |
|---|---|
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| L1 Alert Handling SOP | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md` |
| L1 Escalation Criteria | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Escalation-Criteria.md` |
| Ticket Closure Criteria | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md` |

---

## 21. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / SOC Operations Lead | Initial version |

---

## 22. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**