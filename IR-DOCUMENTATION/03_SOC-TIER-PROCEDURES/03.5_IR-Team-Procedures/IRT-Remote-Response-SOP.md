# SOP: IRT Remote Response Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – IRT Remote Response Procedures |
| Document ID | SOC-IRT-SOP-003 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | IR Team Lead |
| Approved By | CISO |
| Classification | Internal – Restricted Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the operational methodology, workflows, communication standards, evidence handling requirements, and coordination procedures for Incident Response Team (IRT) remote response activities.

Remote IRT response is used when an incident can be effectively investigated, contained, and remediated without physical presence at the affected site.

Remote response is the most common operational model for modern Incident Response operations and supports:

- Rapid response activation
- 24x7 IR coverage
- Cost-efficient operations
- Geographically distributed teams
- Cloud-based incident response
- Multi-client MSSP environments
- Investigation of distributed infrastructure
- Coordinated technical investigations

Remote response is suitable when:

- Affected systems are remotely accessible
- Evidence acquisition can be performed remotely
- Containment can be executed remotely
- Cloud-based investigation is required
- Endpoint-based forensics can be performed via EDR
- No physical evidence collection is required

Improper remote response operations may result in:

- Evidence loss
- Delayed containment
- Investigation gaps
- Communication failures
- Tooling limitations
- Regulatory compliance issues
- MSSP service disruptions

This SOP ensures:

- Structured remote response operations
- Effective coordination
- Proper evidence handling
- Standardized communication procedures
- Audit-ready operational records

---

# 3. Scope

This SOP applies to remote IRT operations involving:

| Incident Type | Example |
|---|---|
| Ransomware investigations | Endpoint encryption |
| Cloud security incidents | IAM abuse |
| Phishing/BEC | Account compromise |
| Insider threats | Unauthorized access |
| Data exfiltration | Cloud upload |
| Malware investigations | Endpoint compromise |
| Credential attacks | Privileged abuse |
| Network intrusion | Lateral movement |
| APT activity | Long-term compromise |
| MSSP client incidents | Customer environments |

---

## 3.1 Remote Response Stakeholders

| Stakeholder | Role |
|---|---|
| IRT Lead | Operational coordination |
| L3 Analysts | Forensic investigation |
| Malware Analysts | Sample analysis |
| Cloud Analysts | Cloud investigation |
| Network Analysts | Traffic investigation |
| Threat Intelligence Analysts | IOC enrichment |
| MSSP Client Teams | Coordination |
| Executive Liaison | Strategic communication |

---

# 4. Remote Response Philosophy (IMPORTANT)

Remote response operations require strong discipline because:

- The IRT lacks direct physical access
- Evidence handling depends on remote tooling
- Coordination relies on virtual communication
- Containment actions are dependent on remote infrastructure
- Investigation depends on telemetry availability

The objective of remote IRT response is to:

- Rapidly investigate
- Effectively contain
- Properly preserve evidence
- Coordinate stakeholders
- Maintain operational visibility

IRT personnel must avoid:

| Poor Practice | Operational Risk |
|---|---|
| Assuming remote access is reliable | Operational disruption |
| Weak evidence preservation | Forensic gaps |
| Poor communication cadence | Operational confusion |
| Weak coordination with internal teams | Containment delays |
| Insufficient documentation | Audit failures |

---

# 5. IRT Remote Response Responsibilities

| Responsibility | Description |
|---|---|
| Remote investigation | Telemetry-based analysis |
| Evidence acquisition | Remote forensic collection |
| Containment execution | Remote isolation |
| Coordination with internal teams | Operational alignment |
| Stakeholder communication | Reporting |
| Documentation | Audit readiness |
| MSSP client coordination | Service management |
| Cloud forensic operations | Cloud investigation |

---

# 6. Remote Response Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Activation Acceptance | Operational ownership |
| Phase 2 | Initial Investigation Planning | Operational structure |
| Phase 3 | Remote Evidence Acquisition | Forensic artifacts |
| Phase 4 | Investigation Execution | Threat reconstruction |
| Phase 5 | Containment Coordination | Threat neutralization |
| Phase 6 | Communication and Reporting | Stakeholder visibility |
| Phase 7 | Remediation Support | Recovery coordination |
| Phase 8 | Closure and Documentation | Audit readiness |

---

# 7. Phase 1 – Activation Acceptance

IRT accepts operational ownership from SOC.

---

## 7.1 Activation Acceptance Requirements

| Requirement | Mandatory |
|---|---|
| Incident summary reviewed | Yes |
| Severity validated | Yes |
| Evidence package reviewed | Yes |
| Scope assessed | Yes |
| Ownership transferred | Yes |

---

## 7.2 Activation Acceptance Checklist

| Validation Item | Completed |
|---|---|
| Incident reviewed | ☐ |
| Evidence reviewed | ☐ |
| Stakeholders identified | ☐ |
| Communication cadence agreed | ☐ |
| Operational ownership accepted | ☐ |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md`

---

# 8. Phase 2 – Initial Investigation Planning

IRT defines investigation scope and operational structure.

---

## 8.1 Planning Areas

| Area | Objective |
|---|---|
| Investigation objectives | Scope clarity |
| Evidence acquisition planning | Forensic readiness |
| Tooling validation | Operational readiness |
| Communication structure | Coordination |
| Resource assignment | Team coordination |

---

## 8.2 Planning Checklist

| Validation Item | Completed |
|---|---|
| Objectives defined | ☐ |
| Tools validated | ☐ |
| Communication cadence set | ☐ |
| Roles assigned | ☐ |
| Initial actions identified | ☐ |

---

## 8.3 Initial Investigation Areas

| Area | Investigation Focus |
|---|---|
| Endpoint compromise | EDR investigation |
| Cloud compromise | Cloud audit logs |
| Credential abuse | Authentication review |
| Network compromise | Traffic investigation |
| Application compromise | Application logs |

---

# 9. Phase 3 – Remote Evidence Acquisition (CRITICAL)

IRT collects evidence using remote forensic tooling.

---

## 9.1 Remote Acquisition Tools

| Tool Type | Example |
|---|---|
| EDR forensic console | CrowdStrike, Defender |
| SIEM exports | Splunk, Sentinel |
| Cloud platform exports | AWS, Azure, GCP |
| Network capture systems | Remote PCAP |
| Identity logs | AD, Entra ID |

---

## 9.2 Evidence Acquisition Standards

| Standard | Mandatory |
|---|---|
| Original evidence preserved | Yes |
| SHA-256 hashing performed | Yes |
| Chain-of-custody maintained | Yes |
| Secure transfer used | Yes |
| Storage in approved repository | Yes |

---

## 9.3 Remote Evidence Priority

Collect in the following order:

1. Volatile memory (via EDR)
2. EDR telemetry
3. Cloud audit logs
4. Authentication logs
5. Network logs
6. SIEM exports
7. Endpoint disk artifacts

---

## 9.4 Evidence Tracking Table

| Evidence ID | Source | Acquired By | Time UTC | SHA-256 |
|---|---|---|---|---|
| | | | | |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`

---

# 10. Phase 4 – Investigation Execution

IRT performs structured investigation using remote tooling.

---

## 10.1 Investigation Areas

| Area | Investigation Focus |
|---|---|
| Endpoint compromise | Process analysis |
| Credential abuse | Authentication anomalies |
| Lateral movement | Internal spread |
| Cloud compromise | IAM abuse |
| Network activity | C2 communication |
| Data exfiltration | Outbound transfers |

---

## 10.2 Investigation Tools

| Tool | Purpose |
|---|---|
| EDR | Endpoint behavior |
| SIEM | Event correlation |
| Cloud monitoring | Cloud forensics |
| Identity platform | Authentication review |
| Network telemetry | Traffic investigation |

---

## 10.3 Critical Investigation Questions

| Question | Purpose |
|---|---|
| Is attacker active? | Urgency |
| Is persistence present? | Long-term compromise |
| Is data exposure confirmed? | Regulatory exposure |
| Is lateral movement occurring? | Scope analysis |
| Is privileged compromise present? | Enterprise risk |

---

# 11. Phase 5 – Containment Coordination

IRT coordinates remote containment activities.

---

## 11.1 Remote Containment Areas

| Area | Example |
|---|---|
| EDR-based isolation | Endpoint quarantine |
| Account disablement | Credential protection |
| Firewall blocking | C2 disruption |
| Cloud key revocation | IAM protection |
| Network segmentation | Spread prevention |

---

## 11.2 Containment Authority

| Action | Approval Required |
|---|---|
| Endpoint isolation | IRT Lead |
| Critical system shutdown | Executive approval |
| Cloud admin key revocation | Cloud Owner + IRT |
| Network segmentation | Network Team + IRT |

---

## 11.3 Emergency Containment Triggers

Immediate containment required if:

- Active ransomware encryption ongoing
- Data exfiltration active
- Domain compromise confirmed
- Cloud admin compromise active
- Critical business systems impacted

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 12. Phase 6 – Communication and Reporting

IRT maintains structured communication during remote operations.

---

## 12.1 Communication Cadence

| Severity | Update Frequency |
|---|---|
| P1 | Every 30 minutes |
| P2 | Every 60 minutes |
| P3 | Every 4 hours |

---

## 12.2 Communication Areas

| Area | Purpose |
|---|---|
| Investigation progress | Operational visibility |
| Containment status | Risk reduction |
| Business impact | Executive awareness |
| Pending actions | Coordination |
| SLA compliance | Operational tracking |

---

## 12.3 Communication Channels

| Channel | Usage |
|---|---|
| Secure conference bridge | Major coordination |
| Secure messaging | Operational updates |
| Ticketing system | Documentation |
| Email | Formal communication |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

---

# 13. Phase 7 – Remediation Support

IRT supports remediation efforts.

---

## 13.1 Remediation Areas

| Area | Example |
|---|---|
| Patch deployment | Vulnerability mitigation |
| Credential rotation | Account protection |
| System rebuild | Threat eradication |
| Cloud hardening | IAM controls |
| Network reconfiguration | Segmentation |

---

## 13.2 Remediation Coordination Requirements

| Requirement | Mandatory |
|---|---|
| Action owner assigned | Yes |
| Operational testing performed | Yes |
| Validation completed | Yes |
| Stakeholders notified | Yes |

---

## 13.3 Remediation Validation Checklist

| Validation Item | Completed |
|---|---|
| Compromised systems remediated | ☐ |
| Persistence removed | ☐ |
| Credentials reset | ☐ |
| Network controls validated | ☐ |
| Detection updates deployed | ☐ |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/`

---

# 14. Phase 8 – Closure and Documentation

IRT formally closes remote operations.

---

## 14.1 Closure Validation Checklist

| Validation Item | Completed |
|---|---|
| Threat eradicated | ☐ |
| Containment validated | ☐ |
| Evidence preserved | ☐ |
| Reports completed | ☐ |
| Stakeholders notified | ☐ |

---

## 14.2 Required Documentation

| Requirement | Mandatory |
|---|---|
| Investigation timeline | Yes |
| Evidence references | Yes |
| Containment actions | Yes |
| Remediation actions | Yes |
| Communication records | Yes |

---

## 14.3 Remote Operations Timeline Table

| Timestamp UTC | Event | Action Owner | Notes |
|---|---|---|---|
| | | | |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Closure-Criteria.md`

---

# 15. Remote Tooling Validation Requirements

Remote operations depend heavily on tool availability and reliability.

---

## 15.1 Tooling Validation Checklist

| Validation Item | Completed |
|---|---|
| EDR access validated | ☐ |
| SIEM access validated | ☐ |
| Cloud console access validated | ☐ |
| Network telemetry available | ☐ |
| Communication tools verified | ☐ |

---

## 15.2 Operational Risk Conditions

Immediate escalation required if:

| Condition | Risk |
|---|---|
| EDR offline | Endpoint visibility loss |
| SIEM outage | Investigation gap |
| Cloud console outage | Cloud blindness |
| Communication failure | Coordination breakdown |

---

# 16. MSSP-Specific Remote Response Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain tenant segregation | Confidentiality |
| Follow client-specific SLA | Contract compliance |
| Restrict cross-client visibility | Compliance |
| Preserve client evidence separately | Audit readiness |
| Use client-approved communication channels | Service standards |

---

# 17. Common Remote Response Mistakes

| Mistake | Operational Risk |
|---|---|
| Weak evidence preservation | Forensic gaps |
| Poor remote coordination | Operational confusion |
| Delayed containment | Increased compromise |
| Weak communication cadence | Operational visibility loss |
| Missing documentation | Audit failures |
| Over-reliance on EDR only | Visibility gaps |

---

# 18. Related Documents

| Document | Path |
|---|---|
| IRT Activation Criteria | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md` |
| IRT Onsite Response SOP | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Onsite-Response-SOP.md` |
| IRT Forensic Collection SOP | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Forensic-Collection-SOP.md` |
| IRT Evidence Chain-of-Custody | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Evidence-Chain-of-Custody.md` |
| IRT Containment Authority Matrix | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md` |
| IRT Closure Criteria | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Closure-Criteria.md` |

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