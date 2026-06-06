# SOP: L1 Escalation Criteria and Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L1 Escalation Criteria and Procedures |
| Document ID | SOC-L1-SOP-003 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / SOC Operations Lead |
| Approved By | SOC Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the escalation criteria, escalation paths, and communication requirements for Level 1 (L1) SOC analysts.

Escalation is one of the most critical operational activities within a SOC because delayed or incorrect escalation can:

- Increase attacker dwell time
- Delay containment actions
- Allow ransomware propagation
- Increase business impact
- Cause SLA violations
- Delay executive notification
- Result in incomplete investigations

This SOP ensures:

- Consistent escalation decisions
- Standardized severity handling
- Timely involvement of L2/L3 and IR teams
- Clear operational accountability
- Reduced confusion during critical incidents
- Proper communication during active attacks

The objective is to ensure that potentially serious incidents are escalated quickly, accurately, and with sufficient technical context.

---

# 3. Scope

Applies to escalation of:

- SIEM alerts
- EDR detections
- Malware incidents
- Phishing/BEC incidents
- Network intrusion alerts
- Cloud compromise indicators
- Data exfiltration alerts
- Identity compromise events
- Zero-day indicators
- APT indicators
- MSSP client incidents

Applies across:

- Internal SOC operations
- MSSP-managed environments
- Hybrid cloud/on-prem environments
- 24x7 SOC operations

---

# 4. Escalation Philosophy (IMPORTANT)

L1 analysts must understand the following principle:

"Escalating early is safer than escalating late."

One of the most damaging operational mistakes in a SOC is hesitation during escalation.

APT actors, ransomware operators, and cloud attackers often move rapidly after initial compromise. Even a 15–30 minute delay may allow:

- Lateral movement
- Privilege escalation
- Data staging
- Log tampering
- Backup destruction
- Cloud persistence establishment

Escalation should therefore be:

- Risk-driven
- Fast
- Evidence-based
- Clearly documented

L1 analysts are NOT expected to fully prove an attack before escalation.

---

# 5. Escalation Levels

| Escalation Level | Target Team | Typical Use Case |
|---|---|---|
| Level 1 | SOC Lead | Operational awareness |
| Level 2 | L2 Analysts | Deep investigation required |
| Level 3 | L3 / IR Team | Advanced or critical incident |
| Executive | Management / CISO | Major business impact |
| External | Client / Vendor / CERT | Approved external escalation |

---

# 6. Escalation Workflow

| Phase | Objective |
|---|---|
| Phase 1 | Validate alert |
| Phase 2 | Assess risk and severity |
| Phase 3 | Determine escalation path |
| Phase 4 | Escalate with evidence |
| Phase 5 | Document escalation |
| Phase 6 | Track acknowledgement |

---

# 7. Severity-Based Escalation Matrix

---

## 7.1 P1 – Critical Incident Escalation

P1 incidents require immediate escalation.

### Examples

| Example | Reason |
|---|---|
| Active ransomware encryption | Immediate business impact |
| Domain admin compromise | Enterprise-wide risk |
| Confirmed data exfiltration | Regulatory risk |
| Cloud root/admin compromise | Critical access loss |
| Multiple systems compromised | Widespread attack |
| Active C2 beaconing on critical system | Live attacker presence |

---

### Mandatory Actions

| Action | Time Requirement |
|---|---|
| Notify SOC Lead | Immediately |
| Escalate to L2/L3 | Immediately |
| Notify IR Team | Immediately |
| Update ticket | Within 5 minutes |
| Join bridge call if requested | Immediate |

---

## 7.2 P2 – High Severity Escalation

### Examples

| Example | Reason |
|---|---|
| Malware execution detected | Possible compromise |
| Suspicious PowerShell execution | Potential attack chain |
| Lateral movement indicators | Active attacker behavior |
| VPN anomaly with privileged account | Credential compromise risk |
| Cloud IAM anomaly | Privilege escalation risk |

---

### Mandatory Actions

| Action | Time Requirement |
|---|---|
| Escalate to L2 | Within SLA |
| Notify SOC Lead if required | Based on severity |
| Update ticket with evidence | Immediate |

---

## 7.3 P3 – Medium Severity Escalation

### Examples

| Example | Reason |
|---|---|
| Suspicious login anomaly | Requires investigation |
| IDS signature hit | Potential attack |
| Unusual outbound traffic | Possible beaconing |
| New admin tool execution | Suspicious activity |

Escalate if:
- Multiple indicators correlate
- Asset is critical
- Activity persists

---

## 7.4 P4 – Informational

Examples:
- Known scanner activity
- Expected vulnerability scans
- Informational policy alerts

Document and monitor.

---

# 8. Immediate Escalation Conditions (CRITICAL)

The following conditions require immediate escalation regardless of uncertainty.

---

## 8.1 Identity and Privilege Escalation

Immediately escalate if:

| Indicator | Escalation Target |
|---|---|
| Domain admin compromise | IR Team |
| MFA bypass | L2/L3 |
| Impossible travel for privileged account | L2 |
| New privileged account creation | L2 |
| Kerberos Golden Ticket indicators | L3 |

---

## 8.2 Malware and Ransomware

Immediately escalate if:

| Indicator | Escalation Target |
|---|---|
| Mass file encryption | IR Team |
| Known ransomware hash | IR Team |
| LSASS credential dumping | L2/L3 |
| Malware spreading laterally | IR Team |
| EDR tampering | L3 |

---

## 8.3 Network Intrusion

Immediately escalate if:

| Indicator | Escalation Target |
|---|---|
| Active C2 communication | L2 |
| Beaconing from critical server | L2/L3 |
| DNS tunneling | L3 |
| Lateral movement detected | IR Team |
| Unauthorized VPN access | L2 |

---

## 8.4 Cloud Security

Immediately escalate if:

| Indicator | Escalation Target |
|---|---|
| Root/admin cloud login anomaly | IR Team |
| CloudTrail logging disabled | L3 |
| Public sensitive bucket exposure | IR Team |
| New cloud access keys created unexpectedly | L2 |
| Cross-account compromise | IR Team |

---

# 9. Escalation Decision Factors

Escalation decisions should consider:

| Factor | Why Important |
|---|---|
| Asset criticality | Business impact |
| Privilege level involved | Escalation risk |
| Number of systems affected | Scope assessment |
| Active attacker behavior | Urgency |
| Data exposure risk | Regulatory impact |
| Threat intelligence match | Confidence increase |

---

# 10. Escalation Communication Standards

Escalation quality is critical.

Poor escalation causes:

- Investigation delays
- Analyst confusion
- Duplicate work
- Missed containment opportunities

---

## 10.1 Required Escalation Content

Every escalation must include:

| Required Item | Example |
|---|---|
| Incident summary | “Potential ransomware execution on server X” |
| Severity | P1 |
| Affected systems | Hostnames/IPs |
| User accounts involved | Username |
| Evidence references | Alert IDs, hashes |
| Timeline | UTC timestamps |
| Actions already taken | Ticket updated |

---

## 10.2 Good Escalation Example

GOOD:
“P1 escalation – EDR detected ransomware encryption behavior on FIN-SRV-01 at 14:22 UTC. Multiple file modifications observed. Domain admin account present on host. No containment executed yet.”

BAD:
“Looks suspicious maybe ransomware.”

---

# 11. Escalation Documentation Requirements

All escalations must be documented.

---

## 11.1 Required Documentation

| Requirement | Status |
|---|---|
| Severity documented | ☐ |
| Escalation timestamp recorded | ☐ |
| Escalation recipient identified | ☐ |
| Supporting evidence attached | ☐ |
| Ticket updated | ☐ |

---

# 12. Escalation Acknowledgement Tracking

L1 analysts must verify escalation acknowledgement.

If escalation not acknowledged:

| Severity | Follow-Up Requirement |
|---|---|
| P1 | Immediate verbal follow-up |
| P2 | Follow up within SLA |
| P3 | Ticket notification sufficient |

---

# 13. Escalation During High Alert Volume (IMPORTANT)

During alert floods or active campaigns:

- Prioritize escalation of high-risk incidents
- Do not suppress alerts without validation
- Notify SOC Lead if backlog develops
- Maintain escalation discipline
- Avoid assuming another analyst already escalated

---

# 14. Escalation Hesitation Indicators

SOC Leads should watch for:

- Analysts repeatedly re-checking obvious incidents
- Tickets remaining in triage too long
- Delayed severity upgrades
- Multiple related alerts not escalated together

These often indicate escalation hesitation.

---

# 15. MSSP Escalation Requirements

For MSSP operations:

- Follow client-specific escalation matrix
- Meet client SLA requirements
- Use approved client communication templates
- Escalate cross-client incidents immediately
- Maintain evidence segregation

Reference:
`09_MSSP-SPECIFIC/`

---

# 16. Common Escalation Mistakes

| Mistake | Risk |
|---|---|
| Waiting for complete certainty | Delayed response |
| Escalating without evidence | Investigation confusion |
| Incorrect severity assignment | SLA impact |
| Poor ticket documentation | Investigation delays |
| Failure to follow up | Missed escalation |

---

# 17. Escalation Quick Reference Matrix

| Incident Type | Severity | Escalate To |
|---|---|---|
| Ransomware | P1 | IR Team |
| Data exfiltration | P1 | IR Team |
| Domain compromise | P1 | L3 / IR |
| Malware execution | P2 | L2 |
| Phishing with credential theft | P2 | L2 |
| Cloud privilege escalation | P1/P2 | L3 |
| Beaconing | P2 | L2 |
| Suspicious PowerShell | P2/P3 | L2 |

---

## 18. Related Documents

| Document | Path |
|---|---|
| L1 Alert Handling SOP | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md` |
| L1 Ticket SOP | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Ticket-Creation-SOP.md` |
| Severity Classification Guide | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/` |
| Escalation Matrix Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/` |
| Emergency P1 Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md` |

---

## 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / SOC Operations Lead | Initial version |

---

## 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**