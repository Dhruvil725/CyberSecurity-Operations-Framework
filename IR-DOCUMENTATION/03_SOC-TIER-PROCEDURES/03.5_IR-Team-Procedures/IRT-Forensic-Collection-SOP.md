# SOP: IRT Forensic Collection Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – IRT Forensic Collection Procedures |
| Document ID | SOC-IRT-SOP-005 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | IR Team Lead / Digital Forensics Lead |
| Approved By | CISO / Legal Counsel |
| Classification | Internal – Restricted Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the methodology, collection standards, operational workflows, evidence handling requirements, and documentation procedures for Incident Response Team (IRT) forensic evidence collection activities.

Forensic collection is a foundational capability of incident response operations because the quality of evidence collected directly determines:

- The accuracy of forensic investigations
- The completeness of incident scope analysis
- The defensibility of forensic findings
- The effectiveness of containment and eradication
- The admissibility of evidence in legal proceedings
- The quality of regulatory reporting
- The reliability of root cause analysis
- The accuracy of lessons learned

Forensic collection activities must support:

- Digital evidence collection
- Memory acquisition
- Disk imaging
- Network capture
- Cloud evidence collection
- Log preservation
- Physical media collection
- Application forensics

Improper forensic collection may result in:

- Evidence contamination
- Loss of volatile artifacts
- Chain-of-custody failures
- Incomplete investigation scope
- Failed legal proceedings
- Regulatory non-compliance
- Incorrect root cause analysis
- Reinfection due to missed persistence

This SOP ensures:

- Standardized forensic collection procedures
- Proper volatile evidence prioritization
- Verified evidence integrity
- Comprehensive collection coverage
- Audit-ready collection documentation
- Legally defensible forensic practices

---

# 3. Scope

This SOP applies to forensic collection activities involving:

| Incident Type | Example |
|---|---|
| Ransomware investigations | Encryption analysis |
| Data breach investigations | Exfiltration evidence |
| Malware investigations | Payload collection |
| APT investigations | Long-term compromise |
| Insider threat investigations | Unauthorized access |
| Cloud security incidents | IAM abuse |
| Supply chain attacks | Trusted software abuse |
| Zero-day exploitation | Exploit artifacts |
| Network intrusion | Traffic evidence |
| Legal investigations | Regulatory collection |

---

## 3.1 Evidence Collection Types

| Evidence Type | Examples |
|---|---|
| Memory captures | RAM dumps |
| Disk images | E01, RAW |
| Log exports | SIEM, EDR |
| Network captures | PCAPs |
| Cloud audit exports | CloudTrail, Azure |
| Authentication logs | AD, Entra ID |
| Email forensic data | PST, MSG |
| Mobile device data | Mobile extractions |
| Physical media | USB, external drives |
| Application logs | Database, web server |

---

# 4. Forensic Collection Philosophy (IMPORTANT)

Forensic collection is evidence preservation under discipline.

The principles guiding forensic collection are:

- Preserve first
- Collect in order of volatility
- Never modify original evidence
- Hash everything
- Document every action
- Maintain chain-of-custody from collection

L3 analysts and IRT forensic analysts must assume:

- Volatile evidence disappears rapidly
- Attackers may have tampered with logs
- Timestamps may be inaccurate
- Anti-forensic tools may have been used
- Multiple attack stages may exist

Collection must be:

- Methodical
- Comprehensive
- Verifiable
- Defensible
- Evidence-centric

---

## 4.1 Common Forensic Collection Failures

| Poor Practice | Operational Risk |
|---|---|
| Rebooting before collection | Volatile evidence loss |
| Working on original evidence | Evidence contamination |
| Weak hashing practices | Integrity failure |
| Missing volatile priority | Lost attacker context |
| Incomplete collection scope | Investigation gaps |
| Delayed collection start | Evidence destruction |

---

# 5. IRT Forensic Collection Responsibilities

| Responsibility | Description |
|---|---|
| Evidence planning | Collection scope definition |
| Volatile evidence collection | Priority acquisition |
| Disk imaging | Forensic acquisition |
| Memory acquisition | RAM capture |
| Network evidence | Traffic collection |
| Cloud evidence | Cloud log collection |
| Log preservation | Log export |
| Integrity verification | Hash validation |
| Chain-of-custody management | Compliance documentation |
| Secure storage | Evidence protection |

---

# 6. Forensic Collection Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Collection Planning | Scope definition |
| Phase 2 | Volatile Evidence Collection | Time-sensitive artifacts |
| Phase 3 | Memory Acquisition | RAM capture |
| Phase 4 | Disk Imaging | Storage acquisition |
| Phase 5 | Network Evidence Collection | Traffic artifacts |
| Phase 6 | Log and Cloud Evidence Collection | Platform exports |
| Phase 7 | Integrity Verification | Hash validation |
| Phase 8 | Chain-of-Custody Documentation | Legal compliance |
| Phase 9 | Secure Storage | Evidence protection |

---

# 7. Phase 1 – Collection Planning

Effective forensic collection begins with structured planning.

---

## 7.1 Planning Objectives

| Objective | Purpose |
|---|---|
| Define collection scope | Operational clarity |
| Identify evidence sources | Collection planning |
| Prioritize volatile evidence | Time-sensitive focus |
| Validate tooling readiness | Operational readiness |
| Assess legal requirements | Compliance |

---

## 7.2 Planning Checklist

| Validation Item | Completed |
|---|---|
| Incident scope reviewed | ☐ |
| Evidence sources identified | ☐ |
| Collection priorities set | ☐ |
| Tools validated | ☐ |
| Legal hold reviewed | ☐ |

---

## 7.3 Tooling Requirements

| Tool Type | Purpose |
|---|---|
| Memory acquisition tools | RAM collection |
| Disk imaging tools | Storage acquisition |
| Write blockers | Evidence protection |
| Log export tools | Platform exports |
| Network capture tools | Traffic collection |
| Hashing tools | Integrity verification |
| Chain-of-custody forms | Legal compliance |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Forensics-Toolkit-Reference.md`

---

# 8. Phase 2 – Volatile Evidence Collection (CRITICAL)

Volatile evidence must be collected immediately before any containment action.

---

## 8.1 Volatile Evidence Priority Order

Collect in the following order:

| Priority | Evidence Type | Reason |
|---|---|---|
| 1 | Active memory | RAM is lost on shutdown |
| 2 | Network connections | Sessions may terminate |
| 3 | Running processes | Processes change rapidly |
| 4 | Logged-in users | Sessions may expire |
| 5 | Authentication tokens | Tokens may expire |
| 6 | Clipboard data | Temporary only |
| 7 | Temporary files | Rapidly overwritten |

---

## 8.2 Volatile Collection Standards

| Standard | Mandatory |
|---|---|
| Collect before isolation | Mandatory |
| Collect before shutdown | Mandatory |
| Document collection order | Mandatory |
| Hash collected artifacts | Mandatory |
| Record all timestamps UTC | Mandatory |

---

## 8.3 Volatile Evidence Tracking Table

| Evidence ID | Type | Collected By | Time UTC | SHA-256 |
|---|---|---|---|---|
| | | | | |

---

# 9. Phase 3 – Memory Acquisition

Memory acquisition captures volatile RAM contents.

---

## 9.1 Memory Acquisition Objectives

| Objective | Purpose |
|---|---|
| Capture running processes | Malware analysis |
| Preserve network connections | C2 identification |
| Capture authentication tokens | Credential theft analysis |
| Preserve injected code | In-memory malware |
| Capture decrypted payloads | Malware analysis |

---

## 9.2 Memory Acquisition Requirements

| Requirement | Standard |
|---|---|
| Approved acquisition tools only | Mandatory |
| Hash immediately after capture | Mandatory |
| UTC timestamp recorded | Mandatory |
| Collector documented | Mandatory |
| Storage location documented | Mandatory |

---

## 9.3 Memory Acquisition Documentation Table

| System | Acquired By | Time UTC | RAM Size | SHA-256 |
|---|---|---|---|---|
| | | | | |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md`

---

# 10. Phase 4 – Disk Imaging

Disk imaging captures persistent storage evidence.

---

## 10.1 Disk Imaging Objectives

| Objective | Purpose |
|---|---|
| Preserve file system | Artifact analysis |
| Recover deleted files | Anti-forensics detection |
| Capture persistence | Malware persistence |
| Preserve registry | Attacker behavior |
| Preserve event logs | Timeline reconstruction |

---

## 10.2 Disk Imaging Requirements

| Requirement | Standard |
|---|---|
| Use write blockers | Mandatory |
| E01 or RAW format preferred | Standard |
| SHA-256 hash generated | Mandatory |
| Original media preserved | Mandatory |
| Analysis performed on copies | Mandatory |

---

## 10.3 Disk Imaging Documentation Table

| Evidence ID | Device | Format | Acquired By | Time UTC | SHA-256 |
|---|---|---|---|---|---|
| | | | | | |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md`

---

# 11. Phase 5 – Network Evidence Collection

Network evidence provides communication analysis capability.

---

## 11.1 Network Evidence Types

| Evidence Type | Purpose |
|---|---|
| Packet captures (PCAP) | Traffic analysis |
| NetFlow records | Traffic patterns |
| Firewall logs | Connection analysis |
| DNS logs | Beaconing analysis |
| Proxy logs | Web activity |
| VPN logs | Remote access |

---

## 11.2 Network Collection Requirements

| Requirement | Standard |
|---|---|
| Capture during active incident | Mandatory |
| Export original format | Mandatory |
| Hash exports | Mandatory |
| UTC timestamps verified | Mandatory |
| Capture window documented | Mandatory |

---

## 11.3 Network Evidence Tracking Table

| Evidence ID | Source | Time Range UTC | Captured By | SHA-256 |
|---|---|---|---|---|
| | | | | |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Network-Evidence-SOP.md`

---

# 12. Phase 6 – Log and Cloud Evidence Collection

Logs provide critical investigation context.

---

## 12.1 Log Evidence Categories

| Log Type | Source |
|---|---|
| SIEM events | SIEM platform |
| Windows Event Logs | Endpoints |
| Authentication logs | AD/Entra ID |
| Cloud audit logs | AWS/Azure/GCP |
| Application logs | Web/DB servers |
| EDR telemetry | Endpoint agents |

---

## 12.2 Log Collection Requirements

| Requirement | Standard |
|---|---|
| Export full time range | Mandatory |
| Preserve original format | Mandatory |
| UTC timestamps verified | Mandatory |
| Hash exported files | Mandatory |
| Document log sources | Mandatory |

---

## 12.3 Cloud Evidence Collection Areas

| Platform | Evidence Type |
|---|---|
| AWS | CloudTrail, S3 logs |
| Azure | Activity logs, Entra ID |
| GCP | Audit logs |
| M365 | Unified audit log |

---

## 12.4 Log Evidence Tracking Table

| Evidence ID | Log Type | Time Range UTC | Collected By | SHA-256 |
|---|---|---|---|---|
| | | | | |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Log-Collection-SOP.md`

---

# 13. Phase 7 – Integrity Verification

All collected evidence must pass integrity verification.

---

## 13.1 Hashing Requirements

| Requirement | Standard |
|---|---|
| SHA-256 minimum | Mandatory |
| Hash at collection | Mandatory |
| Hash at storage | Mandatory |
| Hash at transfer | Mandatory |
| Hash verification records | Mandatory |

---

## 13.2 Hash Verification Table

| Evidence ID | Original Hash | Verification Hash | Verified By | Time UTC |
|---|---|---|---|---|
| | | | | |

---

## 13.3 Hash Mismatch Response

If hash mismatch detected:

| Step | Action |
|---|---|
| 1 | Document mismatch immediately |
| 2 | Isolate affected evidence |
| 3 | Notify IRT Lead |
| 4 | Assess cause and impact |
| 5 | Legal notification if required |

---

# 14. Phase 8 – Chain-of-Custody Documentation

Every piece of evidence requires formal documentation.

---

## 14.1 Documentation Requirements

| Field | Mandatory |
|---|---|
| Evidence ID | Yes |
| Description | Yes |
| Source | Yes |
| Collector | Yes |
| Collection time UTC | Yes |
| Hash value | Yes |
| Storage location | Yes |
| Transfer records | Yes |

---

## 14.2 Evidence Master Documentation Table

| Evidence ID | Description | Source | Collector | Hash | Storage |
|---|---|---|---|---|---|
| | | | | | |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`

---

# 15. Phase 9 – Secure Storage

Collected evidence must be stored in approved repositories.

---

## 15.1 Storage Requirements

| Requirement | Standard |
|---|---|
| Encrypted at rest | Mandatory |
| Access restricted | Mandatory |
| Backup maintained | Mandatory |
| Audit logging enabled | Mandatory |
| Retention schedule followed | Mandatory |

---

## 15.2 Storage Tracking Table

| Evidence ID | Storage Location | Access Restricted | Retention Period |
|---|---|---|---|
| | | | |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

# 16. MSSP-Specific Collection Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain client evidence segregation | Compliance |
| Use client-specific evidence labeling | Traceability |
| Follow client retention requirements | Contract compliance |
| Restrict cross-client visibility | Confidentiality |
| Coordinate client legal requirements | Legal alignment |

---

# 17. Common Forensic Collection Mistakes

| Mistake | Operational Risk |
|---|---|
| Delaying volatile collection | Evidence loss |
| No write blockers | Evidence modification |
| Weak hashing | Integrity failure |
| Missing chain-of-custody | Legal inadmissibility |
| Incomplete collection scope | Investigation gaps |
| Improper storage | Evidence corruption |

---

# 18. Related Documents

| Document | Path |
|---|---|
| IRT Evidence Chain-of-Custody | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Evidence-Chain-of-Custody.md` |
| IRT Onsite Response SOP | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Onsite-Response-SOP.md` |
| Memory Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md` |
| Disk Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md` |
| Log Collection SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Log-Collection-SOP.md` |
| Evidence Retention Schedule | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md` |

---

# 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | IR Team Lead / Digital Forensics Lead | Initial version |

---

# 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**