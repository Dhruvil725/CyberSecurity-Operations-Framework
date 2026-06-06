# SOP: L2 SIEM Deep Investigation Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L2 SIEM Deep Investigation Procedures |
| Document ID | SOC-L2-SOP-005 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / L2 Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the methodology, workflows, investigative standards, and escalation procedures for Level 2 (L2) SIEM-based investigations.

The SIEM platform serves as the primary centralized visibility layer for security monitoring and incident investigations by aggregating telemetry from:

- Endpoints
- Firewalls
- Identity systems
- Cloud platforms
- Network devices
- Security tools
- SaaS platforms
- Threat intelligence feeds

L2 analysts use SIEM investigations to:

- Validate security incidents
- Correlate multi-source telemetry
- Identify attacker behavior
- Investigate lateral movement
- Detect persistence activity
- Reconstruct attack timelines
- Scope affected assets
- Support incident response escalation

Improper SIEM investigations may result in:

- Missed attacker activity
- Incomplete incident scoping
- Delayed containment
- Missed regulatory exposure
- Incorrect severity classification
- Failure to detect lateral movement

This SOP ensures:

- Standardized SIEM investigations
- Consistent investigative methodology
- Proper event correlation
- Accurate severity handling
- Audit-ready investigation records

---

# 3. Scope

This SOP applies to all SIEM investigations involving:

| Incident Type | Example |
|---|---|
| Authentication attacks | Brute force, password spray |
| Malware activity | Endpoint detections |
| Network intrusion | Unauthorized access |
| Insider threat | Privileged misuse |
| Cloud compromise | Suspicious IAM activity |
| Data exfiltration | Large outbound transfers |
| Ransomware indicators | Encryption behavior |
| Lateral movement | RDP/SMB spread |
| Phishing compromise | Account takeover |
| APT activity | Multi-stage attack chains |

---

## 3.1 Applicable SIEM Platforms

| Platform Type | Examples |
|---|---|
| SIEM | Splunk, QRadar, Sentinel |
| Log Analytics | Elastic, Graylog |
| SOAR Integration | Cortex XSOAR, Splunk SOAR |
| Threat Intelligence Platforms | MISP, Recorded Future |

---

# 4. SIEM Investigation Philosophy (IMPORTANT)

SIEM investigation is correlation-driven investigation.

The goal is not simply reviewing individual alerts.

The objective is to identify:

- Attack chains
- Related events
- Cross-platform indicators
- Behavioral anomalies
- Adversary patterns
- Scope of compromise

L2 analysts must investigate:
- What happened
- When it happened
- How it happened
- Which systems were involved
- Which users were affected
- Whether the attacker remains active

---

## 4.1 Common Investigation Failures

| Poor Practice | Operational Risk |
|---|---|
| Reviewing only the triggered alert | Missed attacker activity |
| Ignoring historical logs | Missed persistence |
| No cross-platform correlation | Partial visibility |
| Over-reliance on detection names | Inaccurate conclusions |
| Weak timeline analysis | Investigation gaps |

---

# 5. L2 SIEM Responsibilities

| Responsibility | Description |
|---|---|
| Alert investigation | Validate suspicious activity |
| Event correlation | Cross-source analysis |
| Timeline reconstruction | Event sequencing |
| Threat scoping | Blast radius analysis |
| IOC enrichment | Threat validation |
| Evidence preservation | Export logs/artifacts |
| Escalation | Notify L3/IR Team |
| Documentation | Maintain investigation records |

---

# 6. SIEM Investigation Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Alert Validation | Threat confirmation |
| Phase 2 | Event Correlation | Linked activity |
| Phase 3 | Timeline Reconstruction | Chronology |
| Phase 4 | Identity Analysis | User compromise analysis |
| Phase 5 | Network Activity Review | Communication analysis |
| Phase 6 | Threat Intelligence Enrichment | IOC correlation |
| Phase 7 | Scope Determination | Blast radius |
| Phase 8 | Escalation/Containment | Response coordination |
| Phase 9 | Documentation | Investigation report |

---

# 7. Phase 1 – Alert Validation

The first objective is validating whether the SIEM alert represents malicious activity.

---

## 7.1 Initial Validation Checklist

| Validation Item | Required | Notes |
|---|---|---|
| Alert severity reviewed | ☐ | |
| Triggering rule reviewed | ☐ | |
| Source logs verified | ☐ | |
| Asset criticality reviewed | ☐ | |
| User context reviewed | ☐ | |
| Historical activity checked | ☐ | |
| Related alerts identified | ☐ | |
| MITRE technique reviewed | ☐ | |

---

## 7.2 Alert Validation Questions

| Question | Objective |
|---|---|
| Is the activity malicious? | Threat confirmation |
| Is the activity ongoing? | Urgency analysis |
| Is this isolated? | Scope determination |
| Is persistence indicated? | Long-term compromise |
| Is lateral movement occurring? | Spread analysis |
| Is privileged access involved? | Severity validation |

---

## 7.3 High-Risk Alert Categories

| Alert Type | Risk Level |
|---|---|
| Multiple failed logins | Medium |
| Password spray | High |
| Impossible travel login | High |
| Domain admin login anomaly | Critical |
| Beaconing detection | High |
| Data exfiltration | Critical |
| Ransomware indicator | Critical |
| Cloud root activity anomaly | Critical |

---

# 8. Phase 2 – Event Correlation

SIEM investigations rely heavily on event correlation across multiple telemetry sources.

---

## 8.1 Required Correlation Sources

| Source | Investigation Purpose |
|---|---|
| EDR logs | Endpoint activity |
| Firewall logs | Traffic validation |
| DNS logs | Beaconing analysis |
| Authentication logs | Account compromise |
| Cloud logs | IAM investigation |
| Proxy logs | Web activity |
| VPN logs | Remote access review |
| Email logs | Phishing analysis |

---

## 8.2 Correlation Objectives

The analyst must determine:

- Initial access vector
- Lateral movement
- Persistence mechanisms
- Command-and-control activity
- Privilege escalation
- Data staging activity
- Exfiltration attempts

---

## 8.3 Correlation Best Practices

| Best Practice | Purpose |
|---|---|
| Use UTC timestamps | Timeline consistency |
| Correlate by hostname | Scope accuracy |
| Correlate by username | Account tracking |
| Correlate by IP address | Traffic analysis |
| Correlate by hash | Malware tracking |

---

# 9. Phase 3 – Timeline Reconstruction (CRITICAL)

Timeline reconstruction is mandatory for serious incidents.

---

## 9.1 Timeline Objectives

| Objective | Purpose |
|---|---|
| Identify initial compromise | Root cause analysis |
| Track attacker progression | Threat analysis |
| Detect lateral movement | Scope determination |
| Determine persistence timing | Persistence review |
| Identify exfiltration activity | Regulatory assessment |

---

## 9.2 Required Timeline Events

| Event Type | Example |
|---|---|
| Initial login | VPN access |
| Malware execution | PowerShell launch |
| Privilege escalation | Admin rights obtained |
| Lateral movement | RDP connection |
| Exfiltration | Large outbound upload |

---

## 9.3 Timeline Documentation Table

| Timestamp UTC | Event | Source | Severity | Evidence Ref |
|---|---|---|---|---|
| | | | | |

---

# 10. Phase 4 – Identity and Authentication Analysis

Authentication analysis is critical for identifying account compromise.

---

## 10.1 Authentication Investigation Areas

| Area | Objective |
|---|---|
| Failed logins | Brute-force detection |
| Successful logins | Unauthorized access |
| MFA events | Bypass attempts |
| VPN activity | Remote access review |
| Privileged account use | Admin compromise |
| Service account activity | Automated abuse |

---

## 10.2 High-Risk Authentication Indicators

| Indicator | Meaning |
|---|---|
| Impossible travel | Credential compromise |
| Multiple geo-locations | Session hijacking |
| MFA fatigue | MFA abuse |
| Login outside business hours | Suspicious access |
| Dormant account activity | Account takeover |

---

## 10.3 Privileged Account Escalation Triggers

Immediate escalation required if:

| Condition | Escalation Target |
|---|---|
| Domain admin compromise | IR Team |
| Cloud admin anomaly | IR Team |
| Service account abuse | IR Team |
| Multiple admin logins | L3 / IR Team |

---

# 11. Phase 5 – Network Activity Investigation

Network telemetry helps identify attacker communication patterns.

---

## 11.1 Required Network Analysis Areas

| Area | Purpose |
|---|---|
| External traffic | C2 analysis |
| Internal traffic | Lateral movement |
| DNS requests | Beaconing review |
| Proxy activity | Web access analysis |
| VPN sessions | Remote compromise review |

---

## 11.2 High-Risk Network Indicators

| Indicator | Meaning |
|---|---|
| Repetitive outbound traffic | Beaconing |
| Rare external IPs | Suspicious communication |
| TOR traffic | Anonymization |
| SMB scanning | Lateral movement |
| Large uploads | Exfiltration |

---

## 11.3 Network Investigation Correlation

Correlate network findings with:

- EDR telemetry
- Firewall events
- DNS logs
- Proxy logs
- NetFlow data

Reference:
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Network-Forensics-SOP.md`

---

# 12. Phase 6 – Threat Intelligence Enrichment

Threat intelligence enrichment validates indicators and improves investigation accuracy.

---

## 12.1 IOC Enrichment Areas

| IOC Type | Example |
|---|---|
| IP address | C2 infrastructure |
| Domain | Phishing domain |
| File hash | Malware hash |
| URL | Payload delivery |
| Email address | Phishing sender |

---

## 12.2 Threat Intelligence Sources

| Source Type | Example |
|---|---|
| Commercial TI | Recorded Future |
| Open-source TI | AbuseIPDB |
| Internal TI | IOC repository |
| Government advisories | CERT-In |
| Vendor feeds | Microsoft TI |

---

## 12.3 IOC Validation Table

| IOC | IOC Type | Reputation | Source | Action Taken |
|---|---|---|---|---|
| | | | | |

---

# 13. Phase 7 – Scope Determination

Determine the complete blast radius of the incident.

---

## 13.1 Scope Analysis Areas

| Area | Objective |
|---|---|
| Affected users | User impact |
| Affected endpoints | Endpoint compromise |
| Affected servers | Infrastructure impact |
| Affected cloud resources | Cloud exposure |
| Affected applications | Business impact |

---

## 13.2 Scope Expansion Indicators

| Indicator | Meaning |
|---|---|
| Same IOC on multiple systems | Widespread activity |
| Shared credentials | Lateral movement |
| Same destination IP | Coordinated campaign |
| Similar authentication anomalies | Account compromise |

---

## 13.3 Scope Tracking Table

| Asset | User | Compromised? | Severity | Evidence Ref |
|---|---|---|---|---|
| | | | | |

---

# 14. Phase 8 – Escalation and Containment

---

## 14.1 Escalation Matrix

| Condition | Escalation Target |
|---|---|
| Advanced malware activity | L3 |
| Active ransomware | IR Team |
| Data exfiltration confirmed | IR Team |
| Domain compromise | IR Team |
| Cloud root compromise | IR Team |
| Credential dumping | L3 / IR Team |

---

## 14.2 Standard Containment Recommendations

| Threat Type | Recommended Action |
|---|---|
| Beaconing | Block destination IP |
| Credential abuse | Reset credentials |
| Malware spread | Isolate hosts |
| Exfiltration | Block outbound traffic |
| Suspicious VPN access | Disable account |

---

## 14.3 Emergency Escalation Triggers

Immediate escalation required if:

- Active ransomware spreading
- Ongoing exfiltration detected
- Domain admin compromise confirmed
- EDR visibility lost
- Multiple business-critical systems impacted

---

# 15. Phase 9 – Documentation Standards

All SIEM investigations must include:

- Investigation summary
- UTC timeline
- Correlated events
- IOC analysis
- Scope analysis
- Evidence references
- Escalation decisions
- Containment recommendations

---

## 15.1 Investigation Quality Example

GOOD:
“SIEM correlation identified impossible travel login for user jsmith followed by successful VPN authentication from foreign IP. EDR telemetry confirmed PowerShell execution on FIN-WS-12 within 5 minutes of VPN login. DNS logs showed beaconing to known malicious domain.”

BAD:
“User login looked suspicious.”

---

# 16. Evidence Preservation Requirements

Preserve:

| Evidence Type | Source |
|---|---|
| SIEM search results | SIEM export |
| Authentication logs | AD/IdP |
| Firewall logs | Network platform |
| DNS logs | DNS infrastructure |
| Proxy logs | Proxy platform |
| Correlation screenshots | SIEM evidence |

Reference:
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md`

---

# 17. MSSP-Specific SIEM Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain tenant separation | Prevent data leakage |
| Follow client-specific SLA | Contract compliance |
| Use client escalation matrix | Proper notification |
| Restrict analyst visibility | Compliance |
| Preserve client evidence separately | Audit readiness |

---

# 18. Common SIEM Investigation Mistakes

| Mistake | Operational Risk |
|---|---|
| Investigating only one log source | Partial visibility |
| Weak timeline reconstruction | Missed attack chain |
| Ignoring cloud logs | Incomplete scope |
| No IOC enrichment | Missed threat validation |
| Delayed escalation | Increased attacker dwell time |
| Poor documentation | Audit failure |

---

# 19. Related Documents

| Document | Path |
|---|---|
| L2 Investigation SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md` |
| L2 EDR Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-EDR-Deep-Investigation.md` |
| L2 Network Forensics SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Network-Forensics-SOP.md` |
| L2 Threat Hunting Procedures | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md` |
| SIEM Query Library | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md` |
| SIEM Alert Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md` |

---

# 20. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / L2 Operations Lead | Initial version |

---

# 21. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**