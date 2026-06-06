# SOP: L2 EDR Deep Investigation Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L2 EDR Deep Investigation Procedures |
| Document ID | SOC-L2-SOP-004 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / L2 Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the operational methodology, workflows, analytical requirements, and escalation procedures for Level 2 (L2) Endpoint Detection and Response (EDR) investigations.

EDR/XDR platforms provide deep endpoint telemetry and behavioral visibility that enable analysts to investigate attacker activity beyond traditional signature-based detection.

The purpose of this SOP is to ensure L2 analysts perform:

- Consistent endpoint investigations
- Accurate process analysis
- Effective malware investigation
- Reliable lateral movement analysis
- Proper evidence preservation
- Timely escalation to L3 or IR Team
- Audit-ready investigation documentation

This SOP also establishes standardized investigative procedures to support:

- Enterprise SOC operations
- MSSP multi-tenant environments
- Regulatory investigations
- Forensic investigations
- Threat hunting integration
- Incident response escalation

---

# 3. Scope

This SOP applies to all EDR investigations involving:

| Incident Type | Example |
|---|---|
| Malware execution | Trojan, RAT, spyware |
| Ransomware activity | Encryption behavior |
| Credential theft | LSASS access |
| Insider threat | Unauthorized data access |
| Lateral movement | SMB/RDP movement |
| Living-off-the-land attacks | LOLBins |
| PowerShell abuse | Encoded commands |
| Privilege escalation | SYSTEM privilege abuse |
| Cloud workstation compromise | Cloud-connected endpoint |
| Supply chain compromise | Malicious software update |

---

## 3.1 Applicable Platforms

| Platform Type | Examples |
|---|---|
| EDR/XDR Platforms | CrowdStrike, SentinelOne, Defender |
| SIEM Platforms | Splunk, Sentinel, QRadar |
| Threat Intelligence Platforms | MISP, Recorded Future |
| Identity Platforms | Active Directory, Entra ID |
| Cloud Platforms | AWS, Azure, GCP |

---

# 4. EDR Investigation Philosophy (IMPORTANT)

EDR investigation is not simply reviewing alerts.

The primary objective is to reconstruct attacker behavior using endpoint telemetry.

L2 analysts must think in:

- Attack chains
- Process ancestry
- Execution context
- Privilege escalation
- Persistence behavior
- Lateral movement
- Adversary objectives

L2 analysts must avoid:

| Poor Practice | Risk |
|---|---|
| Investigating only the triggered alert | Missed attacker activity |
| Ignoring parent-child processes | Missed execution chain |
| Closing based only on reputation | False negatives |
| Focusing on a single endpoint | Missed spread |
| Ignoring user context | Incomplete investigation |

---

# 5. L2 EDR Analyst Responsibilities

| Responsibility | Description |
|---|---|
| Alert validation | Confirm malicious activity |
| Endpoint investigation | Analyze host behavior |
| Process tree reconstruction | Trace execution flow |
| Threat scoping | Determine blast radius |
| IOC enrichment | Threat intelligence correlation |
| Evidence preservation | Export telemetry and artifacts |
| Escalation | Escalate advanced threats |
| Containment recommendations | Recommend response actions |
| Documentation | Maintain investigation records |

---

# 6. EDR Investigation Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Alert Validation | Threat confirmation |
| Phase 2 | Process Analysis | Execution chain |
| Phase 3 | File Investigation | Malicious artifact analysis |
| Phase 4 | Persistence Analysis | Persistence identification |
| Phase 5 | Credential Abuse Review | Privilege compromise assessment |
| Phase 6 | Network Investigation | C2/lateral movement analysis |
| Phase 7 | Scope Expansion | Blast radius determination |
| Phase 8 | Escalation/Containment | Response coordination |
| Phase 9 | Documentation | Investigation record |

---

# 7. Phase 1 – Alert Validation

The first objective is determining whether the EDR detection represents legitimate malicious activity.

---

## 7.1 Initial Validation Checklist

| Validation Item | Required | Notes |
|---|---|---|
| Alert severity reviewed | ☐ | |
| Endpoint identified | ☐ | |
| User context reviewed | ☐ | |
| MITRE technique reviewed | ☐ | |
| Detection timestamp validated | ☐ | |
| Alert history reviewed | ☐ | |
| Prior alerts on endpoint checked | ☐ | |
| IOC enrichment completed | ☐ | |

---

## 7.2 Validation Questions

| Question | Investigation Purpose |
|---|---|
| Is the execution malicious? | Threat confirmation |
| Was the action user initiated? | Intent analysis |
| Is persistence present? | Long-term compromise |
| Is the attacker active? | Urgency determination |
| Has activity spread? | Scope determination |
| Is data exposure possible? | Regulatory assessment |

---

## 7.3 High-Risk Alert Categories

The following alert types require immediate prioritization:

| Alert Type | Risk Level |
|---|---|
| Credential dumping | Critical |
| Ransomware behavior | Critical |
| Process injection | High |
| Defense evasion | High |
| PowerShell obfuscation | High |
| Privileged account misuse | Critical |
| EDR tampering | Critical |

---

# 8. Phase 2 – Process Execution Investigation

Process analysis is the core investigative activity during EDR investigations.

The objective is to reconstruct the attacker execution chain.

---

# 8.1 Required Process Analysis Areas

| Analysis Area | Objective |
|---|---|
| Parent process | Identify execution source |
| Child processes | Detect spawned activity |
| Command line | Identify obfuscation |
| User context | Determine privilege |
| Execution path | Detect suspicious locations |
| Hash validation | IOC correlation |
| Signature validation | Legitimacy verification |
| Execution timeline | Event sequencing |

---

# 8.2 Suspicious Parent Process Analysis

| Parent Process | Common Abuse |
|---|---|
| WINWORD.EXE | Macro malware |
| EXCEL.EXE | Malicious spreadsheets |
| powershell.exe | Script execution |
| cmd.exe | Shell abuse |
| wscript.exe | VBScript malware |
| rundll32.exe | LOLBin abuse |
| mshta.exe | HTA payload execution |
| regsvr32.exe | Scriptlet execution |

---

## 8.3 Process Chain Investigation Example

| Process Level | Example |
|---|---|
| Initial Process | WINWORD.EXE |
| Spawned Process | powershell.exe |
| Child Process | cmd.exe |
| Payload Process | ransomware.exe |

---

## 8.4 Command-Line Review Requirements

Review command-line arguments for:

| Indicator | Example |
|---|---|
| Base64 encoding | EncodedCommand |
| Download activity | Invoke-WebRequest |
| Script execution | IEX |
| LOLBin abuse | rundll32 |
| Credential dumping | sekurlsa |
| Hidden execution | -WindowStyle Hidden |

---

# 9. Phase 3 – File Activity Investigation

Investigate suspicious file activity associated with the endpoint.

---

## 9.1 File Analysis Workflow

| Step | Objective |
|---|---|
| Extract file hash | IOC validation |
| Verify reputation | Threat intelligence |
| Check digital signature | Legitimacy review |
| Analyze file path | Malware staging detection |
| Review execution history | Persistence analysis |
| Determine prevalence | Scope analysis |

---

## 9.2 High-Risk File Indicators

| Indicator | Risk |
|---|---|
| Unsigned executable | Unknown origin |
| Execution from TEMP | Malware staging |
| Newly created executable | Payload delivery |
| Renamed system binary | Evasion |
| High entropy file | Packed malware |
| Multiple AV detections | Known malware |

---

## 9.3 Suspicious File Locations

| Location | Investigation Concern |
|---|---|
| AppData\Roaming | User persistence |
| Temp folders | Malware execution |
| ProgramData | Hidden payloads |
| Startup folder | Auto-start persistence |
| Public folders | Shared payload distribution |

---

# 10. Phase 4 – Persistence Investigation (CRITICAL)

Persistence analysis determines whether attackers established long-term access.

---

## 10.1 Common Persistence Mechanisms

| Mechanism | Example |
|---|---|
| Registry Run Keys | Auto-start execution |
| Scheduled Tasks | Timed malware launch |
| Windows Services | Persistent services |
| Startup Folder | Login persistence |
| WMI Event Subscription | Fileless persistence |
| Browser Extensions | Credential theft |
| DLL Hijacking | Execution hijack |

---

## 10.2 Persistence Investigation Checklist

| Validation Item | Completed |
|---|---|
| Registry persistence reviewed | ☐ |
| Scheduled tasks reviewed | ☐ |
| Services reviewed | ☐ |
| Startup entries reviewed | ☐ |
| WMI subscriptions reviewed | ☐ |
| Browser extensions reviewed | ☐ |

---

## 10.3 Critical Persistence Escalation Triggers

Escalate immediately if:

| Condition | Escalation Reason |
|---|---|
| Rootkit indicators detected | Advanced compromise |
| EDR tampering identified | Monitoring impairment |
| Domain controller persistence | Enterprise-wide risk |
| Fileless persistence identified | Advanced attacker capability |
| Multi-host persistence observed | Widespread compromise |

---

# 11. Phase 5 – Credential Abuse Investigation

Credential compromise investigation is a high-priority activity.

---

## 11.1 Credential Theft Indicators

| Indicator | Meaning |
|---|---|
| LSASS access | Credential dumping |
| Mimikatz behavior | Password extraction |
| Pass-the-hash activity | Lateral movement |
| Kerberoasting activity | Service account abuse |
| Token impersonation | Privilege escalation |

---

## 11.2 Credential Investigation Workflow

| Step | Objective |
|---|---|
| Identify affected account | User impact |
| Determine privilege level | Risk assessment |
| Review authentication logs | Abuse validation |
| Check lateral movement | Scope expansion |
| Review MFA logs | Authentication bypass |

---

## 11.3 Immediate Escalation Conditions

| Condition | Escalation Target |
|---|---|
| Domain admin compromise | IR Team |
| Cloud admin token exposure | IR Team |
| Service account compromise | IR Team |
| Privileged lateral movement | IR Team |
| Credential dumping on servers | L3 / IR Team |

---

# 12. Phase 6 – Network Activity Investigation

Network analysis helps identify command-and-control (C2), lateral movement, and exfiltration activity.

---

## 12.1 Required Network Analysis Areas

| Area | Objective |
|---|---|
| External connections | C2 detection |
| Internal SMB traffic | Lateral movement |
| DNS requests | Beaconing analysis |
| RDP activity | Remote access review |
| Outbound traffic volume | Exfiltration review |

---

## 12.2 High-Risk Network Indicators

| Indicator | Meaning |
|---|---|
| Beaconing intervals | C2 communication |
| TOR connectivity | Anonymization |
| Rare geolocation | Suspicious connection |
| Large outbound uploads | Data exfiltration |
| Internal RDP spread | Lateral movement |

---

## 12.3 Required Correlation Sources

Correlate EDR telemetry with:

| Source | Purpose |
|---|---|
| Firewall logs | Traffic validation |
| DNS logs | Beacon analysis |
| Proxy logs | Web activity |
| SIEM events | Event correlation |
| NetFlow records | Traffic scope |

Reference:
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Network-Forensics-SOP.md`

---

# 13. Phase 7 – Scope Expansion and Blast Radius Analysis

The analyst must determine how far the compromise spread.

---

## 13.1 Scope Expansion Indicators

| Indicator | Meaning |
|---|---|
| Same hash across systems | Malware propagation |
| Shared credentials | Account compromise |
| Common persistence artifacts | Coordinated attack |
| Similar network behavior | Campaign activity |
| Shared scheduled task | Automated spread |

---

## 13.2 Endpoint Scope Table

| Hostname | User | Severity | Compromised? | Isolation Status | Evidence Ref |
|---|---|---|---|---|---|
| | | | | | |

---

# 14. Phase 8 – Containment Recommendations

L2 analysts recommend containment actions based on investigation findings.

---

## 14.1 Standard Containment Recommendations

| Threat Type | Recommended Action |
|---|---|
| Malware execution | Endpoint isolation |
| Active beaconing | Block destination IP |
| Credential theft | Reset credentials |
| Ransomware activity | Network segmentation |
| Lateral movement | Disable compromised account |

---

## 14.2 Emergency Containment Triggers

Immediate containment recommendation required if:

- Active ransomware encryption observed
- Data exfiltration ongoing
- Domain compromise confirmed
- EDR disabled or tampered
- Widespread lateral movement active

---

# 15. Phase 9 – Escalation Procedures

---

## 15.1 Escalation Matrix

| Condition | Escalation Target |
|---|---|
| Memory forensics required | L3 |
| Rootkit indicators | L3 |
| Active ransomware | IR Team |
| Data exfiltration confirmed | IR Team |
| Cloud admin compromise | IR Team |
| Advanced malware analysis | L3 |

---

## 15.2 Escalation Package Requirements

Every escalation must include:

| Required Item | Status |
|---|---|
| Incident summary | ☐ |
| Timeline | ☐ |
| Process tree | ☐ |
| Evidence references | ☐ |
| IOC list | ☐ |
| Scope assessment | ☐ |
| Containment actions | ☐ |

---

# 16. Investigation Documentation Standards

All investigations must include:

- UTC timeline
- Process tree screenshots/exports
- IOC references
- User context
- Scope analysis
- Evidence references
- Escalation decisions
- Containment recommendations

---

## 16.1 Documentation Quality Example

GOOD:
“EDR telemetry confirmed WINWORD.EXE spawned powershell.exe with Base64-encoded command at 03:14 UTC. powershell.exe downloaded payload from malicious domain and created scheduled task ‘UpdaterService’. Additional beaconing observed to 185.x.x.x every 60 seconds.”

BAD:
“PowerShell looks suspicious.”

---

# 17. MSSP-Specific EDR Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain tenant segregation | Prevent data leakage |
| Follow client SLA | Contract compliance |
| Use client escalation matrix | Proper notification |
| Restrict telemetry visibility | Data protection |
| Preserve client evidence separately | Compliance |

---

# 18. Common L2 EDR Investigation Mistakes

| Mistake | Operational Risk |
|---|---|
| Ignoring parent process | Missed attack origin |
| Focusing only on hash reputation | Missed behavior |
| No lateral movement review | Incomplete scope |
| Delayed escalation | Increased attacker dwell time |
| Weak evidence preservation | Forensic gaps |
| No persistence review | Reinfection risk |

---

# 19. Related Documents

| Document | Path |
|---|---|
| L2 Investigation SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md` |
| L2 SIEM Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-SIEM-Deep-Investigation.md` |
| L2 Network Forensics SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Network-Forensics-SOP.md` |
| L2 Threat Hunting Procedures | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md` |
| L2 Evidence Handling SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md` |
| EDR Investigation Queries | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Investigation-Queries.md` |

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