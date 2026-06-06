# SOP: L2 Escalation Criteria and Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L2 Escalation Criteria and Procedures |
| Document ID | SOC-L2-SOP-002 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / L2 Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the escalation criteria, escalation paths, and communication requirements for Level 2 (L2) SOC analysts.

L2 escalation is fundamentally different from L1 escalation because:

- L2 analysts have deeper investigation capability
- Escalation decisions are made with more evidence
- Escalation targets are L3 or IR Team
- Escalation may trigger executive involvement
- Escalation may trigger regulatory notification
- Escalation may initiate legal hold procedures

The consequences of incorrect escalation decisions at L2 are therefore more significant.

Delayed L2 escalation to L3 or IR Team can:

- Allow attackers to establish deeper persistence
- Allow data exfiltration to continue
- Allow ransomware to spread
- Delay executive notification
- Create regulatory compliance failures

This SOP ensures:

- Consistent escalation decision-making
- Clear escalation paths
- Proper evidence transfer
- Timely communication
- Accurate severity management

---

# 3. Scope

Applies to L2 escalations involving:

- Advanced malware analysis
- Memory forensics requirements
- Domain controller compromise
- Cloud root/admin compromise
- Ransomware incidents
- Data breach investigations
- APT indicators
- Zero-day exploitation
- Insider threat cases
- Supply chain compromise
- MSSP client critical incidents

---

# 4. Escalation Philosophy (IMPORTANT)

L2 analysts must understand that escalation is a professional responsibility, not a sign of analytical failure.

The purpose of escalation is to ensure:
- The right expertise handles the right problem
- Critical incidents receive maximum response capability
- Business, legal, and regulatory obligations are met on time

L2 analysts sometimes delay escalation because they want to:
- Complete investigation first
- Avoid "bothering" IR Team
- Avoid appearing uncertain

This behavior is operationally dangerous.

The correct principle is:

"If the situation exceeds L2 capability or involves confirmed critical compromise, escalate immediately."

---

# 5. L2 Escalation Target Overview

| Escalation Target | When |
|---|---|
| L3 Analyst | Advanced forensics required |
| IR Team Lead | Critical or major incident |
| SOC Lead | Operational or SLA concern |
| Executive / CISO | Major business impact |
| Legal / Compliance | Regulatory notification required |
| Client (MSSP) | Client-specific notification required |

---

# 6. L2 Escalation Workflow

| Phase | Objective |
|---|---|
| Phase 1 | Confirm escalation requirement |
| Phase 2 | Prepare escalation package |
| Phase 3 | Notify escalation target |
| Phase 4 | Transfer ownership |
| Phase 5 | Document escalation |
| Phase 6 | Track acknowledgement |

---

# 7. Phase 1 – Confirm Escalation Requirement

Before escalating, confirm:

| Validation Item | Purpose |
|---|---|
| Investigation scope exceeds L2 capability | Necessity confirmation |
| Evidence supports critical severity | Accuracy |
| Containment authority required | Action validation |
| Regulatory notification possible | Compliance check |

---

# 8. Escalation Criteria by Severity

---

## 8.1 Immediate IR Team Escalation (CRITICAL)

Escalate to IR Team immediately if:

| Condition | Risk |
|---|---|
| Active ransomware confirmed | Business impact |
| Domain controller compromise | Enterprise-wide |
| Cloud root/admin compromise | Infrastructure |
| Active data exfiltration | Regulatory |
| APT-level indicators identified | Strategic |
| Multiple segments compromised | Widespread |
| Backup systems targeted | Recovery risk |
| EDR tampered | Monitoring loss |

---

## 8.2 Immediate L3 Escalation

Escalate to L3 if:

| Condition | Reason |
|---|---|
| Memory forensics required | L3 tool requirement |
| Advanced malware analysis | Reverse engineering |
| Rootkit indicators | Kernel-level analysis |
| Attribution needed | Threat actor analysis |
| Complex persistence | Deep investigation |
| Advanced evasion detected | Specialist knowledge |

---

## 8.3 SOC Lead Notification

Notify SOC Lead immediately if:

| Condition | Reason |
|---|---|
| SLA breach imminent | Operational risk |
| Major incident activation | Management visibility |
| Cross-client MSSP impact | Business risk |
| Monitoring outage | Visibility risk |

---

## 8.4 Legal and Compliance Escalation

Escalate to Legal/Compliance if:

| Condition | Reason |
|---|---|
| PII or regulated data exposed | Legal obligation |
| Regulatory reporting triggered | Compliance requirement |
| Law enforcement engagement needed | Legal protocol |
| Legal hold required | Evidence preservation |
| Public disclosure likely | Communication planning |

---

# 9. Phase 2 – Escalation Package Preparation (IMPORTANT)

The quality of the escalation package directly impacts response speed.

A poorly prepared escalation wastes IR Team time and delays containment.

---

## 9.1 Required Escalation Package Contents

| Item | Requirement |
|---|---|
| Incident summary | Clear and concise |
| Severity | Validated |
| Affected systems | Complete list |
| Affected accounts | With privilege levels |
| Evidence references | All artifacts linked |
| Timeline | UTC-based |
| Attacker activity summary | What happened |
| Actions already taken | Containment/evidence |
| Escalation reason | Technical justification |
| Recommended next steps | Suggested actions |

---

## 9.2 Escalation Quality Example

GOOD:
"P1 escalation – Ransomware confirmed on FIN-SRV-01. Multiple files encrypted since 02:14 UTC. Domain admin account detected on host. Possible lateral movement via RDP to FIN-SRV-02. EDR confirms lsass.exe memory access at 02:09 UTC. Host not yet isolated pending IR decision."

BAD:
"Ransomware looks active. Please review."

---

# 10. Phase 3 – Escalation Communication

Escalation must reach the correct target immediately.

---

## 10.1 Communication Requirements

| Severity | Communication Method |
|---|---|
| P1 | Verbal + ticket + messaging |
| P2 | Ticket + messaging |
| P3 | Ticket update |

---

## 10.2 Escalation Channels

Use approved channels only:

- SOC bridge call
- Secure messaging platform
- Incident ticketing system
- Email (for non-critical escalations)

Do not escalate:
- Via personal messaging
- Via unencrypted channels
- Without ticket reference

---

# 11. Phase 4 – Ownership Transfer

Escalation does not automatically release L2 from responsibility.

The L2 analyst must:
- Continue investigation until handover confirmed
- Support L3 or IR Team during investigation
- Maintain ticket updates during escalation
- Provide additional evidence if requested

---

# 12. Phase 5 – Escalation Documentation

Every escalation must be documented.

---

## 12.1 Required Documentation

| Requirement | Status |
|---|---|
| Escalation timestamp | ☐ |
| Escalation target | ☐ |
| Escalation reason | ☐ |
| Evidence package reference | ☐ |
| Acknowledgement received | ☐ |

---

## 12.2 Escalation Log Table

| Timestamp (UTC) | Escalation Target | Severity | Reason | Acknowledged? |
|---|---|---|---|---|
| | | | | |

---

# 13. Phase 6 – Acknowledgement Tracking (IMPORTANT)

Unacknowledged escalations are a major operational risk.

---

## 13.1 Follow-Up Requirements

| Severity | Follow-Up |
|---|---|
| P1 | Immediate verbal follow-up |
| P2 | Within SLA |
| P3 | Ticket notification |

If P1 escalation not acknowledged:
- Escalate to SOC Lead immediately
- Contact IR Team Lead directly
- Initiate bridge call if required

---

# 14. Escalation Quick Reference Matrix

| Incident Type | Severity | Escalation Target |
|---|---|---|
| Ransomware | P1 | IR Team |
| Data exfiltration | P1 | IR Team |
| Domain admin compromise | P1 | IR Team |
| Cloud root compromise | P1 | IR Team |
| APT indicators | P1 | L3 / IR Team |
| Memory forensics needed | P2 | L3 |
| Advanced malware | P2 | L3 |
| Credential dumping | P2 | L2/L3 |
| Lateral movement | P2 | IR Team |
| Regulatory breach | P1 | Legal / CISO |

---

# 15. Situations Requiring Additional Approval

The following escalation actions require SOC Lead or executive approval:

| Action | Approval |
|---|---|
| Client notification | SOC Lead |
| Regulatory reporting | CISO |
| Law enforcement engagement | CISO + Legal |
| Public disclosure | CISO + Legal |
| Extended evidence hold | Legal |

---

# 16. MSSP Escalation Requirements

For MSSP-managed environments:

- Follow client-specific escalation matrix
- Notify Service Delivery Manager for P1/P2
- Meet client-specific SLA requirements
- Maintain client evidence segregation
- Escalate cross-client incidents to SOC Lead immediately

Reference:
`09_MSSP-SPECIFIC/09.1_Client-Management/`

---

# 17. Common L2 Escalation Mistakes

| Mistake | Risk |
|---|---|
| Delayed escalation | Increased attacker dwell time |
| Weak escalation package | Investigation delays |
| Wrong escalation target | Ownership confusion |
| No acknowledgement follow-up | Missed response |
| Releasing ownership prematurely | Operational gap |

---

## 18. Related Documents

| Document | Path |
|---|---|
| L2 Investigation SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md` |
| L2 Evidence Handling SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md` |
| Escalation Matrix Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| Emergency P1 Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md` |
| L2 to L3 Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L2-to-L3-Escalation.md` |

---

## 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / L2 Operations Lead | Initial version |

---

## 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**