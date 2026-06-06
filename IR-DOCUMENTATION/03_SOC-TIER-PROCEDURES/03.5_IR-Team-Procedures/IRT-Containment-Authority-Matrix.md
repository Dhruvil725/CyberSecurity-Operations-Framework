# SOP: IRT Containment Authority Matrix

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – IRT Containment Authority Matrix |
| Document ID | SOC-IRT-SOP-006 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | IR Team Lead / SOC Manager |
| Approved By | CISO |
| Classification | Internal – Restricted Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the operational authority, approval requirements, decision-making standards, and governance procedures for containment actions executed during cybersecurity incident response.

Containment is a critical phase of incident response because it directly impacts:

- Attacker dwell time
- Business operations
- Data exposure risk
- Regulatory obligations
- Recovery timeline
- Evidence integrity
- System availability
- MSSP service continuity

Containment actions must be:

- Authorized by appropriate personnel
- Executed by qualified teams
- Documented before and after execution
- Validated for effectiveness
- Communicated to stakeholders

Improper containment authority management may result in:

- Unauthorized system shutdowns
- Business disruption without approval
- Evidence destruction
- Incomplete containment
- Regulatory exposure
- Legal liability
- Conflicting response actions
- Operational confusion

The objectives of this SOP are to:

- Define clear containment authority levels
- Establish containment approval requirements
- Standardize containment execution procedures
- Ensure accountability for containment actions
- Support audit-ready containment documentation
- Align containment authority with incident severity

This SOP ensures:

- Structured containment governance
- Appropriate authority levels
- Documented decision-making
- Effective operational coordination
- Audit-ready containment records
- Business-aligned response actions

---

# 3. Scope

This SOP applies to containment authority management involving:

| Containment Area | Example |
|---|---|
| Endpoint isolation | Workstation quarantine |
| Server isolation | Critical server shutdown |
| Network segmentation | VLAN isolation |
| Account disablement | Privileged account suspension |
| Cloud key revocation | IAM token revocation |
| Firewall blocking | IP/domain blocking |
| Service shutdown | Application suspension |
| Data transfer blocking | Outbound restriction |
| DNS filtering | Domain blocking |
| Email quarantine | Suspicious email suspension |

---

## 3.1 Containment Stakeholders

| Stakeholder | Role |
|---|---|
| SOC Lead | Operational authority |
| SOC Manager | Management authority |
| IRT Lead | Incident response authority |
| CISO | Executive authority |
| IT Operations | Technical execution |
| Network Team | Network containment |
| Cloud Team | Cloud containment |
| Legal Counsel | Legal oversight |
| Executive Management | Business decision authority |

---

# 4. Containment Authority Philosophy (IMPORTANT)

Containment decisions must balance two critical operational requirements:

- Speed of response to minimize attacker impact
- Business impact awareness to prevent unnecessary disruption

The IRT must understand that:

- Aggressive containment may disrupt business operations
- Delayed containment increases attacker opportunity
- Incorrect containment may destroy evidence
- Proper containment protects both operations and investigation

Every containment action must consider:

1. Will this stop the attacker?
2. Will this disrupt business operations?
3. Will this destroy evidence?
4. Is this authorized by the appropriate level?
5. Is this reversible if required?

The guiding principle is:

"Contain with appropriate authority, execute with precision, document with discipline."

---

## 4.1 Common Containment Authority Failures

| Poor Practice | Operational Risk |
|---|---|
| Unauthorized containment | Business disruption |
| Delayed containment approval | Increased attacker access |
| Incomplete containment | Ongoing compromise |
| Evidence-destroying containment | Forensic failure |
| No documentation | Audit failure |

---

# 5. Containment Authority Levels

Containment authority is defined by action severity and business impact.

---

## 5.1 Authority Level Definitions

| Authority Level | Definition |
|---|---|
| Level 1 – Analyst | Low-risk actions with minimal business impact |
| Level 2 – SOC Lead | Moderate-risk actions with operational impact |
| Level 3 – IRT Lead | High-risk actions with significant impact |
| Level 4 – CISO/Executive | Critical actions with major business impact |

---

## 5.2 Authority Level Matrix

| Authority Level | Examples |
|---|---|
| Level 1 | Block single IP, quarantine email |
| Level 2 | Isolate endpoint, disable user account |
| Level 3 | Server isolation, network segmentation |
| Level 4 | Critical system shutdown, public service suspension |

---

# 6. Containment Action Authority Matrix

---

## 6.1 Endpoint Containment Actions

| Containment Action | Authority Level | Approver |
|---|---|---|
| Workstation isolation | Level 2 | SOC Lead |
| Server isolation | Level 3 | IRT Lead |
| Critical server isolation | Level 4 | CISO |
| Domain controller isolation | Level 4 | CISO + Executive |
| OT/ICS endpoint isolation | Level 4 | CISO + OT Lead |

---

## 6.2 Account and Identity Containment

| Containment Action | Authority Level | Approver |
|---|---|---|
| Standard user account disable | Level 2 | SOC Lead |
| Privileged account disable | Level 3 | IRT Lead |
| Domain admin disable | Level 4 | CISO |
| Service account disable | Level 3 | IRT Lead |
| Cloud IAM user disable | Level 3 | IRT Lead |
| Cloud admin key revocation | Level 4 | CISO + Cloud Owner |

---

## 6.3 Network Containment Actions

| Containment Action | Authority Level | Approver |
|---|---|---|
| Single IP block | Level 1 | Analyst |
| Domain block | Level 2 | SOC Lead |
| Outbound traffic restriction | Level 3 | IRT Lead |
| VLAN segmentation | Level 3 | IRT Lead + Network Team |
| Full network segment isolation | Level 4 | CISO |
| DMZ isolation | Level 4 | CISO + Network Lead |

---

## 6.4 Cloud Containment Actions

| Containment Action | Authority Level | Approver |
|---|---|---|
| Cloud VM isolation | Level 3 | IRT Lead |
| Cloud storage access restriction | Level 3 | IRT Lead |
| Cloud admin key revocation | Level 4 | CISO + Cloud Owner |
| Cloud account suspension | Level 4 | CISO |
| Cloud service shutdown | Level 4 | CISO + Executive |

---

## 6.5 Application and Service Containment

| Containment Action | Authority Level | Approver |
|---|---|---|
| Email quarantine | Level 2 | SOC Lead |
| Web application suspension | Level 3 | IRT Lead |
| Business application suspension | Level 4 | CISO + Executive |
| External-facing service shutdown | Level 4 | CISO + Executive |
| Payment service suspension | Level 4 | CISO + CFO |

---

## 6.6 Data Transfer Containment

| Containment Action | Authority Level | Approver |
|---|---|---|
| Block outbound to single IP | Level 2 | SOC Lead |
| Block outbound to domain | Level 2 | SOC Lead |
| Restrict all outbound traffic | Level 4 | CISO |
| Block cloud storage access | Level 3 | IRT Lead |
| Disable FTP/SFTP services | Level 3 | IRT Lead |

---

# 7. Emergency Containment Procedures

Certain critical conditions require emergency containment without standard approval delays.

---

## 7.1 Emergency Containment Authorization

| Emergency Condition | Authorized Action | Approver |
|---|---|---|
| Active ransomware encryption | Endpoint isolation | SOC Lead |
| Active data exfiltration | Outbound block | SOC Lead |
| Domain controller compromise | Emergency lockdown | IRT Lead |
| Cloud admin active abuse | Key revocation | IRT Lead |
| Widespread malware propagation | Network segmentation | IRT Lead |

---

## 7.2 Emergency Containment Rules

| Rule | Requirement |
|---|---|
| Emergency action justified | Documented |
| Retroactive approval required | Mandatory |
| Evidence impact assessed | Mandatory |
| Business impact documented | Mandatory |

---

## 7.3 Emergency Containment Checklist

| Validation Item | Completed |
|---|---|
| Emergency condition confirmed | ☐ |
| Action authorized | ☐ |
| Business impact assessed | ☐ |
| Evidence impact assessed | ☐ |
| Retroactive documentation completed | ☐ |

---

# 8. Containment Execution Standards

Containment execution must follow structured procedures.

---

## 8.1 Pre-Containment Requirements

| Requirement | Purpose |
|---|---|
| Evidence preserved | Forensic protection |
| Business impact assessed | Operational protection |
| Authority confirmed | Governance |
| Containment plan documented | Accountability |
| Reversibility assessed | Recovery planning |

---

## 8.2 Pre-Containment Checklist

| Validation Item | Completed |
|---|---|
| Evidence preserved | ☐ |
| Authority confirmed | ☐ |
| Business impact reviewed | ☐ |
| Stakeholders notified | ☐ |
| Containment plan documented | ☐ |

---

## 8.3 Containment Execution Table

| Action | System/User | Executed By | Time UTC | Authority | Status |
|---|---|---|---|---|---|
| | | | | | |

---

# 9. Containment Validation

After execution, containment must be validated.

---

## 9.1 Validation Objectives

| Objective | Purpose |
|---|---|
| Confirm threat neutralization | Operational assurance |
| Validate effectiveness | Risk reduction |
| Assess business impact | Operational review |
| Confirm monitoring visibility | Detection continuity |

---

## 9.2 Containment Validation Checklist

| Validation Item | Completed |
|---|---|
| Threat activity stopped | ☐ |
| Business impact documented | ☐ |
| Monitoring confirmed | ☐ |
| Stakeholders notified | ☐ |
| Documentation completed | ☐ |

---

# 10. Containment Communication

Containment actions must be communicated to stakeholders.

---

## 10.1 Communication Requirements

| Stakeholder | Communication Trigger |
|---|---|
| Executive Management | Level 4 actions |
| IT Operations | Level 3+ actions |
| Legal/Compliance | Regulatory-impacting actions |
| MSSP Clients | Client-impacting actions |
| Network Team | Network containment |

---

## 10.2 Communication Timing Standards

| Authority Level | Communication Timing |
|---|---|
| Level 4 | Before execution |
| Level 3 | During execution |
| Level 2 | After execution |
| Level 1 | Ticket documentation |

---

## 10.3 Communication Documentation Table

| Action | Notified Party | Time UTC | Communication Method |
|---|---|---|---|
| | | | |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

---

# 11. Containment Documentation Standards

All containment actions must be documented.

---

## 11.1 Documentation Requirements

| Requirement | Mandatory |
|---|---|
| Action description | Yes |
| System/user affected | Yes |
| Executing team | Yes |
| Approval authority | Yes |
| Execution timestamp UTC | Yes |
| Business impact | Yes |
| Validation status | Yes |

---

## 11.2 Containment Action Log Table

| Timestamp UTC | Action | Target | Executed By | Authority | Impact | Status |
|---|---|---|---|---|---|---|
| | | | | | | |

---

# 12. Containment Rollback Procedures

Some containment actions may need to be reversed.

---

## 12.1 Rollback Conditions

| Condition | Reason |
|---|---|
| False positive identified | Incorrect isolation |
| Business impact too severe | Operational necessity |
| Incorrect system targeted | Technical error |
| Executive override | Business decision |

---

## 12.2 Rollback Authority

| Action | Rollback Authority |
|---|---|
| Endpoint isolation | SOC Lead |
| Account disablement | IRT Lead |
| Network segmentation | CISO + Network Lead |
| Cloud suspension | CISO |

---

## 12.3 Rollback Documentation Requirements

| Requirement | Mandatory |
|---|---|
| Rollback justification | Yes |
| Approver documented | Yes |
| Rollback timestamp | Yes |
| Risk assessment | Yes |

---

# 13. SLA Impact of Containment Actions

Containment actions may impact SLA obligations.

---

## 13.1 SLA Awareness Requirements

| Area | Purpose |
|---|---|
| Service impact assessment | Business protection |
| Client SLA review | MSSP obligations |
| Regulatory timeline tracking | Compliance |
| Communication cadence | Stakeholder awareness |

---

## 13.2 SLA Impact Escalation Conditions

Immediate escalation required if:

| Condition | Escalation Target |
|---|---|
| Client service impacted | Service Delivery Manager |
| Regulatory timeline affected | Compliance Team |
| Business-critical service suspended | Executive Management |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLA-Breach-Escalation-Procedure.md`

---

# 14. MSSP-Specific Containment Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain tenant segregation | Compliance |
| Follow client-specific containment authority | Contract compliance |
| Notify clients before Level 3+ actions | SLA alignment |
| Document client impact separately | Audit readiness |
| Coordinate client executive communication | Service management |

---

# 15. Common Containment Authority Mistakes

| Mistake | Operational Risk |
|---|---|
| Unauthorized containment actions | Business disruption |
| Delayed approval process | Increased compromise |
| No rollback plan | Recovery failure |
| Missing documentation | Audit failure |
| Weak communication | Stakeholder confusion |
| No evidence impact assessment | Forensic failure |

---

# 16. Related Documents

| Document | Path |
|---|---|
| IRT Activation Criteria | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md` |
| IRT Onsite Response SOP | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Onsite-Response-SOP.md` |
| IRT Remote Response SOP | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Remote-Response-SOP.md` |
| IRT Closure Criteria | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Closure-Criteria.md` |
| Escalation Matrix Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| SLA Breach Escalation | `00_GOVERNANCE/00.4_SLA-and-SLO/SLA-Breach-Escalation-Procedure.md` |

---

# 17. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | IR Team Lead / SOC Manager | Initial version |

---

# 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**