# SOP: Log Evidence Collection and Handling

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Log Evidence Collection and Handling |
| Document ID | EVD-COL-003 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Evidence Custodian / SOC Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential / Restricted (case-dependent) |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines how to collect, preserve, validate, store, and reference **log evidence** used in investigations, incident response, regulatory reporting, and audits.

Log evidence is critical because:

- Logs provide the primary timeline for attacker activity and response actions
- Logs often roll over quickly, requiring early preservation
- Incorrect time zone handling can invalidate timelines and conclusions
- Evidence integrity must be protected when logs are used for regulatory or legal purposes
- MSSP operations require strict client/tenant segregation and controlled exports

This SOP ensures:

- Consistent log collection standards across SIEM, endpoints, network, identity, and cloud
- Reproducible evidence (queries, filters, time windows documented)
- UTC timestamp standardization
- Evidence-grade integrity controls (hashing and CoC when required)
- Secure storage and access controls aligned to evidence policy

---

# 3. Scope

This SOP applies to log evidence collected from:

| Source Category | Examples |
|---|---|
| SIEM | Correlation alerts, raw events exports |
| Endpoint/Server | Windows EVTX, Sysmon, Linux auth/syslog |
| Identity | AD/DC logs, IdP/SSO/MFA logs |
| Network | Firewall, proxy, VPN, DNS, IDS/IPS logs |
| Cloud | Audit logs, flow logs, storage access logs |
| Email | Message trace, gateway logs |
| Security tools | EDR event exports, DLP/CASB logs |

Out of scope:

- Disk imaging and memory acquisition evidence (handled by separate SOPs)
- Continuous SIEM ingestion engineering (handled by SIEM procedures)

References:  
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Log-Collection-SOP.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Log evidence | Log exports preserved as investigation artifacts |
| Export parameters | Query/filter, time window, and scope used to produce an export |
| UTC | Coordinated Universal Time; mandatory standard for incident timelines |
| Integrity hash | SHA256 checksum used to validate evidence integrity |
| Evidence-grade | Evidence requiring strong integrity controls (hash + CoC as needed) |
| Retention risk | Risk logs will be overwritten/rotated before export |
| Tenant | MSSP client environment |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L1 Analyst | Ensure alert IDs and timestamps captured; request urgent preservation when needed |
| L2 Analyst | Define collection scope; run exports/queries; validate completeness; document parameters |
| L3/Forensics | Validate integrity; support complex sources; ensure evidence-grade handling |
| SOC Lead | Prioritize sources for P1/P2; ensure SLA timelines and documentation quality |
| Evidence Custodian | Controls evidence storage; manages access; ensures retention compliance |
| Compliance/Legal | Determines if evidence-grade handling/CoC is required; reviews external sharing |
| MSSP SDM | Ensures client approvals and tenant segregation in MSSP contexts |

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

# 6. Log Evidence Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Collect early | For P1/P2, export logs immediately to prevent rotation loss |
| Reproducible exports | Record exact query/filter and time window |
| UTC standard | All exported time windows must be UTC or converted to UTC and documented |
| Integrity protection | Hash evidence packages when evidence-grade |
| Store originals | Keep raw exports unchanged; analyze copies where needed |
| Secure storage | Evidence repository only; access-controlled |
| Tenant segregation (MSSP) | Client evidence must be separated and correctly tagged |

---

# 7. Log Evidence Priority (By Severity)

## 7.1 P1/P2 Minimum Log Sources (As Applicable)

Collect within first hours where possible:

- SIEM raw event export + correlation context
- EDR telemetry exports (if used as “logs”)
- Identity logs (AD/DC, SSO/MFA)
- Firewall/proxy/VPN/DNS logs for IOCs and bytes
- Cloud audit logs (API actions)
- Email security logs (phishing/BEC)

## 7.2 P3/P4 Log Sources (Targeted)

Collect only the required subset to confirm FP/TP and document rationale.

---

# 8. Evidence-Grading Decision (When Hash/CoC Required)

Log evidence is treated as **evidence-grade** when:

| Condition | Examples |
|---|---|
| Regulatory reporting required/likely | CERT-In, RBI related incidents |
| Legal hold issued | Breach/extortion/insider cases |
| Law enforcement engagement | Evidence to be shared |
| P1/P2 with significant impact | Domain compromise, ransomware |
| Client contract requires | Regulated client conditions |

Evidence-grade requirements:

- SHA256 hash of exported log bundle
- Controlled access
- Chain-of-custody for transfers (when applicable)

References:  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`

---

# 9. Collection Workflow (Standard)

## 9.1 Step 1 — Define the Log Collection Window

Owner: L2/L3

Minimum guidance:

- P1/P2: capture **±24 hours** around detection (or more if suspected dwell time)
- Include:
  - first seen time (if known)
  - detection time
  - containment start and end times
  - last observed malicious activity time

Record the window in UTC and document any timezone conversion.

---

## 9.2 Step 2 — Identify Log Sources and Entities

Owner: L2

Define:

- Which systems (hosts, users, services) are in scope
- Which log sources can validate each hypothesis (entry point, lateral movement, exfil)
- Which log fields are required (src/dst, action, bytes, process, user, event id)

---

## 9.3 Step 3 — Export Logs (Preferred Order)

Preferred order (to reduce rotation risk):

1. Volatile/short-retention sources (firewall buffers, VPN gateways)
2. Cloud audit logs (API action windows)
3. SIEM raw exports (may be retained but still export early for evidence)
4. Endpoint/server logs (EVTX/journal)
5. Email tracing logs (if relevant)

---

## 9.4 Step 4 — Record Export Parameters (Mandatory)

For every export, record:

| Parameter | Requirement |
|---|---|
| Tool/platform | Mandatory (SIEM, firewall, cloud console) |
| Query/filter used | Mandatory (exact string or screenshot) |
| Time range (UTC) | Mandatory |
| Entities | Mandatory (hosts/users/IPs) |
| Export format | Mandatory (CSV/JSON/EVTX) |
| Export filename | Mandatory |
| Export location | Mandatory |
| Collector | Mandatory |
| Export time (UTC) | Mandatory |

---

## 9.5 Step 5 — Validate Export Completeness

Owner: L2/L3

Validation checks:

- File is not empty and contains expected fields
- Time window aligns to requested range
- Entity identifiers match (hostname normalization, user IDs)
- Any known gaps are documented (e.g., “DNS logs not available for window”)

---

## 9.6 Step 6 — Hash and Store (Evidence-Grade)

Owner: Evidence Custodian / L3

If evidence-grade:

- Bundle exports into a package (ZIP/TAR)
- Compute SHA256 hash for the package
- Store in evidence repository with restricted access
- Record hash and storage path in ticket and evidence log

---

# 10. Source-Specific Collection Guidance (Minimum Standards)

## 10.1 SIEM Exports

Must include:

- triggering alert context
- raw events supporting the alert
- related events for scope expansion
- query used and time window

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md`

## 10.2 Windows EVTX

Preferred logs (as applicable):

- Security, System, Application
- Sysmon
- PowerShell logs (if enabled)
- RDP and logon events

Export as EVTX and avoid opening/editing original log files.

## 10.3 Linux Logs

Collect:

- auth logs
- syslog/journal exports
- web logs (if relevant)

Record timezone and OS version.

## 10.4 Network Logs

Collect:

- firewall allow/deny with rule references
- proxy URL logs with bytes
- VPN auth logs
- DNS query logs

Record device name and interface/zone context.

## 10.5 Cloud Logs

Collect:

- audit log events for affected principals
- key/role changes
- storage access logs
- flow logs (if enabled)

Record tenant/subscription/account IDs.

---

# 11. Storage and Naming Standards

## 11.1 Storage Location Requirements

- Evidence repository only
- Access-controlled
- Tenant-segregated (MSSP)

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

## 11.2 Naming Convention (Recommended)

`INC-[ID]_LOG_[SOURCE]_[ENTITY]_[YYYYMMDD_HHMM]UTC.[ext]`

Examples:

- `INC-2026-0102_LOG_SIEM_export_FIN-WS-12_20260530_0415UTC.csv`
- `INC-2026-0102_LOG_Firewall_outbound_20260530_0400UTC.json`

---

# 12. MSSP Multi-Tenant Requirements (Mandatory)

| Requirement | Standard |
|---|---|
| Client ID in ticket and export metadata | Mandatory |
| Exports must be tenant-scoped | Mandatory |
| Separate storage paths and ACLs | Mandatory |
| Client approval (if required) | Mandatory for sensitive sources |
| Client-safe references | Ensure client can access only what is intended |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 13. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Not recording query/time window | Non-reproducible evidence | Export parameters mandatory |
| Local timezone confusion | Incorrect timeline | UTC mandatory + conversion notes |
| Logs exported too late | Loss due to rotation | P1/P2 prioritization |
| Evidence modified during review | Integrity loss | Store originals; analyze copies |
| Missing hashing for evidence-grade | Evidence challenge | SHA256 mandatory |
| Cross-tenant exports (MSSP) | Compliance breach | Tenant verification checklist |

---

# 14. Related Documents

| Document | Path |
|---|---|
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Digital Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Digital-Evidence-Handling.md` |
| Memory Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Memory-Evidence-SOP.md` |
| Network Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Network-Evidence-SOP.md` |
| CoC Digital Evidence | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| SIEM Query Library | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md` |
| Log Collection SOP (Forensics Tools) | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Log-Collection-SOP.md` |

---

# 15. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Evidence Custodian / SOC Lead | Initial version |

---

# 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**