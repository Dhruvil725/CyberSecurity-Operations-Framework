# Digital Evidence Handling (Guidelines)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Guideline – Digital Evidence Handling |
| Document ID | EVD-COL-002 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Evidence Custodian / IR Team Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This document defines the mandatory handling rules for **digital evidence** collected during security investigations and incident response, including:

- integrity protection (hashing),
- secure storage and access control,
- evidence labeling and traceability,
- secure transfer,
- prevention of evidence contamination,
- MSSP tenant segregation.

Digital evidence handling is critical because:

- Evidence can be challenged during audits, regulatory inquiries, or legal proceedings
- Improper handling can alter artifacts and invalidate conclusions
- Sensitive evidence often contains credentials, PII, proprietary data, or regulated information
- MSSP operations have high risk of cross-tenant disclosure without strict controls
- Evidence must remain accessible, verifiable, and protected throughout the incident lifecycle

This guideline ensures:

- evidence is defensible, consistent, and audit-ready
- analysts follow standard do’s/don’ts for handling evidence artifacts
- evidence storage and transfer follow security and compliance requirements
- chain-of-custody triggers are understood and applied

---

# 3. Scope

This guideline applies to all digital evidence types, including:

| Evidence Type | Examples |
|---|---|
| Logs and exports | SIEM exports, firewall logs, cloud audit logs |
| Endpoint artifacts | EDR timelines, suspicious files, registry hives |
| Forensic acquisitions | disk images, memory dumps |
| Network artifacts | PCAP, NetFlow exports |
| Communications | phishing emails, headers, screenshots |
| Configuration snapshots | firewall rules, IAM policies (sanitized) |
| Reports | incident summaries, IOC lists, timelines |

Out of scope:

- Physical evidence handling (separate CoC physical evidence document)
- Evidence destruction process (covered under evidence destruction SOP)

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Physical-Evidence.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Destruction-SOP.md`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Evidence integrity | Evidence remains unchanged from time of collection |
| Evidence contamination | Unintended modification or mixing of evidence |
| Hash | Cryptographic checksum to verify integrity (SHA256 preferred) |
| Evidence repository | Approved secure storage location for evidence |
| CoC | Chain of Custody record of evidence possession and transfers |
| Sanitization | Removing/redacting sensitive information not required for purpose |
| Tenant segregation | Separation of client evidence in MSSP contexts |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| Evidence Custodian | Controls evidence repository access; validates storage; manages transfers and retention |
| IR Team Lead | Ensures evidence handling follows policy; confirms CoC triggers |
| L2/L3 Analysts | Collect evidence; compute hashes; document artifacts and context; avoid contamination |
| SOC Lead | Ensures ticket documentation and evidence references are complete |
| Legal Counsel | Advises on legal hold, disclosure restrictions, privilege handling |
| Compliance Lead | Ensures evidence readiness for regulatory reporting and audits |
| MSSP SDM | Ensures tenant segregation and client evidence handling requirements |

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

---

# 6. Evidence Handling Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Integrity first | Protect evidence from modification; hash where required |
| Minimum necessary | Collect/store only what is needed to support investigation and obligations |
| Secure by default | Evidence stored encrypted and access-controlled |
| Traceability | Every artifact must be linked to incident ticket and evidence log |
| Reproducibility | Exports and queries must be repeatable (document parameters) |
| Segregation (MSSP) | Store client evidence separately; never mix |
| Controlled sharing | No external sharing without approvals; use secure transfer only |
| UTC standard | All timestamps must be UTC and recorded consistently |

---

# 7. Evidence Categories and Handling Requirements

## 7.1 Evidence Sensitivity Levels (Guidance)

| Level | Typical Content | Handling Requirement |
|---|---|---|
| Restricted | Memory dumps, disk images, credentials, customer data | Access limited to IR/Forensics + Legal; CoC often required |
| Confidential | SIEM/EDR exports, network logs, investigation notes | Need-to-know access; hashing for P1/P2 packages |
| Internal | Sanitized summaries, IOC bulletins | Broader internal access, still controlled |

---

# 8. Evidence Collection and Preservation Controls

## 8.1 Evidence Labeling (Mandatory)

Each evidence artifact must have:

- Incident ID
- Evidence ID (unique per artifact)
- Collector name/role
- Date/time collected (UTC)
- Source system/tool
- Short description
- Classification level
- Storage location reference
- Hash value(s) (when required)

Recommended Evidence ID format:

`EVD-[INC-ID]-[0001..]`

Example:
`EVD-INC-2026-0102-0007`

---

## 8.2 Hashing Requirements (Mandatory)

SHA256 hashing is required for:

- disk images
- memory dumps
- PCAP files (when evidence-grade)
- log bundles exported manually
- any evidence shared externally (when permitted)

Hashing guidance:

| Artifact Type | Hash Required? | Notes |
|---|---|---|
| Disk image | Yes | Always |
| Memory dump | Yes | Always |
| SIEM export (CSV/JSON) | Yes for P1/P2 | Recommended otherwise |
| EDR timeline export | Yes for P1/P2 | Recommended otherwise |
| Screenshots | Recommended | Especially if used in reporting |
| Email (.eml/.msg) | Yes if evidence-grade | Preserve headers and body |

Important:
- If evidence is re-zipped/repackaged, re-hash the new package and record both hashes.

---

## 8.3 Time Standard (UTC)

All evidence-related timestamps must be recorded in UTC:

- collection time
- export time window
- transfer time
- analysis time (for major findings)

If source logs are in local time:

- record the timezone and offset
- document conversion method and any suspected clock drift

---

# 9. Evidence Storage Rules (Mandatory)

## 9.1 Approved Storage Locations

Evidence must be stored only in approved repositories:

- secure evidence file store
- forensic evidence vault
- tenant-scoped MSSP evidence storage (for clients)

Do not store evidence on:

- local desktops
- personal drives
- unsecured shared folders
- non-approved cloud file sharing tools

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

## 9.2 Naming Conventions (Recommended)

Use consistent naming:

`INC-[ID]/[evidence-type]/[asset]/[YYYYMMDD]/[artifact-name]`

Examples:

- `INC-2026-0102/logs/FIN-WS-12/20260530/siem-export.csv`
- `INC-2026-0102/memory/FIN-WS-12/20260530/FIN-WS-12_MEM_20260530_0415UTC.raw`
- `INC-2026-0102/disk/SRV-APP-01/20260530/SRV-APP-01_DISK_E01.e01`

---

## 9.3 Access Control Requirements

| Control | Requirement |
|---|---|
| Role-based access | Mandatory |
| Separate access for Restricted evidence | Mandatory |
| Access logging | Mandatory for Restricted evidence |
| Temporary access | Time-bound; documented approval |
| MSSP tenant separation | Mandatory (separate storage paths and ACLs) |

---

# 10. Evidence Transfer Rules (Mandatory)

Evidence transfer is allowed only when:

- recipient is authorized and verified
- method is secure and approved
- transfer is documented (CoC if required)
- evidence integrity is verified after transfer (re-hash recommended)

Approved transfer methods (examples):

- secure file transfer portal (authenticated + encrypted)
- encrypted removable media with custody controls
- secure cloud bucket with strict ACLs (tenant-scoped)

Never transfer evidence via:

- plain email attachments
- public file sharing links
- unencrypted USB drives
- unapproved messaging apps

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`

---

# 11. Chain-of-Custody (CoC) Triggers

CoC is required when any apply:

| Trigger | Examples |
|---|---|
| P1/P2 with regulatory/legal risk | breach, extortion |
| Insider threat involving HR/legal | disciplinary/legal proceedings likely |
| Law enforcement engagement | evidence to be shared |
| Client contract requires forensic-grade handling | regulated client requirements |
| Evidence may be used in court | litigation expected |

CoC requirements:

- evidence ID and description
- hash value(s)
- collector identity and time (UTC)
- every transfer recorded (who/when/why)
- storage location and custodian

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`

---

# 12. Sanitization and Redaction (Mandatory When Sharing)

When sharing evidence with:

- management,
- clients (MSSP),
- vendors,
- regulators,
- law enforcement,

apply sanitization principles:

- remove unrelated PII
- remove credentials/tokens
- remove unrelated internal IP ranges (if unnecessary)
- include only relevant excerpts and evidence references

Any sanitization must be documented:

- what was removed
- why
- who performed sanitization
- time (UTC)

---

# 13. MSSP Multi-Tenant Requirements (Mandatory)

For MSSP operations:

| Requirement | Standard |
|---|---|
| Evidence stored per client tenant | Mandatory |
| No cross-client artifacts in bundles | Mandatory |
| Client approval for sensitive evidence actions | Mandatory (contract-dependent) |
| Client-safe references | Mandatory (no internal-only links the client can’t access unless agreed) |
| Sharing controls | Must follow contract and TLP restrictions |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 14. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Editing evidence files | Integrity loss | Write-protect; keep originals unchanged |
| No hashes for key artifacts | Evidence challenge | SHA256 mandatory where required |
| Storing evidence locally | Data leak/loss | Approved evidence repository only |
| Mixing tenants (MSSP) | Compliance breach | Tenant segregation controls |
| Untracked transfers | Audit failure | CoC + transfer logging |
| No export parameters | Non-reproducible evidence | Record queries/filters/time windows |

---

# 15. Related Documents

| Document | Path |
|---|---|
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Log Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Log-Evidence-SOP.md` |
| Memory Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Memory-Evidence-SOP.md` |
| Network Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Network-Evidence-SOP.md` |
| CoC Digital Evidence | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| MSSP Client Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md` |

---

# 16. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Evidence Custodian / IR Team Lead | Initial version |

---

# 17. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**