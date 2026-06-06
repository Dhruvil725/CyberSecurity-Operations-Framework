# SOP: L3 Advanced Forensics Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L3 Advanced Forensics Procedures |
| Document ID | SOC-L3-SOP-001 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Digital Forensics Lead |
| Approved By | IR Team Lead / CISO |
| Classification | Internal – Restricted Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the operational methodology, forensic standards, workflows, escalation requirements, and evidence handling procedures for Level 3 (L3) advanced forensic investigations.

Advanced forensics is performed when incidents exceed standard SOC investigative capability and require specialized forensic analysis techniques.

The purpose of advanced forensics is to:

- Determine the full scope of compromise
- Reconstruct attacker activity
- Identify persistence mechanisms
- Detect stealth and evasion techniques
- Recover deleted or hidden artifacts
- Support legal and regulatory investigations
- Provide evidence for root cause analysis
- Support incident response decision-making
- Enable attribution and intelligence analysis

Advanced forensic investigations may involve:

- Memory analysis
- Disk analysis
- Malware reverse engineering
- Timeline reconstruction
- Deleted artifact recovery
- Log reconstruction
- Cloud forensic analysis
- Persistence analysis
- Lateral movement analysis

Improper forensic procedures may result in:

- Evidence contamination
- Loss of forensic integrity
- Failed legal admissibility
- Incomplete attacker reconstruction
- Missed persistence
- Incorrect attribution
- Regulatory non-compliance

This SOP ensures:

- Forensic integrity preservation
- Standardized forensic methodology
- Chain-of-custody compliance
- Legally defensible evidence handling
- Consistent forensic reporting
- Audit-ready investigative practices

---

# 3. Scope

This SOP applies to advanced forensic investigations involving:

| Investigation Type | Example |
|---|---|
| Ransomware forensics | Encryption analysis |
| APT investigations | Multi-stage compromise |
| Insider threat investigations | Data theft |
| Malware analysis | Reverse engineering |
| Cloud compromise | IAM abuse |
| Credential theft | LSASS analysis |
| Persistence investigations | Rootkits |
| Data exfiltration | Hidden transfer analysis |
| Supply chain compromise | Trusted software abuse |
| Zero-day exploitation | Exploit artifact analysis |

---

## 3.1 Applicable Forensic Sources

| Source Type | Examples |
|---|---|
| Disk images | E01, RAW |
| Memory captures | RAM dumps |
| SIEM exports | Correlated logs |
| EDR telemetry | Endpoint events |
| Cloud audit logs | AWS CloudTrail |
| Network captures | PCAP |
| Authentication logs | AD, Entra ID |
| Email artifacts | PST/MSG |
| Mobile artifacts | Device extraction |

---

# 4. Advanced Forensics Philosophy (IMPORTANT)

Advanced forensics is evidence-driven reconstruction.

The purpose is not only identifying malicious activity, but understanding:

- What happened
- How it happened
- When it happened
- What the attacker achieved
- Whether persistence exists
- Whether data was exposed
- Whether compromise remains active

L3 forensic analysts must assume:

- Evidence may be incomplete
- Attackers attempted evasion
- Logs may be altered
- Persistence may be hidden
- Multiple attack stages may exist

The forensic process must therefore be:

- Methodical
- Verifiable
- Repeatable
- Defensible
- Evidence-centric

---

## 4.1 Common Advanced Forensics Failures

| Poor Practice | Operational Risk |
|---|---|
| Working on original evidence | Evidence contamination |
| Weak chain-of-custody | Legal inadmissibility |
| No timeline normalization | Analysis inconsistency |
| Ignoring volatile evidence | Lost attacker context |
| Overwriting artifacts | Forensic corruption |
| Incomplete scope analysis | Missed compromise |

---

# 5. L3 Advanced Forensics Responsibilities

| Responsibility | Description |
|---|---|
| Evidence acquisition | Forensic collection |
| Artifact analysis | Deep forensic investigation |
| Timeline reconstruction | Attack chain analysis |
| Persistence investigation | Hidden access review |
| Malware analysis coordination | Reverse engineering support |
| Root cause determination | Compromise origin |
| Forensic reporting | Technical documentation |
| Escalation support | IR coordination |

---

# 6. Advanced Forensics Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Case Intake and Validation | Investigation scope |
| Phase 2 | Evidence Preservation | Forensic integrity |
| Phase 3 | Evidence Acquisition | Forensic artifacts |
| Phase 4 | Artifact Analysis | Threat findings |
| Phase 5 | Timeline Reconstruction | Attack chronology |
| Phase 6 | Persistence Analysis | Long-term compromise assessment |
| Phase 7 | Scope Expansion | Blast radius |
| Phase 8 | Reporting and Escalation | Technical reporting |
| Phase 9 | Evidence Archival | Long-term retention |

---

# 7. Phase 1 – Case Intake and Validation

The investigation begins with formal intake and scope definition.

---

## 7.1 Case Intake Requirements

| Requirement | Purpose |
|---|---|
| Incident severity validated | Priority determination |
| Escalation reason reviewed | Scope understanding |
| Evidence sources identified | Collection planning |
| Legal considerations reviewed | Compliance |
| Regulatory exposure assessed | Reporting obligations |

---

## 7.2 Initial Intake Checklist

| Validation Item | Completed |
|---|---|
| Incident ticket reviewed | ☐ |
| Scope defined | ☐ |
| Evidence sources identified | ☐ |
| Chain-of-custody initiated | ☐ |
| Stakeholders identified | ☐ |
| Legal hold requirements reviewed | ☐ |

---

# 8. Phase 2 – Evidence Preservation (CRITICAL)

Evidence preservation is the highest forensic priority.

---

## 8.1 Evidence Preservation Principles

| Principle | Requirement |
|---|---|
| Preserve original evidence | Never modify originals |
| Capture volatile evidence first | Prevent data loss |
| Hash all evidence | Integrity validation |
| Maintain chain-of-custody | Legal defensibility |
| Use forensic tooling only | Evidence protection |

---

## 8.2 Volatile Evidence Priority

Collect immediately:

1. Active memory
2. Network connections
3. Running processes
4. Logged-in users
5. Authentication tokens
6. Temporary files

---

## 8.3 Evidence Integrity Checklist

| Requirement | Completed |
|---|---|
| SHA-256 hash generated | ☐ |
| Original evidence preserved | ☐ |
| Collection timestamp recorded | ☐ |
| Collector documented | ☐ |
| Storage location documented | ☐ |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`

---

# 9. Phase 3 – Evidence Acquisition

Forensic acquisition must follow approved procedures.

---

## 9.1 Evidence Acquisition Types

| Evidence Type | Purpose |
|---|---|
| Memory acquisition | Volatile analysis |
| Disk imaging | Full artifact analysis |
| Log exports | Timeline reconstruction |
| PCAP collection | Network analysis |
| Cloud snapshot | Cloud forensics |

---

## 9.2 Forensic Acquisition Standards

| Requirement | Standard |
|---|---|
| Disk imaging format | E01 preferred |
| Hash algorithm | SHA-256 minimum |
| Time standard | UTC |
| Evidence storage | Encrypted repository |
| Transfer method | Approved secure channel |

---

## 9.3 Acquisition Documentation Table

| Evidence ID | Evidence Type | Collected By | Time UTC | Hash |
|---|---|---|---|---|
| | | | | |

---

# 10. Phase 4 – Artifact Analysis

The analyst must identify attacker artifacts and forensic indicators.

---

## 10.1 Artifact Categories

| Artifact Type | Example |
|---|---|
| Registry artifacts | Run keys |
| File artifacts | Malware payloads |
| Persistence artifacts | Scheduled tasks |
| Browser artifacts | Download history |
| Authentication artifacts | Login sessions |
| Cloud artifacts | IAM changes |

---

## 10.2 Advanced Analysis Areas

| Analysis Area | Objective |
|---|---|
| Persistence analysis | Hidden access |
| Privilege escalation | Elevated compromise |
| Lateral movement | Internal spread |
| Anti-forensics | Evasion detection |
| Data staging | Exfiltration prep |

---

## 10.3 High-Risk Findings

Immediate escalation required if:

| Finding | Risk |
|---|---|
| Domain-wide persistence | Enterprise compromise |
| Rootkit indicators | Advanced threat |
| EDR tampering | Visibility loss |
| Active exfiltration | Regulatory exposure |
| Wiper malware | Data destruction |

---

# 11. Phase 5 – Timeline Reconstruction (CRITICAL)

All advanced forensic investigations require detailed timeline reconstruction.

---

## 11.1 Timeline Objectives

| Objective | Purpose |
|---|---|
| Determine initial access | Root cause |
| Identify attack progression | Threat reconstruction |
| Track lateral movement | Scope analysis |
| Detect persistence timing | Long-term compromise |
| Identify exfiltration timing | Regulatory assessment |

---

## 11.2 Timeline Event Categories

| Event Type | Example |
|---|---|
| Initial compromise | Phishing execution |
| Malware execution | Payload launch |
| Privilege escalation | Admin token abuse |
| Lateral movement | SMB spread |
| Exfiltration | Cloud upload |

---

## 11.3 Timeline Tracking Table

| Timestamp UTC | Event | Source | Severity | Evidence Ref |
|---|---|---|---|---|
| | | | | |

---

# 12. Phase 6 – Persistence Analysis

The analyst must determine whether attackers established persistent access.

---

## 12.1 Persistence Investigation Areas

| Area | Example |
|---|---|
| Registry persistence | Run keys |
| Services | Malicious service |
| Scheduled tasks | Automated execution |
| WMI subscriptions | Fileless persistence |
| Startup folders | User persistence |
| Cloud persistence | IAM abuse |

---

## 12.2 Persistence Escalation Triggers

Immediate escalation required if:

| Condition | Escalation Target |
|---|---|
| Rootkit persistence | IR Team |
| Domain controller persistence | IR Team |
| Cloud admin persistence | IR Team |
| Multi-host persistence | IR Team |

---

# 13. Phase 7 – Scope Expansion

Determine the complete impact of the compromise.

---

## 13.1 Scope Analysis Areas

| Area | Objective |
|---|---|
| Endpoints affected | Infrastructure impact |
| Accounts compromised | Identity impact |
| Servers impacted | Business risk |
| Cloud resources affected | Cloud exposure |
| Sensitive data accessed | Regulatory impact |

---

## 13.2 Scope Expansion Indicators

| Indicator | Meaning |
|---|---|
| Shared malware hash | Malware spread |
| Shared persistence | Coordinated compromise |
| Shared C2 communication | Campaign activity |
| Shared credentials | Lateral movement |

---

## 13.3 Scope Tracking Table

| Asset | User | IOC Found | Severity | Escalated |
|---|---|---|---|---|
| | | | | |

---

# 14. Phase 8 – Reporting and Escalation

Advanced forensic findings must be formally documented.

---

## 14.1 Reporting Requirements

| Requirement | Mandatory |
|---|---|
| Technical summary | Yes |
| Timeline reconstruction | Yes |
| Evidence references | Yes |
| Scope analysis | Yes |
| Root cause findings | Yes |
| Persistence findings | Yes |
| IOC summary | Yes |
| Containment recommendations | Yes |

---

## 14.2 Escalation Matrix

| Condition | Escalation Target |
|---|---|
| Regulatory exposure | Legal / Compliance |
| Critical infrastructure impact | Executive Management |
| Active attacker presence | IR Team |
| Advanced malware | Malware Analysis Team |

---

# 15. Phase 9 – Evidence Archival

Evidence must be archived securely for future investigations and legal requirements.

---

## 15.1 Archival Requirements

| Requirement | Standard |
|---|---|
| Encrypted storage | Mandatory |
| Retention schedule followed | Mandatory |
| Chain-of-custody maintained | Mandatory |
| Access restricted | Mandatory |
| Backup maintained | Mandatory |

---

## 15.2 Evidence Retention Categories

| Evidence Type | Retention Recommendation |
|---|---|
| Critical incident evidence | 7 years |
| Regulatory investigation evidence | Per legal requirement |
| Routine investigations | 1–3 years |
| Malware samples | Controlled retention |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`

---

# 16. MSSP-Specific Forensic Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain tenant segregation | Prevent data leakage |
| Preserve client evidence separately | Compliance |
| Follow client retention rules | Regulatory compliance |
| Restrict forensic access | Data protection |
| Follow contractual escalation | SLA compliance |

---

# 17. Common Advanced Forensics Mistakes

| Mistake | Operational Risk |
|---|---|
| Working on original evidence | Evidence contamination |
| Weak chain-of-custody | Legal inadmissibility |
| Missing volatile evidence | Lost attacker context |
| No persistence analysis | Reinfection risk |
| Weak timeline reconstruction | Incomplete investigation |
| Delayed escalation | Increased attacker dwell time |

---

# 18. Related Documents

| Document | Path |
|---|---|
| L3 Memory Forensics SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Memory-Forensics-SOP.md` |
| L3 Disk Forensics SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Disk-Forensics-SOP.md` |
| L3 Malware Analysis SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Malware-Analysis-SOP.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| CoC Master Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md` |
| RCA Template | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md` |

---

# 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / Digital Forensics Lead | Initial version |

---

# 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**