# GUIDE: EDR Alert Handling Guide

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | GUIDE – EDR Alert Handling Guide |
| Document ID | TOOL-EDR-001 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Endpoint Security Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This guide defines the standardized approach for handling Endpoint Detection and Response (EDR) alerts within SOC operations. EDR alerts are high-value signals that provide endpoint-level telemetry and response capability.

This guide ensures:

- Consistent and accurate alert handling across L1/L2/L3
- Proper triage, validation, and prioritization
- Effective evidence preservation
- Clear escalation decisions to L2/L3/IR Team
- Appropriate containment recommendations and execution (as authorized)
- Audit-ready documentation

Improper EDR alert handling may result in:

- Missed compromise indicators
- Delayed containment
- Increased attacker dwell time
- False incident declarations
- Loss of forensic evidence
- Reinfection due to missed persistence
- SLA breaches (MSSP)

---

# 3. Scope

Applies to all EDR alerts including:

| Alert Category | Examples |
|---|---|
| Malware detection | Trojan, worm, ransomware |
| Suspicious execution | PowerShell, cmd abuse |
| Credential access | LSASS access, dumping |
| Persistence | Scheduled tasks, services |
| Lateral movement | Remote execution |
| Defense evasion | EDR tampering |
| Exploit behavior | Vulnerability exploitation |
| Data access anomalies | Sensitive file access |
| Cloud-connected endpoints | Hybrid identities |
| Insider threat indicators | Suspicious admin tools |

This guide applies to all endpoints under EDR coverage in:

- Corporate IT environments
- Production servers (where EDR is deployed)
- MSSP-managed client endpoints (tenant-controlled)

---

# 4. Alert Handling Philosophy (IMPORTANT)

EDR alerts are not equal. Some alerts are highly reliable, others are heuristic.

The objective is to identify:

- Whether compromise occurred
- Whether the attacker is active
- What the scope is
- What containment is needed
- Whether escalation is required

Analysts must focus on **behavior** and **context**:

- Parent/child process lineage
- Command line parameters
- User context and privileges
- Execution location (path)
- Network connections and destinations
- Persistence mechanisms
- Additional affected hosts

Avoid:

| Poor Practice | Risk |
|---|---|
| Closing based on detection name only | False negatives |
| Ignoring process ancestry | Missed root cause |
| Containment without evidence preservation | Lost forensics |
| Not checking lateral movement | Missed spread |
| Over-whitelisting | Detection gaps |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L1 Analyst | Initial triage, validation, ticket creation, escalation to L2 |
| L2 Analyst | Deep investigation, scoping, evidence preservation, containment recommendations |
| L3 Analyst | Advanced forensics, malware analysis, root cause determination |
| SOC Lead | Severity validation, escalation management, P1/P2 coordination |
| IR Team | Major incident response, containment authority for critical incidents |
| Endpoint Team | Remediation support, agent health, containment execution support |

---

# 6. EDR Alert Handling Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Alert Intake | Ticket with baseline details |
| Phase 2 | Initial Validation | True positive vs false positive |
| Phase 3 | Severity Assessment | P1–P4 classification |
| Phase 4 | Investigation & Scoping | Process tree + scope |
| Phase 5 | Evidence Preservation | Exports + hashes (if required) |
| Phase 6 | Containment Decision | Recommend/execute containment |
| Phase 7 | Escalation | L2/L3/IR engagement |
| Phase 8 | Documentation & Closure | Audit-ready ticket |

---

# 7. Phase 1 – Alert Intake

Upon receiving an alert:

---

## 7.1 Mandatory Alert Intake Fields

Capture the following in the ticket:

| Field | Requirement |
|---|---|
| Alert ID | Mandatory |
| Detection name/type | Mandatory |
| Severity (EDR-provided) | Mandatory |
| Hostname/Device ID | Mandatory |
| Username/Account | Mandatory |
| Timestamp (UTC) | Mandatory |
| Process name | Mandatory |
| Command line | Mandatory (if available) |
| Parent process | Mandatory (if available) |
| File hash (SHA-256) | If available |
| File path | Mandatory (if available) |
| Network connections | If available |
| EDR action taken | Quarantine/kill/isolate status |

---

## 7.2 Intake Checklist

| Validation Item | Completed |
|---|---|
| Alert details recorded | ☐ |
| Host criticality checked | ☐ |
| User privilege checked | ☐ |
| Related alerts searched | ☐ |
| Ticket created/updated | ☐ |

---

# 8. Phase 2 – Initial Validation

Determine if the alert represents malicious activity.

---

## 8.1 Validation Questions

| Question | Why it matters |
|---|---|
| Is this behavior malicious or expected? | Avoid false positives |
| Is the alert confidence high? | Prioritize correctly |
| Is the endpoint critical (server/DC)? | Severity impact |
| Is the user privileged? | Escalation criteria |
| Is there evidence of persistence? | Reinfection risk |
| Is there active network C2? | Active attacker risk |

---

## 8.2 Common False Positive Drivers

| Driver | Example |
|---|---|
| IT tools | Remote admin tools, scripts |
| Security scans | Vulnerability scanner |
| Patch deployment | Software installers |
| Automation | DevOps agents |
| Vendor management tools | SCCM-like |

**Important:** If suspected false positive, document *why* and verify through supporting telemetry.

---

## 8.3 True Positive Indicators (High Confidence)

| Indicator | Meaning |
|---|---|
| Encoded PowerShell | Obfuscation |
| Execution from Temp/AppData | Malware staging |
| Unsigned binary + unknown path | Suspicious payload |
| Process injection/hollowing | Advanced malware |
| LSASS access | Credential dumping |
| Shadow copy deletion | Ransomware precursor |
| EDR tampering | Active evasion |

---

# 9. Phase 3 – Severity Assessment

Use organization severity standards for the ticket (P1–P4). EDR severity alone is not sufficient.

---

## 9.1 Severity Decision Inputs

| Input | Example |
|---|---|
| Asset criticality | Domain controller |
| Attacker activity status | Ongoing C2 |
| Scope | Multiple hosts |
| Data exposure risk | Sensitive files accessed |
| Privilege level | Domain admin |
| Business impact | Service disruption |

---

## 9.2 Severity Mapping Guidance

| Condition | Recommended Severity |
|---|---|
| Active ransomware or encryption | P1 |
| Confirmed credential dumping | P1/P2 (depends on scope) |
| Privileged account compromise | P1 |
| Single endpoint malware contained | P2/P3 |
| Suspicious but unconfirmed execution | P3 |
| Informational / low risk | P4 |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

# 10. Phase 4 – Investigation & Scoping (L1 vs L2)

---

## 10.1 Minimum L1 Investigation (Before Escalation)

| Step | Objective |
|---|---|
| Review alert summary | Understand detection |
| Identify host and user | Context |
| Check parent process | Initial lineage |
| Check file path | Suspicious location |
| Check EDR action | Was it blocked? |
| Search related alerts | Trend |
| Escalate to L2 if needed | Deep analysis |

---

## 10.2 L2 Deep Investigation Requirements

L2 must perform:

| Area | Required Output |
|---|---|
| Process tree reconstruction | Parent-child chain |
| Command line analysis | Intent and tools |
| Network connections review | C2/exfil |
| Persistence check | Tasks/services/run keys |
| Lateral movement review | Remote execution signs |
| Scope expansion | Similar activity elsewhere |

Reference:
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-EDR-Deep-Investigation.md`

---

## 10.3 Investigation Notes Table (Ticket Standard)

| Item | Findings |
|---|---|
| Process Tree |  |
| Command Line |  |
| File/Hash |  |
| Network |  |
| User Context |  |
| Persistence |  |
| Lateral Movement |  |
| Scope |  |

---

# 11. Phase 5 – Evidence Preservation

Before containment (where feasible), preserve evidence.

---

## 11.1 Evidence Types to Preserve

| Evidence | Source |
|---|---|
| Alert details export | EDR console |
| Process tree screenshot/export | EDR telemetry |
| File hash and metadata | EDR/file events |
| Network connections | EDR/network telemetry |
| Host timeline events | EDR |
| Memory capture request | L3 / EDR (if supported) |

---

## 11.2 Evidence Preservation Rules

| Rule | Requirement |
|---|---|
| Use UTC timestamps | Mandatory |
| Do not modify original artifacts | Mandatory |
| Hash exported files | SHA-256 recommended |
| Store securely | Per evidence policy |
| Maintain chain-of-custody for major incidents | Mandatory for P1/P2 |

Reference:
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md`

---

# 12. Phase 6 – Containment Decision

Containment is not always immediate; it must be balanced with evidence collection and business impact.

---

## 12.1 Containment Options (Typical)

| Containment Action | When Used |
|---|---|
| Isolate endpoint | Active malware/C2 |
| Kill process | Active malicious execution |
| Quarantine file | Known malware payload |
| Block hash | Prevent execution across fleet |
| Network block (IP/domain) | Confirmed C2 |
| Disable account | Credential compromise |

Containment authority must follow:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 12.2 Emergency Containment Triggers

Immediate containment recommendation/escalation required if:

- Active ransomware encryption
- Credential dumping on server/DC
- Active C2 communication
- EDR tampering observed
- Multi-host propagation suspected

---

# 13. Phase 7 – Escalation Criteria

---

## 13.1 Escalate to L2 Immediately If (from L1)

| Condition | Reason |
|---|---|
| Privileged user involved | High risk |
| Server/DC affected | High impact |
| Encoded PowerShell | Likely malicious |
| LSASS interaction | Credential theft |
| Multiple similar alerts | Widespread |
| EDR tampering | Visibility risk |
| Suspected ransomware | Critical |

---

## 13.2 Escalate to L3 / IR Team If (from L2)

| Condition | Escalation Target |
|---|---|
| Memory forensics required | L3 |
| Rootkit / injection suspected | L3 |
| Confirmed ransomware | IR Team |
| Confirmed data exfiltration | IR Team + Legal/Compliance |
| Domain compromise | IR Team |
| Cloud admin compromise linked to endpoint | IR Team |

Reference:
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Escalation-Criteria.md`

---

# 14. Phase 8 – Documentation & Closure Standards

An EDR alert can be closed only if:

- The behavior is confirmed benign OR malicious activity is contained and escalated appropriately
- Scope check is completed (where required)
- Evidence references are included
- Ticket notes are complete and reproducible
- Closure rationale is clear and defensible

---

## 14.1 Closure Checklist

| Requirement | Completed |
|---|---|
| Severity validated | ☐ |
| Investigation notes complete | ☐ |
| Evidence preserved (if required) | ☐ |
| Scope checked | ☐ |
| Containment executed/recommended | ☐ |
| Escalations recorded | ☐ |
| Closure reason documented | ☐ |

---

## 14.2 Closure Reason Codes (Recommended)

| Code | Meaning |
|---|---|
| FP-IT | Legit IT/admin activity |
| FP-TOOL | Known tool behavior |
| TP-CONTAINED | Malicious, contained |
| TP-ESCALATED | Malicious, escalated |
| INFO | Informational |
| MONITOR | Monitor due to low confidence |

---

# 15. MSSP Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Validate client tenant scope | Prevent data leakage |
| Follow client SLA for notifications | Compliance |
| Use client-approved containment authority | Contract compliance |
| Maintain evidence segregation | Audit readiness |
| Communicate in client-approved channels | Governance |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/`

---

# 16. Common Mistakes

| Mistake | Risk |
|---|---|
| Closing without scope check | Missed spread |
| Containment without evidence | Forensic loss |
| Ignoring parent process | Missed root cause |
| Over-whitelisting | Detection gaps |
| Not checking user privilege | Under-severity |
| Missing documentation | Audit failure |

---

# 17. Related Documents

| Document | Path |
|---|---|
| L2 EDR Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-EDR-Deep-Investigation.md` |
| EDR Containment Commands | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Containment-Commands.md` |
| EDR Investigation Queries | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Investigation-Queries.md` |
| L2 Evidence Handling SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md` |
| Escalation Matrix Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| Severity Classification Guide | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md` |

---

# 18. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | Endpoint Security Lead | Initial version |

---

# 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**