# Tool Chain of Custody

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Tool Chain of Custody |
| Document ID | TOOL-FOR-005 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | IR Team Lead / Digital Forensics Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines how forensic tools, acquisition kits, and controlled media are managed with a **Tool Chain of Custody** process to ensure:

- Tool integrity (tools have not been altered or tampered with)
- Repeatability and defensibility of forensic actions
- Prevention of cross-case and cross-client contamination (especially MSSP)
- Audit readiness for investigations and regulatory inspections

Tool custody is critical because:

- Compromised tools can corrupt evidence or produce unreliable results
- Untracked tool usage can create legal/audit challenges
- Shared portable media can leak data between incidents or tenants
- Offline acquisition kits are often used in high-impact incidents and must be controlled

This SOP ensures:

- Controlled storage, issuance, usage logging, and return of forensic kits/tools
- Integrity verification for tool media and scripts
- Secure handling of removable media used in evidence collection
- Clear accountability for who had which tool, when, and for what case

---

# 3. Scope

This SOP applies to:

| Asset Type | Examples |
|---|---|
| Offline acquisition kits | External drives, write blockers, boot media, cable sets |
| Portable tool media | USBs with acquisition tools, bootable forensic OS |
| Forensics workstations | Dedicated IR/forensics laptops and desktops |
| Tool repositories | Internal tool server, signed tool packages |
| Scripts and collectors | KAPE modules, collection scripts, parsing scripts |
| Licenses/dongles (if any) | Commercial tool license keys/dongles |

Out of scope:

- Evidence chain-of-custody for collected data (handled under Evidence/CoC SOPs)
- General IT asset management (covered by IT policies)

---

# 4. Definitions

| Term | Definition |
|---|---|
| Tool custody | Accountability record of tool possession and usage |
| Tool kit | Packaged set of tools/media used for forensics acquisition |
| Golden media | Verified clean baseline tool media, hashed and controlled |
| Integrity verification | Ensuring tools match approved hashes/signatures |
| Contamination | Unintended mixing of data or tool artifacts across cases/clients |
| Break-glass | Emergency use of tools outside normal issuance workflow with post-review |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| Digital Forensics Lead | Owns tool inventory and custody controls; approves changes |
| IR Team Lead | Ensures custody is followed during incidents; approves break-glass use |
| Evidence Custodian | Stores tools in secure location; manages issuance/return logs |
| L3 Forensics Analyst | Checks out tools; validates integrity; logs usage per case |
| L2 Analyst (authorized) | Uses limited kits as approved; follows logging requirements |
| SOC Manager | Oversight; ensures audit readiness and quarterly review execution |
| MSSP Service Delivery | Confirms tenant restrictions; ensures no cross-client tool contamination |

---

# 6. Tool Custody Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Controlled storage | Tools must be stored securely when not in use |
| Accountable issuance | Every tool checkout must be logged |
| Integrity assurance | Hash/signature validation must be performed routinely |
| Cleanliness | Tools/media must not store client data post-use |
| Least sharing | Dedicated kits preferred for sensitive clients/incidents |
| Segregation | MSSP: avoid reusing portable media across clients without sanitization |
| Audit logging | Custody logs must be retained per policy |
| Break-glass is exceptional | Emergency use must be justified and reviewed |

---

# 7. Tool Inventory Register (Mandatory)

Maintain a **Tool Inventory Register** (controlled document or asset system) containing:

| Field | Requirement |
|---|---|
| Tool/Kit ID | Mandatory (unique) |
| Description | Mandatory |
| Serial number / asset tag | Mandatory where applicable |
| Owner/custodian | Mandatory |
| Storage location | Mandatory |
| Contents list | Mandatory for kits |
| Tool versions (for software media) | Mandatory |
| Hashes/signatures | Mandatory for golden media |
| License details (if applicable) | Mandatory |
| Status | Available / Checked out / Under maintenance / Retired |
| Last integrity check date | Mandatory |
| Next review date | Mandatory |

---

# 8. Storage Requirements (Mandatory)

Tools and kits must be stored:

- In a secured cabinet/locker or restricted room
- With access limited to authorized personnel
- With an access log (physical or electronic)
- In a condition that prevents tampering (sealed kits where feasible)

Minimum controls:

| Control | Requirement |
|---|---|
| Physical security | Locked storage |
| Access list | Approved users only |
| Environmental protection | Protect from heat/moisture damage |
| Tamper evidence | Seals/labels for kits (recommended) |

---

# 9. Checkout / Issuance Procedure

## 9.1 Preconditions (Mandatory)

Before checkout:

| Check | Requirement |
|---|---|
| Request linked to incident/ticket ID | Mandatory |
| Requester authorized | Mandatory |
| Intended use documented | Mandatory |
| Client/tenant scope documented (MSSP) | Mandatory |
| Expected return date/time | Mandatory |

## 9.2 Checkout Steps (Mandatory)

1. Evidence custodian verifies requester identity
2. Tool/kit ID confirmed and recorded
3. Custody log entry created with:
   - Incident/ticket ID
   - Requester name/role
   - Checkout time (UTC)
   - Intended use
   - Destination (site/client)
   - Condition of kit (seal intact, components present)
4. Requester signs/acknowledges receipt (physical or electronic)

## 9.3 Custody Log (Minimum Fields)

| Field | Requirement |
|---|---|
| Tool/Kit ID | Mandatory |
| Checked out by | Mandatory |
| Checkout time (UTC) | Mandatory |
| Ticket/Incident ID | Mandatory |
| Client/Tenant ID (MSSP) | Mandatory if applicable |
| Purpose | Mandatory |
| Storage media IDs included | Mandatory |
| Expected return time | Mandatory |
| Approved by | Mandatory for high-risk kits |
| Notes | Optional |

---

# 10. Tool Integrity Verification

## 10.1 Integrity Check Requirements

| Tool Type | Integrity Check | Frequency |
|---|---|---|
| Golden USB/boot media | Hash verification | Before use + quarterly |
| Scripts/collectors | Hash/signature verification | Before deployment + after updates |
| Forensic workstation image | Baseline validation | Quarterly or after major incident |
| Hardware write blockers | Functional verification | Quarterly |

## 10.2 Integrity Check Procedure (Minimum)

1. Verify tool package version against approved list
2. Verify hash/signature matches the approved baseline
3. Record results in tool inventory register:
   - Date/time (UTC)
   - Checker name
   - Tool ID
   - Result (pass/fail)
   - Actions taken if fail

If integrity fails:

- Remove from service immediately
- Notify Forensics Lead and SOC Manager
- Investigate potential tampering
- Replace with verified media
- Document incident and corrective actions

---

# 11. Usage Rules (During Investigations)

## 11.1 Mandatory Usage Documentation

During tool use, the analyst must document in the incident ticket:

| Item | Requirement |
|---|---|
| Tool/kit ID | Mandatory |
| Tool name and version | Mandatory |
| Usage time window (UTC) | Mandatory |
| Actions performed | Mandatory |
| Outputs generated | Mandatory |
| Any anomalies/errors | Mandatory |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

## 11.2 Data Contamination Controls (Mandatory)

| Control | Requirement |
|---|---|
| No evidence stored on tool media | Mandatory unless media is dedicated evidence drive |
| Dedicated evidence drives | Must be labeled and tracked separately |
| Sanitization after use | Mandatory for reusable media |
| MSSP segregation | Do not reuse portable tool media across clients without sanitization and approval |
| Malware sample isolation | Keep malware samples in dedicated isolated storage |

---

# 12. Return Procedure (Mandatory)

Upon return:

1. Custodian receives tool/kit and verifies:
   - All components present
   - Seal status (if used)
   - Physical condition
2. Requester confirms:
   - No client data remains on tool media
   - Any issues encountered are recorded
3. Custodian updates custody log with:
   - Return time (UTC)
   - Condition
   - Any missing/damaged components
   - Any sanitization required/performed

If sanitization is required:

- Perform secure wipe procedure (documented)
- Re-verify integrity for golden media where applicable
- Update inventory status to “Available” after completion

---

# 13. Break-Glass (Emergency) Tool Use

Break-glass use is allowed only when:

- Immediate response is required (P1)
- Normal issuance process is not feasible
- IR Team Lead authorizes the action (or SOC Lead if IR unavailable)

Break-glass requirements:

| Requirement | Standard |
|---|---|
| Document justification | Mandatory |
| Document tools used | Mandatory |
| Document times (UTC) | Mandatory |
| Post-incident review within 48 hours | Mandatory |
| Update custody logs retroactively | Mandatory |

Reference:
`03_SOC-TIER-PROCEDURES/03.4_SOC-Lead-Procedures/SOCLead-P1-P2-Bridge-Call-SOP.md`

---

# 14. Tool Updates and Change Control

All tool updates must be controlled:

| Change | Requirement |
|---|---|
| Add new tool | Approval by Forensics Lead + SOC Manager |
| Update tool version | Change record + integrity baseline update |
| Retire tool | Document reason; remove from repository/kits |
| Modify scripts | Version control + hashing + peer review |

---

# 15. Retention of Custody Records

Custody logs and integrity check records must be retained according to evidence retention policy and audit requirements.

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`

---

# 16. MSSP Client Requirements (Mandatory)

For MSSP operations:

| Requirement | Standard |
|---|---|
| Client/tenant ID recorded in custody log | Mandatory |
| Avoid cross-client reuse of portable media | Mandatory unless sanitized and approved |
| Client restrictions on tooling honored | Mandatory |
| Client evidence handling requirements followed | Mandatory |
| Custody records available for client audit (sanitized) | As requested/contracted |

Reference:
`09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-Audit-Readiness-Checklist.md`

---

# 17. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Using untracked USB media | Contamination/audit failure | Custody log mandatory |
| No integrity check before use | Compromised tools | Pre-use validation |
| Storing evidence on tool media | Data leakage | Separate evidence drives only |
| Missing return checks | Kit drift and missing components | Return checklist |
| Cross-client tool reuse (MSSP) | Compliance breach | Segregation + sanitization |
| No break-glass documentation | Audit failure | Post-event logging requirement |

---

# 18. Related Documents

| Document | Path |
|---|---|
| Forensics Toolkit Reference | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Forensics-Toolkit-Reference.md` |
| Disk Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md` |
| Memory Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md` |
| Log Collection SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Log-Collection-SOP.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Tool Chain of Custody | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| Policy Exception Register | `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md` |

---

# 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | IR Team Lead / Digital Forensics Lead | Initial version |

---

# 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**