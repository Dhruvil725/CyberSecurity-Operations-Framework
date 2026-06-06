# Ticket Priority Matrix

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Ticket Priority Matrix |
| Document ID | TOOL-TKT-002 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Manager / SOC Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This document defines the priority classification matrix for all security tickets within the SOC ticketing system.

Priority assignment is critical because:

- It determines SLA response timelines
- It drives escalation decisions
- It controls resource allocation
- It defines management notification thresholds
- It ensures audit-ready incident records
- It aligns with MSSP client contractual SLA obligations

This matrix ensures:

- Consistent priority assignment across all analysts
- Objective criteria-based classification
- Alignment with severity classification framework
- Reduction in misclassification errors
- SLA compliance across all incident types

---

# 3. Scope

This matrix applies to all ticket types:

| Ticket Type | Examples |
|---|---|
| Security alerts | SIEM/EDR triggered alerts |
| Confirmed incidents | Active malware, breach, ransomware |
| Change requests | Firewall block, network isolation |
| Service requests | Client notification, evidence handling |
| Operational tasks | Health checks, coverage gaps |
| MSSP client incidents | Client-specific security events |
| Post-incident actions | RCA, lessons learned tracking |

---

# 4. Priority Levels Overview

| Priority | Label | Description | Response Posture |
|---|---|---|---|
| P1 | Critical | Active compromise with immediate business impact | Emergency response |
| P2 | High | Likely compromise or significant risk | Urgent investigation |
| P3 | Medium | Suspicious activity requiring investigation | Standard investigation |
| P4 | Low | Informational or low-risk events | Routine handling |

---

# 5. P1 – Critical Priority

---

## 5.1 Definition

P1 tickets represent active or confirmed security incidents with severe and immediate impact to business operations, data, or critical systems.

---

## 5.2 Classification Criteria

| Criterion | Examples |
|---|---|
| Active ransomware execution | File encryption observed |
| Confirmed data exfiltration | Large outbound transfer to unknown IP |
| Domain controller compromise | DCSync, credential dumping on DC |
| Active lateral movement | Multiple hosts compromised |
| Complete service outage | DDoS causing full unavailability |
| Active C2 communication | Confirmed beaconing to threat actor |
| Privileged account takeover | Domain admin credential confirmed stolen |
| Critical infrastructure impact | Payment systems, core banking affected |
| Supply chain compromise | Trusted vendor delivering malicious payload |
| Zero-day exploit confirmed | Active exploitation in environment |

---

## 5.3 SLA Requirements

| SLA Metric | Requirement |
|---|---|
| Ticket creation | Immediate upon detection |
| Initial triage completion | Within 15 minutes |
| SOC Lead notification | Within 15 minutes |
| Management notification | Within 30 minutes |
| Escalation to IR Team | Within 30 minutes |
| Status update frequency | Every 30 minutes |
| Bridge call initiation | Within 30 minutes |

---

## 5.4 Approval and Escalation Authority

| Action | Authority |
|---|---|
| Priority assignment | L1 / SOC Lead |
| Containment execution | IR Team Lead |
| Management notification | SOC Manager / CISO |
| Priority downgrade | SOC Manager only |
| Ticket closure | IR Team Lead + SOC Manager |

---

## 5.5 Mandatory Actions

| Action | Requirement |
|---|---|
| Activate IR playbook | Mandatory |
| Initiate bridge call | Mandatory |
| Preserve evidence | Mandatory |
| Notify management | Mandatory |
| Regulatory notification check | Mandatory |
| MSSP client notification | If applicable |

---

# 6. P2 – High Priority

---

## 6.1 Definition

P2 tickets represent likely security incidents or significant threats that have not yet caused confirmed widespread impact but carry high risk of escalation.

---

## 6.2 Classification Criteria

| Criterion | Examples |
|---|---|
| Privileged account suspicious activity | Admin login from unusual location |
| Malware confirmed on endpoint | Trojan/RAT confirmed active |
| Phishing with credential harvesting | Multiple users targeted |
| Unauthorized access to sensitive system | Finance or HR system access |
| Suspicious internal reconnaissance | Port scanning from internal host |
| BEC confirmed | Email rule manipulation detected |
| Insider threat indicators | Data staging behavior observed |
| Cloud misconfiguration with exposure | S3 bucket publicly accessible |
| Multiple failed authentications | Brute force against privileged accounts |
| Threat intel IOC match | High-confidence IOC observed in environment |

---

## 6.3 SLA Requirements

| SLA Metric | Requirement |
|---|---|
| Ticket creation | Within 15 minutes |
| Initial triage completion | Within 30 minutes |
| SOC Lead notification | Within 30 minutes |
| Escalation to L2 | Within 30 minutes |
| Management notification | Within 1 hour |
| Status update frequency | Every 60 minutes |

---

## 6.4 Approval and Escalation Authority

| Action | Authority |
|---|---|
| Priority assignment | L1 / SOC Lead |
| Containment execution | SOC Lead / IR Team |
| Management notification | SOC Lead |
| Priority upgrade to P1 | SOC Lead with justification |
| Ticket closure | SOC Lead |

---

## 6.5 Mandatory Actions

| Action | Requirement |
|---|---|
| Activate relevant playbook | Mandatory |
| Assign L2 investigator | Mandatory |
| Preserve evidence | Mandatory |
| Notify SOC Lead | Mandatory |
| Document investigation timeline | Mandatory |

---

# 7. P3 – Medium Priority

---

## 7.1 Definition

P3 tickets represent suspicious activity or potential threats that require investigation but do not present immediate confirmed risk of compromise.

---

## 7.2 Classification Criteria

| Criterion | Examples |
|---|---|
| Suspicious process execution | Encoded PowerShell on standard workstation |
| Anomalous user behavior | Login at unusual hours |
| Potential phishing email | Reported but not clicked |
| Low-confidence IOC match | Threat intel match with low fidelity |
| Non-critical vulnerability exploitation attempt | Web app scan detected |
| Unusual outbound connection | Single connection to unknown IP |
| Policy violation | Unauthorized software installation |
| Repeated authentication failures | Normal user account |
| Suspicious scheduled task | New task created outside change window |
| USB device usage | On non-approved endpoint |

---

## 7.3 SLA Requirements

| SLA Metric | Requirement |
|---|---|
| Ticket creation | Within 30 minutes |
| Initial triage completion | Within 2 hours |
| L2 escalation if required | Within 2 hours |
| Status update frequency | At key investigation milestones |
| Resolution target | Within 24 hours |

---

## 7.4 Approval and Escalation Authority

| Action | Authority |
|---|---|
| Priority assignment | L1 Analyst |
| Investigation | L1 / L2 Analyst |
| Priority upgrade to P2 | L2 / SOC Lead with justification |
| Ticket closure | L2 Analyst (SOC Lead review) |

---

# 8. P4 – Low Priority

---

## 8.1 Definition

P4 tickets represent informational events, low-risk alerts, or operational tasks that require tracking but carry minimal immediate risk.

---

## 8.2 Classification Criteria

| Criterion | Examples |
|---|---|
| Informational security alerts | Low-fidelity detection rule firing |
| Routine policy notifications | User account expiry warning |
| Confirmed false positive with tuning required | Known tool generating alert |
| Operational health checks | SIEM agent offline notification |
| Awareness reports | Phishing simulation result |
| Minor vulnerability notification | Low CVSS score finding |
| Routine access review flag | Scheduled review item |
| Housekeeping tasks | IOC aging, ticket cleanup |

---

## 8.3 SLA Requirements

| SLA Metric | Requirement |
|---|---|
| Ticket creation | Within 1 hour |
| Initial triage | Within 4 hours |
| Resolution target | Within 72 hours |
| Update frequency | At completion |

---

## 8.4 Approval and Escalation Authority

| Action | Authority |
|---|---|
| Priority assignment | L1 Analyst |
| Investigation | L1 Analyst |
| Ticket closure | L1 / L2 Analyst |

---

# 9. Priority Assignment Decision Flow

| Step | Question | Yes → | No → |
|---|---|---|---|
| Step 1 | Is there confirmed active compromise? | P1 | Go to Step 2 |
| Step 2 | Is privileged account or critical system involved? | P2 | Go to Step 3 |
| Step 3 | Does activity require active investigation? | P3 | Go to Step 4 |
| Step 4 | Is this informational or low risk? | P4 | Review again |

---

# 10. Priority Escalation Criteria

Priority must be upgraded when:

| Trigger | Action |
|---|---|
| Scope expands to additional hosts | Upgrade priority |
| Privileged account confirmed compromised | Upgrade to P1/P2 |
| Data exfiltration evidence found | Upgrade to P1 |
| Lateral movement confirmed | Upgrade to P1 |
| Business impact confirmed | Upgrade to P1 |
| Threat intelligence match upgraded | Reassess priority |

---

## 10.1 Priority Downgrade Requirements

| Requirement | Standard |
|---|---|
| Written justification in ticket | Mandatory |
| SOC Lead approval | Mandatory for P1/P2 downgrade |
| Evidence supporting downgrade | Mandatory |

---

# 11. MSSP Client Priority Considerations

For MSSP-managed environments:

| Consideration | Requirement |
|---|---|
| Client criticality profile | Must be consulted before priority assignment |
| Client-specific SLA applied | Priority drives client SLA compliance |
| Critical asset tag | Automatically elevates priority |
| Client notification threshold | Defined per client contract |
| Client environment profile reference | Must be checked during triage |

Reference:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`

---

# 12. Priority Matrix Summary Table

| Factor | P1 Critical | P2 High | P3 Medium | P4 Low |
|---|---|---|---|---|
| Active compromise | Yes | Possible | No | No |
| Business impact | Severe | Significant | Limited | Minimal |
| Scope | Multi-system | Single/few | Contained | Isolated |
| Data at risk | Confirmed | Possible | Unknown | No |
| Privilege level | Domain/Admin | Privileged | Standard | Standard |
| Urgency | Immediate | Urgent | Standard | Routine |
| IR team required | Yes | Possible | No | No |
| Management notification | Immediate | 1 hour | As needed | Not required |
| Bridge call | Yes | As needed | No | No |

---

# 13. Common Priority Misclassification Examples

| Scenario | Incorrect | Correct | Reason |
|---|---|---|---|
| Admin account login from new country | P3 | P2 | Privileged account involved |
| Ransomware note found on one host | P2 | P1 | Active ransomware indicator |
| Low-fidelity IOC match | P2 | P3 | Insufficient evidence for high priority |
| DDoS causing full service outage | P2 | P1 | Complete service unavailability |
| Single failed login - standard user | P3 | P4 | Low risk, informational |

---

# 14. Related Documents

| Document | Path |
|---|---|
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| Ticket Escalation Workflow | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Escalation-Workflow.md` |
| Ticket Closure Criteria | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md` |
| Severity Classification Guide | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md` |
| Internal SLA Definitions | `00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md` |
| Client Environment Profile | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md` |

---

# 15. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / SOC Operations Lead | Initial version |

---

# 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**