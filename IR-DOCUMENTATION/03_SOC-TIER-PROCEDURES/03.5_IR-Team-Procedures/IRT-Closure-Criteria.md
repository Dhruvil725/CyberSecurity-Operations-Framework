# SOP: IRT Closure Criteria and Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – IRT Closure Criteria and Procedures |
| Document ID | SOC-IRT-SOP-007 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | IR Team Lead / SOC Manager |
| Approved By | CISO |
| Classification | Internal – Restricted Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the criteria, validation standards, workflows, communication requirements, and governance procedures for formal Incident Response Team (IRT) incident closure.

Incident closure is a critical milestone in the incident response lifecycle because:

- Premature closure may leave threats active
- Incomplete closure may miss residual compromise
- Poor closure documentation creates audit gaps
- Weak closure validation creates reinfection risk
- Improper closure communication creates regulatory exposure
- Missing lessons learned reduces future resilience

IRT incident closure ensures:

- Comprehensive threat eradication
- Validated containment effectiveness
- Evidence preservation completeness
- Regulatory and legal compliance
- Stakeholder notification
- Post-incident activity initiation
- Audit-ready closure documentation
- Continuous improvement tracking

The objectives of this SOP are to:

- Define clear closure criteria
- Establish closure validation standards
- Standardize closure communication procedures
- Ensure lessons learned are captured
- Support regulatory compliance
- Maintain audit-ready closure records

This SOP ensures:

- Structured incident closure
- Validated threat eradication
- Complete evidence handling
- Appropriate stakeholder communication
- Post-incident activity coordination
- Audit-ready closure documentation

---

# 3. Scope

This SOP applies to IRT closure activities involving:

| Incident Type | Example |
|---|---|
| Ransomware incidents | Active encryption |
| Data breach incidents | Exfiltration events |
| APT investigations | Long-term compromise |
| Insider threat incidents | Unauthorized access |
| Cloud security incidents | IAM abuse |
| Malware outbreaks | Endpoint infections |
| Network intrusions | Lateral movement |
| Supply chain incidents | Trusted software abuse |
| Zero-day exploitation | Unpatched vulnerability |
| MSSP client incidents | Multi-tenant events |

---

## 3.1 Closure Stakeholders

| Stakeholder | Role |
|---|---|
| IRT Lead | Closure authorization |
| SOC Manager | Operational validation |
| CISO | Executive sign-off |
| Legal/Compliance | Regulatory confirmation |
| IT Operations | Remediation validation |
| MSSP Clients | Customer closure notification |
| Executive Management | Leadership awareness |

---

# 4. Closure Philosophy (IMPORTANT)

Incident closure is not simply closing a ticket.

Closure represents formal confirmation that:

- The threat has been eradicated
- The environment has been secured
- Evidence has been properly preserved
- Stakeholders have been informed
- Regulatory obligations have been met
- Post-incident activities have been initiated

IRT personnel must understand:

"An incident is not closed until every closure criterion is validated and documented."

Closure decisions must be:

- Evidence-based
- Validated technically
- Approved by appropriate authority
- Communicated to all stakeholders
- Documented for audit readiness

---

## 4.1 Common Closure Failures

| Poor Practice | Operational Risk |
|---|---|
| Premature closure | Residual threat activity |
| Weak validation | Missed persistence |
| Incomplete evidence handling | Legal exposure |
| Missing stakeholder notification | Communication gaps |
| No post-incident activities | Repeat incidents |
| Weak documentation | Audit failures |

---

# 5. IRT Closure Responsibilities

| Responsibility | Description |
|---|---|
| Closure criteria validation | Technical confirmation |
| Eradication validation | Threat removal confirmation |
| Evidence preservation review | Completeness check |
| Regulatory compliance review | Legal confirmation |
| Stakeholder communication | Closure notification |
| Post-incident initiation | Improvement activities |
| Closure documentation | Audit readiness |

---

# 6. Incident Closure Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Closure Readiness Assessment | Validation scope |
| Phase 2 | Technical Validation | Threat eradication confirmation |
| Phase 3 | Evidence Review | Completeness validation |
| Phase 4 | Regulatory and Legal Review | Compliance confirmation |
| Phase 5 | Stakeholder Communication | Closure notifications |
| Phase 6 | Post-Incident Initiation | Improvement activities |
| Phase 7 | Formal Closure Documentation | Audit records |

---

# 7. Phase 1 – Closure Readiness Assessment

The IRT Lead conducts a formal closure readiness review.

---

## 7.1 Assessment Objectives

| Objective | Purpose |
|---|---|
| Validate threat eradication | Security confirmation |
| Review investigation completeness | Scope validation |
| Assess regulatory obligations | Compliance |
| Review evidence preservation | Legal readiness |
| Assess business recovery | Operational confirmation |

---

## 7.2 Closure Readiness Checklist

| Validation Item | Completed |
|---|---|
| Threat eradicated | ☐ |
| Containment validated | ☐ |
| Investigation complete | ☐ |
| Evidence preserved | ☐ |
| Regulatory obligations reviewed | ☐ |

---

## 7.3 Premature Closure Risk Indicators

Do not close if:

| Condition | Risk |
|---|---|
| Attacker activity suspected | Ongoing threat |
| Persistence not fully validated | Reinfection risk |
| Data exposure unconfirmed | Regulatory risk |
| Regulatory reporting pending | Compliance exposure |
| Evidence incomplete | Legal risk |

---

# 8. Phase 2 – Technical Validation (CRITICAL)

All technical conditions must be validated before closure.

---

## 8.1 Eradication Validation Areas

| Area | Validation Requirement |
|---|---|
| Malware removal | All endpoints verified clean |
| Persistence removal | All persistence mechanisms removed |
| Credential rotation | All compromised credentials reset |
| Vulnerability patching | Exploitation vector patched |
| Backdoor removal | All backdoors removed |
| Monitoring restoration | Full visibility confirmed |

---

## 8.2 Technical Validation Checklist

| Validation Item | Completed |
|---|---|
| Malware removed | ☐ |
| Persistence removed | ☐ |
| Compromised credentials reset | ☐ |
| Vulnerability patched | ☐ |
| EDR coverage restored | ☐ |
| SIEM coverage restored | ☐ |
| Backdoors removed | ☐ |

---

## 8.3 Affected Systems Validation Table

| System | Threat Removed | Persistence Removed | Credential Reset | Status |
|---|---|---|---|---|
| | | | | |

---

## 8.4 Critical Technical Conditions

Closure must be blocked if:

| Condition | Risk |
|---|---|
| Malware still active | Ongoing compromise |
| Persistence still present | Reinfection risk |
| C2 communication ongoing | Active attacker |
| Elevated account still active | Privilege abuse |
| EDR/SIEM coverage degraded | Visibility loss |

---

# 9. Phase 3 – Evidence Review

All evidence must be reviewed and preserved before closure.

---

## 9.1 Evidence Review Areas

| Area | Requirement |
|---|---|
| Evidence inventory | Completeness |
| Hash verification | Integrity |
| Chain-of-custody | Legal compliance |
| Storage confirmation | Retention compliance |
| Legal hold review | Legal confirmation |

---

## 9.2 Evidence Review Checklist

| Validation Item | Completed |
|---|---|
| Evidence inventory completed | ☐ |
| All hashes verified | ☐ |
| Chain-of-custody confirmed | ☐ |
| Storage location confirmed | ☐ |
| Legal hold reviewed | ☐ |
| Retention schedule confirmed | ☐ |

---

## 9.3 Evidence Status Table

| Evidence ID | Type | Hash Verified | Storage Confirmed | Legal Hold |
|---|---|---|---|---|
| | | | | |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`

---

# 10. Phase 4 – Regulatory and Legal Review

Regulatory obligations must be confirmed before closure.

---

## 10.1 Regulatory Review Areas

| Area | Requirement |
|---|---|
| RBI reporting | Filed if required |
| CERT-In reporting | Filed if required |
| Data breach notification | Completed if required |
| Client notification | Completed per SLA |
| Legal hold status | Confirmed |

---

## 10.2 Regulatory Compliance Checklist

| Validation Item | Completed |
|---|---|
| Reporting obligations reviewed | ☐ |
| Required reports filed | ☐ |
| Legal hold status confirmed | ☐ |
| Client notifications sent | ☐ |
| Legal counsel confirmed | ☐ |

---

## 10.3 Regulatory Escalation Conditions

Closure must be delayed if:

| Condition | Risk |
|---|---|
| Regulatory report pending | Compliance exposure |
| Data breach notification pending | Legal obligation |
| Legal proceedings active | Evidence preservation |
| Law enforcement engaged | Legal coordination |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

# 11. Phase 5 – Stakeholder Communication

Closure requires formal stakeholder notification.

---

## 11.1 Mandatory Closure Notifications

| Stakeholder | Notification Requirement |
|---|---|
| CISO | All P1/P2 closures |
| Executive Management | Business-impacting incidents |
| Legal/Compliance | Regulatory-impacting incidents |
| IT Operations | Remediation confirmation |
| MSSP Clients | Client-impacting incidents |
| SOC Team | Operational awareness |

---

## 11.2 Closure Communication Requirements

| Requirement | Mandatory |
|---|---|
| Incident summary | Yes |
| Root cause summary | Yes |
| Remediation actions | Yes |
| Current operational status | Yes |
| Follow-up actions | Yes |
| Lessons learned summary | Yes |

---

## 11.3 Communication Documentation Table

| Stakeholder | Notification Time UTC | Communication Method | Acknowledged |
|---|---|---|---|
| | | | |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Incident-Closure-Notification.md`

---

# 12. Phase 6 – Post-Incident Initiation

Closure triggers post-incident improvement activities.

---

## 12.1 Post-Incident Activities

| Activity | Purpose |
|---|---|
| Lessons learned review | Process improvement |
| Root cause analysis | Control gap identification |
| Detection tuning | Monitoring enhancement |
| Security control improvements | Risk reduction |
| Playbook updates | Documentation improvement |

---

## 12.2 Post-Incident Scheduling

| Activity | Timing |
|---|---|
| PIR meeting | Within 5 business days |
| RCA completion | Within 10 business days |
| Lessons learned report | Within 15 business days |
| Improvement tracking | Ongoing |

---

## 12.3 Post-Incident Tracking Table

| Activity | Owner | Due Date | Status |
|---|---|---|---|
| | | | |

Reference:
`08_POST-INCIDENT/08.1_Lessons-Learned/`

---

# 13. Phase 7 – Formal Closure Documentation

Incident closure must be formally documented.

---

## 13.1 Closure Documentation Requirements

| Requirement | Mandatory |
|---|---|
| Closure timestamp UTC | Yes |
| IRT Lead sign-off | Yes |
| Technical validation | Yes |
| Evidence review | Yes |
| Regulatory confirmation | Yes |
| Stakeholder notifications | Yes |
| Post-incident initiation | Yes |

---

## 13.2 Formal Closure Record Table

| Field | Information |
|---|---|
| Incident ID | |
| Closure Timestamp UTC | |
| IRT Lead | |
| CISO Approval | |
| Regulatory Status | |
| Evidence Status | |
| Post-Incident Status | |

---

## 13.3 Closure Approval Authority

| Incident Severity | Closure Authority |
|---|---|
| P1 | CISO + IRT Lead |
| P2 | IRT Lead + SOC Manager |
| P3 | SOC Manager |
| P4 | SOC Lead |

---

# 14. Post-Closure Monitoring

After formal closure, enhanced monitoring is recommended.

---

## 14.1 Post-Closure Monitoring Areas

| Area | Duration |
|---|---|
| Affected endpoints | 30 days |
| Compromised accounts | 30 days |
| Network communication | 30 days |
| Cloud environment | 30 days |
| Authentication activity | 30 days |

---

## 14.2 Reactivation Triggers

IRT must be reactivated if:

| Condition | Risk |
|---|---|
| Similar IOCs detected | Persistent threat |
| Attacker activity resumed | Failed eradication |
| New persistence found | Missed artifact |
| New compromise detected | Lateral spread |

---

# 15. MSSP-Specific Closure Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain client segregation | Compliance |
| Follow client SLA for closure notification | Contract compliance |
| Provide client-specific closure report | Service transparency |
| Coordinate client regulatory reporting | Legal alignment |
| Archive client evidence separately | Audit readiness |

---

# 16. Common Closure Mistakes

| Mistake | Operational Risk |
|---|---|
| Premature closure | Residual threat |
| Weak technical validation | Reinfection |
| Missing evidence review | Legal exposure |
| Incomplete stakeholder notification | Communication gaps |
| No post-incident initiation | Repeat incidents |
| Weak documentation | Audit failures |

---

# 17. Related Documents

| Document | Path |
|---|---|
| IRT Activation Criteria | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md` |
| IRT Onsite Response SOP | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Onsite-Response-SOP.md` |
| IRT Remote Response SOP | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Remote-Response-SOP.md` |
| IRT Evidence Chain-of-Custody | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Evidence-Chain-of-Custody.md` |
| Lessons Learned Template | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md` |
| Incident Closure Notification | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Incident-Closure-Notification.md` |

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