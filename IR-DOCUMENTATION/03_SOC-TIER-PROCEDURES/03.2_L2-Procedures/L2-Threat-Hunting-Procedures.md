# SOP: L2 Threat Hunting Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L2 Threat Hunting Procedures |
| Document ID | SOC-L2-SOP-006 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Threat Hunting Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the methodology, workflows, operational standards, and documentation requirements for Level 2 (L2) proactive threat hunting activities.

Threat hunting is a proactive cybersecurity activity focused on identifying:

- Undetected attacker activity
- Hidden persistence mechanisms
- Malicious behaviors
- Advanced threats bypassing controls
- Credential abuse
- Lateral movement
- Insider threats
- Early-stage compromise indicators

Unlike reactive alert investigation, threat hunting assumes that some malicious activity may already exist inside the environment without triggering alerts.

The objectives of threat hunting are to:

- Identify threats before major impact occurs
- Reduce attacker dwell time
- Improve detection capability
- Discover control gaps
- Validate defensive visibility
- Enhance SOC maturity
- Support continuous security improvement

This SOP ensures:

- Consistent hunting methodology
- Repeatable investigative processes
- Structured hypothesis-driven hunting
- Proper evidence preservation
- Accurate documentation
- Effective escalation procedures

---

# 3. Scope

This SOP applies to proactive hunting activities involving:

| Threat Category | Examples |
|---|---|
| Malware activity | Trojans, RATs |
| Credential abuse | Password spraying |
| Persistence mechanisms | Scheduled tasks |
| Insider threats | Unauthorized access |
| Ransomware precursors | Enumeration behavior |
| Lateral movement | RDP/SMB movement |
| Cloud compromise | IAM abuse |
| Living-off-the-land attacks | LOLBins |
| APT activity | Multi-stage operations |
| Data exfiltration | Unusual outbound traffic |

---

## 3.1 Hunting Data Sources

| Data Source | Purpose |
|---|---|
| SIEM logs | Event correlation |
| EDR telemetry | Endpoint behavior |
| DNS logs | Beaconing analysis |
| Firewall logs | Traffic investigation |
| Proxy logs | Web activity |
| Cloud audit logs | Cloud threat hunting |
| Identity logs | Authentication analysis |
| Threat intelligence | IOC/TTP enrichment |

---

# 4. Threat Hunting Philosophy (IMPORTANT)

Threat hunting is hypothesis-driven investigation.

The objective is not to search randomly for anomalies.

The hunter must:

- Develop a threat hypothesis
- Use telemetry to validate/refute the hypothesis
- Investigate suspicious patterns
- Correlate findings across systems
- Determine attacker intent
- Identify hidden compromise indicators

Threat hunting focuses on:
- Behaviors
- Patterns
- Tactics
- Techniques
- Operational anomalies

Threat hunting is NOT:
- Alert triage
- Basic IOC searching only
- Compliance reporting
- Passive monitoring

---

## 4.1 Common Threat Hunting Failures

| Poor Practice | Operational Risk |
|---|---|
| Hunting without hypothesis | Ineffective investigation |
| Hunting only known IOCs | Missed unknown threats |
| Ignoring low-volume anomalies | Missed stealth attackers |
| No documentation | Lost findings |
| Weak scope expansion | Incomplete analysis |

---

# 5. L2 Threat Hunting Responsibilities

| Responsibility | Description |
|---|---|
| Develop hunting hypotheses | Threat-based investigation |
| Perform telemetry analysis | Multi-source analysis |
| Investigate suspicious behavior | Threat validation |
| Correlate findings | Cross-platform investigation |
| Identify hidden threats | Undetected compromise |
| Preserve evidence | Artifact collection |
| Escalate findings | Notify L3/IR Team |
| Document hunts | Audit-ready reporting |

---

# 6. Threat Hunting Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Define Hunt Hypothesis | Hunting objective |
| Phase 2 | Identify Data Sources | Telemetry scope |
| Phase 3 | Execute Hunt Queries | Findings |
| Phase 4 | Analyze Results | Threat validation |
| Phase 5 | Scope Related Activity | Blast radius |
| Phase 6 | Escalate Findings | Incident escalation |
| Phase 7 | Improve Detection | Detection enhancement |
| Phase 8 | Document Hunt | Hunt report |

---

# 7. Phase 1 – Define Hunt Hypothesis

Every hunt must begin with a defined hypothesis.

---

## 7.1 Hunt Hypothesis Examples

| Hypothesis | Threat Scenario |
|---|---|
| Attackers may be abusing PowerShell | Fileless malware |
| Dormant accounts may be compromised | Account takeover |
| Beaconing traffic may exist | C2 communication |
| Service accounts may be abused | Privilege misuse |
| LOLBins may bypass controls | Defense evasion |

---

## 7.2 Hunt Planning Checklist

| Planning Item | Completed |
|---|---|
| Threat hypothesis defined | ☐ |
| Scope identified | ☐ |
| Data sources confirmed | ☐ |
| Hunt objectives documented | ☐ |
| IOC/TTP references identified | ☐ |
| Expected behaviors documented | ☐ |

---

## 7.3 Hunt Prioritization Criteria

| Priority | Example |
|---|---|
| Critical | Domain compromise indicators |
| High | Credential dumping behavior |
| Medium | Suspicious PowerShell activity |
| Low | Rare application execution |

---

# 8. Phase 2 – Identify Data Sources

Threat hunting requires multiple telemetry sources.

---

## 8.1 Primary Hunting Sources

| Source | Hunting Purpose |
|---|---|
| EDR telemetry | Endpoint behaviors |
| SIEM correlation | Event aggregation |
| DNS logs | Beacon detection |
| Firewall logs | Network anomalies |
| Authentication logs | Account abuse |
| Cloud logs | IAM anomalies |

---

## 8.2 Threat Hunting Visibility Validation

Before hunting:

| Validation Item | Status |
|---|---|
| Logs available | ☐ |
| Time synchronization confirmed | ☐ |
| Retention period validated | ☐ |
| Required integrations operational | ☐ |
| EDR coverage validated | ☐ |

---

# 9. Phase 3 – Execute Hunt Queries

Hunting queries are used to identify suspicious behavior patterns.

---

## 9.1 Common Hunt Categories

| Hunt Category | Objective |
|---|---|
| PowerShell abuse | Detect script attacks |
| LOLBin abuse | Detect native tool misuse |
| Rare process execution | Detect anomalies |
| Beaconing detection | Identify C2 |
| Lateral movement | Detect internal spread |
| Credential abuse | Detect account compromise |

---

## 9.2 PowerShell Hunting Examples

Investigate:

| Indicator | Risk |
|---|---|
| Encoded commands | Obfuscation |
| DownloadString usage | Payload delivery |
| Hidden execution | Stealth execution |
| Base64 content | Concealment |
| AMSI bypass attempts | Defense evasion |

---

## 9.3 LOLBin Hunting Targets

| LOLBin | Common Abuse |
|---|---|
| rundll32.exe | Payload execution |
| regsvr32.exe | Script execution |
| mshta.exe | HTA malware |
| certutil.exe | File download |
| bitsadmin.exe | Payload transfer |

---

## 9.4 Beaconing Detection Indicators

| Indicator | Meaning |
|---|---|
| Regular interval traffic | Automated beacon |
| Small outbound packets | Heartbeat traffic |
| Rare external destinations | Suspicious communication |
| Long-duration connections | Persistent C2 |

---

# 10. Phase 4 – Analyze Hunt Results

The analyst must determine whether findings indicate malicious activity.

---

## 10.1 Hunt Analysis Questions

| Question | Objective |
|---|---|
| Is the behavior malicious? | Threat validation |
| Is the activity authorized? | Context review |
| Is persistence present? | Long-term compromise |
| Is lateral movement occurring? | Scope analysis |
| Is attacker activity active? | Urgency validation |

---

## 10.2 Threat Validation Criteria

| Validation Type | Example |
|---|---|
| IOC validation | Malicious IP |
| Behavioral analysis | Credential dumping |
| Historical correlation | Repeated beaconing |
| Threat intelligence | Known malware hash |
| MITRE mapping | ATT&CK technique |

---

## 10.3 High-Risk Hunt Findings

Immediate escalation required if:

| Finding | Escalation Reason |
|---|---|
| Active ransomware indicators | Business disruption |
| Domain admin abuse | Enterprise compromise |
| Data exfiltration | Regulatory exposure |
| C2 communication | Active attacker |
| Credential dumping | Privilege compromise |

---

# 11. Phase 5 – Scope Related Activity

Determine how widespread the activity is.

---

## 11.1 Scope Expansion Areas

| Area | Objective |
|---|---|
| Additional hosts | Spread analysis |
| User accounts | Account compromise |
| Shared IOCs | Campaign activity |
| Similar process activity | Coordinated execution |
| Shared persistence | Multi-host compromise |

---

## 11.2 Scope Tracking Table

| Host | User | IOC Found | Severity | Escalated? |
|---|---|---|---|---|
| | | | | |

---

# 12. Phase 6 – Escalation Procedures

Threat hunting findings may require immediate escalation.

---

## 12.1 Escalation Matrix

| Condition | Escalation Target |
|---|---|
| Advanced malware | L3 |
| Active attacker | IR Team |
| Domain compromise | IR Team |
| Data exfiltration | IR Team |
| Cloud admin abuse | IR Team |
| Rootkit indicators | L3 |

---

## 12.2 Escalation Package Requirements

Every escalation must include:

| Requirement | Status |
|---|---|
| Hunt hypothesis | ☐ |
| Hunt findings | ☐ |
| Evidence references | ☐ |
| IOC list | ☐ |
| Scope analysis | ☐ |
| Timeline | ☐ |
| Recommended actions | ☐ |

---

# 13. Phase 7 – Detection Improvement

Threat hunting must improve defensive capability.

---

## 13.1 Detection Improvement Activities

| Activity | Purpose |
|---|---|
| Create new SIEM rules | Improve detection |
| Tune EDR detections | Reduce blind spots |
| Update IOC feeds | Improve blocking |
| Add correlation logic | Improve visibility |
| Improve alert severity | Better prioritization |

---

## 13.2 Detection Gap Tracking

| Gap Identified | Impact | Improvement Action |
|---|---|---|
| | | |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 14. Phase 8 – Documentation Standards

Every hunt must be documented.

---

## 14.1 Required Hunt Documentation

| Requirement | Status |
|---|---|
| Hunt objective documented | ☐ |
| Hypothesis documented | ☐ |
| Queries documented | ☐ |
| Findings documented | ☐ |
| Scope analysis completed | ☐ |
| Escalation decisions documented | ☐ |
| Detection improvements identified | ☐ |

---

## 14.2 Hunt Documentation Example

GOOD:
“Hunt focused on detecting encoded PowerShell execution across privileged endpoints. SIEM correlation identified Base64-encoded PowerShell execution on FIN-SRV-02 by svc_backup account. EDR telemetry confirmed outbound beaconing to suspicious external IP every 45 seconds.”

BAD:
“PowerShell activity found.”

---

# 15. Threat Hunting Metrics

Track hunting effectiveness.

---

## 15.1 Threat Hunting KPI Examples

| KPI | Objective |
|---|---|
| Hunts completed monthly | Activity tracking |
| Threats identified proactively | Detection maturity |
| Mean hunt completion time | Operational efficiency |
| Detection improvements created | Capability growth |
| Escalations generated | Hunt effectiveness |

---

# 16. MSSP Threat Hunting Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain client segregation | Prevent data leakage |
| Use client-approved scope | Contract compliance |
| Follow client SLA | Notification requirements |
| Restrict tenant visibility | Compliance |
| Preserve evidence separately | Audit readiness |

---

# 17. Common Threat Hunting Mistakes

| Mistake | Operational Risk |
|---|---|
| Hunting without scope | Inefficient analysis |
| Ignoring behavioral anomalies | Missed threats |
| Weak documentation | Lost intelligence |
| No detection improvement | Repeated blind spots |
| Delayed escalation | Increased attacker dwell time |

---

# 18. Related Documents

| Document | Path |
|---|---|
| L2 Investigation SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md` |
| L2 SIEM Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-SIEM-Deep-Investigation.md` |
| L2 EDR Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-EDR-Deep-Investigation.md` |
| Threat Intel Integration | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-SIEM.md` |
| MITRE ATT&CK Reference | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md` |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |

---

# 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / Threat Hunting Lead | Initial version |

---

# 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**