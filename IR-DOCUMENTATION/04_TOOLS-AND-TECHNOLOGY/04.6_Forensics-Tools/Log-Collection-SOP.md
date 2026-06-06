# SOP: Log Collection (Forensic / Incident Response)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Log Collection (Forensic / IR) |
| Document ID | TOOL-FOR-003 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | IR Team Lead / Digital Forensics Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the standardized process to **identify, collect, preserve, validate, store, and reference logs** required for security investigations and incident response.

Log collection is critical because:

- Logs form the primary evidence layer for detection validation, scoping, and root cause analysis
- Poor collection practices lead to missing timelines, incomplete scope, and audit gaps
- Logs can be overwritten quickly (short retention / rolling buffers)
- Evidence integrity requires controlled handling, timestamps, and (when applicable) hashing
- MSSP operations require strict tenant segregation and client-specific evidence handling

This SOP ensures:

- Consistent collection standards across OS, network, cloud, and security tooling
- Time-bound, priority-driven collection aligned to P1/P2 response needs
- Evidence traceability (what collected, who collected, when, how, and where stored)
- Secure storage and chain-of-custody alignment where required
- Audit-ready documentation for ISO/NIST/RBI-aligned IR operations

---

# 3. Scope

This SOP applies to log collection for:

| Environment | Examples |
|---|---|
| Endpoint | Windows/macOS/Linux endpoints |
| Server | AD/DC, application servers, database servers, file servers |
| Network | Firewall, proxy, VPN, IDS/IPS, DNS, DHCP, NAC |
| Cloud | CloudTrail/Activity logs, IAM logs, VPC flow logs, storage access logs |
| Security tools | SIEM, EDR, email security, CASB, DLP |
| SaaS | M365 audit logs, IdP logs, SSO logs (where applicable) |

Log collection types:

- Remote collection (preferred when reliable and secure)
- Local collection (onsite/remote access)
- Export from consoles (SIEM/EDR/cloud portals)
- Snapshot/export from cloud logging services

Out of scope:

- Disk imaging and memory acquisition (separate SOPs)
- Long-term SIEM ingestion engineering (covered under SIEM procedures)

---

# 4. Definitions

| Term | Definition |
|---|---|
| Artifact | Any collected data point used as evidence (logs, exports, screenshots) |
| EVTX | Windows Event Log file format |
| UTC | Coordinated Universal Time; mandatory timestamp standard |
| Integrity hash | Cryptographic checksum (SHA256 preferred) |
| Evidence repository | Approved secure storage for investigation evidence |
| CoC | Chain of Custody |
| Collection window | Time range for logs to be collected |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L1 Analyst | Opens ticket; documents initial context; triggers immediate log preservation requests |
| L2 Analyst | Defines log scope; executes/coordinates collection; validates completeness |
| L3 Forensics Analyst | Performs evidence-grade collection; ensures integrity controls; supports complex sources |
| SOC Lead | Prioritizes and coordinates collection in P1/P2; ensures SLA alignment |
| IR Team Lead | Authorizes evidence collection scope for major incidents; ensures CoC requirements |
| SIEM Engineer | Provides SIEM exports, correlation results, raw log extracts (as needed) |
| EDR Admin | Provides EDR telemetry exports and endpoint timelines |
| IT Ops / System Owner | Provides access, credentials, and change windows; supports host access |
| Evidence Custodian | Manages secure storage, access, retention, and evidence transfers |
| MSSP Service Delivery | Ensures client approvals/constraints; tenant segregation; communications |

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 6. Log Collection Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Collect early | Logs roll over; prioritize collection immediately for P1/P2 |
| Define scope | Collect only relevant sources but ensure timeline completeness |
| Use UTC | All time references must be in UTC (convert and document if needed) |
| Preserve integrity | Use hashes for exported logs when evidence-grade |
| Avoid modification | Prefer export/copy over opening/editing in-place |
| Maintain traceability | Every log set must map to ticket and evidence log |
| Secure handling | Encrypt transfers; restrict access; tenant segregation (MSSP) |
| Document limitations | If logs are missing/rotated, document explicitly |

---

# 7. Collection Triggers (When to Collect Logs)

Log collection should start when:

| Trigger | Examples |
|---|---|
| P1/P2 incident declared | Ransomware, breach, privileged compromise |
| Suspicious activity requiring scoping | Lateral movement, persistence |
| Threat intel match with high confidence | Known C2 infrastructure |
| Regulatory reporting likely | Data breach indicators, service disruption |
| Evidence preservation requirement | Insider threat, legal involvement |

---

# 8. Ticket and Evidence Documentation Requirements (Mandatory)

Every log collection activity must be linked to an incident ticket.

Minimum ticket fields:

| Field | Requirement |
|---|---|
| Incident/Ticket ID | Mandatory |
| Collection request time (UTC) | Mandatory |
| Collector name/role | Mandatory |
| Systems/log sources | Mandatory |
| Collection window (UTC) | Mandatory (start/end) |
| Method | Remote/local/export |
| Tools used | Name/version (where applicable) |
| Output location | Evidence repository path/reference |
| Hashes | SHA256 for evidence-grade exports |
| Access restrictions | Mandatory |
| CoC required? | Yes/No with rationale |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

# 9. Log Collection Prioritization (By Severity)

## 9.1 Priority Targets (Guidance)

| Priority | Minimum Log Sources to Collect (as applicable) |
|---|---|
| P1 | EDR telemetry, Windows Security logs/ Sysmon, AD/DC logs, firewall/proxy/VPN, DNS, cloud audit logs, email logs, SIEM raw events |
| P2 | EDR + key host logs + relevant network logs + SIEM extracts |
| P3 | Host logs + SIEM correlation + limited network logs (as needed) |
| P4 | SIEM alert evidence + minimal supporting logs |

## 9.2 SLA Targets (Guidance)

| Priority | Start Collection Target | Notes |
|---|---:|---|
| P1 | ≤ 30 minutes | Begin preservation/exports immediately |
| P2 | ≤ 2 hours | Collect high-value sources first |
| P3 | ≤ 8 hours | Within shift where feasible |
| P4 | ≤ 72 hours | Routine collection if needed |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

# 10. Pre-Collection Checklist (Mandatory)

Before collecting:

| Check | Requirement |
|---|---|
| Confirm affected systems, users, and timeline | Mandatory |
| Identify required log sources (host/network/cloud/tool) | Mandatory |
| Confirm retention risk (overwrite/rollover) | Mandatory |
| Confirm access method and credentials | Mandatory |
| Confirm time sync status (NTP drift concerns) | Recommended |
| Confirm data sensitivity (PII/financial/regulated) | Mandatory |
| Confirm tenant/client scope (MSSP) | Mandatory |
| Prepare evidence repository location | Mandatory |
| Confirm CoC requirement | Mandatory |

---

# 11. Standard Log Sources (Collection Checklist)

> Select applicable sources based on incident type.

## 11.1 Windows (Endpoints/Servers)

Recommended logs/artifacts:

- Windows Security Event Logs (EVTX)
- System and Application logs
- PowerShell logs (Module/Script Block if enabled)
- Sysmon logs (if deployed)
- RDP/Logon events
- Scheduled task logs
- Windows Defender / AV logs (if applicable)

## 11.2 Linux

Recommended logs/artifacts:

- `/var/log/auth.log` or `/var/log/secure`
- syslog/journal logs
- SSH logs
- sudo logs
- web server logs (nginx/apache) if relevant
- cron logs
- package manager logs (apt/yum) if relevant

## 11.3 Identity and Access / Directory Services

- AD/DC Security logs
- ADFS/IdP logs (if applicable)
- IAM audit logs (cloud)
- SSO/MFA logs

## 11.4 Network and Perimeter

- Firewall traffic logs (allow/deny)
- Proxy logs (URL, user, bytes)
- DNS resolver logs
- VPN logs
- IDS/IPS alerts/logs
- WAF logs (if applicable)

## 11.5 Cloud / SaaS (as applicable)

- Cloud audit logs (API actions)
- Storage access logs (object access)
- Flow logs (VPC/VNET)
- Email audit and message trace logs
- Admin activity logs

## 11.6 Security Tools

- SIEM alert raw events + correlation context
- EDR detections + process tree + network connections + timeline export
- Email security gateway logs
- DLP/CASB alerts (if relevant)

---

# 12. Collection Procedures (Standard)

> Exact commands vary. Follow tool-specific guidance but meet documentation requirements.

## 12.1 Procedure A — SIEM Export (Preferred for Centralized Logs)

Steps:

1. Identify time window and entities (hosts/users/IPs)
2. Export:
   - Raw events that triggered detection
   - Surrounding context (±24 hours for P1/P2 unless otherwise scoped)
3. Record:
   - Query used (or report name)
   - Time window (UTC)
   - Export format and location
4. Store export in evidence repository
5. Hash export file(s) (SHA256) if evidence-grade
6. Reference export path + hash in the ticket

References:  
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md`  
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md`

---

## 12.2 Procedure B — EDR Export (Telemetry and Timeline)

Steps:

1. Identify affected host(s)
2. Export:
   - Detection details
   - Process tree
   - Network connections
   - File events and hashes
   - User logon context (if available)
3. Record:
   - Export time (UTC)
   - Host identifiers
   - Export scope/time window
4. Store in evidence repository (client-segregated for MSSP)
5. Reference artifacts in ticket

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Alert-Handling-Guide.md`

---

## 12.3 Procedure C — Host-Based Windows Log Collection (EVTX)

Steps (minimum outcomes):

1. Identify target host and time window
2. Export relevant event logs (EVTX) (do not modify originals)
3. Capture:
   - System time settings (timezone) and hostname
   - Any noted clock drift (if observed)
4. Compress exports (ZIP) and record contents
5. Hash the export bundle (SHA256) for evidence-grade work
6. Transfer securely to evidence repository
7. Document in ticket and evidence log

---

## 12.4 Procedure D — Host-Based Linux Log Collection

Steps (minimum outcomes):

1. Identify target host and time window
2. Collect relevant `/var/log/*` files and/or journal exports for the time window
3. Record:
   - Hostname, OS version, timezone settings
4. Bundle logs into a TAR/ZIP package
5. Hash package (SHA256) for evidence-grade work
6. Transfer securely and store in evidence repository
7. Document in ticket and evidence log

---

## 12.5 Procedure E — Network Device Log Export

Steps:

1. Identify device and relevant policy context (firewall rule IDs, IDS signatures)
2. Export logs for time window and entities:
   - src/dst, ports, action, bytes, rule name
3. Export config snapshot if needed for evidence (sanitized, access-controlled)
4. Store exports and compute hashes where required
5. Reference in ticket with timestamps

References:  
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Rule-Change-Process.md`  
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/IDS-IPS-Tuning-Guide.md`

---

## 12.6 Procedure F — Cloud / SaaS Log Export

Steps:

1. Identify tenant/subscription/account (MSSP tenant scope mandatory)
2. Export audit logs for time window:
   - Admin actions
   - IAM changes
   - Storage access events
3. Store exports in evidence repository
4. Record export parameters and API query references (if available)
5. Hash exported files (SHA256) for evidence-grade work
6. Document in ticket

---

# 13. Integrity Verification (Hashing) Requirements

Hashing is mandatory for:

- P1/P2 evidence packages
- Any log bundle intended for legal/regulatory/audit evidence
- Any manual export where integrity assurance is required

Minimum standard:

| Requirement | Standard |
|---|---|
| Hash algorithm | SHA256 |
| Hash recorded | In ticket + evidence log |
| File naming stable | Do not rename after hashing unless documented and re-hashed |
| Re-hash after transfer (recommended) | Confirm transfer integrity |

---

# 14. Evidence Storage and Access Control

## 14.1 Storage Requirements (Mandatory)

Logs must be stored:

- In an approved evidence repository
- Encrypted at rest
- With restricted access (IR/Forensics only for P1/P2)
- With client segregation for MSSP cases

## 14.2 Naming Standard (Recommended)

`/evidence/INC-[ID]/logs/[SOURCE]-[HOST]-[YYYYMMDD]/`

Example:
`/evidence/INC-2026-0102/logs/windows-evtx-FIN-WS-12-20260525/`

---

# 15. Chain of Custody (CoC)

CoC is required when:

- P1/P2 incidents with potential regulatory/legal impact
- Insider threat investigations involving HR/legal
- Client contract requires forensic-grade evidence handling

Minimum CoC requirements:

- Record collector, time (UTC), method
- Record evidence identifiers and hashes
- Record storage location and custodian
- Record every transfer

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`

---

# 16. MSSP Multi-Tenant Requirements (Mandatory)

For MSSP log collection:

| Requirement | Standard |
|---|---|
| Client ID recorded | Mandatory |
| Tenant scope verified before export | Mandatory |
| Evidence storage segregated by client | Mandatory |
| No cross-client logs in bundles | Mandatory |
| Client approval documented (as required) | Mandatory |
| Client communication documented (P1/P2) | Mandatory |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 17. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Collecting too late (logs overwritten) | Lost evidence | Prioritize early collection for P1/P2 |
| Wrong time zone interpretation | Incorrect timeline | Use UTC; record local TZ and conversions |
| Not recording queries/filters | Non-reproducible evidence | Document exact query/export parameters |
| No hashes | Integrity risk | SHA256 for evidence-grade packages |
| Storing logs on local devices | Data leakage | Evidence repository only |
| Cross-tenant export (MSSP) | Compliance breach | Tenant checks + segregation |
| Incomplete scope | Missed attacker activity | Use standard source checklist |

---

# 18. Related Documents

| Document | Path |
|---|---|
| Disk Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md` |
| Memory Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md` |
| Tool Chain of Custody | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Tool-Chain-of-Custody.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Log Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Log-Evidence-SOP.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| SIEM Query Library | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md` |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |

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