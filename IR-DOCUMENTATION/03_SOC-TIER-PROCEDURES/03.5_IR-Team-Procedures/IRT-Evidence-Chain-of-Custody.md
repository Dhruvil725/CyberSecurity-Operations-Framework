# SOP: IRT Evidence Chain-of-Custody Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – IRT Evidence Chain-of-Custody Procedures |
| Document ID | SOC-IRT-SOP-004 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | IR Team Lead / Digital Forensics Lead |
| Approved By | CISO / Legal Counsel |
| Classification | Internal – Restricted Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the methodology, evidence handling standards, documentation requirements, and operational workflows for Incident Response Team (IRT) chain-of-custody management.

Chain-of-custody (CoC) is the formal, documented process used to preserve the integrity, authenticity, and traceability of digital and physical evidence collected during incident response, forensic investigations, regulatory investigations, and legal proceedings.

Chain-of-custody documentation is mandatory because evidence handled by IRT may be used:

- During incident investigations
- For internal disciplinary actions
- For regulatory reporting
- For law enforcement investigations
- For legal proceedings
- For litigation support
- For audit examinations
- For MSSP client investigations

Improper chain-of-custody handling may result in:

- Evidence inadmissibility in court
- Failed regulatory investigations
- Compromised forensic findings
- Legal exposure
- Operational accountability issues
- Audit failures
- Client compliance issues
- Loss of investigative credibility

The objectives of this SOP are to:

- Standardize chain-of-custody handling
- Preserve evidence integrity
- Ensure traceability of evidence transfers
- Maintain forensic defensibility
- Align with legal and regulatory frameworks
- Support audit and compliance obligations

This SOP ensures:

- Documented evidence handling
- Verified integrity through cryptographic hashing
- Secure evidence storage
- Proper evidence transfer procedures
- Audit-ready documentation
- Legally defensible processes

---

# 3. Scope

This SOP applies to all evidence handling activities involving:

| Evidence Type | Example |
|---|---|
| Digital evidence | Logs, disk images |
| Memory captures | RAM dumps |
| Network captures | PCAP files |
| Cloud audit exports | CloudTrail, Azure AD |
| Endpoint forensic images | E01, RAW |
| Malware samples | Suspicious files |
| Configuration exports | Firewall configs |
| Authentication logs | AD/Entra ID exports |
| Email forensic data | PST/MSG files |
| Physical media | USB drives, hard disks |

---

## 3.1 Chain-of-Custody Stakeholders

| Stakeholder | Role |
|---|---|
| IRT Lead | Evidence ownership |
| Forensic Analysts | Evidence collection |
| Custodians | Storage management |
| Legal Counsel | Compliance oversight |
| Auditors | Compliance validation |
| Regulators | Investigation review |
| Law enforcement | Legal coordination |

---

# 4. Chain-of-Custody Philosophy (IMPORTANT)

Chain-of-custody is a legal and operational discipline.

The CoC process must ensure:

- Every piece of evidence is traceable
- Every action on evidence is documented
- Every transfer of evidence is recorded
- Every storage location is documented
- Every analyst handling evidence is identified
- Every integrity check is logged

The CoC process must protect:

- Evidence authenticity
- Evidence integrity
- Evidence confidentiality
- Evidence usability

The IRT must operate under the principle:

"If it is not documented, it did not happen."

---

## 4.1 Common Chain-of-Custody Failures

| Poor Practice | Operational/Legal Risk |
|---|---|
| Missing transfer records | Inadmissible evidence |
| Inconsistent timestamps | Timeline disputes |
| Weak hashing practices | Integrity failure |
| Insufficient documentation | Audit failure |
| Improper storage | Evidence corruption |
| Unauthorized access | Legal exposure |

---

# 5. IRT Chain-of-Custody Responsibilities

| Responsibility | Description |
|---|---|
| Evidence identification | Recognize relevant evidence |
| Evidence collection | Approved acquisition |
| Evidence preservation | Integrity protection |
| Evidence transfer | Tracked handoffs |
| Evidence storage | Secure repositories |
| Evidence documentation | CoC compliance |
| Evidence destruction | Approved disposal |
| Evidence access control | Restricted access |

---

# 6. Chain-of-Custody Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Evidence Identification | Documented scope |
| Phase 2 | Evidence Collection | Verified artifacts |
| Phase 3 | Integrity Verification | Hash validation |
| Phase 4 | Evidence Documentation | CoC records |
| Phase 5 | Secure Storage | Controlled custody |
| Phase 6 | Evidence Transfer | Documented handoffs |
| Phase 7 | Evidence Access Logging | Auditable usage |
| Phase 8 | Evidence Retention/Destruction | Lifecycle management |

---

# 7. Phase 1 – Evidence Identification

The IRT identifies items of evidentiary value.

---

## 7.1 Identification Objectives

| Objective | Purpose |
|---|---|
| Determine evidence types | Scope clarity |
| Identify storage locations | Operational planning |
| Identify volatile evidence | Acquisition prioritization |
| Identify legal hold items | Compliance |

---

## 7.2 Evidence Identification Checklist

| Validation Item | Completed |
|---|---|
| Evidence types identified | ☐ |
| Acquisition method confirmed | ☐ |
| Legal hold reviewed | ☐ |
| Volatile evidence prioritized | ☐ |

---

## 7.3 Common Evidence Categories

| Category | Example |
|---|---|
| Volatile evidence | Memory dumps |
| Persistent evidence | Disk images |
| Network evidence | PCAPs |
| Cloud evidence | Audit logs |
| Application evidence | Database logs |

---

# 8. Phase 2 – Evidence Collection (CRITICAL)

Evidence must be collected using approved forensic procedures.

---

## 8.1 Collection Standards

| Standard | Mandatory |
|:--|:--|
| Use approved forensic tools | Yes |
| Use write blockers when applicable | Yes |
| Maintain UTC timestamps | Yes |
| Document collector identity | Yes |
| Document acquisition method | Yes |

---

## 8.2 Volatile Evidence Priority

Collect first:

1. Active memory
2. Network connections
3. Running processes
4. Logged-in users
5. Authentication tokens
6. Temporary artifacts

---

## 8.3 Collection Documentation Table

| Evidence ID | Source | Collected By | Time UTC | Acquisition Method |
|---|---|---|---|---|
| | | | | |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`

---

# 9. Phase 3 – Integrity Verification

Evidence integrity must be validated through cryptographic hashing.

---

## 9.1 Integrity Verification Requirements

| Requirement | Standard |
|---|---|
| Hash algorithm | SHA-256 minimum |
| Hashing performed at acquisition | Mandatory |
| Hashing performed at storage | Mandatory |
| Hashing performed at transfer | Mandatory |
| Verification records retained | Mandatory |

---

## 9.2 Hash Validation Table

| Evidence ID | SHA-256 Hash | Verified By | Time UTC |
|---|---|---|---|
| | | | |

---

## 9.3 Integrity Failure Conditions

Immediate escalation required if:

| Condition | Risk |
|---|---|
| Hash mismatch detected | Integrity failure |
| Storage corruption detected | Evidence loss |
| Unauthorized access detected | Compliance violation |

---

# 10. Phase 4 – Evidence Documentation

Every evidence item must be formally documented.

---

## 10.1 Required Documentation

| Field | Mandatory |
|---|---|
| Evidence ID | Yes |
| Evidence description | Yes |
| Source system | Yes |
| Acquisition method | Yes |
| Collector | Yes |
| Date/time UTC | Yes |
| Hash value | Yes |
| Storage location | Yes |

---

## 10.2 Evidence Master Record Table

| Evidence ID | Description | Source | Collected By | Hash | Storage Location |
|---|---|---|---|---|---|
| | | | | | |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`

---

# 11. Phase 5 – Secure Storage

Evidence must be stored in approved repositories.

---

## 11.1 Storage Requirements

| Requirement | Standard |
|---|---|
| Encrypted at rest | Mandatory |
| Access controlled | Mandatory |
| Tamper-resistant storage | Mandatory |
| Physical access controlled (if physical) | Mandatory |
| Backup maintained | Mandatory |

---

## 11.2 Approved Storage Locations

| Storage Type | Example |
|---|---|
| Forensic evidence vault | Secure server |
| Encrypted external drives | Forensic transport |
| Cloud-based forensic storage | Cloud evidence repository |
| Physical evidence safe | Hardware media |

---

## 11.3 Storage Tracking Table

| Evidence ID | Storage Location | Custodian | Access Restricted |
|---|---|---|---|
| | | | |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

# 12. Phase 6 – Evidence Transfer

Evidence transfers must be documented thoroughly.

---

## 12.1 Transfer Requirements

| Requirement | Mandatory |
|---|---|
| Transfer authorization | Yes |
| Transfer timestamp | Yes |
| Transferring party | Yes |
| Receiving party | Yes |
| Hash re-verification | Yes |
| Storage location confirmation | Yes |

---

## 12.2 Transfer Documentation Table

| Evidence ID | Transferred From | Transferred To | Time UTC | Verified Hash |
|---|---|---|---|---|
| | | | | |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`

---

## 12.3 Transfer Risk Conditions

Transfers must be re-validated if:

| Condition | Risk |
|---|---|
| Transit through external network | Integrity risk |
| Transfer to third-party investigator | Compliance risk |
| Transfer to law enforcement | Legal coordination |
| Transfer to client (MSSP) | Confidentiality risk |

---

# 13. Phase 7 – Evidence Access Logging

All evidence access must be logged.

---

## 13.1 Required Logging Areas

| Area | Mandatory |
|---|---|
| User access | Yes |
| Access timestamp | Yes |
| Action taken | Yes |
| Duration of access | Yes |

---

## 13.2 Access Log Table

| Evidence ID | Accessed By | Action | Time UTC | Duration |
|---|---|---|---|---|
| | | | | |

---

## 13.3 Unauthorized Access Escalation Triggers

Immediate escalation required if:

| Condition | Risk |
|---|---|
| Unauthorized access detected | Compliance failure |
| Storage tampering identified | Integrity loss |
| Hash mismatch identified | Forensic failure |

---

# 14. Phase 8 – Evidence Retention and Destruction

Evidence lifecycle must follow approved retention rules.

---

## 14.1 Retention Categories

| Evidence Type | Retention Period |
|---|---|
| Routine investigations | 1–3 years |
| Major incidents | 7 years |
| Regulatory cases | As per legal requirement |
| Legal hold | Until released |
| MSSP client evidence | Per contract |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`

---

## 14.2 Destruction Requirements

| Requirement | Mandatory |
|---|---|
| Authorized destruction approval | Yes |
| Cryptographic erasure or shredding | Yes |
| Destruction record maintained | Yes |
| Witness verification | Recommended |

---

## 14.3 Destruction Tracking Table

| Evidence ID | Destruction Date | Destroyed By | Method |
|---|---|---|---|
| | | | |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Destruction-SOP.md`

---

# 15. Legal Hold Considerations

Legal hold suspends standard retention rules.

---

## 15.1 Legal Hold Activation Conditions

| Trigger | Reason |
|---|---|
| Active litigation | Legal requirement |
| Regulatory investigation | Compliance |
| Law enforcement involvement | Legal coordination |
| Internal disciplinary action | HR/Legal |

---

## 15.2 Legal Hold Responsibilities

| Responsibility | Owner |
|---|---|
| Legal hold activation | Legal Counsel |
| Hold notification | IR Team Lead |
| Hold enforcement | Custodian |
| Hold release | Legal Counsel |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

---

# 16. MSSP-Specific CoC Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain client evidence segregation | Confidentiality |
| Use client-specific evidence labeling | Compliance |
| Follow client retention requirements | Contract compliance |
| Restrict cross-client visibility | Data protection |
| Coordinate client legal requirements | Legal alignment |

---

# 17. Common Chain-of-Custody Mistakes

| Mistake | Operational/Legal Risk |
|---|---|
| Weak hashing practices | Integrity failure |
| Missing transfer documentation | Legal inadmissibility |
| Improper storage | Evidence corruption |
| Unauthorized access | Compliance violation |
| Weak access logging | Audit failure |
| Premature destruction | Legal exposure |

---

# 18. Related Documents

| Document | Path |
|---|---|
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| CoC Master Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md` |
| CoC Transfer Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| Evidence Retention Schedule | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md` |
| Evidence Destruction SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Destruction-SOP.md` |

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