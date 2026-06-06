# SOP: L2 Investigation Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L2 Investigation Procedures |
| Document ID | SOC-L2-SOP-001 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / L2 Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the operational responsibilities, workflows, and investigation methodology for Level 2 (L2) SOC analysts.

L2 analysts operate as the primary investigative tier within the SOC and are responsible for validating, scoping, and escalating security incidents identified by L1 analysts or automated detection systems.

Unlike L1 analysts, who focus primarily on alert triage and initial validation, L2 analysts are responsible for:

- Deep investigation and correlation
- Multi-source log analysis
- Threat scoping and impact assessment
- Identification of attacker behavior
- Evidence preservation
- Investigation documentation
- Escalation to L3 or IR Team
- Containment recommendations

This SOP ensures investigations are:

- Consistent
- Technically defensible
- Operationally efficient
- Audit-ready
- Aligned with IR standards and regulatory requirements

---

# 3. Scope

Applies to all L2 investigations involving:

- Malware incidents
- Ransomware activity
- Credential attacks
- Network intrusions
- Cloud security incidents
- Phishing/BEC compromise
- Data exfiltration
- Insider threats
- Zero-day indicators
- APT-related activity
- MSSP-managed client incidents

Applies across:

- SIEM platforms
- EDR/XDR platforms
- Cloud monitoring systems
- Authentication systems
- Network telemetry platforms
- Threat intelligence integrations

---

# 4. L2 Investigation Philosophy (IMPORTANT)

L2 investigation is not simply “reviewing alerts.”

The purpose of L2 operations is to determine:

- What actually happened
- Whether compromise occurred
- Which systems/users are affected
- How the attacker moved
- Whether persistence exists
- Whether data exposure occurred
- Whether escalation is required

An effective L2 analyst must think in:

- Attack chains
- Timelines
- Adversary objectives
- Behavioral patterns
- Operational impact

L2 analysts must avoid:
- Tunnel vision on single alerts
- Over-reliance on signatures
- Premature false positive closure
- Assumptions without evidence

---

# 5. L2 Responsibilities

The L2 analyst is responsible for:

| Responsibility | Description |
|---|---|
| Deep investigation | Multi-source analysis |
| Correlation | Cross-platform event analysis |
| Threat scoping | Determine blast radius |
| Evidence preservation | Preserve forensic artifacts |
| Escalation | Escalate to L3/IR |
| Containment guidance | Recommend response actions |
| Documentation | Maintain detailed records |
| Threat validation | Confirm malicious activity |

---

# 6. L2 Investigation Workflow

| Phase | Objective |
|---|---|
| Phase 1 | Receive escalation |
| Phase 2 | Validate incident |
| Phase 3 | Scope affected assets |
| Phase 4 | Correlate related activity |
| Phase 5 | Determine impact |
| Phase 6 | Preserve evidence |
| Phase 7 | Recommend containment |
| Phase 8 | Escalate or close |

---

# 7. Phase 1 – Receive and Review Escalation

L2 investigations usually begin after escalation from L1.

---

## 7.1 Escalation Review Requirements

The L2 analyst must review:

| Item | Purpose |
|---|---|
| Ticket notes | Understand prior actions |
| Alert timeline | Identify progression |
| Severity assigned | Validate urgency |
| Evidence attached | Confirm supporting telemetry |
| Asset context | Determine business impact |
| Escalation reason | Understand concern |

---

## 7.2 Escalation Validation (IMPORTANT)

The L2 analyst must validate:
- Whether escalation was appropriate
- Whether severity is accurate
- Whether immediate escalation to IR is required

If severity underestimated:
- Upgrade immediately
- Notify SOC Lead

---

# 8. Phase 2 – Incident Validation

The first L2 objective is determining whether malicious activity actually occurred.

---

## 8.1 Validation Activities

| Activity | Objective |
|---|---|
| SIEM review | Correlate events |
| EDR review | Validate endpoint behavior |
| Authentication review | Detect account compromise |
| TI enrichment | Identify known threats |
| Historical review | Detect persistence |

---

## 8.2 Validation Questions

| Question | Purpose |
|---|---|
| Is the activity malicious? | Incident confirmation |
| Is the activity ongoing? | Urgency assessment |
| Is this isolated or widespread? | Scope determination |
| Is persistence likely? | Long-term risk |
| Is data exposure possible? | Regulatory assessment |

---

# 9. Phase 3 – Scope Affected Assets (CRITICAL)

L2 analysts must determine the blast radius of the incident.

---

## 9.1 Asset Scope Categories

| Category | Example |
|---|---|
| Endpoint systems | Workstations, servers |
| User accounts | Privileged users |
| Cloud assets | IAM roles, workloads |
| Network segments | Internal VLANs |
| SaaS platforms | M365, Google Workspace |

---

## 9.2 Scope Expansion Indicators

Immediately expand scope if:

| Indicator | Meaning |
|---|---|
| Same hash on multiple systems | Malware spread |
| Shared credentials | Lateral movement |
| Same C2 destination | Campaign activity |
| Multiple geographies | Account compromise |
| Shared service account usage | Wider compromise |

---

## 9.3 Scope Tracking Table

| Asset | Role | Compromised? | Evidence Ref |
|---|---|---|---|
| | | | |

---

# 10. Phase 4 – Correlation and Investigation

L2 analysts must correlate activity across multiple telemetry sources.

---

## 10.1 Required Correlation Sources

| Source | Investigation Use |
|---|---|
| SIEM | Event aggregation |
| EDR | Endpoint behavior |
| Firewall logs | Traffic analysis |
| DNS logs | Beaconing and tunneling |
| Authentication logs | Account abuse |
| Cloud logs | IAM anomalies |
| Proxy logs | Exfiltration review |

---

## 10.2 Correlation Objectives

The analyst must determine:

- Initial access method
- Lateral movement
- Persistence mechanisms
- C2 communication
- Data staging
- Exfiltration attempts
- Privilege escalation

---

## 10.3 Timeline Reconstruction (IMPORTANT)

Every serious incident must include a UTC timeline.

---

### Required Timeline Events

| Event | Example |
|---|---|
| Initial access | Phishing click |
| Malware execution | PowerShell launch |
| Credential dumping | LSASS access |
| Lateral movement | RDP connection |
| Exfiltration | Large upload |

---

# 11. Phase 5 – Impact Assessment

L2 analysts must determine operational and security impact.

---

## 11.1 Impact Categories

| Category | Example |
|---|---|
| Operational impact | Service outage |
| Security impact | Privilege compromise |
| Data impact | Sensitive file access |
| Regulatory impact | PII exposure |
| Client impact | MSSP tenant affected |

---

## 11.2 Critical Impact Indicators

Immediately escalate if:

| Indicator | Impact |
|---|---|
| Domain admin compromise | Enterprise-wide risk |
| Data exfiltration | Regulatory exposure |
| Ransomware encryption | Business disruption |
| Cloud admin compromise | Infrastructure risk |

---

# 12. Phase 6 – Evidence Preservation (IMPORTANT)

L2 analysts must preserve evidence before containment when possible.

---

## 12.1 Evidence Categories

| Evidence | Source |
|---|---|
| SIEM logs | SIEM export |
| EDR telemetry | Endpoint console |
| Memory artifacts | EDR/L3 |
| Authentication logs | AD/IdP |
| PCAPs | Network capture |
| Cloud audit logs | Cloud platform |

---

## 12.2 Evidence Preservation Rules

- Preserve original timestamps
- Export logs before rotation
- Maintain UTC time consistency
- Record evidence references in ticket
- Avoid modifying compromised systems unnecessarily

Reference:
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md`

---

# 13. Phase 7 – Containment Recommendations

L2 analysts do not typically execute containment directly unless authorized.

However, L2 analysts must recommend containment actions.

---

## 13.1 Common Containment Recommendations

| Incident | Recommendation |
|---|---|
| Malware infection | Isolate endpoint |
| Credential compromise | Reset credentials |
| Cloud IAM abuse | Disable keys/tokens |
| Beaconing | Block destination |
| Data exfiltration | Block outbound traffic |

---

## 13.2 Containment Escalation Triggers

Immediate containment recommendation required if:

- Active ransomware observed
- Data exfiltration active
- Beaconing ongoing
- Domain compromise confirmed
- Privileged account misuse active

---

# 14. Phase 8 – Escalation or Closure

---

## 14.1 Escalation Conditions

Escalate to L3 or IR if:

| Condition | Escalation Target |
|---|---|
| Advanced malware analysis needed | L3 |
| Memory forensics required | L3 |
| Domain compromise | IR Team |
| Cloud root compromise | IR Team |
| Active APT indicators | IR Team |
| Data breach confirmed | IR Team |

---

## 14.2 Closure Conditions

An investigation may only be closed if:

- Threat disproven
- No malicious indicators remain
- Evidence reviewed completely
- Ticket documentation complete
- No escalation required

---

# 15. Investigation Documentation Standards

L2 documentation must include:

- Timeline
- Scope
- Evidence references
- Investigation queries used
- Severity rationale
- Escalation decisions
- Containment recommendations

---

## 15.1 Good Documentation Example

GOOD:
“EDR telemetry confirmed PowerShell execution spawned from WINWORD.EXE at 14:12 UTC. Beaconing to known malicious IP identified. Additional host communication observed with FIN-SRV-02.”

BAD:
“Looks malicious.”

---

# 16. Investigation Prioritization During High Alert Volume

When alert backlog increases:

| Priority | Incident Type |
|---|---|
| 1 | Active compromise |
| 2 | Data exfiltration |
| 3 | Privileged account abuse |
| 4 | Ransomware indicators |
| 5 | Malware execution |
| 6 | Low-confidence anomalies |

---

# 17. MSSP-Specific L2 Considerations

For MSSP operations:

- Maintain tenant segregation
- Follow client-specific SLA
- Avoid cross-client data exposure
- Use client-specific escalation procedures
- Document client impact separately

---

# 18. Common L2 Investigation Mistakes

| Mistake | Risk |
|---|---|
| Focusing only on one host | Missed lateral movement |
| Ignoring cloud logs | Partial visibility |
| Weak timeline reconstruction | Incomplete investigation |
| Delayed escalation | Increased attacker dwell time |
| Poor evidence preservation | Lost forensic value |

---

# 19. Related Documents

| Document | Path |
|---|---|
| L2 SIEM Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-SIEM-Deep-Investigation.md` |
| L2 EDR Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-EDR-Deep-Investigation.md` |
| L2 Evidence Handling SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md` |
| L2 Escalation Criteria | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Escalation-Criteria.md` |
| L2 Threat Hunting Procedures | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md` |

---

## 20. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / L2 Operations Lead | Initial version |

---

## 21. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**