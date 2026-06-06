# SOP: Evidence Collection

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Evidence Collection |
| Document ID | EVD-COL-001 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | IR Team Lead / Evidence Custodian |
| Approved By | CISO |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines the standard process for collecting evidence during security investigations and incident response, ensuring evidence is:

- identified and prioritized correctly,
- collected safely and consistently,
- preserved with integrity,
- stored securely,
- traceable and audit-ready, and
- handled according to chain-of-custody (CoC) requirements where applicable.

Evidence collection is critical because:

- Evidence supports incident confirmation, scoping, containment decisions, and RCA
- Improper collection can destroy volatile data or alter artifacts
- Regulatory reporting and audits require defensible evidence handling and documentation
- Legal proceedings may require chain-of-custody and integrity verification (hashing)
- MSSP operations require strict client/tenant segregation and controlled evidence access

This SOP ensures:

- consistent evidence collection standards across SOC tiers and IR/forensics teams
- defined evidence priority by incident severity (P1/P2 vs P3/P4)
- standardized evidence logging, labeling, and storage procedures
- secure evidence transfer and retention alignment
- clear escalation and approvals for evidence-grade collection activities

---

# 3. Scope

This SOP applies to evidence collection for:

| Evidence Category | Examples |
|---|---|
| Endpoint evidence | EDR telemetry exports, file artifacts, triage packages |
| Server evidence | OS logs, application logs, database logs, configs (sanitized) |
| Network evidence | firewall/proxy logs, PCAP, IDS/IPS exports |
| Identity evidence | AD/DC logs, IAM logs, SSO/MFA logs |
| Cloud evidence | audit logs, flow logs, storage access logs |
| Email evidence | headers, message trace, attachments/URLs (sanitized) |
| Forensics evidence | memory dumps, disk images, hash lists |
| Communications evidence | notification timestamps, approvals, bridge call notes |

Out of scope:

- Detailed forensic acquisition steps for disk/memory (covered in Forensics Tools SOPs)
- Legal hold issuance process (covered under legal engagement SOP; referenced here)

References:  
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Evidence | Data collected to support investigation, response, audit, or legal needs |
| Artifact | Specific data item (log export, file, screenshot, PCAP) |
| Volatile evidence | Evidence lost on reboot/power-off (RAM, live connections) |
| Integrity | Evidence unchanged from collection to analysis (verified via hashing) |
| Hash | Cryptographic checksum (SHA256 preferred) |
| CoC | Chain of custody documenting control and transfer of evidence |
| Evidence repository | Approved secure storage location for evidence packages |
| Tenant | Client environment in MSSP operations |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L1 Analyst | Capture initial evidence references (alert IDs, screenshots); ensure ticket has timestamps |
| L2 Analyst | Define evidence needs; collect/export logs and telemetry; ensure evidence references are complete |
| L3/Forensics Analyst | Evidence-grade collection (memory/disk); integrity hashing; advanced artifact validation |
| IR Team Lead | Authorizes evidence scope; ensures preservation prior to containment where feasible |
| SOC Lead | Coordinates urgency and SLA; ensures evidence tasks are assigned and tracked |
| Evidence Custodian | Owns evidence storage, access control, retention, and CoC records |
| Compliance/Legal | Determines legal hold and disclosure constraints; reviews evidence sharing |
| MSSP SDM | Ensures client approvals and tenant segregation for evidence handling |

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

# 6. Evidence Handling Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Preserve first | Prioritize evidence collection before disruptive containment where feasible |
| Minimize contamination | Use approved tools and minimal interactions with target systems |
| Integrity validation | Hash evidence packages for P1/P2 and evidence-grade artifacts |
| Complete documentation | Every artifact must be referenced in ticket and evidence log |
| Least disclosure | Do not expose sensitive data beyond need-to-know |
| Secure storage | Store evidence only in approved repositories with access control |
| CoC when required | Use chain-of-custody for legal/regulatory sensitive cases |
| UTC standard | All timestamps must be recorded in UTC |
| MSSP segregation | Evidence must be client/tenant segregated, always |

---

# 7. Evidence Collection Priority (By Severity)

## 7.1 P1/P2 Evidence Priorities (Immediate)

Collect as early as possible:

- EDR detection details + process tree + timeline export
- SIEM raw events + correlation context (± context window)
- Identity logs (AD/IdP/MFA) related to affected accounts
- Network logs (firewall/proxy/DNS) for suspicious destinations and volumes
- Volatile evidence (memory capture) if credential theft/in-memory malware suspected
- Disk imaging if persistence/root cause requires deep analysis (as approved)
- Communication records (management/client notifications, approvals)

## 7.2 P3/P4 Evidence Priorities (Targeted)

Collect evidence sufficient for:

- confirming FP/TP decisions,
- documenting rationale for closure,
- enabling tuning/improvements if needed.

---

# 8. Ticketing and Evidence Traceability Requirements (Mandatory)

Every evidence activity must be linked to an incident ticket.

Minimum ticket requirements:

| Item | Requirement |
|---|---|
| Incident/ticket ID | Mandatory |
| Evidence request time (UTC) | Mandatory |
| Collector name/role | Mandatory |
| Artifact description | Mandatory |
| Source system/tool | Mandatory |
| Time window (UTC) | Mandatory (for logs) |
| Storage location reference | Mandatory |
| Hashes (SHA256) | Mandatory for P1/P2 evidence packages and forensic artifacts |
| CoC required? | Mandatory (Yes/No) |
| Access restrictions | Mandatory (who can access evidence) |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 9. Evidence Collection Workflow (End-to-End)

## 9.1 Step 1 — Identify Evidence Requirements

Owner: L2/L3/IR Team

Define:

- What must be proven/answered (scope, entry point, persistence, exfil, lateral movement)
- Which sources can answer each question
- The time window to collect (UTC)
- Priority order (volatile first)

## 9.2 Step 2 — Obtain Approvals (If Required)

Approvals required when:

- collecting disk/memory from critical systems
- shutting down systems to preserve evidence
- collecting from regulated/sensitive environments
- collecting in MSSP context where client approval required
- sharing evidence externally

References:  
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

## 9.3 Step 3 — Collect Evidence (Use Category SOPs)

Follow the appropriate category SOP:

- Logs: `Log-Evidence-SOP.md`
- Memory: `Memory-Evidence-SOP.md`
- Network: `Network-Evidence-SOP.md`
- Digital handling: `Digital-Evidence-Handling.md`

For forensic disk/memory acquisition, use:
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/`

## 9.4 Step 4 — Validate Integrity (Hashing)

- SHA256 hashing required for evidence-grade items
- Record hashes in ticket and evidence log
- Re-hash after transfers where feasible

## 9.5 Step 5 — Store and Restrict Access

- Store in approved evidence repository
- Apply access controls (least privilege)
- Apply tenant segregation for MSSP
- Record storage path and custodian

## 9.6 Step 6 — Document and Maintain Evidence Log

Maintain an evidence log entry per artifact with:

- artifact ID
- description
- collector
- times
- hashes
- storage path
- transfers (if any)

## 9.7 Step 7 — Evidence Transfer (If Required)

- Use secure transfer
- Update chain-of-custody records
- Confirm recipient authorization
- Record transfer times and custody handoff

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`

---

# 10. Evidence Classification and Access Control (Mandatory)

## 10.1 Evidence Sensitivity Levels (Guidance)

| Level | Examples | Access |
|---|---|---|
| Restricted | Memory dumps, disk images, customer data | IR/Forensics + Legal only |
| Confidential | SIEM exports, EDR reports, network logs | SOC/IR on need-to-know |
| Internal | Sanitized summaries and non-sensitive artifacts | SOC + relevant teams |

## 10.2 Access Rules

- Use role-based access wherever possible
- Log access for Restricted evidence
- Do not share Restricted evidence via email/chat

---

# 11. Evidence Quality Standards (Mandatory)

Every artifact must be:

- reproducible (query recorded or export parameters documented),
- time-bounded (UTC start/end),
- attributable (who collected),
- integrity-protected (hash when required),
- stored securely with consistent naming.

Recommended naming convention:

`INC-[ID]_[SOURCE]_[ASSET]_[YYYYMMDD_HHMM]UTC.[ext]`

Examples:
- `INC-2026-0102_SIEM_EXPORT_FinWS12_20260530_0415UTC.zip`
- `INC-2026-0102_EDR_TIMELINE_FinWS12_20260530_0430UTC.json`

---

# 12. MSSP Multi-Tenant Requirements (Mandatory)

For MSSP evidence:

| Requirement | Standard |
|---|---|
| Client ID tagged in ticket and evidence | Mandatory |
| Client-segregated storage paths | Mandatory |
| No cross-client artifacts | Mandatory |
| Client approval for sensitive collection | Mandatory (contract-dependent) |
| Secure transfer method per client agreement | Mandatory |
| Client evidence retention constraints | Mandatory if specified |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md`

---

# 13. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Collecting too late | Logs overwritten | P1/P2 early collection priority |
| No UTC timestamps | Timeline errors | UTC mandatory standard |
| No query/export parameters | Non-reproducible evidence | Record queries/filters |
| Missing hashes | Integrity risk | SHA256 mandatory for evidence-grade |
| Storing evidence locally | Loss/leak | Evidence repository only |
| Cross-client evidence mixing (MSSP) | Compliance breach | Tenant segregation controls |
| No CoC when required | Legal/audit issues | CoC triggers enforced |

---

# 14. Related Documents

| Document | Path |
|---|---|
| Digital Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Digital-Evidence-Handling.md` |
| Log Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Log-Evidence-SOP.md` |
| Memory Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Memory-Evidence-SOP.md` |
| Network Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Network-Evidence-SOP.md` |
| CoC Digital Evidence | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| Legal Counsel Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |

---

# 15. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | IR Team Lead / Evidence Custodian | Initial version |

---

# 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**