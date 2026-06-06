# SOP: L2 Evidence Handling Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L2 Evidence Handling Procedures |
| Document ID | SOC-L2-SOP-003 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / L2 Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the evidence handling requirements and procedures for Level 2 (L2) SOC analysts during security incident investigations.

Evidence handling is one of the most operationally and legally sensitive responsibilities in incident response because:

- Improperly handled evidence may become inadmissible in legal proceedings
- Modified evidence may corrupt forensic analysis
- Lost evidence may create investigation gaps
- Incomplete chain-of-custody may undermine regulatory compliance
- Premature evidence deletion may violate legal hold obligations

The purpose of this SOP is to ensure:

- Evidence integrity throughout the investigation
- Consistent documentation practices
- Chain-of-custody compliance
- Audit-ready evidence management
- Legal and regulatory alignment
- Support for forensic analysis by L3 and IR Team

---

# 3. Scope

Applies to evidence handling during:

- Malware incidents
- Ransomware investigations
- Cloud security incidents
- Insider threat investigations
- Data breach investigations
- Network intrusion cases
- APT campaign investigations
- Credential compromise cases
- MSSP client incident investigations

Evidence types covered:

- Digital log exports
- Memory artifacts
- Disk images
- Network captures
- Cloud audit logs
- Authentication logs
- Email forensics
- EDR telemetry exports

---

# 4. Evidence Handling Principles (IMPORTANT)

L2 evidence handling must follow these non-negotiable principles.

---

## 4.1 Preserve First

Before any investigation action that may alter data:

- Export relevant logs
- Snapshot affected systems where applicable
- Capture volatile evidence first
- Record original state

Example:
Before isolating a compromised endpoint, capture active network connections.

---

## 4.2 Do Not Modify Original Evidence

L2 analysts must:

- Work from copies where possible
- Never overwrite original log files
- Never modify timestamps
- Never alter file metadata
- Never delete attacker artifacts prematurely

---

## 4.3 Document Everything

Every evidence collection action must be recorded including:

- What was collected
- When it was collected
- Who collected it
- Where it was stored
- Hash values

---

## 4.4 Maintain Chain of Custody

Chain-of-custody must be established for all major evidence items.

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`

---

# 5. Evidence Categories

---

## 5.1 Category 1 – Volatile Evidence

Volatile evidence is time-sensitive and may be lost if systems are modified.

| Evidence Type | Example |
|---|---|
| Active network connections | netstat output |
| Running processes | Process list |
| Logged-in users | Session list |
| Memory contents | RAM dump |
| Temporary files | TEMP directory |
| Active authentication tokens | Session tokens |

Volatile evidence must be captured before:
- System reboot
- Endpoint isolation
- Network disconnection
- User logoff

---

## 5.2 Category 2 – Log Evidence

| Evidence Type | Source |
|---|---|
| SIEM event exports | SIEM platform |
| Windows Event Logs | Endpoint |
| Authentication logs | Active Directory |
| Firewall logs | Network platform |
| DNS logs | DNS server |
| Proxy logs | Web proxy |
| Cloud audit logs | Cloud platform |

---

## 5.3 Category 3 – Endpoint Evidence

| Evidence Type | Source |
|---|---|
| EDR telemetry | EDR console |
| Prefetch files | Windows endpoint |
| Registry hives | Windows endpoint |
| Scheduled tasks | Endpoint |
| Browser artifacts | Endpoint |

---

## 5.4 Category 4 – Network Evidence

| Evidence Type | Source |
|---|---|
| Packet captures | Network tap |
| NetFlow records | Flow collector |
| IDS/IPS logs | Security platform |

---

## 5.5 Category 5 – Cloud Evidence

| Evidence Type | Source |
|---|---|
| CloudTrail logs | AWS |
| Azure Activity Logs | Azure |
| GCP Audit Logs | GCP |
| IAM records | Cloud platform |
| Storage access logs | Cloud storage |

---

# 6. Evidence Collection Workflow

| Phase | Objective |
|---|---|
| Phase 1 | Identify required evidence |
| Phase 2 | Prioritize volatile evidence |
| Phase 3 | Collect and export |
| Phase 4 | Hash and verify |
| Phase 5 | Store securely |
| Phase 6 | Record chain-of-custody |

---

# 7. Phase 1 – Identify Required Evidence

Before collection:

| Step | Objective |
|---|---|
| Define incident scope | Determine what evidence applies |
| Identify affected systems | Target evidence sources |
| Confirm log retention | Validate availability |
| Identify legal hold requirements | Confirm scope |

---

# 8. Phase 2 – Prioritize Volatile Evidence (IMPORTANT)

Volatile evidence disappears rapidly.

L2 analysts must prioritize:

1. Active network connections
2. Running processes
3. Logged-in users
4. Memory state
5. Temporary artifacts
6. Active sessions

Collect before:
- Isolation
- Shutdown
- Patch application
- User logoff

---

# 9. Phase 3 – Evidence Collection Procedures

---

## 9.1 Log Export Procedures

| Log Type | Export Method |
|---|---|
| SIEM events | SIEM export function |
| Windows Event Logs | EVTX export |
| Authentication logs | AD export |
| Cloud logs | Cloud console export |

Requirements:
- Export original format
- Include all fields
- Include UTC timestamps
- Export full time range

---

## 9.2 EDR Evidence Export

| Evidence | Export Method |
|---|---|
| Process telemetry | EDR console export |
| File events | EDR console |
| Network connections | EDR console |
| Alert details | EDR export |

---

## 9.3 Network Evidence Collection

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md`

Requirements:
- Capture full packets where authorized
- Export NetFlow records
- Export firewall logs in original format

---

# 10. Phase 4 – Hashing and Verification (CRITICAL)

Every evidence file must be hashed immediately after collection.

---

## 10.1 Hashing Requirements

| Requirement | Standard |
|---|---|
| Hash algorithm | SHA-256 minimum |
| Hash timing | Immediately after collection |
| Hash storage | Separate from evidence file |
| Verification | Hash before and after transfer |

---

## 10.2 Evidence Hash Log

| Evidence ID | File Name | SHA-256 Hash | Collection Time UTC |
|---|---|---|---|
| | | | |

---

# 11. Phase 5 – Secure Storage

Evidence must be stored securely.

---

## 11.1 Storage Requirements

| Requirement | Standard |
|---|---|
| Storage location | Designated evidence repository |
| Access control | Restricted to investigators |
| Encryption | Encrypted at rest |
| Backup | Backup copy maintained |
| Retention | Per retention schedule |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

## 11.2 MSSP Evidence Segregation (IMPORTANT)

For MSSP environments:

- Maintain strict client segregation
- Never store cross-client evidence together
- Label evidence with client identifier
- Apply client-specific retention rules
- Restrict access to authorized analysts only

---

# 12. Phase 6 – Chain-of-Custody Documentation

Every piece of evidence must have documented chain-of-custody.

---

## 12.1 Chain-of-Custody Requirements

| Field | Required |
|---|---|
| Evidence ID | Yes |
| Description | Yes |
| Collected by | Yes |
| Collection timestamp UTC | Yes |
| Collection method | Yes |
| Storage location | Yes |
| Hash value | Yes |
| Transfer records | Yes |

---

## 12.2 Chain-of-Custody Table

| Evidence ID | Description | Collected By | Time (UTC) | Hash | Location | Transferred To |
|---|---|---|---|---|---|---|
| | | | | | | |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`

---

# 13. Evidence During Active Incident (IMPORTANT)

During active P1 incidents:

- Prioritize evidence collection before containment
- Do not allow evidence-destroying actions without documentation
- Coordinate with IR Team before major containment
- Preserve as much volatile evidence as operational situation allows

If containment must happen before evidence collection:
- Document decision and approvals
- Capture as much as possible before isolation
- Record what was not captured

---

# 14. Legal Hold Awareness

If legal proceedings are possible:

- Do not delete any evidence
- Notify Legal team immediately
- Maintain evidence beyond standard retention
- Stop automated deletion processes
- Document all evidence preservation decisions

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

---

# 15. Evidence Handling Mistakes

| Mistake | Risk |
|---|---|
| No hashing | Evidence integrity failure |
| Incorrect timestamps | Timeline corruption |
| Modifying original files | Forensic failure |
| No chain-of-custody | Legal inadmissibility |
| Premature deletion | Legal liability |
| Insecure storage | Data breach |

---

# 16. Documentation Requirements

Before investigation closure:

| Requirement | Status |
|---|---|
| Evidence inventory completed | ☐ |
| All items hashed | ☐ |
| Chain-of-custody recorded | ☐ |
| Storage confirmed | ☐ |
| Legal hold assessed | ☐ |
| Retention period confirmed | ☐ |

---

## 17. Related Documents

| Document | Path |
|---|---|
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| CoC Master Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |
| Legal Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |

---

## 18. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / L2 Operations Lead | Initial version |

---

## 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**