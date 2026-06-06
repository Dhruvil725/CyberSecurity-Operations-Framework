# SOP: L2 Log Analysis Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L2 Log Analysis Procedures |
| Document ID | SOC-L2-SOP-008 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / SOC Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the methodology, workflows, operational standards, and analytical procedures for Level 2 (L2) security log analysis activities.

Security log analysis is one of the most critical functions within a Security Operations Center (SOC) because logs provide:

- Evidence of attacker activity
- Timeline reconstruction capability
- Visibility into system behavior
- Authentication tracking
- Network activity records
- Application-level events
- Cloud activity visibility
- Compliance evidence

L2 analysts use logs to:

- Validate security incidents
- Correlate attacker behavior
- Detect compromise indicators
- Investigate lateral movement
- Identify persistence mechanisms
- Detect exfiltration attempts
- Support forensic investigations
- Assist escalation decisions

Improper log analysis may result in:

- Missed attacker activity
- Incorrect incident severity
- Incomplete investigations
- Delayed escalation
- Loss of forensic evidence
- Regulatory non-compliance
- False conclusions

This SOP ensures:

- Standardized log analysis methodology
- Accurate event correlation
- Proper evidence handling
- Reliable timeline reconstruction
- Consistent investigation documentation
- Audit-ready investigative processes

---

# 3. Scope

This SOP applies to all L2 investigations involving security log analysis.

---

## 3.1 Log Sources Covered

| Log Source | Examples |
|---|---|
| Authentication logs | Active Directory, Entra ID |
| Endpoint logs | Windows Event Logs |
| SIEM logs | Correlated events |
| Firewall logs | Network traffic |
| VPN logs | Remote access |
| Proxy logs | Internet access |
| DNS logs | Resolution activity |
| Cloud logs | AWS CloudTrail |
| EDR logs | Endpoint telemetry |
| Email logs | Exchange, M365 |

---

## 3.2 Incident Types Covered

| Incident Type | Example |
|---|---|
| Credential attacks | Password spray |
| Malware execution | Suspicious PowerShell |
| Insider threats | Unauthorized access |
| Data exfiltration | Large transfers |
| Ransomware | Encryption events |
| Lateral movement | RDP spread |
| Cloud compromise | IAM abuse |
| APT activity | Multi-stage attacks |

---

# 4. Log Analysis Philosophy (IMPORTANT)

Logs must be analyzed as part of a broader attack narrative.

The objective is not simply identifying isolated events.

The analyst must determine:

- What happened
- When it happened
- How it happened
- Which systems were involved
- Which users were affected
- Whether the attacker remains active
- Whether the compromise spread

Effective log analysis focuses on:

- Correlation
- Sequence
- Context
- Behavior
- Timing
- Relationships between events

---

## 4.1 Common Log Analysis Failures

| Poor Practice | Operational Risk |
|---|---|
| Reviewing isolated events only | Missed attack chain |
| Ignoring historical logs | Missed persistence |
| Weak timestamp analysis | Timeline corruption |
| No cross-source correlation | Incomplete visibility |
| Premature closure | Missed compromise |

---

# 5. L2 Log Analysis Responsibilities

| Responsibility | Description |
|---|---|
| Event analysis | Review suspicious logs |
| Event correlation | Link related events |
| Timeline reconstruction | Sequence attacker activity |
| IOC identification | Detect compromise indicators |
| Scope analysis | Determine affected assets |
| Evidence preservation | Export relevant logs |
| Escalation | Notify L3/IR Team |
| Documentation | Maintain investigation records |

---

# 6. Log Analysis Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Validate Events | Event confirmation |
| Phase 2 | Identify Relevant Logs | Scope definition |
| Phase 3 | Correlate Related Events | Attack chain |
| Phase 4 | Timeline Reconstruction | Chronology |
| Phase 5 | Threat Validation | Incident confirmation |
| Phase 6 | Scope Expansion | Blast radius |
| Phase 7 | Escalation/Containment | Response coordination |
| Phase 8 | Documentation | Investigation record |

---

# 7. Phase 1 – Validate Events

The first objective is determining whether suspicious logs indicate malicious activity.

---

## 7.1 Event Validation Checklist

| Validation Item | Completed |
|---|---|
| Event source validated | ☐ |
| Timestamp verified | ☐ |
| Severity reviewed | ☐ |
| Asset identified | ☐ |
| User context reviewed | ☐ |
| Event frequency checked | ☐ |
| Historical comparison completed | ☐ |
| Related alerts reviewed | ☐ |

---

## 7.2 Event Validation Questions

| Question | Objective |
|---|---|
| Is the event malicious? | Threat confirmation |
| Is this expected behavior? | Baseline comparison |
| Is the event isolated? | Scope analysis |
| Is attacker persistence likely? | Long-term compromise |
| Is escalation required? | Severity validation |

---

## 7.3 High-Risk Event Categories

| Event Type | Risk Level |
|---|---|
| Multiple failed logins | Medium |
| Privileged login anomaly | High |
| PowerShell execution | High |
| New admin account creation | Critical |
| EDR tampering | Critical |
| Large outbound transfer | Critical |
| Domain admin login anomaly | Critical |

---

# 8. Phase 2 – Identify Relevant Logs

The analyst must identify all relevant telemetry sources.

---

## 8.1 Log Source Identification

| Scenario | Required Logs |
|---|---|
| Credential attack | AD, VPN, MFA logs |
| Malware execution | EDR, Windows logs |
| Data exfiltration | Proxy, firewall logs |
| Lateral movement | SMB, RDP logs |
| Cloud compromise | CloudTrail, IAM logs |

---

## 8.2 Log Collection Checklist

| Collection Item | Status |
|---|---|
| Time range identified | ☐ |
| UTC normalization confirmed | ☐ |
| Required log sources available | ☐ |
| Log retention validated | ☐ |
| Evidence export initiated | ☐ |

---

## 8.3 Log Retention Considerations

| Log Type | Minimum Recommended Retention |
|---|---|
| Authentication logs | 90 days |
| Firewall logs | 90 days |
| DNS logs | 30–90 days |
| EDR telemetry | 90 days |
| Cloud audit logs | 180 days |
| SIEM correlation logs | 1 year |

---

# 9. Phase 3 – Correlate Related Events

Event correlation is critical for identifying attacker behavior.

---

## 9.1 Correlation Objectives

| Objective | Purpose |
|---|---|
| Identify attack chain | Threat reconstruction |
| Link affected systems | Scope determination |
| Identify persistence | Long-term compromise |
| Detect lateral movement | Spread analysis |
| Identify exfiltration | Regulatory impact |

---

## 9.2 Correlation Techniques

| Technique | Example |
|---|---|
| IP correlation | Shared attacker IP |
| Username correlation | Shared account abuse |
| Hash correlation | Malware spread |
| Time correlation | Related event timing |
| Hostname correlation | Multi-system compromise |

---

## 9.3 Common Correlation Sources

| Source | Investigation Use |
|---|---|
| SIEM | Centralized correlation |
| EDR | Endpoint behavior |
| DNS | Beaconing analysis |
| Proxy logs | Web activity |
| Firewall logs | Traffic analysis |
| Cloud logs | IAM anomalies |

---

# 10. Phase 4 – Timeline Reconstruction (CRITICAL)

Every major investigation must include a timeline.

---

## 10.1 Timeline Objectives

| Objective | Purpose |
|---|---|
| Identify initial access | Root cause analysis |
| Track attacker movement | Threat analysis |
| Determine persistence timing | Persistence investigation |
| Identify exfiltration activity | Regulatory assessment |

---

## 10.2 Required Timeline Events

| Event Type | Example |
|---|---|
| Initial login | VPN authentication |
| Malware execution | PowerShell launch |
| Privilege escalation | Admin rights granted |
| Lateral movement | RDP activity |
| Exfiltration | Large upload |

---

## 10.3 Timeline Tracking Table

| Timestamp UTC | Event | Source | Severity | Evidence Ref |
|---|---|---|---|---|
| | | | | |

---

# 11. Phase 5 – Threat Validation

Determine whether findings indicate confirmed malicious activity.

---

## 11.1 Threat Validation Criteria

| Validation Type | Example |
|---|---|
| IOC validation | Known malicious IP |
| Behavioral analysis | Credential dumping |
| Threat intelligence | Malware hash match |
| Historical correlation | Repeated activity |
| MITRE mapping | ATT&CK technique |

---

## 11.2 Common Threat Indicators

| Indicator | Meaning |
|---|---|
| Encoded PowerShell | Obfuscation |
| Repeated failed logins | Password spray |
| Unusual VPN geolocation | Account compromise |
| Beaconing traffic | C2 communication |
| New scheduled task | Persistence |

---

## 11.3 Immediate Escalation Conditions

Immediate escalation required if:

| Condition | Escalation Target |
|---|---|
| Domain admin compromise | IR Team |
| Active ransomware | IR Team |
| Data exfiltration confirmed | IR Team |
| Rootkit indicators | L3 |
| Advanced malware | L3 |

---

# 12. Phase 6 – Scope Expansion

Determine the blast radius of the incident.

---

## 12.1 Scope Analysis Areas

| Area | Objective |
|---|---|
| Users affected | Identity impact |
| Systems affected | Infrastructure impact |
| Applications affected | Business impact |
| Cloud resources affected | Cloud exposure |
| Client impact | MSSP exposure |

---

## 12.2 Scope Expansion Indicators

| Indicator | Meaning |
|---|---|
| Same IOC on multiple systems | Malware spread |
| Shared credentials | Account compromise |
| Similar login anomalies | Coordinated attack |
| Shared persistence artifacts | Multi-host compromise |

---

## 12.3 Scope Tracking Table

| Asset | User | IOC Found | Severity | Escalated |
|---|---|---|---|---|
| | | | | |

---

# 13. Phase 7 – Escalation and Containment

---

## 13.1 Escalation Matrix

| Condition | Escalation Target |
|---|---|
| Memory forensics required | L3 |
| Active attacker activity | IR Team |
| Domain compromise | IR Team |
| Data exfiltration | IR Team |
| Cloud root compromise | IR Team |
| Advanced persistence | L3 |

---

## 13.2 Standard Containment Recommendations

| Threat | Recommended Action |
|---|---|
| Credential abuse | Reset passwords |
| Beaconing | Block destination |
| Malware spread | Isolate hosts |
| Data exfiltration | Block outbound transfer |
| Suspicious VPN access | Disable account |

---

## 13.3 Emergency Escalation Conditions

Immediate escalation required if:

- Active exfiltration detected
- Domain-wide compromise observed
- Ransomware spreading
- EDR visibility lost
- Multiple business-critical systems impacted

---

# 14. Phase 8 – Documentation Standards

Every log analysis investigation must include:

- Investigation summary
- Timeline reconstruction
- IOC references
- Correlated events
- Scope analysis
- Escalation actions
- Containment recommendations
- Evidence references

---

## 14.1 Investigation Documentation Example

GOOD:
“Authentication logs identified multiple failed VPN login attempts against user jsmith followed by successful login from foreign IP at 01:12 UTC. EDR telemetry confirmed PowerShell execution on FIN-WS-12 4 minutes later. DNS logs showed beaconing to known malicious domain.”

BAD:
“Suspicious login observed.”

---

# 15. Evidence Preservation Requirements

Preserve:

| Evidence Type | Source |
|---|---|
| SIEM exports | SIEM platform |
| Windows Event Logs | Endpoint |
| Authentication logs | AD/IdP |
| DNS logs | DNS infrastructure |
| Proxy logs | Proxy platform |
| Firewall logs | Firewall platform |

Reference:
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md`

---

# 16. MSSP-Specific Log Analysis Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain tenant segregation | Prevent data leakage |
| Use client-specific retention rules | Compliance |
| Follow client SLA | Contract obligations |
| Preserve client evidence separately | Audit readiness |
| Restrict analyst access | Data protection |

---

# 17. Common Log Analysis Mistakes

| Mistake | Operational Risk |
|---|---|
| Reviewing only one log source | Partial visibility |
| Ignoring historical activity | Missed persistence |
| Weak timeline reconstruction | Investigation gaps |
| No IOC enrichment | Missed threat validation |
| Delayed escalation | Increased attacker dwell time |
| Poor documentation | Audit failure |

---

# 18. Related Documents

| Document | Path |
|---|---|
| L2 Investigation SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md` |
| L2 SIEM Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-SIEM-Deep-Investigation.md` |
| L2 EDR Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-EDR-Deep-Investigation.md` |
| L2 Network Forensics SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Network-Forensics-SOP.md` |
| SIEM Query Library | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |

---

# 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / SOC Operations Lead | Initial version |

---

# 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**