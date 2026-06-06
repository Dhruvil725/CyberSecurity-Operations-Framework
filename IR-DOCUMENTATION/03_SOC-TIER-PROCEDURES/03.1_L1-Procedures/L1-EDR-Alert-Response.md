# SOP: L1 EDR Alert Response Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L1 EDR Alert Response Procedures |
| Document ID | SOC-L1-SOP-007 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Endpoint Security Lead |
| Approved By | SOC Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the process for handling Endpoint Detection and Response (EDR) alerts at the Level 1 (L1) SOC tier.

EDR alerts are among the highest-value alerts within a SOC because they provide:

- Real-time endpoint telemetry
- Process execution visibility
- Behavioral analytics
- Memory-based detection
- Credential theft indicators
- Persistence detection
- Lateral movement evidence
- Malware execution visibility

Unlike traditional signature-based antivirus alerts, EDR alerts often indicate:

- Active attacker behavior
- Hands-on-keyboard activity
- Advanced malware execution
- Living-off-the-land abuse
- Memory injection
- Privilege escalation
- Ransomware execution
- Credential compromise

This SOP ensures:

- Structured EDR alert triage
- Proper process tree analysis
- Correct escalation decisions
- Preservation of endpoint evidence
- Rapid response to active threats
- Consistent handling of high-risk endpoint detections

---

# 3. Scope

Applies to alerts generated from:

- EDR/XDR platforms
- Endpoint behavioral detection systems
- Memory protection engines
- Endpoint exploit prevention systems
- Endpoint anti-malware systems

Applicable systems include:

- Windows endpoints
- Linux servers
- macOS systems
- Cloud workloads
- VDI infrastructure
- MSSP-managed client endpoints

---

# 4. EDR Alert Response Philosophy (IMPORTANT)

EDR alerts frequently represent real attacker behavior rather than generic anomalies.

This is especially true for:

- Memory injection alerts
- Credential dumping alerts
- LOLBin abuse
- PowerShell execution anomalies
- Ransomware behavior
- Lateral movement indicators

L1 analysts must avoid the common mistake of assuming:

“EDR already blocked it, so it’s safe.”

Even blocked activity may indicate:

- Initial compromise attempt
- Active phishing infection
- Insider abuse
- Credential compromise
- Early-stage ransomware
- Advanced attacker reconnaissance

Every EDR alert must therefore be investigated contextually.

---

# 5. EDR Alert Handling Workflow

| Phase | Objective |
|---|---|
| Phase 1 | Alert review and acknowledgement |
| Phase 2 | Process tree analysis |
| Phase 3 | Context and enrichment |
| Phase 4 | Threat classification |
| Phase 5 | Severity assignment |
| Phase 6 | Escalation or containment recommendation |
| Phase 7 | Documentation |

---

# 6. Phase 1 – Alert Review and Acknowledgement

The analyst must begin by reviewing the complete EDR alert context.

---

## 6.1 Required Initial Review Fields

| Field | Example |
|---|---|
| Hostname | FIN-WS-22 |
| Username | j.smith |
| Process name | powershell.exe |
| Parent process | WINWORD.EXE |
| Detection type | Suspicious PowerShell |
| Hash | SHA256 |
| Timestamp | UTC |
| EDR action | Detected / Blocked / Quarantined |

---

## 6.2 Critical Immediate Escalation Alerts

The following EDR detections require immediate escalation:

| Alert Type | Escalation |
|---|---|
| Ransomware behavior | Immediate IR escalation |
| LSASS memory access | L2/L3 |
| Credential dumping | L2/L3 |
| Domain controller compromise | IR Team |
| EDR tampering | L3 |
| Active malware spreading | IR Team |
| Memory injection into system process | L3 |

---

# 7. Phase 2 – Process Tree Analysis (CRITICAL)

Process tree analysis is one of the most important EDR triage skills.

Many attacks become obvious only when parent-child relationships are analyzed.

---

## 7.1 Process Tree Review Requirements

The analyst must identify:

| Item | Purpose |
|---|---|
| Parent process | Execution source |
| Child process | Malicious behavior |
| Command line | Payload visibility |
| User context | Privilege analysis |
| Process path | Masquerading detection |
| Execution timing | Timeline analysis |

---

## 7.2 Suspicious Parent-Child Relationships

| Parent | Child | Risk |
|---|---|---|
| WINWORD.EXE | powershell.exe | High |
| excel.exe | cmd.exe | High |
| outlook.exe | mshta.exe | High |
| browser.exe | powershell.exe | High |
| wscript.exe | rundll32.exe | High |

---

## 7.3 LOLBin Abuse Awareness (IMPORTANT)

Attackers frequently abuse legitimate binaries.

Common LOLBins:

| LOLBin | Typical Abuse |
|---|---|
| powershell.exe | Malware execution |
| certutil.exe | Payload download |
| regsvr32.exe | Script execution |
| mshta.exe | Remote payload execution |
| rundll32.exe | DLL execution |
| wmic.exe | Remote execution |

Do not assume legitimacy because the binary is signed.

---

# 8. Phase 3 – Context and Enrichment

EDR alerts must be enriched with operational context.

---

## 8.1 Required Enrichment

| Enrichment Type | Purpose |
|---|---|
| Asset criticality | Business impact |
| User privilege level | Risk assessment |
| Historical activity | Pattern analysis |
| Threat intelligence | Malware classification |
| Related SIEM alerts | Correlation |
| Network connections | C2 validation |

---

## 8.2 Threat Intelligence Enrichment

Check:

- File hash reputation
- Domain reputation
- IP reputation
- Malware family association
- Sandbox analysis
- Threat actor linkage

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/`

---

## 8.3 Asset Context (IMPORTANT)

The same alert may have different risk levels depending on asset.

Example:

| Asset | Same Alert Risk |
|---|---|
| User workstation | Medium |
| Domain controller | Critical |
| Cloud management server | Critical |
| Production database | Critical |

---

# 9. Phase 4 – Threat Classification

L1 analysts must classify activity appropriately.

---

## 9.1 Threat Categories

| Category | Description |
|---|---|
| Benign | Legitimate activity |
| Suspicious | Requires deeper investigation |
| Malicious | Confirmed attacker activity |
| Critical | Immediate operational risk |

---

## 9.2 Common High-Risk EDR Behaviors

| Behavior | Typical Threat |
|---|---|
| LSASS access | Credential dumping |
| Process injection | Malware |
| PowerShell with Base64 | Obfuscated execution |
| Unsigned driver load | Rootkit |
| Mass file modification | Ransomware |
| New service creation | Persistence |

---

# 10. Phase 5 – Severity Assignment

Severity should reflect:

- Threat confidence
- Endpoint criticality
- Scope
- Privilege level
- Potential impact

---

## 10.1 Severity Examples

| Severity | Example |
|---|---|
| P1 | Active ransomware |
| P1 | Domain admin credential dumping |
| P2 | Suspicious PowerShell execution |
| P2 | Memory injection |
| P3 | Unusual script execution |
| P4 | Informational detection |

---

## 10.2 Severity Escalation Factors

Increase severity if:

- Multiple endpoints affected
- Privileged accounts involved
- Persistence established
- Malware spread detected
- Data staging observed
- Domain controller involved

---

# 11. Phase 6 – Escalation and Response

---

## 11.1 Escalation Conditions

| Condition | Escalate To |
|---|---|
| Ransomware behavior | IR Team |
| Credential dumping | L2/L3 |
| Beaconing confirmed | L2 |
| Persistence creation | L2 |
| EDR tampering | L3 |
| Domain compromise indicators | IR Team |

Reference:
`03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Escalation-Criteria.md`

---

## 11.2 Containment Awareness (IMPORTANT)

L1 analysts must NOT initiate containment unless authorized.

However, L1 analysts should identify when containment may be required.

Examples:

| Behavior | Possible Containment |
|---|---|
| Active ransomware | Endpoint isolation |
| Beaconing malware | Network isolation |
| Credential dumping | Account disablement |
| Worm-like spread | Segment isolation |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Containment-Commands.md`

---

# 12. Memory and Persistence Awareness

Many advanced attacks are memory-resident.

---

## 12.1 Memory-Based Indicators

| Indicator | Risk |
|---|---|
| RWX memory region | Shellcode |
| Injected DLL | Malware |
| Hollowed process | Evasion |
| Unsigned memory module | Malicious injection |

---

## 12.2 Persistence Indicators

| Indicator | Typical Technique |
|---|---|
| New scheduled task | Persistence |
| New service | Malware |
| Registry autorun | Startup persistence |
| Startup folder change | Persistence |

---

# 13. EDR Telemetry Gaps (IMPORTANT)

L1 analysts must identify possible telemetry gaps.

---

## 13.1 Common EDR Visibility Issues

| Issue | Risk |
|---|---|
| Endpoint offline | Visibility loss |
| Sensor disabled | Monitoring gap |
| Telemetry delay | Delayed detection |
| Policy mismatch | Incomplete visibility |

Immediately notify SOC Lead if:
- EDR telemetry missing from critical systems
- Multiple agents disconnect simultaneously
- EDR management console unavailable

---

# 14. MSSP EDR Handling

For MSSP operations:

- Maintain tenant segregation
- Use client-specific severity guidance
- Follow client escalation matrix
- Avoid cross-client evidence exposure
- Track client-specific EDR policy gaps

---

# 15. Common EDR Handling Mistakes

| Mistake | Risk |
|---|---|
| Ignoring process trees | Missed attack chain |
| Assuming blocked means safe | Missed compromise |
| Ignoring LOLBins | Missed advanced attacks |
| Closing detections too quickly | False negatives |
| Missing persistence indicators | Reinfection |

---

## 16. Related Documents

| Document | Path |
|---|---|
| L1 Alert Handling SOP | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md` |
| L1 Escalation Criteria | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Escalation-Criteria.md` |
| EDR Investigation Queries | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Investigation-Queries.md` |
| EDR Containment Commands | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Containment-Commands.md` |
| L1 Ticket SOP | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Ticket-Creation-SOP.md` |

---

## 17. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / Endpoint Security Lead | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**