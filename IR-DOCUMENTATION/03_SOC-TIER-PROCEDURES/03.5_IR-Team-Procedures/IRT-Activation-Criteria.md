# SOP: IRT Activation Criteria and Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – IRT Activation Criteria and Procedures |
| Document ID | SOC-IRT-SOP-001 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | IR Team Lead / SOC Manager |
| Approved By | CISO |
| Classification | Internal – Restricted Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the activation criteria, decision-making standards, operational workflows, communication requirements, and governance procedures for Incident Response Team (IRT) activation.

The Incident Response Team (IRT) is a specialized response capability activated when cybersecurity incidents exceed standard SOC investigative and containment capability.

IRT activation ensures:

- Appropriate response expertise is engaged rapidly
- Major incidents receive maximum investigative capability
- Business disruption is minimized
- Regulatory obligations are met
- Legal considerations are properly managed
- Executive awareness is established
- Containment and eradication are executed effectively

Delayed or improper IRT activation may result in:

- Increased attacker dwell time
- Widespread compromise
- Data exfiltration
- Regulatory reporting failures
- Business continuity failures
- Evidence loss
- Reputational damage
- Legal exposure

The purpose of this SOP is to ensure:

- Clear and objective activation criteria
- Timely IRT engagement
- Structured activation workflows
- Proper stakeholder coordination
- Audit-ready activation records
- Consistent governance standards

---

# 3. Scope

This SOP applies to IRT activation scenarios involving:

| Incident Type | Example |
|---|---|
| Ransomware | Active encryption |
| Data breach | Sensitive data exfiltration |
| Nation-state/APT activity | Long-term persistence |
| Domain compromise | Privileged account abuse |
| Cloud infrastructure compromise | Admin account takeover |
| Insider threat | Authorized user abuse |
| Supply chain compromise | Trusted software attack |
| Zero-day exploitation | Unpatched vulnerability |
| Critical infrastructure attack | Business-critical systems |
| MSSP multi-client compromise | Cross-tenant exposure |

---

## 3.1 IRT Structure

| Role | Responsibility |
|---|---|
| IRT Lead | Overall response coordination |
| Forensic Analyst | Evidence collection |
| Malware Analyst | Malware reverse engineering |
| Network Analyst | Traffic investigation |
| Cloud Analyst | Cloud forensics |
| Threat Intel Analyst | Intelligence integration |
| Legal Liaison | Legal coordination |
| Executive Liaison | Leadership communication |

---

# 4. IRT Activation Philosophy (IMPORTANT)

IRT activation is a critical decision that must be made objectively and rapidly.

The IRT is not activated for every incident.

Activation is required when incidents:

- Exceed standard SOC response capability
- Involve confirmed or suspected major compromise
- Require specialized forensic capability
- Have significant business impact potential
- May have regulatory reporting obligations
- Involve senior stakeholder notification requirements

SOC Leads and L3 analysts must understand:

"Delaying IRT activation while attempting to investigate a major incident independently increases attacker dwell time and business risk."

The correct principle is:

"Activate IRT early and adjust scope as investigation progresses."

---

## 4.1 Common IRT Activation Failures

| Poor Practice | Operational Risk |
|---|---|
| Delayed activation | Increased attacker persistence |
| Insufficient evidence review | Incorrect activation decision |
| Poor stakeholder notification | Governance failure |
| Weak activation documentation | Audit gaps |
| Scope underestimation | Inadequate response |

---

# 5. IRT Activation Authority

| Role | Activation Authority |
|---|---|
| L3 Analyst | Recommend activation |
| SOC Lead | Authorize activation |
| SOC Manager | Authorize activation |
| CISO | Mandatory notification |
| IR Team Lead | Accept and initiate response |

---

# 6. IRT Activation Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Incident Review and Assessment | Activation justification |
| Phase 2 | Activation Decision | Formal activation |
| Phase 3 | IRT Notification | Team engagement |
| Phase 4 | Stakeholder Communication | Operational awareness |
| Phase 5 | Initial Briefing | IRT coordination |
| Phase 6 | Transition to Active Response | Operational handoff |
| Phase 7 | Activation Documentation | Audit records |

---

# 7. Phase 1 – Incident Review and Assessment

The activation decision begins with incident assessment.

---

## 7.1 Assessment Objectives

| Objective | Purpose |
|---|---|
| Validate incident severity | Priority confirmation |
| Review investigation findings | Evidence assessment |
| Determine scope | Blast radius analysis |
| Assess business impact | Operational risk |
| Evaluate regulatory exposure | Compliance assessment |

---

## 7.2 Pre-Activation Assessment Checklist

| Validation Item | Completed |
|---|---|
| Incident severity validated | ☐ |
| Scope reviewed | ☐ |
| Evidence reviewed | ☐ |
| Business impact assessed | ☐ |
| Regulatory exposure reviewed | ☐ |

---

## 7.3 Critical Assessment Questions

| Question | Purpose |
|---|---|
| Is the attacker active? | Urgency validation |
| Is the scope enterprise-wide? | Scale assessment |
| Is data exposure confirmed? | Regulatory assessment |
| Does investigation exceed SOC capability? | Activation necessity |
| Is legal involvement required? | Compliance planning |

---

# 8. Phase 2 – Activation Decision (CRITICAL)

The activation decision must be made rapidly and objectively.

---

## 8.1 Mandatory IRT Activation Criteria

IRT must be activated immediately if any of the following are confirmed:

| Activation Trigger | Risk Level |
|---|---|
| Active ransomware encryption | Critical |
| Confirmed domain admin compromise | Critical |
| Active data exfiltration | Critical |
| Cloud admin account compromise | Critical |
| Confirmed APT/nation-state activity | Critical |
| Active insider threat with data access | Critical |
| Zero-day exploitation confirmed | Critical |
| Supply chain compromise identified | Critical |
| Multi-host ransomware propagation | Critical |
| Backup system compromise | Critical |

---

## 8.2 Recommended IRT Activation Criteria

IRT should be activated if any of the following are present:

| Activation Trigger | Risk Level |
|---|---|
| Widespread malware infection | High |
| Suspected major data breach | High |
| Advanced persistent threat indicators | High |
| Critical business systems compromised | High |
| Multiple privileged accounts compromised | High |
| Regulatory reporting likely | High |
| Evidence suggests attacker persistence | High |

---

## 8.3 IRT Activation Decision Table

| Condition | Activation Decision |
|---|---|
| Critical trigger confirmed | Immediate activation |
| High risk trigger confirmed | SOC Lead authorization required |
| Investigation scope exceeds SOC capability | Activation recommended |
| Executive notification required | Activation mandatory |

---

# 9. Phase 3 – IRT Notification

After activation decision, IRT must be notified immediately.

---

## 9.1 Notification Requirements

| Requirement | Mandatory |
|---|---|
| IRT Lead notified | Yes |
| Incident summary provided | Yes |
| Evidence package shared | Yes |
| Severity classification confirmed | Yes |
| Initial scope communicated | Yes |

---

## 9.2 IRT Notification Channels

| Channel | Usage |
|---|---|
| Direct phone call | Immediate notification |
| Secure messaging | Operational coordination |
| Bridge call | Team coordination |
| Ticketing system | Documentation |

---

## 9.3 IRT Notification Package Requirements

Every activation notification must include:

| Required Item | Purpose |
|---|---|
| Incident summary | Context |
| Severity classification | Prioritization |
| Affected systems list | Scope |
| Evidence references | Investigation support |
| Timeline | Chronology |
| Actions taken | Prior response |
| Recommended next steps | IRT direction |

---

# 10. Phase 4 – Stakeholder Communication

IRT activation requires immediate stakeholder notification.

---

## 10.1 Mandatory Stakeholder Notifications

| Stakeholder | Notification Trigger |
|---|---|
| CISO | All P1 activations |
| Executive Leadership | Business-impacting incidents |
| Legal/Compliance | Data exposure incidents |
| IT Operations | Containment coordination |
| MSSP Clients | Client-impacting incidents |

---

## 10.2 Notification Timing Standards

| Stakeholder | Notification Timing |
|---|---|
| IRT Lead | Immediate |
| CISO | Within 15 minutes of activation |
| Executive Management | Within 30 minutes of activation |
| Legal/Compliance | Within 30 minutes if required |
| MSSP Clients | Per SLA |

---

## 10.3 Communication Checklist

| Validation Item | Completed |
|---|---|
| IRT Lead notified | ☐ |
| CISO notified | ☐ |
| Executive notified | ☐ |
| Legal engaged if needed | ☐ |
| Client notified if needed | ☐ |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md`

---

# 11. Phase 5 – Initial IRT Briefing

IRT Lead conducts initial operational briefing.

---

## 11.1 Initial Briefing Requirements

| Requirement | Mandatory |
|---|---|
| Incident summary | Yes |
| Timeline | Yes |
| Scope | Yes |
| Evidence status | Yes |
| Containment status | Yes |
| Attacker activity status | Yes |
| Immediate priorities | Yes |

---

## 11.2 Initial Briefing Agenda

| Area | Content |
|---|---|
| Incident overview | What happened |
| Current scope | Affected systems |
| Attacker activity | Active or inactive |
| Evidence available | What is collected |
| Containment status | Actions taken |
| Immediate actions | Priorities |

---

# 12. Phase 6 – Transition to Active Response

SOC transitions operational control to IRT.

---

## 12.1 Transition Requirements

| Requirement | Mandatory |
|---|---|
| Evidence package transferred | Yes |
| Investigation ownership transferred | Yes |
| Ticketing ownership updated | Yes |
| SOC support role defined | Yes |
| Communication cadence established | Yes |

---

## 12.2 Transition Checklist

| Validation Item | Completed |
|---|---|
| IRT Lead accepted ownership | ☐ |
| Evidence package transferred | ☐ |
| Ticket ownership updated | ☐ |
| SOC support role confirmed | ☐ |
| Communication cadence set | ☐ |

---

# 13. Phase 7 – Activation Documentation

All activation activities must be documented.

---

## 13.1 Documentation Requirements

| Requirement | Mandatory |
|---|---|
| Activation timestamp | Yes |
| Activation trigger | Yes |
| Activation authority | Yes |
| IRT notification timestamp | Yes |
| Stakeholder notifications | Yes |
| Evidence transferred | Yes |

---

## 13.2 Activation Record Table

| Field | Information |
|---|---|
| Incident ID | |
| Activation Timestamp UTC | |
| Activation Trigger | |
| Authorized By | |
| IRT Lead Notified | |
| CISO Notified | |
| Evidence Package Transferred | |

---

# 14. IRT Activation Escalation Matrix

| Activation Type | Escalation Target |
|---|---|
| Active ransomware | CISO + Executive |
| Data breach | Legal + Compliance |
| Cloud compromise | Cloud Operations |
| APT activity | CISO + Threat Intel |
| Multi-client MSSP | MSSP Director |

---

# 15. MSSP-Specific Activation Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain tenant segregation | Prevent data leakage |
| Follow client activation SLA | Contract compliance |
| Notify client per contractual obligations | Client transparency |
| Preserve client evidence separately | Compliance |
| Coordinate client executive communication | Service management |

---

# 16. Common IRT Activation Mistakes

| Mistake | Operational Risk |
|---|---|
| Delayed activation | Increased attacker persistence |
| Incomplete notification | Stakeholder gaps |
| Poor evidence transfer | Investigation continuity |
| Weak documentation | Audit failures |
| Incorrect severity assessment | Misaligned response |
| No scope definition | Investigative confusion |

---

# 17. Related Documents

| Document | Path |
|---|---|
| IRT Onsite Response SOP | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Onsite-Response-SOP.md` |
| IRT Remote Response SOP | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Remote-Response-SOP.md` |
| IRT Closure Criteria | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Closure-Criteria.md` |
| Emergency P1 Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md` |
| Escalation Matrix Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| Management Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md` |

---

# 18. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | IR Team Lead / SOC Manager | Initial version |

---

# 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**