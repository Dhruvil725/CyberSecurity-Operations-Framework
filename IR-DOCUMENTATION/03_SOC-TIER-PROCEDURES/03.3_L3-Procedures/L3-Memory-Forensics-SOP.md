# SOP: L3 Memory Forensics Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L3 Memory Forensics Procedures |
| Document ID | SOC-L3-SOP-003 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Digital Forensics Lead |
| Approved By | IR Team Lead / CISO |
| Classification | Internal – Restricted Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the methodology, workflows, forensic standards, and evidence handling requirements for Level 3 (L3) memory forensic investigations.

Memory forensics is the process of analyzing volatile memory (RAM) to identify attacker activity, malware execution, credential theft, persistence mechanisms, and in-memory artifacts that may not exist on disk.

Memory analysis is critical because modern attackers frequently use:

- Fileless malware
- In-memory payloads
- Reflective DLL injection
- Process hollowing
- Credential dumping
- Token theft
- In-memory persistence
- Evasion techniques

The purpose of memory forensics is to:

- Identify active attacker processes
- Detect hidden or injected code
- Recover malicious artifacts
- Identify credential theft activity
- Detect active network connections
- Identify persistence mechanisms
- Reconstruct attacker activity timelines
- Support incident response containment

Improper memory acquisition or analysis may result in:

- Loss of volatile evidence
- Corrupted memory artifacts
- Incomplete forensic analysis
- Missed active compromise
- Failed credential theft detection
- Incorrect incident scope

This SOP ensures:

- Proper volatile evidence preservation
- Standardized memory analysis procedures
- Forensic integrity protection
- Accurate artifact extraction
- Reliable reporting and escalation
- Audit-ready forensic documentation

---

# 3. Scope

This SOP applies to memory forensic investigations involving:

| Investigation Type | Example |
|---|---|
| Malware investigations | Fileless malware |
| Ransomware analysis | Active encryption processes |
| Credential theft | LSASS dumping |
| Insider threats | Unauthorized access |
| APT investigations | Advanced persistence |
| Rootkit analysis | Hidden processes |
| Cloud workload compromise | In-memory abuse |
| Lateral movement | Token theft |
| Zero-day investigations | Exploit analysis |
| EDR bypass analysis | Defense evasion |

---

## 3.1 Memory Sources Covered

| Source Type | Example |
|---|---|
| Endpoint RAM captures | Windows/Linux/macOS |
| Virtual machine memory | Hypervisor snapshots |
| Cloud memory snapshots | Cloud instances |
| EDR memory captures | Endpoint telemetry |
| Live response captures | Incident response acquisition |

---

# 4. Memory Forensics Philosophy (IMPORTANT)

Memory analysis focuses on active system state.

Unlike disk forensics, memory forensics provides visibility into:

- Running processes
- Active network connections
- Loaded DLLs
- Authentication tokens
- In-memory malware
- Process injection
- Decrypted payloads
- Live attacker activity

L3 analysts must assume:

- Attackers may operate entirely in memory
- Malware may never touch disk
- Attackers may use anti-forensic techniques
- Memory artifacts are time-sensitive
- Volatile evidence may disappear rapidly

Memory evidence is extremely fragile and must be prioritized immediately during active incidents.

---

## 4.1 Common Memory Forensics Failures

| Poor Practice | Operational Risk |
|---|---|
| Delayed memory acquisition | Lost volatile evidence |
| Rebooting affected systems | Memory destruction |
| Using non-approved tools | Evidence contamination |
| Weak chain-of-custody | Legal inadmissibility |
| No hash verification | Integrity failure |
| Ignoring injected processes | Missed compromise |

---

# 5. L3 Memory Forensics Responsibilities

| Responsibility | Description |
|---|---|
| Memory acquisition | Capture volatile memory |
| Process analysis | Investigate active processes |
| Injection detection | Detect hidden code |
| Credential theft analysis | LSASS/token review |
| Network session analysis | Active connection review |
| Malware extraction | Recover payloads |
| Timeline reconstruction | Activity analysis |
| Reporting and escalation | Technical documentation |

---

# 6. Memory Forensics Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Incident Validation | Scope confirmation |
| Phase 2 | Memory Acquisition | RAM capture |
| Phase 3 | Integrity Verification | Hash validation |
| Phase 4 | Process Analysis | Active process review |
| Phase 5 | Injection and Malware Analysis | In-memory malware detection |
| Phase 6 | Credential Theft Analysis | Authentication compromise review |
| Phase 7 | Network Connection Analysis | Communication review |
| Phase 8 | Timeline Reconstruction | Attack chronology |
| Phase 9 | Reporting and Escalation | Technical findings |

---

# 7. Phase 1 – Incident Validation

Memory analysis is typically initiated during high-risk incidents.

---

## 7.1 Common Triggers for Memory Analysis

| Trigger | Reason |
|---|---|
| Credential dumping suspected | LSASS analysis |
| Fileless malware indicators | Memory-only payloads |
| Process injection detected | Hidden execution |
| Rootkit indicators | Hidden processes |
| EDR tampering | Defense evasion |
| Ransomware execution | Active encryption review |

---

## 7.2 Initial Validation Checklist

| Validation Item | Completed |
|---|---|
| Incident severity reviewed | ☐ |
| System still active | ☐ |
| Volatile evidence priority confirmed | ☐ |
| Acquisition tooling available | ☐ |
| Chain-of-custody initiated | ☐ |

---

# 8. Phase 2 – Memory Acquisition (CRITICAL)

Memory acquisition must occur before shutdown or isolation whenever operationally feasible.

---

## 8.1 Memory Acquisition Requirements

| Requirement | Standard |
|---|---|
| Approved forensic tools only | Mandatory |
| UTC timestamps recorded | Mandatory |
| Hash generated immediately | Mandatory |
| Original memory image preserved | Mandatory |
| Acquisition logged | Mandatory |

---

## 8.2 Volatile Evidence Priority

Collect in the following order when possible:

1. Active memory capture
2. Network connections
3. Running processes
4. Logged-in users
5. Authentication sessions
6. Clipboard data
7. Temporary artifacts

---

## 8.3 Memory Acquisition Documentation Table

| Evidence ID | Hostname | Acquired By | Time UTC | SHA-256 |
|---|---|---|---|---|
| | | | | |

---

## 8.4 Acquisition Risks

| Risk | Operational Impact |
|---|---|
| System reboot | Evidence loss |
| Malware self-deletion | Lost artifacts |
| Encryption activity | Corrupted evidence |
| Live attacker response | Evidence tampering |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md`

---

# 9. Phase 3 – Integrity Verification

All memory images must be validated before analysis.

---

## 9.1 Integrity Verification Requirements

| Requirement | Standard |
|---|---|
| SHA-256 hash validation | Mandatory |
| Original image preservation | Mandatory |
| Analysis copy creation | Mandatory |
| Secure storage | Mandatory |

---

## 9.2 Verification Checklist

| Validation Item | Completed |
|---|---|
| Hash generated | ☐ |
| Hash verified | ☐ |
| Evidence stored securely | ☐ |
| Chain-of-custody updated | ☐ |

---

# 10. Phase 4 – Process Analysis

Process analysis identifies suspicious or malicious activity.

---

## 10.1 Process Analysis Objectives

| Objective | Purpose |
|---|---|
| Identify hidden processes | Rootkit detection |
| Detect malicious execution | Malware analysis |
| Identify parent-child anomalies | Attack chain analysis |
| Detect privilege abuse | Elevated compromise |
| Review process integrity | Injection detection |

---

## 10.2 High-Risk Process Indicators

| Indicator | Meaning |
|---|---|
| Unsigned process | Suspicious execution |
| Process without parent | Hidden execution |
| LSASS access | Credential theft |
| Process hollowing | Malware injection |
| Suspicious PowerShell | Script abuse |

---

## 10.3 Process Analysis Table

| Process | PID | Parent Process | Suspicious? | Notes |
|---|---|---|---|---|
| | | | | |

---

# 11. Phase 5 – Injection and Malware Analysis

Memory forensics is critical for detecting injected malware.

---

## 11.1 Injection Detection Areas

| Area | Example |
|---|---|
| DLL injection | Reflective loading |
| Process hollowing | Code replacement |
| Shellcode injection | In-memory payload |
| API hooking | Defense evasion |
| Hidden modules | Stealth malware |

---

## 11.2 Malware Extraction Objectives

| Objective | Purpose |
|---|---|
| Recover payloads | Malware analysis |
| Extract configuration | IOC generation |
| Identify C2 infrastructure | Threat intelligence |
| Detect persistence | Long-term compromise |

---

## 11.3 Critical Escalation Conditions

Immediate escalation required if:

| Condition | Escalation Target |
|---|---|
| Active ransomware process | IR Team |
| Rootkit indicators | IR Team |
| Domain-wide malware | IR Team |
| Credential dumping active | IR Team |
| EDR bypass malware | IR Team |

---

# 12. Phase 6 – Credential Theft Analysis

Credential theft investigation is a primary memory forensic activity.

---

## 12.1 Credential Theft Indicators

| Indicator | Meaning |
|---|---|
| LSASS access | Credential dumping |
| Token impersonation | Privilege abuse |
| Kerberos ticket extraction | Lateral movement |
| Cached credential extraction | Persistence |

---

## 12.2 Credential Analysis Objectives

| Objective | Purpose |
|---|---|
| Identify compromised accounts | Scope determination |
| Detect privilege escalation | Severity assessment |
| Identify token abuse | Persistence review |
| Detect lateral movement | Internal spread |

---

## 12.3 Privileged Account Escalation Triggers

Immediate escalation required if:

- Domain admin credentials compromised
- Cloud admin tokens exposed
- Service account abuse detected
- Kerberos ticket abuse identified

---

# 13. Phase 7 – Network Connection Analysis

Review active and historical memory-resident network connections.

---

## 13.1 Network Analysis Areas

| Area | Objective |
|---|---|
| Active connections | C2 analysis |
| Listening ports | Persistence detection |
| DNS artifacts | Beaconing review |
| Suspicious external IPs | Threat validation |
| Internal SMB sessions | Lateral movement |

---

## 13.2 High-Risk Indicators

| Indicator | Meaning |
|---|---|
| Repeated beaconing | Active C2 |
| TOR connections | Anonymization |
| Rare external destinations | Suspicious communication |
| SMB spread | Internal propagation |

---

## 13.3 Connection Tracking Table

| Source Process | Destination IP | Protocol | Suspicious? |
|---|---|---|---|
| | | | |

---

# 14. Phase 8 – Timeline Reconstruction

Memory artifacts contribute to attack chronology reconstruction.

---

## 14.1 Timeline Objectives

| Objective | Purpose |
|---|---|
| Determine initial execution | Root cause analysis |
| Identify persistence timing | Long-term compromise |
| Detect lateral movement | Scope determination |
| Identify exfiltration timing | Regulatory assessment |

---

## 14.2 Timeline Tracking Table

| Timestamp UTC | Event | Artifact Source | Severity |
|---|---|---|---|
| | | | |

---

# 15. Phase 9 – Reporting and Escalation

All memory forensic findings must be formally documented.

---

## 15.1 Reporting Requirements

| Requirement | Mandatory |
|---|---|
| Executive summary | Yes |
| Process analysis findings | Yes |
| Injection analysis | Yes |
| Credential theft findings | Yes |
| IOC summary | Yes |
| Timeline reconstruction | Yes |
| Containment recommendations | Yes |

---

## 15.2 Escalation Matrix

| Condition | Escalation Target |
|---|---|
| Active attacker presence | IR Team |
| Credential theft confirmed | IR Team |
| Domain compromise | Executive Management |
| Rootkit indicators | IR Team |
| Widespread malware | IR Team |

---

# 16. Evidence Preservation and Storage

Memory images must be stored securely.

---

## 16.1 Storage Requirements

| Requirement | Standard |
|---|---|
| Encrypted storage | Mandatory |
| Access restricted | Mandatory |
| Hash verification maintained | Mandatory |
| Retention schedule followed | Mandatory |

---

## 16.2 Evidence Tracking Table

| Evidence ID | Host | Storage Location | Retention Period |
|---|---|---|---|
| | | | |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

# 17. MSSP-Specific Memory Forensics Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain tenant evidence segregation | Prevent data leakage |
| Restrict memory image access | Compliance |
| Follow client retention requirements | Regulatory obligations |
| Use client escalation paths | SLA compliance |
| Protect sensitive memory artifacts | Confidentiality |

---

# 18. Common Memory Forensics Mistakes

| Mistake | Operational Risk |
|---|---|
| Delayed memory capture | Lost evidence |
| Rebooting systems | Memory destruction |
| Weak evidence hashing | Integrity failure |
| Ignoring injected processes | Missed compromise |
| Weak timeline analysis | Incomplete investigation |
| Poor chain-of-custody | Legal inadmissibility |

---

# 19. Related Documents

| Document | Path |
|---|---|
| L3 Advanced Forensics SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Advanced-Forensics-SOP.md` |
| L3 Malware Analysis SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Malware-Analysis-SOP.md` |
| L3 Disk Forensics SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Disk-Forensics-SOP.md` |
| Memory Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| CoC Master Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md` |

---

# 20. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / Digital Forensics Lead | Initial version |

---

# 21. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**