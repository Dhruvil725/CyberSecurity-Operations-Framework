# SOP: L3 Disk Forensics Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L3 Disk Forensics Procedures |
| Document ID | SOC-L3-SOP-004 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Digital Forensics Lead |
| Approved By | IR Team Lead / CISO |
| Classification | Internal – Restricted Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the methodology, forensic standards, workflows, evidence handling requirements, and reporting procedures for Level 3 (L3) disk forensic investigations.

Disk forensics is the process of acquiring, preserving, analyzing, and interpreting data stored on physical or virtual storage media to reconstruct attacker activity and identify compromise artifacts.

Disk forensics is used to:

- Recover deleted artifacts
- Identify persistence mechanisms
- Investigate malware execution
- Reconstruct attacker timelines
- Detect lateral movement
- Analyze user activity
- Identify exfiltration staging
- Recover hidden or encrypted files
- Support legal and regulatory investigations

The objectives of disk forensics are to:

- Preserve evidence integrity
- Reconstruct attacker actions
- Determine compromise scope
- Identify attacker persistence
- Support containment and eradication
- Provide legally defensible evidence
- Support incident response and root cause analysis

Improper forensic procedures may result in:

- Evidence contamination
- Loss of deleted artifacts
- Timeline corruption
- Missed persistence mechanisms
- Incomplete compromise analysis
- Failed legal admissibility

This SOP ensures:

- Standardized forensic imaging procedures
- Proper evidence handling
- Accurate forensic analysis
- Chain-of-custody compliance
- Reliable reporting and escalation
- Audit-ready forensic practices

---

# 3. Scope

This SOP applies to disk forensic investigations involving:

| Investigation Type | Example |
|---|---|
| Malware investigations | Trojan execution |
| Ransomware investigations | Encryption analysis |
| Insider threat investigations | Unauthorized access |
| Data breach investigations | Staged exfiltration |
| APT investigations | Persistence analysis |
| Rootkit investigations | Hidden artifacts |
| Supply chain attacks | Malicious installers |
| Credential theft | Browser/session artifacts |
| Cloud workload compromise | Virtual disk analysis |
| Legal investigations | Evidence preservation |

---

## 3.1 Storage Media Covered

| Storage Type | Examples |
|---|---|
| Physical disks | HDD, SSD |
| Virtual disks | VMDK, VHD |
| Removable media | USB drives |
| Cloud storage snapshots | Cloud volumes |
| Mobile device storage | Mobile extraction |
| External drives | Backup disks |

---

# 4. Disk Forensics Philosophy (IMPORTANT)

Disk forensics is evidence-centric reconstruction.

The objective is not only identifying malicious files, but understanding:

- How the attacker entered
- What the attacker executed
- What files were accessed
- Whether persistence exists
- Whether data was staged or exfiltrated
- Whether compromise spread
- Whether evidence was deleted or tampered with

L3 analysts must assume:

- Attackers attempted anti-forensics
- Logs may be incomplete
- Artifacts may be deleted
- Timestamps may be manipulated
- Persistence may be hidden
- Multiple attack stages may exist

All analysis must preserve original evidence integrity.

---

## 4.1 Common Disk Forensics Failures

| Poor Practice | Operational Risk |
|---|---|
| Analyzing original disks directly | Evidence contamination |
| Weak chain-of-custody | Legal inadmissibility |
| No write blockers used | Artifact modification |
| Weak timeline normalization | Analysis inconsistency |
| Ignoring deleted artifacts | Missed compromise |
| Weak evidence hashing | Integrity failure |

---

# 5. L3 Disk Forensics Responsibilities

| Responsibility | Description |
|---|---|
| Disk acquisition | Forensic imaging |
| Artifact analysis | File and metadata review |
| Deleted file recovery | Hidden artifact recovery |
| Timeline reconstruction | Chronology analysis |
| Persistence investigation | Long-term compromise |
| User activity analysis | Behavioral reconstruction |
| Reporting and escalation | Technical documentation |
| Evidence preservation | Integrity protection |

---

# 6. Disk Forensics Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Incident Validation | Investigation scope |
| Phase 2 | Evidence Acquisition | Forensic image |
| Phase 3 | Integrity Verification | Hash validation |
| Phase 4 | File System Analysis | Artifact review |
| Phase 5 | Persistence Investigation | Hidden access analysis |
| Phase 6 | User Activity Reconstruction | Behavioral analysis |
| Phase 7 | Timeline Reconstruction | Attack chronology |
| Phase 8 | Reporting and Escalation | Technical findings |
| Phase 9 | Evidence Archival | Secure retention |

---

# 7. Phase 1 – Incident Validation

Disk forensics is initiated when deeper artifact analysis is required.

---

## 7.1 Common Triggers for Disk Forensics

| Trigger | Reason |
|---|---|
| Ransomware activity | File impact analysis |
| Deleted artifacts suspected | Recovery requirement |
| Persistence indicators | Long-term compromise |
| Insider threat investigation | User activity reconstruction |
| Malware infection | Payload analysis |
| Data breach investigation | Staging/exfiltration analysis |

---

## 7.2 Initial Validation Checklist

| Validation Item | Completed |
|---|---|
| Incident severity validated | ☐ |
| Scope defined | ☐ |
| Storage media identified | ☐ |
| Legal hold assessed | ☐ |
| Chain-of-custody initiated | ☐ |

---

# 8. Phase 2 – Evidence Acquisition (CRITICAL)

Forensic acquisition must preserve original evidence integrity.

---

## 8.1 Disk Acquisition Requirements

| Requirement | Standard |
|---|---|
| Use approved forensic tools | Mandatory |
| Use write blockers | Mandatory |
| Generate SHA-256 hashes | Mandatory |
| Preserve original media | Mandatory |
| Record acquisition timestamps | Mandatory |

---

## 8.2 Acquisition Formats

| Format | Usage |
|---|---|
| E01 | Preferred forensic format |
| RAW/DD | Raw forensic image |
| AFF | Advanced forensic format |
| VMDK/VHD | Virtual disk analysis |

---

## 8.3 Acquisition Documentation Table

| Evidence ID | Device | Acquired By | Time UTC | SHA-256 |
|---|---|---|---|---|
| | | | | |

---

## 8.4 Acquisition Risks

| Risk | Operational Impact |
|---|---|
| Live system modification | Evidence contamination |
| No write blocker | Metadata alteration |
| Weak storage handling | Evidence corruption |
| Delayed acquisition | Lost artifacts |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md`

---

# 9. Phase 3 – Integrity Verification

All forensic images must be validated before analysis.

---

## 9.1 Integrity Requirements

| Requirement | Standard |
|---|---|
| SHA-256 verification | Mandatory |
| Original image preserved | Mandatory |
| Working copies created | Mandatory |
| Secure storage used | Mandatory |

---

## 9.2 Verification Checklist

| Validation Item | Completed |
|---|---|
| Hash generated | ☐ |
| Hash verified | ☐ |
| Analysis copy created | ☐ |
| Storage secured | ☐ |

---

# 10. Phase 4 – File System Analysis

The analyst must investigate artifacts stored on disk.

---

## 10.1 File System Analysis Areas

| Area | Objective |
|---|---|
| File metadata | Timeline reconstruction |
| Executables | Malware identification |
| Registry hives | Persistence review |
| Browser artifacts | User activity |
| Event logs | Timeline analysis |
| Scheduled tasks | Persistence |

---

## 10.2 Common Forensic Artifacts

| Artifact | Investigation Use |
|---|---|
| Prefetch files | Execution history |
| Registry keys | Persistence |
| Browser history | User behavior |
| Jump lists | File access |
| Shellbags | Folder access |
| Event logs | Timeline reconstruction |

---

## 10.3 High-Risk Artifact Indicators

| Indicator | Meaning |
|---|---|
| Recently deleted executables | Anti-forensics |
| Unsigned binaries | Suspicious execution |
| New scheduled tasks | Persistence |
| Obfuscated scripts | Malware |
| Hidden directories | Concealed activity |

---

# 11. Phase 5 – Persistence Investigation

Determine whether attackers established persistent access.

---

## 11.1 Persistence Areas

| Area | Example |
|---|---|
| Registry Run Keys | Auto-start |
| Services | Persistent malware |
| Scheduled Tasks | Timed execution |
| Startup folders | User persistence |
| WMI persistence | Fileless persistence |

---

## 11.2 Persistence Escalation Conditions

Immediate escalation required if:

| Condition | Escalation Target |
|---|---|
| Domain controller persistence | IR Team |
| Rootkit indicators | IR Team |
| EDR tampering | IR Team |
| Multi-host persistence | IR Team |

---

# 12. Phase 6 – User Activity Reconstruction

Reconstruct user and attacker activity.

---

## 12.1 User Activity Analysis Areas

| Area | Purpose |
|---|---|
| Browser history | Access review |
| File access history | Data exposure analysis |
| USB artifacts | Removable media review |
| Login artifacts | Authentication analysis |
| Application usage | Behavioral analysis |

---

## 12.2 User Activity Indicators

| Indicator | Meaning |
|---|---|
| Access outside business hours | Suspicious activity |
| Large file copies | Data staging |
| USB insertion artifacts | Potential exfiltration |
| Unauthorized admin tools | Insider threat |

---

## 12.3 Activity Tracking Table

| Timestamp UTC | User | Activity | Artifact Source |
|---|---|---|---|
| | | | |

---

# 13. Phase 7 – Timeline Reconstruction (CRITICAL)

All disk forensic investigations require timeline reconstruction.

---

## 13.1 Timeline Objectives

| Objective | Purpose |
|---|---|
| Identify initial compromise | Root cause |
| Track attacker progression | Threat reconstruction |
| Detect persistence timing | Long-term compromise |
| Identify exfiltration timing | Regulatory assessment |

---

## 13.2 Timeline Event Categories

| Event Type | Example |
|---|---|
| Initial execution | Malware launch |
| Privilege escalation | Admin token abuse |
| Lateral movement | SMB activity |
| Data staging | Archive creation |
| Exfiltration | Cloud upload |

---

## 13.3 Timeline Tracking Table

| Timestamp UTC | Event | Source | Severity | Evidence Ref |
|---|---|---|---|---|
| | | | | |

---

# 14. Phase 8 – Reporting and Escalation

All findings must be formally documented.

---

## 14.1 Reporting Requirements

| Requirement | Mandatory |
|---|---|
| Executive summary | Yes |
| Artifact findings | Yes |
| Timeline reconstruction | Yes |
| Persistence findings | Yes |
| IOC summary | Yes |
| Scope analysis | Yes |
| Containment recommendations | Yes |

---

## 14.2 Escalation Matrix

| Condition | Escalation Target |
|---|---|
| Active compromise | IR Team |
| Data breach evidence | Legal / Compliance |
| Rootkit persistence | IR Team |
| Widespread malware | Executive Management |
| Regulatory exposure | Compliance Team |

---

# 15. Phase 9 – Evidence Archival

Forensic images must be archived securely.

---

## 15.1 Archival Requirements

| Requirement | Standard |
|---|---|
| Encrypted storage | Mandatory |
| Restricted access | Mandatory |
| Hash verification maintained | Mandatory |
| Retention schedule followed | Mandatory |
| Backup maintained | Mandatory |

---

## 15.2 Evidence Tracking Table

| Evidence ID | Media Type | Storage Location | Retention Period |
|---|---|---|---|
| | | | |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`

---

# 16. MSSP-Specific Disk Forensics Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain tenant evidence segregation | Prevent data leakage |
| Follow client retention requirements | Compliance |
| Restrict analyst access | Confidentiality |
| Preserve client-specific chain-of-custody | Legal defensibility |
| Use client escalation matrix | SLA compliance |

---

# 17. Common Disk Forensics Mistakes

| Mistake | Operational Risk |
|---|---|
| Analyzing original media | Evidence contamination |
| Weak hashing procedures | Integrity failure |
| Ignoring deleted artifacts | Missed compromise |
| Weak timeline analysis | Incomplete investigation |
| Poor evidence storage | Evidence corruption |
| Delayed escalation | Increased attacker dwell time |

---

# 18. Related Documents

| Document | Path |
|---|---|
| L3 Advanced Forensics SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Advanced-Forensics-SOP.md` |
| L3 Memory Forensics SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Memory-Forensics-SOP.md` |
| L3 Malware Analysis SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Malware-Analysis-SOP.md` |
| Disk Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| CoC Transfer Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md` |

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