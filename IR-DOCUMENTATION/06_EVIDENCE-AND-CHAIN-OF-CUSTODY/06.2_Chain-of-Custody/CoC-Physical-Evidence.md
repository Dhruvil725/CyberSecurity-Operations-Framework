# Chain of Custody (CoC) – Physical Evidence

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Chain of Custody (Physical Evidence) |
| Document ID | EVD-COC-003 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Evidence Custodian / IR Team Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines the mandatory process for establishing and maintaining **Chain of Custody (CoC)** for **physical evidence** associated with security incidents.

Physical CoC is critical because:

- Physical items may be required for legal, regulatory, HR, or internal investigations
- Mishandling can compromise integrity, admissibility, and credibility of findings
- Physical evidence can be lost, tampered with, or accessed by unauthorized personnel
- Physical evidence often contains sensitive data (storage media, printouts, access cards)
- MSSP/onsite response may involve evidence collected from client premises requiring strict controls

This SOP ensures:

- standardized identification, packaging, labeling, and storage of physical evidence
- documented custody and transfer records for every movement of evidence
- secure storage and restricted access for physical artifacts
- integration with digital evidence handling where hybrid evidence exists (e.g., seized laptop)
- audit-ready evidence records

---

# 3. Scope

This SOP applies to physical evidence such as:

| Evidence Type | Examples |
|---|---|
| Storage media | HDD/SSD, USB drives, backup tapes, SD cards |
| Devices | Laptops, mobile phones, routers, IoT devices |
| Printed materials | Access logs, screenshots, documents, notes |
| Access artifacts | Access cards, badges, keys, tokens |
| Hardware components | Removed disks, write blockers (if used as evidence of tool chain) |
| CCTV/physical security artifacts | DVR drives, access control exports (physical media) |
| Tamper evidence | Seals, tamper tags, packaging labels |

Out of scope:

- Digital evidence CoC (handled separately)
- Physical incident response procedures (covered under physical incident playbook)

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`  
`01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/CAT-14-Physical-Security-Incident.md`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Physical evidence | Tangible item collected to support investigation |
| Evidence packaging | Bags/boxes used to secure evidence and prevent tampering |
| Tamper-evident seal | Seal that shows visible sign if opened |
| Evidence locker | Controlled physical storage location |
| Custody | Documented possession and responsibility |
| Evidence label | Unique identifier tag attached to evidence item |
| Hybrid evidence | Physical device containing digital evidence (e.g., laptop, phone) |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| Evidence Custodian | Maintains evidence locker, CoC records, check-in/check-out logs |
| IR Team Lead | Authorizes collection of physical evidence; coordinates investigations |
| SOC Manager | Oversight; approves sensitive collection decisions; coordinates management escalation |
| Physical Security / Facilities | Supports access to CCTV/access systems; provides physical support |
| IT Ops | Supports device handling and safe shutdown/transport guidance |
| HR + Legal Counsel | Insider/disciplinary cases; legal hold and disclosure constraints |
| MSSP SDM (if applicable) | Coordinates client approvals and onsite handling rules |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Internal-Contacts-Master.md`

---

# 6. Physical Evidence Handling Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Safety first | Do not place staff at risk; follow site safety policies |
| Preserve integrity | Prevent tampering, damage, and environmental exposure |
| Minimum handling | Handle as little as possible; avoid unnecessary power-on |
| Documentation | Record every custody change with UTC timestamps |
| Secure packaging | Use tamper-evident packaging and labels |
| Access control | Evidence stored in secure locker with limited access |
| Hybrid caution | Devices may contain volatile evidence; coordinate before shutdown |
| Tenant/client controls | MSSP: follow client site rules and approvals |

---

# 7. When Physical CoC Is Required (Triggers)

Physical CoC is mandatory when:

| Trigger | Examples |
|---|---|
| Insider threat investigations | unauthorized removal of assets, sabotage |
| Potential legal action | litigation or law enforcement involvement likely |
| Regulatory inquiry | evidence required for inspection/investigation |
| Device seizure | compromised laptop, rogue access device |
| Physical intrusion | unauthorized access to secure areas, theft |
| MSSP onsite response | client site evidence collection |

If unsure, treat as CoC required and escalate to Legal Counsel.

---

# 8. Physical Evidence Collection Workflow (End-to-End)

## 8.1 Step 1 — Authorization and Planning

Owner: IR Team Lead + Legal/HR (as applicable)

Before collection:

- confirm authority to collect/seize evidence item
- confirm whether legal hold applies
- confirm whether device contains volatile evidence (coordinate with forensics before shutdown)
- prepare packaging materials and labels
- identify safe transport and storage location

---

## 8.2 Step 2 — Identify and Label Evidence

Owner: Collector + Evidence Custodian (as available)

Mandatory label fields:

- Evidence ID (unique)
- Incident/Ticket ID
- Item description (device type, brand/model)
- Serial number / asset tag (if present)
- Location collected (site/room)
- Date/time collected (UTC)
- Collector name/role
- Classification (Restricted by default for devices/media)

Recommended Evidence ID format:
- `PHY-[INC-ID]-[0001..]`

Example:
- `PHY-INC-2026-0102-0002`

---

## 8.3 Step 3 — Photograph and Document Condition (Recommended)

Record:

- photographs of the item and any connected cables/ports
- photographs of serial numbers/asset tags
- condition notes (damage, tamper indicators)
- whether device is powered on/off

For powered-on devices, consult forensics guidance before powering off.

---

## 8.4 Step 4 — Package the Evidence (Mandatory)

Packaging requirements:

| Requirement | Standard |
|---|---|
| Use tamper-evident bag/box | Mandatory |
| Apply evidence label externally | Mandatory |
| Apply tamper seal | Mandatory |
| Record seal ID/number | Mandatory |
| Include anti-static packaging for electronics | Recommended |
| Avoid magnets/heat/moisture | Mandatory |

---

## 8.5 Step 5 — Transfer to Evidence Custodian (Mandatory)

- Evidence custodian must check-in the item
- CoC record must document:
  - time (UTC)
  - from/to
  - seal status
  - storage location assignment

Use the **CoC Transfer Form** for each transfer.

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`

---

## 8.6 Step 6 — Secure Storage (Mandatory)

Store physical evidence:

- in secured evidence locker/cabinet/room
- with access limited to custodian and approved individuals
- with check-in/check-out logging
- with environmental protections (where applicable)

Record:

- locker ID/location
- access restrictions
- custodian

---

## 8.7 Step 7 — Analysis and Handling of Hybrid Evidence (Devices)

If device requires forensic analysis:

- treat device as physical evidence (this SOP) and digital evidence (digital CoC)
- coordinate with forensics for:
  - disk imaging
  - memory capture (if possible and approved)
- document any actions that change device state
- create working copies for analysis; preserve originals

References:  
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md`

---

## 8.8 Step 8 — Disposition (Return/Archive/Destruction)

Disposition must follow:

- legal hold status
- retention schedule
- client/organizational policy

Disposition options:

- return to owner (document authorization)
- long-term archive storage
- secure destruction (if approved and legally permitted)

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Destruction-SOP.md`

---

# 9. Documentation Requirements (Mandatory)

For each physical evidence item, record:

| Field | Requirement |
|---|---|
| Evidence ID | Mandatory |
| Incident/Ticket ID | Mandatory |
| Item description | Mandatory |
| Serial/asset tag | Mandatory if available |
| Collection location | Mandatory |
| Collector identity | Mandatory |
| Collection time (UTC) | Mandatory |
| Seal ID and status | Mandatory |
| Storage location | Mandatory |
| Transfer history | Mandatory |
| Final disposition | Mandatory |

Use CoC Master Form + Transfer Form references.

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`

---

# 10. MSSP and Onsite Collection Considerations (Mandatory)

For MSSP onsite collection:

- obtain client authorization and document it
- follow client site security rules
- ensure evidence remains tenant-scoped
- coordinate with client legal/security contacts
- avoid removing devices/media from client site without written approval (contract-dependent)

References:  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/MSSP-Client-Contacts.md`  
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 11. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| No tamper seal / missing seal ID | Integrity challenge | Tamper-evident packaging required |
| Missing serial/asset tag | Identification issues | Document identifiers and photos |
| Unlogged transfers | Audit/legal failure | Transfer form mandatory |
| Storing evidence unsecured | Loss/tampering | Evidence locker required |
| Powering off device without forensics coordination | Volatile evidence loss | Coordinate with forensics/IR lead |
| Removing client device without approval (MSSP) | Contract breach | Written approval required |

---

# 12. Related Documents

| Document | Path |
|---|---|
| CoC Digital Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| CoC Master Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md` |
| CoC Transfer Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| Disk Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md` |
| Memory Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md` |
| Insider Threat HR/Legal Coordination | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md` |

---

# 13. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Evidence Custodian / IR Team Lead | Initial version |

---

# 14. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**