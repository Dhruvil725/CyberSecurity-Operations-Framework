# SOP: L1 Alert Handling Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L1 Alert Handling Procedures |
| Document ID | SOC-L1-SOP-002 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / L1 Operations Lead |
| Approved By | SOC Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the standardized process for handling security alerts at the Level 1 (L1) SOC tier.

L1 alert handling is one of the most critical operational functions within a Security Operations Center because:

- L1 analysts are the first human reviewers of security events
- Early detection quality directly impacts incident severity
- Delayed triage can allow attackers to escalate privileges or move laterally
- Improper classification can lead to missed incidents or unnecessary escalations
- Inconsistent handling creates operational and audit risks

The purpose of this SOP is to ensure:

- Consistent and repeatable alert triage
- Proper severity classification
- Accurate ticket creation and escalation
- Timely response within SLA
- Effective communication with L2/L3 teams
- Operational discipline during high alert volume

This SOP must be followed for every alert regardless of perceived severity.

---

# 3. Scope

Applies to all alerts generated from:

- SIEM platforms
- EDR/XDR platforms
- IDS/IPS systems
- Firewall monitoring
- Email security gateways
- Threat intelligence feeds
- Cloud security platforms
- Authentication monitoring
- Data loss prevention systems
- MSSP-managed client environments

---

# 4. Objectives of L1 Alert Handling

The primary objectives of L1 alert handling are:

| Objective | Description |
|---|---|
| Validate Alerts | Determine whether alert is legitimate |
| Reduce False Positives | Prevent unnecessary escalations |
| Identify Real Threats Quickly | Escalate confirmed threats rapidly |
| Maintain SLA Compliance | Meet operational response timelines |
| Preserve Evidence | Avoid losing critical telemetry |
| Maintain Documentation | Ensure accurate incident records |

---

# 5. L1 Analyst Responsibilities

The L1 analyst is responsible for:

- Reviewing incoming alerts continuously
- Performing initial triage
- Validating whether activity is malicious
- Enriching alerts with context and threat intelligence
- Creating and updating tickets
- Assigning initial severity
- Escalating according to defined criteria
- Communicating urgent incidents immediately
- Documenting all actions accurately

L1 analysts must not:

- Attempt unauthorized containment
- Delete evidence or logs
- Ignore low-confidence alerts without validation
- Delay escalation waiting for complete certainty

---

# 6. Alert Handling Workflow

| Phase | Objective |
|---|---|
| Phase 1 | Alert receipt and acknowledgement |
| Phase 2 | Initial validation |
| Phase 3 | Context enrichment |
| Phase 4 | Threat assessment |
| Phase 5 | Severity classification |
| Phase 6 | Ticket creation/update |
| Phase 7 | Escalation or closure |

---

# 7. Phase 1 – Alert Receipt and Acknowledgement

Every alert must be acknowledged within the defined SLA.

---

## 7.1 Initial Alert Validation

Upon receiving an alert:

- Confirm alert source platform
- Confirm timestamp is accurate
- Confirm log ingestion is functioning
- Identify source and destination systems
- Identify associated user accounts
- Determine whether the alert is duplicated

---

## 7.2 SLA Awareness (IMPORTANT)

L1 analysts must always monitor SLA timers.

Failure to acknowledge high-severity alerts within SLA may:

- Delay containment
- Increase incident impact
- Trigger compliance violations
- Create audit findings

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 7.3 Immediate Escalation Alerts

The following alerts require immediate escalation even before full triage:

| Alert Type | Escalation |
|---|---|
| Ransomware execution | Immediate IR escalation |
| Domain admin compromise | Immediate L2/L3 escalation |
| Confirmed data exfiltration | Immediate IR escalation |
| Cloud root/admin compromise | Immediate IR escalation |
| Active malware outbreak | Immediate escalation |
| Critical infrastructure compromise | Immediate escalation |

---

# 8. Phase 2 – Initial Validation

Initial validation determines whether the alert may represent legitimate malicious activity.

---

## 8.1 Validation Questions

| Question | Purpose |
|---|---|
| Is the alert source reliable? | Alert quality assessment |
| Is the affected system critical? | Business impact assessment |
| Has this alert occurred before? | Pattern analysis |
| Is activity expected or approved? | False positive validation |
| Does behavior match known attack patterns? | Threat assessment |

---

## 8.2 Common False Positive Sources

| Source | Example |
|---|---|
| Vulnerability scanners | Nessus, Qualys |
| Admin scripts | PowerShell automation |
| Backup systems | High-volume data movement |
| IT tools | PsExec, RMM tools |
| Cloud automation | Infrastructure provisioning |

---

## 8.3 False Positive Validation (IMPORTANT)

False positives must never be dismissed casually.

Before closing as false positive:

- Validate source system
- Confirm business context
- Check previous occurrences
- Confirm expected activity with owner if required
- Document justification clearly

Reference:
`03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-False-Positive-Handling.md`

---

# 9. Phase 3 – Context Enrichment

Context enrichment transforms raw alerts into actionable intelligence.

---

## 9.1 Required Enrichment Activities

| Enrichment Type | Purpose |
|---|---|
| Asset enrichment | Determine criticality |
| User enrichment | Identify privilege level |
| Threat intelligence | Check malicious reputation |
| Historical activity | Identify recurring behavior |
| Geolocation | Identify suspicious origin |
| Authentication correlation | Detect account abuse |

---

## 9.2 Threat Intelligence Checks

For external IPs/domains:

- Check reputation
- Check malware association
- Check C2 classification
- Check sandbox references
- Check recent campaign association

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md`

---

## 9.3 Contextual Risk Indicators

Indicators increasing risk:

| Indicator | Risk Level |
|---|---|
| Privileged account involved | High |
| Critical server targeted | High |
| Multiple systems involved | High |
| Known malicious IP | High |
| Beaconing behavior | Critical |
| Impossible travel login | High |

---

# 10. Phase 4 – Threat Assessment

L1 analysts must determine whether observed activity appears:

- Benign
- Suspicious
- Malicious
- Critical

---

## 10.1 Threat Assessment Categories

| Category | Description |
|---|---|
| Benign | Legitimate activity |
| Suspicious | Requires further investigation |
| Malicious | Confirmed attacker activity |
| Critical | Immediate organizational risk |

---

## 10.2 Behavioral Indicators (IMPORTANT)

Behavior often matters more than signatures.

Examples:

| Behavior | Potential Threat |
|---|---|
| Repeated failed logins | Password spraying |
| Consistent outbound beaconing | C2 activity |
| PowerShell spawning from Office | Phishing compromise |
| DNS high-entropy queries | Tunneling |
| LSASS memory access | Credential dumping |

---

# 11. Phase 5 – Severity Classification

Severity determines escalation urgency and response priority.

---

## 11.1 Severity Assignment Matrix

| Severity | Description |
|---|---|
| P1 | Critical business impact or active compromise |
| P2 | High-confidence malicious activity |
| P3 | Suspicious activity requiring investigation |
| P4 | Informational or low-risk activity |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/`

---

## 11.2 Severity Escalation Factors

Severity increases if:

- Multiple systems affected
- Privileged accounts involved
- Data exfiltration suspected
- Malware execution confirmed
- Cloud admin accounts affected
- Critical business systems impacted

---

# 12. Phase 6 – Ticket Creation and Documentation

Every confirmed or suspicious alert requires a properly documented ticket.

---

## 12.1 Required Ticket Fields

| Field | Requirement |
|---|---|
| Alert source | Mandatory |
| Timestamp (UTC) | Mandatory |
| Affected asset | Mandatory |
| User/account | Mandatory |
| Severity | Mandatory |
| Alert summary | Mandatory |
| Analyst actions | Mandatory |
| Escalation details | Mandatory |

---

## 12.2 Ticket Documentation Standards

Tickets must be:

- Clear
- Technically accurate
- Timestamped
- Professional
- Action-oriented

Avoid vague notes such as:
- “Looks suspicious”
- “Probably malware”
- “Investigating”

Instead use:
- “PowerShell spawned from WINWORD.EXE observed on workstation X”
- “Outbound HTTPS beaconing to known malicious IP confirmed”

---

# 13. Phase 7 – Escalation Procedures

Escalation must occur immediately once criteria met.

---

## 13.1 Escalation Criteria

| Condition | Escalation Target |
|---|---|
| Malware execution | L2 |
| Credential dumping | L2/L3 |
| Data exfiltration | IR Team |
| Ransomware indicators | IR Team |
| Cloud admin compromise | IR Team |
| Multiple hosts affected | L2 |

Reference:
`03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Escalation-Criteria.md`

---

## 13.2 Escalation Quality (IMPORTANT)

Poor escalation causes investigation delays.

A good escalation must include:

- Clear summary
- Severity
- Evidence references
- Timeline
- Actions already taken
- Current risk assessment

---

# 14. Alert Prioritization Strategy

When alert volume is high, prioritize:

| Priority | Alert Type |
|---|---|
| 1 | Active compromise |
| 2 | Data exfiltration |
| 3 | Credential abuse |
| 4 | Malware execution |
| 5 | Lateral movement |
| 6 | Policy violations |

---

# 15. Monitoring Discipline During High Alert Volume

High alert volume is one of the biggest SOC operational risks.

During alert floods:

- Continue risk-based prioritization
- Do not skip enrichment
- Do not bulk-close alerts without validation
- Notify SOC Lead if backlog develops
- Track SLA exposure continuously

---

# 16. MSSP-Specific Alert Handling

For MSSP operations:

- Maintain tenant segregation
- Follow client-specific SLA
- Use client-specific escalation matrix
- Document all client interactions
- Escalate cross-client incidents immediately

Reference:
`09_MSSP-SPECIFIC/`

---

# 17. Common L1 Alert Handling Mistakes

| Mistake | Operational Risk |
|---|---|
| Delayed escalation | Increased attacker dwell time |
| Poor ticket notes | Investigation delays |
| Ignoring low-confidence alerts | Missed APT activity |
| Over-reliance on signatures | Missed behavioral attacks |
| Closing alerts without context | False negative risk |

---

# 18. Related Documents

| Document | Path |
|---|---|
| L1 Daily Shift Checklist | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Daily-Shift-Checklist.md` |
| L1 Escalation Criteria | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Escalation-Criteria.md` |
| L1 Ticket Creation SOP | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Ticket-Creation-SOP.md` |
| L1 SIEM Alert Response | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-SIEM-Alert-Response.md` |
| L1 EDR Alert Response | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-EDR-Alert-Response.md` |
| False Positive Handling | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-False-Positive-Handling.md` |

---

## 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / L1 Operations Lead | Initial version |

---

## 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**