# SOP: L2 Network Forensics Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L2 Network Forensics Procedures |
| Document ID | SOC-L2-SOP-007 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Network Security Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the methodology, workflows, operational standards, and evidence handling requirements for Level 2 (L2) network forensic investigations.

Network forensics is a critical capability used to:

- Identify attacker communication
- Investigate lateral movement
- Detect command-and-control (C2) activity
- Analyze suspicious traffic
- Investigate exfiltration attempts
- Validate network compromise
- Reconstruct attacker activity timelines
- Support containment and escalation decisions

Unlike endpoint-only investigations, network forensics provides visibility into:

- Internal east-west traffic
- External communications
- DNS activity
- VPN activity
- Proxy traffic
- Beaconing behavior
- Data transfer patterns

Improper network investigation may result in:

- Missed active attacker communication
- Failure to detect lateral movement
- Incomplete incident scoping
- Delayed containment
- Missed exfiltration activity
- Inaccurate incident severity classification

This SOP ensures:

- Standardized network investigations
- Consistent traffic analysis
- Proper forensic evidence handling
- Accurate timeline reconstruction
- Effective escalation procedures
- Audit-ready documentation

---

# 3. Scope

This SOP applies to network forensic investigations involving:

| Incident Type | Example |
|---|---|
| Malware communication | C2 traffic |
| Data exfiltration | Large outbound uploads |
| Credential attacks | Lateral authentication traffic |
| Insider threats | Unauthorized transfers |
| Ransomware | SMB propagation |
| Cloud compromise | Suspicious API traffic |
| DNS tunneling | Data concealment |
| Beaconing | Periodic communication |
| VPN compromise | Unauthorized remote access |
| APT activity | Multi-stage communications |

---

## 3.1 Applicable Data Sources

| Source Type | Examples |
|---|---|
| Firewall logs | Palo Alto, Fortinet |
| IDS/IPS logs | Snort, Suricata |
| DNS logs | Internal DNS |
| NetFlow/sFlow | Network collectors |
| Packet captures | PCAP files |
| Proxy logs | Zscaler, Bluecoat |
| VPN logs | Remote access systems |
| Cloud network logs | VPC Flow Logs |

---

# 4. Network Forensics Philosophy (IMPORTANT)

Network forensics focuses on behavior, communication patterns, and attacker movement.

The objective is not simply reviewing firewall alerts.

The analyst must determine:

- Who communicated
- What communicated
- When communication occurred
- Whether traffic was malicious
- Whether data left the environment
- Whether lateral movement occurred
- Whether attacker infrastructure exists

Network investigations must focus on:

- Patterns
- Timing
- Frequency
- Protocols
- Traffic direction
- Behavioral anomalies

---

## 4.1 Common Investigation Failures

| Poor Practice | Operational Risk |
|---|---|
| Reviewing only blocked traffic | Missed successful attacks |
| Ignoring DNS activity | Missed beaconing |
| No lateral movement review | Incomplete scope |
| Weak timeline analysis | Missed attack progression |
| No traffic baselining | False assumptions |

---

# 5. L2 Network Forensics Responsibilities

| Responsibility | Description |
|---|---|
| Traffic analysis | Investigate network activity |
| PCAP review | Analyze packet captures |
| Beaconing analysis | Detect C2 communication |
| Lateral movement analysis | Identify internal spread |
| Exfiltration investigation | Detect data theft |
| IOC correlation | Threat validation |
| Evidence preservation | Preserve network artifacts |
| Escalation | Escalate advanced threats |

---

# 6. Network Forensics Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Validate Alert/Incident | Threat confirmation |
| Phase 2 | Collect Network Evidence | Traffic visibility |
| Phase 3 | Analyze Communication Patterns | Behavioral analysis |
| Phase 4 | Investigate Lateral Movement | Internal spread analysis |
| Phase 5 | Investigate Exfiltration | Data theft validation |
| Phase 6 | Correlate Threat Intelligence | IOC enrichment |
| Phase 7 | Scope Related Activity | Blast radius |
| Phase 8 | Escalation/Containment | Incident coordination |
| Phase 9 | Documentation | Investigation report |

---

# 7. Phase 1 – Validate Alert or Incident

The first objective is validating whether suspicious traffic represents malicious activity.

---

## 7.1 Initial Validation Checklist

| Validation Item | Completed |
|---|---|
| Alert severity reviewed | ☐ |
| Source IP identified | ☐ |
| Destination IP identified | ☐ |
| Protocol identified | ☐ |
| Asset criticality reviewed | ☐ |
| Traffic timestamps validated | ☐ |
| Historical activity reviewed | ☐ |
| Related alerts reviewed | ☐ |

---

## 7.2 Initial Investigation Questions

| Question | Objective |
|---|---|
| Is communication malicious? | Threat validation |
| Is communication ongoing? | Urgency assessment |
| Is traffic internal or external? | Scope analysis |
| Is this normal behavior? | Baseline comparison |
| Is data exposure possible? | Regulatory assessment |

---

## 7.3 High-Risk Network Indicators

| Indicator | Risk |
|---|---|
| Repeated outbound beaconing | Active C2 |
| TOR traffic | Anonymization |
| Large outbound uploads | Exfiltration |
| SMB scanning | Lateral movement |
| DNS tunneling | Data concealment |
| VPN login anomalies | Remote compromise |

---

# 8. Phase 2 – Collect Network Evidence

Network evidence must be preserved immediately when malicious activity is suspected.

---

## 8.1 Required Network Evidence

| Evidence Type | Purpose |
|---|---|
| Firewall logs | Traffic validation |
| DNS logs | Domain analysis |
| NetFlow records | Traffic pattern analysis |
| Packet captures | Deep forensic analysis |
| Proxy logs | Web traffic review |
| VPN logs | Remote access investigation |

---

## 8.2 Evidence Collection Requirements

| Requirement | Standard |
|---|---|
| Preserve UTC timestamps | Timeline accuracy |
| Export original log format | Evidence integrity |
| Preserve raw PCAPs | Forensic analysis |
| Hash exported files | Integrity verification |
| Document collection time | Chain-of-custody |

Reference:
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md`

---

## 8.3 Volatile Evidence Priority

Collect first:

1. Active connections
2. Current firewall sessions
3. DNS cache records
4. VPN session data
5. Active NetFlow records

---

# 9. Phase 3 – Analyze Communication Patterns

The analyst must determine whether network behavior indicates malicious activity.

---

## 9.1 Communication Analysis Areas

| Area | Objective |
|---|---|
| Source-destination mapping | Traffic relationships |
| Frequency analysis | Beacon detection |
| Protocol analysis | Abuse detection |
| Port usage analysis | Service misuse |
| Data volume review | Exfiltration analysis |

---

## 9.2 Beaconing Detection Indicators

| Indicator | Meaning |
|---|---|
| Regular interval traffic | Automated beacon |
| Consistent packet size | C2 heartbeat |
| Long-duration sessions | Persistent connection |
| Rare external destinations | Suspicious infrastructure |

---

## 9.3 Suspicious Protocol Usage

| Protocol | Common Abuse |
|---|---|
| DNS | Tunneling |
| SMB | Lateral movement |
| RDP | Unauthorized access |
| HTTPS | Encrypted C2 |
| FTP/SFTP | Data exfiltration |

---

## 9.4 Communication Timeline Table

| Timestamp UTC | Source IP | Destination IP | Protocol | Action |
|---|---|---|---|---|
| | | | | |

---

# 10. Phase 4 – Lateral Movement Investigation

Lateral movement analysis identifies internal attacker spread.

---

## 10.1 Lateral Movement Indicators

| Indicator | Meaning |
|---|---|
| SMB connections to multiple hosts | Internal spread |
| RDP activity across segments | Unauthorized movement |
| PsExec traffic | Remote execution |
| WMI traffic anomalies | Remote management abuse |
| Admin share access | Privilege abuse |

---

## 10.2 Internal Spread Investigation Workflow

| Step | Objective |
|---|---|
| Identify source host | Patient zero analysis |
| Map destination systems | Scope determination |
| Review authentication logs | Credential abuse |
| Correlate EDR telemetry | Endpoint validation |
| Identify persistence | Ongoing compromise |

---

## 10.3 Immediate Escalation Conditions

Escalate immediately if:

| Condition | Escalation Reason |
|---|---|
| Domain-wide lateral movement | Enterprise compromise |
| Privileged account spread | Critical risk |
| Ransomware propagation | Business disruption |
| Multiple VLANs affected | Widespread compromise |

---

# 11. Phase 5 – Data Exfiltration Investigation

Exfiltration analysis is critical for regulatory and legal obligations.

---

## 11.1 Exfiltration Indicators

| Indicator | Meaning |
|---|---|
| Large outbound transfers | Possible data theft |
| Uploads to rare destinations | Suspicious activity |
| Encrypted outbound traffic spikes | Concealed transfer |
| Cloud storage uploads | Data staging |
| DNS tunneling | Stealth exfiltration |

---

## 11.2 Exfiltration Investigation Checklist

| Validation Item | Completed |
|---|---|
| Data volume analyzed | ☐ |
| Destination reviewed | ☐ |
| Transfer timing reviewed | ☐ |
| User context analyzed | ☐ |
| Sensitive assets involved | ☐ |
| Regulatory impact assessed | ☐ |

---

## 11.3 Regulatory Escalation Triggers

Immediate escalation required if:

| Condition | Escalation Target |
|---|---|
| PII exposure suspected | Legal / Compliance |
| Financial data exposure | IR Team |
| Client data transferred | Executive Management |
| Regulated systems affected | Compliance Team |

---

# 12. Phase 6 – Threat Intelligence Correlation

Threat intelligence enrichment validates suspicious infrastructure.

---

## 12.1 IOC Correlation Areas

| IOC Type | Example |
|---|---|
| IP address | Known C2 |
| Domain | Malicious infrastructure |
| URL | Payload delivery |
| ASN | Threat hosting provider |
| SSL certificate | Infrastructure reuse |

---

## 12.2 IOC Validation Table

| IOC | IOC Type | Reputation | Source | Action Taken |
|---|---|---|---|---|
| | | | | |

---

# 13. Phase 7 – Scope Related Activity

Determine the full impact of suspicious communication.

---

## 13.1 Scope Expansion Indicators

| Indicator | Meaning |
|---|---|
| Same destination across hosts | Coordinated compromise |
| Similar beaconing intervals | Shared malware |
| Shared user accounts | Credential abuse |
| Shared persistence indicators | Multi-host compromise |

---

## 13.2 Scope Tracking Table

| Host | User | IOC Detected | Severity | Escalated |
|---|---|---|---|---|
| | | | | |

---

# 14. Phase 8 – Escalation and Containment

---

## 14.1 Escalation Matrix

| Condition | Escalation Target |
|---|---|
| Active C2 communication | IR Team |
| Data exfiltration confirmed | IR Team |
| DNS tunneling detected | L3 |
| Multi-host lateral movement | IR Team |
| Advanced network evasion | L3 |

---

## 14.2 Standard Containment Recommendations

| Threat | Recommended Action |
|---|---|
| C2 communication | Block destination IP/domain |
| Exfiltration | Block outbound traffic |
| Lateral movement | Segment isolation |
| DNS tunneling | Block DNS requests |
| Unauthorized VPN access | Disable account/session |

---

## 14.3 Emergency Escalation Conditions

Immediate escalation required if:

- Active exfiltration ongoing
- Widespread lateral movement detected
- Critical systems compromised
- Ransomware propagation active
- Regulatory exposure likely

---

# 15. Phase 9 – Documentation Standards

Every network forensic investigation must include:

- UTC timeline
- Source and destination mapping
- IOC analysis
- Scope analysis
- Exfiltration findings
- Correlated telemetry
- Escalation decisions
- Containment recommendations

---

## 15.1 Investigation Quality Example

GOOD:
“NetFlow analysis identified repeated HTTPS beaconing from FIN-WS-12 to malicious external IP every 60 seconds beginning at 02:14 UTC. DNS logs confirmed repeated resolution attempts to known malicious domain. EDR telemetry correlated PowerShell execution 3 minutes before beacon initiation.”

BAD:
“Suspicious traffic detected.”

---

# 16. Evidence Preservation Requirements

Preserve:

| Evidence Type | Source |
|---|---|
| Firewall exports | Firewall platform |
| NetFlow records | Flow collector |
| DNS logs | DNS server |
| PCAP files | Packet capture |
| Proxy logs | Proxy solution |
| VPN logs | VPN infrastructure |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Network-Evidence-SOP.md`

---

# 17. MSSP-Specific Network Investigation Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain client traffic segregation | Prevent data leakage |
| Follow client escalation matrix | SLA compliance |
| Restrict tenant visibility | Compliance |
| Preserve client evidence separately | Audit readiness |
| Follow client retention requirements | Regulatory compliance |

---

# 18. Common Network Forensics Mistakes

| Mistake | Operational Risk |
|---|---|
| Ignoring DNS activity | Missed tunneling |
| No lateral movement review | Incomplete scope |
| Weak timeline reconstruction | Missed progression |
| No IOC enrichment | Missed threat validation |
| Delayed escalation | Increased attacker dwell time |
| Poor evidence preservation | Forensic gaps |

---

# 19. Related Documents

| Document | Path |
|---|---|
| L2 Investigation SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md` |
| L2 SIEM Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-SIEM-Deep-Investigation.md` |
| L2 EDR Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-EDR-Deep-Investigation.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |
| IDS/IPS Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/IDS-IPS-Tuning-Guide.md` |
| Evidence Handling SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md` |

---

# 20. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / Network Security Lead | Initial version |

---

# 21. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**