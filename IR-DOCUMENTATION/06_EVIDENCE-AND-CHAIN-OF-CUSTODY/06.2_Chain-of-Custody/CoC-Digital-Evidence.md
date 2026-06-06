# Chain of Custody (CoC) – Digital Evidence

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Chain of Custody (Digital Evidence) |
| Document ID | EVD-COC-001 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Evidence Custodian / Digital Forensics Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines the mandatory process for establishing and maintaining **Chain of Custody (CoC)** for **digital evidence** collected during security investigations and incident response.

Digital CoC is critical because:

- Evidence may be required for regulatory inquiries, audits, contractual disputes, or legal proceedings
- Digital artifacts are easy to copy/modify; CoC provides defensible integrity and accountability
- Mishandled evidence can invalidate findings or create legal/compliance exposure
- Certain incident types (breach/extortion/insider) require higher evidentiary standards
- MSSP operations require strict tenant segregation and controlled evidence handling

This SOP ensures:

- consistent CoC initiation criteria and procedures
- integrity verification (hashing) and documented custody transfers
- controlled access and secure storage of evidence-grade artifacts
- clear documentation linking ticket → evidence log → CoC records → transfers
- audit-ready evidence management for internal and MSSP client incidents

---

# 3. Scope

This SOP applies to **digital evidence** including (not limited to):

| Digital Evidence Type | Examples |
|---|---|
| Forensic acquisitions | Disk images (E01/RAW), memory dumps |
| Log evidence bundles | SIEM exports, firewall/proxy/DNS/VPN exports, cloud audit exports |
| Network evidence | PCAP, flow logs (when exported as evidence package) |
| Endpoint artifacts | Suspicious binaries/scripts, registry hives, triage packages |
| Email evidence | .eml/.msg files, headers, attachments/URLs (sanitized where needed) |
| Reporting artifacts | IOC lists, timelines, screenshots used as evidence |

Out of scope:

- Physical evidence CoC (handled under `CoC-Physical-Evidence.md`)
- Evidence storage/retention policy (handled under Evidence Storage documents)

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Physical-Evidence.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Chain of Custody (CoC) | A documented record of evidence collection, control, transfer, and storage from creation to disposition |
| Evidence custodian | Role responsible for secure evidence storage and controlled access |
| Evidence-grade | Evidence requiring integrity assurance and controlled custody (hash + transfer records) |
| Hash | Cryptographic checksum (SHA256 preferred) used to verify evidence integrity |
| Original evidence | The first preserved copy of the artifact (must not be modified) |
| Working copy | Copy used for analysis; created from the original and validated via hashes |
| Transfer | Any movement of evidence between people, systems, or locations |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| Evidence Custodian | Maintains CoC records; controls evidence repository access; validates transfer documentation |
| Digital Forensics Lead / L3 | Ensures evidence integrity; computes/validates hashes; creates working copies; advises on evidentiary needs |
| IR Team Lead | Confirms CoC triggers; authorizes evidence handling scope for major incidents |
| SOC Lead | Ensures ticket documentation; coordinates timelines and stakeholder needs |
| L2 Analyst | Collects/export evidence under guidance; documents parameters; hands off to custodian |
| Legal Counsel | Advises on legal hold, privilege, and external sharing; approves evidence disclosure |
| Compliance Lead | Ensures regulatory readiness; confirms record retention for audits |
| MSSP SDM | Ensures tenant/client segregation and client approval requirements (MSSP) |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`

---

# 6. CoC Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Integrity | Evidence must be protected from modification; hashes must verify integrity |
| Accountability | Every custody change must be documented (who/when/why) |
| Least handling | Minimize copying/movement; store originals securely and analyze working copies |
| Secure storage | Store evidence only in approved evidence vaults with access controls |
| Reproducibility | Evidence provenance and collection parameters must be documented |
| Separation of duties (recommended) | Collector ≠ custodian where feasible |
| Tenant segregation (MSSP) | Evidence must be stored and handled per client tenant without cross-client mixing |
| UTC timestamps | All CoC records must use UTC |

---

# 7. When CoC Is Required (Trigger Criteria)

CoC is mandatory for digital evidence when any apply:

## 7.1 Mandatory Triggers

| Trigger | Examples |
|---|---|
| P1/P2 major incident | ransomware, domain compromise, exfiltration |
| Regulatory reporting required/likely | RBI/CERT-In candidate incidents |
| Legal hold issued | suspected breach, extortion, litigation risk |
| Law enforcement engagement | evidence sharing planned/possible |
| Insider threat (HR/Legal sensitive) | employee misconduct leading to disciplinary/legal actions |
| Client contract requires evidence-grade handling | regulated MSSP clients |

## 7.2 Optional (Risk-Based) Triggers

- repeated incidents indicating systemic control failure
- high-value assets involved (core banking/payment/identity)
- high reputational risk cases

If uncertain: treat as CoC required and confirm with IR Team Lead / Legal.

---

# 8. CoC Artifacts and Forms (Repository Standards)

This folder provides the standardized CoC documentation set:

- **Master CoC Form:** `CoC-Master-Form.md`
- **Digital Evidence CoC Guidance:** (this document)
- **Transfer Form:** `CoC-Transfer-Form.md`
- **Physical Evidence CoC:** `CoC-Physical-Evidence.md` (separate SOP)

---

# 9. Digital Evidence CoC Workflow (End-to-End)

## 9.1 Step 1 — Create Evidence ID and Register the Artifact

Owner: Collector (L2/L3) + Evidence Custodian

Mandatory fields to register:

- Incident/Ticket ID
- Evidence ID (unique)
- Evidence type (log bundle, memory dump, disk image, PCAP)
- Source system/device
- Collection method
- Collector name/role
- Collection start/end time (UTC)
- Initial storage location (staging)
- Classification (Restricted/Confidential)

Recommended Evidence ID format:
- `EVD-[INC-ID]-[0001..]` (sequential per incident)

Example:
- `EVD-INC-2026-0102-0007`

---

## 9.2 Step 2 — Acquire and Preserve “Original Evidence”

Owner: Collector (L2/L3/Forensics)

Mandatory controls:

| Control | Requirement |
|---|---|
| Minimal modification | Collect using approved tooling and minimal interactions |
| Preserve acquisition logs | Mandatory where tools generate logs |
| Record export parameters | Mandatory for log exports (query, time window, scope) |
| Do not edit files | Originals must remain unchanged |

---

## 9.3 Step 3 — Hashing and Integrity Verification (Mandatory)

Owner: L3/Forensics or Evidence Custodian

Hash requirements:

| Evidence Type | SHA256 Required | Notes |
|---|---|---|
| Disk images | Yes | Always |
| Memory dumps | Yes | Always |
| PCAP (evidence-grade) | Yes | Always when CoC required |
| Log bundles (P1/P2/regulatory) | Yes | Required |
| Single SIEM CSV export | Yes (P1/P2) | Recommended for lower severity |
| Email files (.eml/.msg) | Yes when evidence-grade | Preserve original message file |

Rules:

- Record hash values in CoC record and evidence log
- If the artifact is archived/compressed later, re-hash the new package and record both hashes
- If transfer occurs, re-hash after transfer (recommended) to confirm integrity

---

## 9.4 Step 4 — Secure Storage and Custody Assignment

Owner: Evidence Custodian

Evidence must be moved to approved evidence storage:

- encrypted at rest
- access controlled (least privilege)
- access logging enabled for Restricted evidence (where feasible)
- tenant segregated (MSSP)

Custody assignment:

- Custodian records custody acceptance (time UTC, storage location)
- Collector hands off and documents transfer (use transfer form if custody changes)

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

## 9.5 Step 5 — Working Copy Creation (Analysis Use)

Owner: L3/Forensics

Rules:

- Do not analyze on the original evidence file
- Create a working copy in an analysis workspace
- Compute hash for working copy and record linkage to original
- Ensure working copy remains tenant-scoped (MSSP)

Minimum record:

- original evidence ID + hash
- working copy ID/path + hash
- who created it + time (UTC)

---

## 9.6 Step 6 — Evidence Transfers (Custody Changes)

Owner: Evidence Custodian

Transfers include:

- custodian → analyst
- analyst → external IR retainer
- organization → client (MSSP)
- organization → regulator/law enforcement (only if approved)

Mandatory actions for each transfer:

- complete transfer form
- verify recipient authorization
- record time (UTC), purpose, and method
- confirm hashes before/after transfer (recommended)
- record any access restrictions

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`

---

## 9.7 Step 7 — Closure, Retention, and Disposition

Owner: Evidence Custodian + Compliance/Legal

- Evidence retained per retention schedule and legal hold requirements
- Destruction only per approved destruction SOP after retention period and legal approval (if required)
- Record disposition (destroyed/archived/returned) with time (UTC) and approver

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Destruction-SOP.md`

---

# 10. Documentation Requirements (Mandatory)

## 10.1 Minimum Required CoC Record Elements (Digital)

| Field | Requirement |
|---|---|
| Evidence ID | Mandatory |
| Incident/Ticket ID | Mandatory |
| Evidence description | Mandatory |
| Source device/system | Mandatory |
| Collection date/time (UTC) | Mandatory |
| Collector name/role | Mandatory |
| Collection method/tool + version | Mandatory (where available) |
| Hash algorithm + hash values | Mandatory (SHA256) |
| Storage location | Mandatory |
| Custodian | Mandatory |
| Access restrictions | Mandatory |
| Transfer history | Mandatory (when applicable) |
| Notes | Optional (errors/limitations) |

## 10.2 Ticket-Level Logging (High-Level Only)

Incident ticket must reference:

- Evidence IDs
- Storage paths (or evidence vault reference IDs)
- Hash references (as appropriate)
- CoC form IDs/locations

Do not paste raw sensitive evidence into tickets.

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 11. MSSP Multi-Tenant Requirements (Mandatory)

For MSSP evidence CoC:

| Requirement | Standard |
|---|---|
| Tenant/client scope verified | Mandatory before collection and before any transfer |
| Evidence stored in client-specific repository | Mandatory |
| Client approval for transfer/disclosure | Mandatory (contract-dependent) |
| No cross-client identifiers | Mandatory (sanitization required) |
| Client-safe evidence references | Mandatory for client reporting |
| Separate CoC records per client incident | Mandatory |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 12. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Not hashing evidence | Integrity challenge | SHA256 mandatory for CoC evidence |
| Editing/renaming after hashing | Hash mismatch | Freeze originals; re-hash if changed |
| Analyzing originals | Contamination | Working copies only |
| Unlogged transfers | Audit/legal failure | Transfer form required |
| Storing evidence outside vault | Data leak | Approved storage only |
| Cross-client evidence mixing | Compliance breach | Tenant segregation controls |

---

# 13. Related Documents

| Document | Path |
|---|---|
| CoC Master Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md` |
| CoC Transfer Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md` |
| CoC Physical Evidence | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Physical-Evidence.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Digital Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Digital-Evidence-Handling.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| Third-Party IR Retainer Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Third-Party-IR-Retainer-Contacts.md` |
| Legal Counsel Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |

---

# 14. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Evidence Custodian / Digital Forensics Lead | Initial version |

---

# 15. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**