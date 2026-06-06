# MSSP Client Evidence Handling

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – MSSP Client Evidence Handling |
| Document ID | EVD-STR-004 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | MSSP Service Delivery Manager (SDM) / Evidence Custodian |
| Approved By | SOC Manager |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines how evidence is collected, stored, accessed, transferred, retained, and destroyed for **MSSP-managed client incidents** in a way that ensures:

- strict tenant/client segregation,
- contractual and regulatory compliance,
- audit readiness,
- secure evidence handling practices aligned with the organization’s IR standards.

MSSP client evidence handling is critical because:

- cross-client evidence leakage is a severe compliance and contractual breach
- clients may have regulated data (BFSI, healthcare, government) with strict handling obligations
- client approvals may be required before certain collections (disk/memory/PCAP)
- evidence may need to be shared with clients, their auditors, regulators, or external IR retainers
- data residency requirements may restrict where evidence can be stored or processed
- MSSP reporting depends on accurate, traceable evidence records

This SOP ensures:

- consistent client evidence governance and procedures
- clear responsibilities between MSSP and client (RACI alignment)
- secure client evidence packaging and transfer processes
- retention/destruction aligned to contract and legal holds
- reliable audit artifacts for client compliance reviews

---

# 3. Scope

This SOP applies to evidence associated with MSSP client incidents and investigations:

| Evidence Type | Examples |
|---|---|
| Logs | SIEM exports, firewall/proxy/DNS/VPN logs, cloud audit exports |
| Endpoint/EDR | EDR detections, timeline exports, quarantined file hashes |
| Network evidence | PCAP, flow logs, IDS/IPS exports |
| Forensic evidence | memory dumps, disk images, triage bundles |
| Communication records | client notifications, approvals, bridge call notes |
| Regulatory artifacts | CERT-In/RBI support drafts, submissions where authorized |

Out of scope:

- client internal evidence handling procedures (unless MSSP is operating under client policies)
- non-client internal incidents (covered by standard evidence policy)

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`  
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Tenant | Client’s logically separated environment (SIEM/EDR/data storage) |
| Client evidence | Any artifact collected from/for a client investigation |
| Data residency | Legal/contract requirement for where data must be stored/processed |
| Client approval | Client authorization required before specific evidence actions |
| Evidence package | Collection of artifacts + metadata + hash manifest + references |
| Sanitization | Removal of unrelated sensitive content before sharing |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| MSSP SDM | Owns client comms and approvals tracking; ensures SLA compliance |
| Evidence Custodian | Manages client evidence vault areas, access controls, retention/destruction |
| SOC Lead | Ensures tenant verification before actions; ensures ticket documentation |
| IR Team Lead | Approves high-impact collections; ensures CoC and evidence-grade handling |
| L2/L3 Analysts | Collect/export evidence in tenant; document parameters; package with hashes |
| Legal Counsel | Advises on disclosures, cross-border constraints, and privilege |
| Compliance Lead | Advises on regulatory requirements for client; supports report readiness |
| Client POC | Provides approvals, requests, and instructions; may control regulator submissions |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/MSSP-Client-Contacts.md`  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`

---

# 6. Mandatory MSSP Evidence Handling Principles

| Principle | Requirement |
|---|---|
| Tenant verification first | Confirm correct client/tenant before any evidence collection/export/share |
| Segregation by design | Separate storage roots and ACLs per client |
| Minimum necessary collection | Collect only what is required for investigation and obligations |
| Secure storage | Encrypt at rest; strict access control and access logging |
| Evidence integrity | Hash evidence packages (SHA256) for P1/P2 and evidence-grade items |
| CoC enforcement | CoC required for legal/regulatory sensitive client incidents |
| Controlled sharing | Do not share evidence externally without approvals and secure transfer |
| Contract-driven | Follow client contract for notification, approvals, retention, and reporting |

---

# 7. Client Evidence Segregation Controls (Mandatory)

## 7.1 Storage Segregation

Evidence must be stored using:

- dedicated per-client root paths, e.g.:
  - `/evidence/clients/CLIENT-ABC/INC-.../`
- separate ACLs per client evidence area
- separate encryption keys (where feasible and required)

## 7.2 Processing Segregation

- Do not process client evidence on shared environments that risk cross-client contamination
- Use client-scoped analysis workspaces when handling Restricted artifacts (memory/disk)

## 7.3 Identity and Access Segregation

- Analysts must access only the tenants/clients assigned
- Temporary access must be time-bound and approved
- Access logs must be retained per retention policy

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 8. Client Evidence Collection Approvals (Contract-Driven)

## 8.1 Common Client Approval Requirements (Guidance)

| Evidence Action | Typical Approval Needed? |
|---|---|
| Export SIEM logs | Usually No (if MSSP operates SIEM) |
| Export EDR telemetry | Usually No (if MSSP operates EDR) |
| Network PCAP capture | Often Yes |
| Disk imaging | Yes |
| Memory acquisition | Yes |
| Accessing sensitive systems | Yes |
| Sharing evidence with third party | Yes + Legal |

## 8.2 Approval Documentation (Mandatory)

For approvals, record:

- approval request time (UTC)
- approver (name/title)
- approval result (approved/denied/conditional)
- constraints (e.g., “do not isolate,” “only after-hours”)
- time (UTC) and method (email/phone/portal)

Record approvals in incident ticket and, if needed, attach approval evidence to client evidence package.

---

# 9. Evidence Packaging Standards (Client Evidence Packages)

Client evidence packages must include:

## 9.1 Mandatory Package Contents

| Item | Requirement |
|---|---|
| Evidence artifacts | Mandatory |
| Evidence index | Mandatory (list artifacts and descriptions) |
| Export parameters | Mandatory (queries/filters/time windows) |
| Hash manifest (SHA256) | Mandatory for evidence-grade |
| Collection notes | Mandatory (collector, times, tools) |
| CoC references | Mandatory if CoC required |
| Sanitization notes | Mandatory if redactions were performed |

## 9.2 Naming Convention (Recommended)

`CLIENT-[ID]_INC-[ID]_EVDPKG_[YYYYMMDD_HHMM]UTC.zip`

Example:
`CLIENT-ABC_INC-2026-0102_EVDPKG_20260530_0600UTC.zip`

---

# 10. Client Evidence Transfer and Sharing

## 10.1 Approved Transfer Methods (Mandatory)

Use only approved methods:

- client secure portal / client ticketing attachment mechanism (if approved)
- encrypted file transfer portal with MFA
- encrypted removable media with CoC (for highly sensitive)
- secure cloud object storage with strict ACLs (client-specific)

Do not use:

- plain email attachments
- public links
- non-approved messaging apps

## 10.2 Transfer Controls (Mandatory)

| Control | Requirement |
|---|---|
| Client authorization verified | Mandatory |
| Recipient identity verified | Mandatory |
| Minimum necessary evidence shared | Mandatory |
| Hash manifest included | Mandatory for evidence-grade |
| CoC transfer form completed | Mandatory when CoC required |
| Transfer logged in ticket | Mandatory |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`

---

# 11. Retention and Destruction (Client Evidence)

## 11.1 Retention Requirements

Client evidence retention is:

- defined by contract, and
- must meet minimum retention schedule if contract is silent.

If client requires longer retention, apply longer retention and document.

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`

## 11.2 Destruction Requirements

Evidence destruction must:

- meet secure destruction standards
- require approvals (MSSP SDM + Evidence Custodian + client where required)
- respect legal holds and regulatory inquiries

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Destruction-SOP.md`

---

# 12. Regulatory Reporting Support (Client Context)

If the client is RBI/CERT-In regulated:

- MSSP provides evidence package and technical write-up support
- client typically submits regulator report unless MSSP is authorized in writing
- ensure evidence shared is tenant-scoped and sanitized

References:  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`

---

# 13. Documentation Requirements (Ticket-Level) (Mandatory)

Incident ticket must include:

| Item | Requirement |
|---|---|
| Client ID and tenant verification note | Mandatory |
| Evidence IDs and storage paths | Mandatory |
| Approvals (client) | Mandatory where required |
| Transfers (what/when/to whom) | Mandatory |
| Hash references | Mandatory for evidence-grade |
| CoC references | Mandatory when applicable |
| Retention/destruction notes | Mandatory if actioned |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 14. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Cross-client evidence stored together | Severe compliance breach | Separate roots + ACLs + reviews |
| Sharing evidence without approval | Contract breach | Approval workflow mandatory |
| No hash manifest | Integrity challenge | SHA256 manifest required |
| Evidence transferred via email | Data leak | Approved secure transfer only |
| Retention mismatched to contract | Audit finding | Contract mapping + retention schedule enforcement |
| No client tenant verification | Wrong client notified/shared | Tenant verification checklist |

---

# 15. Related Documents

| Document | Path |
|---|---|
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| Evidence Retention Schedule | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md` |
| Evidence Destruction SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Destruction-SOP.md` |
| CoC Digital Evidence | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| CoC Transfer Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md` |
| Internal-to-MSSP Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md` |
| MSSP Client Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/MSSP-Client-Contacts.md` |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |

---

# 16. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | MSSP SDM / Evidence Custodian | Initial version |

---

# 17. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**