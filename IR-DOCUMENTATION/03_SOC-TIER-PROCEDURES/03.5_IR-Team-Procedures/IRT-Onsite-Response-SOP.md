# SOP: IRT Onsite Response Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – IRT Onsite Response Procedures |
| Document ID | SOC-IRT-SOP-002 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | IR Team Lead |
| Approved By | CISO |
| Classification | Internal – Restricted Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the operational methodology, deployment standards, coordination workflows, evidence handling requirements, and communication procedures for Incident Response Team (IRT) onsite response activities.

Onsite IRT response is required when an incident cannot be effectively contained, investigated, or remediated through remote operations and requires physical presence at:

- Customer premises
- Data center facilities
- Critical infrastructure sites
- Cloud collocation facilities
- MSSP client locations
- Disaster recovery sites
- Manufacturing or OT/ICS environments

Onsite IRT response supports:

- Physical evidence collection
- Hands-on forensic acquisition
- Direct system isolation
- Hardware-level investigation
- Coordination with site personnel
- OT/ICS environment incident response
- Sensitive investigations requiring physical access
- Regulatory or legal investigations

Improper onsite IRT operations may result in:

- Evidence contamination
- Loss of forensic integrity
- Delayed containment
- Operational disruption
- Compliance failures
- Personnel safety risks
- Insufficient documentation
- Cross-team coordination breakdowns

This SOP ensures:

- Structured onsite response operations
- Proper evidence preservation
- Safe and controlled deployment
- Standardized coordination procedures
- Audit-ready operational records

---

# 3. Scope

This SOP applies to onsite IRT response activities involving:

| Scenario | Example |
|---|---|
| Major ransomware events | Multi-site encryption |
| Domain compromise | Privileged compromise |
| Data breach investigations | Sensitive data exposure |
| Cloud-physical hybrid attacks | Coordinated incident |
| Insider threat investigations | Authorized user abuse |
| OT/ICS incidents | Manufacturing impact |
| Supply chain compromise | Trusted vendor abuse |
| Legal investigations | Evidence preservation |
| Critical infrastructure response | Business continuity |
| MSSP client onsite engagement | Customer support |

---

## 3.1 Onsite Response Stakeholders

| Stakeholder | Role |
|---|---|
| IRT Lead | Onsite coordination |
| Forensic Analysts | Evidence acquisition |
| Malware Analysts | Sample analysis |
| Network Analysts | Traffic investigation |
| Cloud Analysts | Cloud forensics |
| Legal Liaison | Legal coordination |
| Executive Liaison | Strategic communication |
| Site Personnel | Local coordination |

---

# 4. Onsite Response Philosophy (IMPORTANT)

Onsite response must be conducted with operational discipline, forensic integrity, and personnel safety as primary priorities.

The objective of onsite response is to:

- Establish physical access
- Preserve volatile evidence
- Execute containment
- Support forensic investigation
- Coordinate with site teams
- Document all actions

IRT personnel must understand:

- Onsite operations carry elevated forensic risk
- Improper handling may destroy critical evidence
- Coordination with onsite stakeholders is critical
- Operational missteps may impact business operations

---

## 4.1 Common Onsite Response Failures

| Poor Practice | Operational Risk |
|---|---|
| Insufficient pre-deployment planning | Operational confusion |
| Weak evidence handling | Forensic failure |
| Poor coordination with site personnel | Operational delays |
| Inadequate documentation | Audit gaps |
| Inadequate PPE/safety planning | Personnel risk |
| Insufficient toolkit preparation | Mission failure |

---

# 5. IRT Onsite Response Responsibilities

| Responsibility | Description |
|---|---|
| Deployment planning | Pre-deployment readiness |
| Onsite evidence collection | Forensic acquisition |
| Containment execution | Physical isolation |
| Coordination with site personnel | Operational alignment |
| Investigation execution | Onsite analysis |
| Documentation | Audit readiness |
| Stakeholder communication | Operational reporting |
| Travel and safety coordination | Personnel safety |

---

# 6. Onsite Response Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Onsite Deployment Authorization | Approved deployment |
| Phase 2 | Pre-Deployment Planning | Operational readiness |
| Phase 3 | Onsite Arrival and Coordination | Site readiness |
| Phase 4 | Evidence Acquisition | Forensic artifacts |
| Phase 5 | Containment Execution | Threat neutralization |
| Phase 6 | Investigation Support | Forensic analysis |
| Phase 7 | Operational Communication | Stakeholder updates |
| Phase 8 | Demobilization and Documentation | Audit closure |

---

# 7. Phase 1 – Onsite Deployment Authorization

Onsite deployment requires formal authorization.

---

## 7.1 Authorization Triggers

| Trigger | Reason |
|---|---|
| Critical onsite incident | Physical access required |
| Active ransomware in physical environment | Containment urgency |
| OT/ICS incident | Operational risk |
| Legal/regulatory investigation | Evidence preservation |
| MSSP client onsite request | Contract obligation |

---

## 7.2 Authorization Requirements

| Requirement | Approver |
|---|---|
| Onsite deployment | IR Team Lead |
| Executive notification | CISO |
| Client coordination | Service Delivery Manager |
| Legal coordination | Legal Counsel |
| Travel approval | Operations Lead |

---

## 7.3 Authorization Checklist

| Validation Item | Completed |
|---|---|
| Deployment approved | ☐ |
| Executive notified | ☐ |
| Client notified if applicable | ☐ |
| Legal review completed | ☐ |
| Travel authorized | ☐ |

---

# 8. Phase 2 – Pre-Deployment Planning

Effective onsite response requires structured pre-deployment readiness.

---

## 8.1 Pre-Deployment Planning Areas

| Area | Objective |
|---|---|
| Mission scope | Operational clarity |
| Toolkit preparation | Forensic readiness |
| Travel logistics | Personnel coordination |
| Site coordination | Operational alignment |
| Safety planning | Personnel protection |
| Communication setup | Reporting readiness |

---

## 8.2 IRT Toolkit Requirements

| Toolkit Item | Purpose |
|---|---|
| Forensic laptops | Investigation |
| Write blockers | Evidence integrity |
| Forensic imaging hardware | Disk acquisition |
| Memory acquisition tools | Volatile evidence |
| Network capture devices | Traffic analysis |
| Encrypted storage media | Evidence transport |
| Chain-of-custody forms | Legal compliance |
| Communication devices | Coordination |

---

## 8.3 Pre-Deployment Checklist

| Validation Item | Completed |
|---|---|
| Forensic toolkit prepared | ☐ |
| Travel logistics confirmed | ☐ |
| Site contact established | ☐ |
| Safety planning completed | ☐ |
| Communication channels confirmed | ☐ |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Forensics-Toolkit-Reference.md`

---

# 9. Phase 3 – Onsite Arrival and Coordination

Upon arrival, IRT establishes operational coordination.

---

## 9.1 Arrival Procedures

| Step | Objective |
|---|---|
| Site check-in | Access validation |
| Operational briefing | Situational awareness |
| Site contact identification | Coordination |
| Workspace setup | Operational readiness |
| Communication validation | Reporting readiness |

---

## 9.2 Site Coordination Requirements

| Coordination Area | Purpose |
|---|---|
| Site security | Physical access |
| IT teams | System access |
| Facility personnel | Environment awareness |
| Legal representatives | Evidence handling |
| MSSP client representatives | Operational alignment |

---

## 9.3 Initial Onsite Briefing Areas

| Area | Content |
|---|---|
| Current incident status | Operational state |
| Affected systems | Scope review |
| Site safety considerations | Risk awareness |
| Onsite resource availability | Coordination planning |
| Communication cadence | Reporting structure |

---

# 10. Phase 4 – Evidence Acquisition (CRITICAL)

Evidence acquisition is the primary onsite forensic activity.

---

## 10.1 Evidence Acquisition Standards

| Standard | Mandatory |
|---|---|
| Use approved forensic tools | Yes |
| Use write blockers | Yes |
| Generate SHA-256 hashes | Yes |
| Maintain chain-of-custody | Yes |
| Preserve original evidence | Yes |

---

## 10.2 Volatile Evidence Priority

Collect first:

1. Active memory
2. Network connections
3. Running processes
4. Logged-in users
5. Authentication tokens
6. Temporary artifacts

---

## 10.3 Evidence Acquisition Areas

| Area | Example |
|---|---|
| Endpoint memory | RAM acquisition |
| Endpoint disks | Forensic imaging |
| Network captures | PCAP collection |
| Authentication logs | AD/IdP exports |
| Cloud logs | Cloud platform exports |
| Application logs | Business systems |

---

## 10.4 Evidence Tracking Table

| Evidence ID | Source | Acquired By | Time UTC | SHA-256 |
|---|---|---|---|---|
| | | | | |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`

---

# 11. Phase 5 – Containment Execution

IRT supports onsite containment activities.

---

## 11.1 Containment Areas

| Area | Example |
|---|---|
| Endpoint isolation | Network disconnection |
| Credential reset | Account protection |
| Firewall blocking | C2 disruption |
| Service shutdown | Threat neutralization |
| Cloud key revocation | IAM protection |

---

## 11.2 Containment Authority

| Action | Approval Required |
|---|---|
| Endpoint isolation | IRT Lead |
| Critical system shutdown | Executive Approval |
| Network segmentation | Network Team + IRT Lead |
| Cloud admin key revocation | Cloud Owner + IRT Lead |

---

## 11.3 Emergency Containment Triggers

Immediate containment required if:

- Active ransomware encryption ongoing
- Data exfiltration confirmed
- Domain compromise active
- Critical OT/ICS systems impacted

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 12. Phase 6 – Investigation Support

IRT performs hands-on investigation onsite.

---

## 12.1 Investigation Areas

| Area | Objective |
|---|---|
| Endpoint analysis | Attacker behavior |
| Memory analysis | Active compromise |
| Disk analysis | Persistence review |
| Network analysis | C2 investigation |
| Cloud investigation | IAM analysis |

---

## 12.2 Investigation Coordination

| Coordination Area | Purpose |
|---|---|
| SOC remote support | Investigation continuity |
| L3 forensic team | Advanced analysis |
| Malware analysis team | Sample evaluation |
| Threat intelligence team | IOC correlation |

---

# 13. Phase 7 – Operational Communication

IRT maintains structured communication throughout onsite operations.

---

## 13.1 Communication Cadence

| Severity | Update Frequency |
|---|---|
| P1 | Every 30 minutes |
| P2 | Every 60 minutes |
| P3 | Every 4 hours |

---

## 13.2 Communication Areas

| Area | Example |
|---|---|
| Operational status | Investigation progress |
| Containment status | Threat neutralization |
| Business impact | Operational risk |
| Pending actions | Coordination needs |

---

## 13.3 Communication Channels

| Channel | Usage |
|---|---|
| Secure bridge call | Major coordination |
| Secure messaging | Operational updates |
| Ticketing platform | Documentation |
| Email | Formal communication |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

---

# 14. Phase 8 – Demobilization and Documentation

Onsite operations conclude with structured demobilization.

---

## 14.1 Demobilization Checklist

| Validation Item | Completed |
|---|---|
| Evidence secured | ☐ |
| Containment validated | ☐ |
| Site personnel briefed | ☐ |
| Documentation completed | ☐ |
| Transition to remote IRT confirmed | ☐ |

---

## 14.2 Documentation Requirements

| Requirement | Mandatory |
|---|---|
| Onsite timeline | Yes |
| Evidence collected | Yes |
| Containment actions | Yes |
| Investigation findings | Yes |
| Stakeholder communications | Yes |
| Chain-of-custody records | Yes |

---

## 14.3 Onsite Operational Timeline Table

| Timestamp UTC | Event | Action Owner | Notes |
|---|---|---|---|
| | | | |

---

# 15. Safety and Personnel Considerations

Personnel safety must be maintained during onsite operations.

---

## 15.1 Safety Areas

| Area | Example |
|---|---|
| Physical site safety | Hazard awareness |
| Travel safety | Personnel protection |
| OT/ICS safety | Operational risk |
| Confidentiality safety | Information protection |
| Emergency procedures | Site evacuation |

---

## 15.2 Safety Escalation Conditions

Immediate escalation required if:

- Personnel safety threatened
- Site environment hazardous
- Hostile interactions occur
- Legal or compliance complications arise

---

# 16. MSSP-Specific Onsite Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain client confidentiality | Compliance |
| Follow client-specific access procedures | Operational alignment |
| Preserve client evidence separately | Audit readiness |
| Coordinate client executive communication | Service management |
| Maintain tenant segregation | Data protection |

---

# 17. Common Onsite Response Mistakes

| Mistake | Operational Risk |
|---|---|
| Weak pre-deployment planning | Operational confusion |
| Poor evidence handling | Forensic failure |
| Weak site coordination | Operational delays |
| Missing chain-of-custody | Legal inadmissibility |
| Insufficient safety planning | Personnel risk |
| Weak documentation | Audit failures |

---

# 18. Related Documents

| Document | Path |
|---|---|
| IRT Activation Criteria | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md` |
| IRT Remote Response SOP | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Remote-Response-SOP.md` |
| IRT Forensic Collection SOP | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Forensic-Collection-SOP.md` |
| IRT Evidence Chain-of-Custody | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Evidence-Chain-of-Custody.md` |
| IRT Containment Authority Matrix | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md` |
| Forensics Toolkit Reference | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Forensics-Toolkit-Reference.md` |

---

# 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | IR Team Lead | Initial version |

---

# 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**