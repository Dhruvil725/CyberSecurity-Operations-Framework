# Evidence Storage Policy

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Policy – Evidence Storage |
| Document ID | EVD-STR-001 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Evidence Custodian / SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This policy defines the mandatory requirements for **secure storage, access control, integrity protection, retention alignment, and audit readiness** of evidence collected during investigations and incident response.

Evidence storage is critical because:

- Evidence often contains sensitive data (credentials, PII, customer data, proprietary data)
- Evidence must remain available and verifiable for audits, regulatory inquiries, and legal needs
- Inadequate storage controls increase risk of tampering, loss, unauthorized disclosure, or cross-tenant leakage (MSSP)
- Storage decisions impact chain-of-custody defensibility and operational readiness
- Evidence must be retained and destroyed according to defined schedules and legal holds

This policy ensures:

- approved storage locations and minimum security controls
- consistent naming, indexing, and traceability to incident tickets and CoC forms
- role-based access and access logging for sensitive artifacts
- encryption, backup, and integrity controls for evidence vaults
- tenant segregation requirements for MSSP clients
- alignment with evidence retention and destruction procedures

---

# 3. Scope

This policy applies to all evidence stored for incident response and investigations, including:

| Evidence Type | Examples |
|---|---|
| Digital evidence | logs, exports, screenshots, email files, IOC lists |
| Forensic evidence | disk images, memory dumps, triage bundles |
| Network evidence | PCAP, flow exports, firewall/proxy bundles |
| CoC documentation | CoC master forms, transfer forms |
| Incident comms artifacts | status updates, regulatory submission copies |

Out of scope:

- Non-security operational data unrelated to incidents
- General enterprise backups unless used specifically for evidence preservation

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Evidence repository / evidence vault | Approved storage system used for storing evidence |
| Restricted evidence | Highly sensitive artifacts (memory dumps, disk images, customer data) |
| Evidence-grade | Evidence requiring integrity controls (hashing) and often CoC |
| Legal hold | Instruction to preserve evidence beyond normal retention/destruction |
| Tenant segregation | Separation of client evidence for MSSP operations |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| Evidence Custodian | Owns evidence vault administration, access provisioning, evidence indexing, retention coordination |
| SOC Manager | Governance oversight; approves access exceptions and emergency access |
| IR Team Lead | Ensures evidence is stored and referenced correctly; confirms CoC triggers |
| L2/L3 Analysts | Store evidence in correct location; follow naming/packaging rules; do not store locally |
| Legal Counsel | Defines legal hold scope; approves external disclosures and evidence transfers |
| Compliance Lead | Ensures evidence readiness for audits/regulators; validates retention compliance |
| MSSP SDM | Ensures client evidence storage segregation and contract constraints |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`

---

# 6. Evidence Storage Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Approved locations only | Evidence must be stored only in approved vaults/repositories |
| Encrypt and restrict | Encryption at rest + role-based access required |
| Integrity preserved | Originals must not be modified; hashes recorded where required |
| Traceability | Evidence must be linked to incident ticket and evidence IDs |
| Access is logged | Restricted evidence access must be logged |
| Backups for evidence vault | Evidence storage must be backed up and recoverable |
| Tenant segregation (MSSP) | Separate storage areas and ACLs per client |
| No local storage | No evidence on analyst desktops or unsecured shares |

---

# 7. Approved Evidence Storage Locations

## 7.1 Evidence Vault Types (Examples)

Approved evidence storage may include:

- dedicated secure file server / evidence vault
- encrypted object storage bucket with strict ACLs and audit logs
- dedicated forensic evidence management system
- offline encrypted storage (for highly sensitive cases)

Each organization must document its actual storage platforms and access model.

## 7.2 Prohibited Storage Locations (Mandatory)

Evidence must not be stored in:

- analyst personal devices or desktops
- unencrypted removable media (unless evidence drive with CoC controls)
- consumer file-sharing services
- email attachments or public links
- shared folders without access control

---

# 8. Access Control Requirements

## 8.1 Role-Based Access (Minimum Standard)

| Evidence Type | Minimum Access |
|---|---|
| Restricted (disk/memory/customer data) | IR/Forensics + Evidence Custodian + Legal (need-to-know) |
| Confidential (logs/exports) | SOC/IR teams (need-to-know) |
| Internal (sanitized summaries) | SOC + relevant IT stakeholders |

## 8.2 Access Provisioning Rules

| Rule | Requirement |
|---|---|
| Access must be ticketed | Mandatory |
| Time-bound access | Recommended for Restricted evidence |
| Least privilege | Mandatory |
| Separation of duties | Custodian should control access provisioning |
| Access revocation | Mandatory upon role change/offboarding |

## 8.3 Access Logging

For Restricted evidence:

- access logs must capture user, time (UTC), action, and artifact reference
- logs must be retained per retention schedule

---

# 9. Evidence Organization and Naming Standards

## 9.1 Folder Structure (Recommended)

`/evidence/INC-[ID]/`
- `logs/`
- `edr/`
- `network/`
- `memory/`
- `disk/`
- `reports/`
- `coc/`
- `comms/`

## 9.2 Naming Convention (Recommended)

`INC-[ID]_[TYPE]_[SOURCE/ASSET]_[YYYYMMDD_HHMM]UTC.[ext]`

Examples:
- `INC-2026-0102_LOG_SIEM_export_20260530_0415UTC.csv`
- `INC-2026-0102_MEM_FIN-WS-12_20260530_0415UTC.raw`
- `INC-2026-0102_PCAP_exfilSuspect_20260530_0430UTC.pcap`

## 9.3 Evidence Indexing (Mandatory)

For every incident, maintain an evidence index (can be a file or ticket section) capturing:

- Evidence ID
- Artifact description
- Storage path/reference
- Hash (if applicable)
- CoC references (if applicable)

---

# 10. Integrity Controls (Hashing and Originals)

## 10.1 Originals vs Working Copies

| Artifact | Rule |
|---|---|
| Original evidence | Must remain unchanged; stored in vault |
| Working copy | Used for analysis; linked to original via hash |

## 10.2 Hashing Requirements

SHA256 required for:

- disk images
- memory dumps
- evidence-grade log bundles
- PCAP (evidence-grade)
- any evidence transferred externally (when approved)

Record hashes in:

- ticket evidence references
- evidence index
- CoC forms (when required)

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`

---

# 11. Backup and Recovery Requirements (Evidence Vault)

Evidence vault must have:

| Requirement | Standard |
|---|---|
| Backup schedule | Defined and tested |
| Restore testing | Quarterly or per policy |
| Integrity checks | Periodic validation of stored evidence hashes (risk-based) |
| RPO/RTO | Defined for evidence vault availability |
| Disaster recovery | Documented for evidence vault platform |

---

# 12. Retention and Legal Holds

Evidence retention must follow:

- evidence retention schedule
- legal hold instructions (override retention/destruction)
- contractual requirements (MSSP)

If legal hold exists:

- evidence must not be destroyed
- retention end date must be adjusted/blocked
- access must be restricted and monitored

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

---

# 13. MSSP Tenant Segregation Requirements (Mandatory)

| Requirement | Standard |
|---|---|
| Separate client storage roots | Mandatory |
| Separate ACLs per client | Mandatory |
| No cross-client evidence bundles | Mandatory |
| Client approval for evidence export/transfer | Mandatory (contract-dependent) |
| Client-specific retention | Mandatory when required by contract/regulation |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md`

---

# 14. Evidence Transfer and External Sharing Controls

External sharing is permitted only with:

- legal and compliance approval (as required)
- CoC transfer documentation (when evidence-grade)
- secure transfer method
- documented scope of disclosure (minimum necessary)

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`

---

# 15. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Evidence stored on local devices | Loss/leak | Approved vault only |
| No access logging | Unauthorized access undetected | Enable access logs for Restricted evidence |
| No naming/structure | Evidence cannot be found | Folder + naming standards |
| Originals modified | Integrity failure | Originals read-only; working copy rule |
| Cross-client storage (MSSP) | Compliance breach | Tenant segregation requirements |
| Retention not enforced | Audit finding | Retention schedule + custodian ownership |

---

# 16. Related Documents

| Document | Path |
|---|---|
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Digital Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Digital-Evidence-Handling.md` |
| CoC Digital Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| Evidence Retention Schedule | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md` |
| Evidence Destruction SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Destruction-SOP.md` |
| MSSP Client Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md` |

---

# 17. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Evidence Custodian / SOC Manager | Initial version |

---

# 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**