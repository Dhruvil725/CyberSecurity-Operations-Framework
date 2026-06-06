# SOP: L1 Daily Shift Checklist

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | SOP – L1 Daily Shift Checklist                               |
| Document ID    | SOC-L1-SOP-001                                               |
| Version        | 1.0                                                          |
| Effective Date | 22-May-2026                                                  |
| Owner          | SOC Manager / L1 Team Lead                                   |
| Approved By    | SOC Lead                                                     |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly                                                    |

---

## 2. Purpose

This Standard Operating Procedure (SOP) defines the mandatory daily operational checklist for Level 1 (L1) SOC analysts.

The objective of this checklist is to ensure:

- Consistent shift readiness
- Proper monitoring coverage
- Timely alert handling
- Accurate ticket management
- Effective communication and escalation
- Operational continuity between shifts
- Compliance with SOC SLAs and procedures

The L1 analyst is the first line of defense within the SOC. Failure to follow daily operational discipline can result in:

- Missed security alerts
- Delayed incident escalation
- Incomplete investigations
- SLA violations
- Monitoring gaps
- Operational risk during active incidents

This checklist must be completed at the beginning, during, and end of every shift.

---

## 3. Scope

Applies to:

- All L1 SOC analysts
- Internal SOC operations
- MSSP monitoring operations
- 24x7 monitoring shifts
- Remote and onsite SOC operations

Applicable environments:

- SIEM platforms
- EDR platforms
- Firewall monitoring
- Threat intelligence monitoring
- Ticketing systems
- Cloud security monitoring
- Email security monitoring

---

## 4. L1 Shift Responsibilities

During every shift, the L1 analyst is responsible for:

- Monitoring alert queues continuously
- Performing initial alert triage
- Creating and updating tickets
- Escalating incidents according to SOP
- Monitoring SIEM and EDR health
- Maintaining shift documentation
- Tracking SLA compliance
- Communicating major incidents immediately
- Performing proper shift handover

---

# 5. Pre-Shift Preparation Checklist

The following activities must be completed before actively handling alerts.

---

## 5.1 Workstation and Access Validation

| Task | Status |
|------|--------|
| SOC workstation operational | ☐ |
| VPN connected (if remote) | ☐ |
| MFA authentication completed | ☐ |
| Internet connectivity verified | ☐ |
| Secure communication tools available | ☐ |

---

## 5.2 Tool Access Verification

Verify access to all required operational platforms.

| Platform | Verification Required | Status |
|----------|----------------------|--------|
| SIEM | Login successful | ☐ |
| EDR Console | Login successful | ☐ |
| Ticketing Platform | Operational | ☐ |
| Threat Intelligence Portal | Accessible | ☐ |
| Email Security Console | Accessible | ☐ |
| Firewall Monitoring Console | Accessible | ☐ |
| Cloud Security Platform | Accessible | ☐ |

Any access issue must be escalated immediately to SOC Lead or platform owner.

---

## 5.3 Monitoring Health Verification

Before beginning shift duties:

- Confirm SIEM ingestion active
- Confirm EDR telemetry active
- Confirm ticketing synchronization working
- Check for delayed log ingestion
- Review monitoring dashboard for outages
- Review health alerts from previous shift

---

## 5.4 Review Previous Shift Handover (IMPORTANT)

The incoming analyst must carefully review the previous shift handover notes.

Mandatory review items:

| Review Item | Status |
|-------------|--------|
| Open P1/P2 incidents reviewed | ☐ |
| Escalated tickets reviewed | ☐ |
| Pending investigations reviewed | ☐ |
| Monitoring gaps identified | ☐ |
| Client-specific issues reviewed | ☐ |
| Tool outages reviewed | ☐ |

Failure to review handover information may lead to duplicate work, missed escalation, or delayed response.

Reference:
`03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Shift-Handover-Template.md`

---

# 6. Start-of-Shift Activities

These activities must be completed within the first 15–30 minutes of the shift.

---

## 6.1 Alert Queue Review

Review:

- New alerts generated since previous shift
- Unassigned alerts
- Alerts nearing SLA breach
- Correlated alerts related to active incidents
- Reopened incidents

---

## 6.2 Priority Incident Review

Special attention required for:

| Incident Type | Priority |
|---------------|----------|
| P1 incidents | Critical |
| Active ransomware alerts | Critical |
| Data breach indicators | Critical |
| Cloud admin compromise | Critical |
| Network intrusion alerts | High |
| VPN compromise | High |

Immediately notify SOC Lead if any active P1 incident lacks analyst ownership.

---

## 6.3 SLA Validation

Review all active tickets for SLA status.

| Check | Status |
|------|--------|
| No SLA breach pending | ☐ |
| Escalations completed on time | ☐ |
| Aging tickets reviewed | ☐ |
| High-priority incidents acknowledged | ☐ |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

# 7. Continuous Monitoring Activities

These activities are continuous throughout the shift.

---

## 7.1 SIEM Monitoring

Monitor:

- High-severity alerts
- Correlation rule triggers
- Authentication anomalies
- Malware detections
- Network intrusion alerts
- Cloud anomaly alerts
- Data exfiltration indicators

---

## 7.2 EDR Monitoring

Review:

- Malware detections
- Memory injection alerts
- Suspicious process trees
- Credential dumping alerts
- Privilege escalation attempts
- Suspicious outbound connections

Reference:
`03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-EDR-Alert-Response.md`

---

## 7.3 Threat Intelligence Monitoring

Check:

- New IoC feed updates
- High-confidence IoCs
- Active threat advisories
- Sector-specific alerts
- Zero-day notifications

---

## 7.4 Ticket Queue Management

Ensure:

- All alerts tracked with ticket
- Tickets updated regularly
- Escalations documented
- Duplicate tickets merged
- Ticket severity validated

---

# 8. Incident Escalation Validation

L1 analysts must validate escalation requirements continuously.

---

## 8.1 Escalate Immediately If:

| Condition | Escalation Target |
|-----------|------------------|
| Confirmed malware outbreak | L2 / SOC Lead |
| Active ransomware indicators | IR Team |
| Data exfiltration suspected | L2 / IR |
| Domain admin compromise | IR Team |
| Cloud root/admin compromise | IR Team |
| Multiple systems affected | L2 |
| SIEM outage | SOC Lead |

Reference:
`03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Escalation-Criteria.md`

---

# 9. Communication Responsibilities

Throughout the shift:

- Respond promptly to SOC Lead requests
- Participate in bridge calls if assigned
- Document all critical communications
- Notify management for SLA risk if directed
- Coordinate with L2 during escalation

---

## 9.1 Communication Rules

Do not:

- Share incident details outside authorized channels
- Communicate directly with clients unless authorized
- Make assumptions in incident notes
- Use informal or ambiguous language in tickets

All communication must remain:

- Professional
- Accurate
- Timestamped
- Action-oriented

---

# 10. Mid-Shift Operational Checks

At least once every 4 hours:

| Check | Status |
|------|--------|
| SIEM ingestion verified | ☐ |
| EDR telemetry active | ☐ |
| No monitoring backlog | ☐ |
| Ticket queue healthy | ☐ |
| SLA compliance maintained | ☐ |

---

# 11. End-of-Shift Activities (IMPORTANT)

Proper shift closure is critical for 24x7 SOC operations.

---

## 11.1 Open Incident Review

Before handover:

- Review all active incidents
- Update all tickets
- Document pending actions
- Confirm escalation status
- Identify SLA risks

---

## 11.2 Shift Handover Preparation

The outgoing analyst must prepare a complete handover summary.

Mandatory handover items:

| Item | Status |
|------|--------|
| Open incidents documented | ☐ |
| P1/P2 status updated | ☐ |
| Pending investigations noted | ☐ |
| Tool issues documented | ☐ |
| Escalations documented | ☐ |
| Monitoring gaps identified | ☐ |

Reference:
`03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Shift-Handover-Template.md`

---

## 11.3 Final Operational Validation

Before logging out:

- Confirm no unassigned alerts remain
- Confirm critical alerts escalated
- Save investigation notes
- Securely log out of all platforms
- Lock workstation if onsite

---

# 12. MSSP-Specific Operational Requirements

For MSSP-managed SOC operations:

- Validate client segregation
- Follow client-specific SLA requirements
- Maintain separate client ticketing
- Ensure client notifications handled per escalation matrix
- Escalate cross-client incidents immediately

Reference:
`09_MSSP-SPECIFIC/`

---

# 13. Performance and Compliance Expectations

L1 analysts are expected to:

- Meet alert response SLA
- Maintain documentation quality
- Follow escalation procedures
- Avoid unauthorized actions
- Maintain operational discipline
- Participate in continuous improvement

Failure to follow SOP may result in:

- SLA violations
- Audit findings
- Incident response delays
- Operational risk

---

# 14. Common L1 Shift Mistakes

| Mistake | Risk |
|---------|------|
| Not reviewing handover | Missed incidents |
| Delayed ticket updates | SLA breaches |
| Ignoring low-confidence alerts | Missed early compromise |
| Failing to escalate quickly | Expanded incident scope |
| Poor documentation | Investigation gaps |
| Leaving alerts unassigned | Monitoring failure |

---

## 15. Related Documents

| Document | Path |
|----------|------|
| L1 Alert Handling SOP | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md` |
| L1 Escalation Criteria | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Escalation-Criteria.md` |
| L1 SIEM Alert Response | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-SIEM-Alert-Response.md` |
| L1 EDR Alert Response | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-EDR-Alert-Response.md` |
| L1 Ticket Creation SOP | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Ticket-Creation-SOP.md` |
| Shift Handover Template | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Shift-Handover-Template.md` |

---

## 16. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 22-May-2026 | SOC Manager / L1 Team Lead | Initial version |

---

## 17. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**