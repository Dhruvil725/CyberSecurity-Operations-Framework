# REFERENCE: EDR Containment Commands and Response Actions

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | REFERENCE – EDR Containment Commands and Response Actions |
| Document ID | TOOL-EDR-002 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Endpoint Security Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This reference provides an **approved, standardized list of EDR containment actions** and operational guidance for executing endpoint containment safely and consistently during incident response.

EDR containment actions are high-impact because they can:

- Stop active attacker activity quickly (ransomware, C2, lateral movement)
- Prevent spread across the environment
- Reduce attacker dwell time
- Also potentially disrupt business operations or destroy volatile evidence if executed incorrectly

This document ensures:

- Containment actions are executed with proper authorization
- Evidence preservation is considered before containment (where feasible)
- Actions are documented in an audit-ready way
- MSSP client approval and segregation rules are followed

---

# 3. Scope

This reference applies to EDR-based response actions for:

| Category | Examples |
|---|---|
| Endpoint isolation (network containment) | Quarantine/isolate host |
| Process containment | Kill process, block execution |
| File containment | Quarantine/remove file, block hash |
| Account containment support | Disable user (identity team) |
| Triage collection | Collect investigation package, fetch artifacts |
| IOC-based blocking | Hash block, IOC ban |
| Rollback/release actions | Unisolate host, restore access |
| Multi-host containment | Bulk isolate group of endpoints |

**Out of Scope:** Offensive actions, persistence deployment, or any activity not related to incident containment.

---

# 4. Containment Safety Principles (IMPORTANT)

Containment actions must follow these principles:

| Principle | Standard |
|---|---|
| Authority first | Confirm approval level before execution |
| Preserve evidence when possible | Export telemetry before isolation/kill |
| Least disruption | Contain precisely; avoid unnecessary outage |
| Validate before and after | Confirm threat activity stopped |
| Document everything | Time (UTC), reason, evidence, approval |
| Reversibility | Have a rollback plan (uncontain/restore) |

---

# 5. Authorization and Approval (Do Not Skip)

Containment authority must align with:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 5.1 Quick Approval Matrix (Operational Summary)

| Action | Typical Authority | Notes |
|---|---|---|
| Isolate a workstation | SOC Lead / IRT Lead | Preferred for active C2/malware |
| Isolate a server | IRT Lead | Consider business impact and evidence |
| Isolate a domain controller | CISO + IRT Lead | High business risk; executive approval |
| Kill suspicious process | SOC Lead / L2 (per policy) | Preserve evidence first if possible |
| Quarantine file | SOC Lead | Validate hash/path; avoid critical OS files |
| Block hash (global) | Detection Engineering / IRT Lead | Risk of false positives; requires review |
| Unisolate host | SOC Lead / IRT Lead | Only after validation and remediation |

---

## 5.2 Emergency Containment Rule

If any of the following are confirmed, **contain immediately** and escalate:

- Active ransomware encryption
- Active exfiltration tooling on endpoint
- Credential dumping in progress (especially server/DC)
- EDR tampering
- Confirmed lateral movement from the host

Document the emergency justification and obtain retroactive approval as required.

---

# 6. Standard Containment Workflow (Recommended)

| Step | Action | Output |
|---|---|---|
| 1 | Confirm incident severity and scope | P1/P2/P3 classification |
| 2 | Capture minimal evidence fast (telemetry export) | Evidence reference in ticket |
| 3 | Confirm authority/approval | Approval documented |
| 4 | Execute containment action | Host/process/file contained |
| 5 | Validate containment effectiveness | No active C2 / encryption stopped |
| 6 | Expand scope if needed | Related hosts identified |
| 7 | Escalate to IR/L3 if required | Ownership and actions tracked |
| 8 | Remediate and plan recovery | Patch, reset creds, rebuild |
| 9 | Release/uncontain after validation | Host restored safely |

---

# 7. Evidence to Capture Before Containment (When Feasible)

**Goal:** Preserve enough evidence to support forensics without delaying urgent containment.

| Evidence | Why | How (Typical) |
|---|---|---|
| Alert details export | Investigation record | Export alert JSON/CSV |
| Process tree | Attack chain | Screenshot/export |
| Command line | Intent | Copy from telemetry |
| Network connections | C2/exfil | Export network events |
| File hash/path | IOC generation | Record SHA-256 + path |
| Logged-in user context | Scope | User + privilege level |

Reference:
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md`

---

# 8. Containment Action Reference (Vendor-Agnostic)

---

## 8.1 Host Isolation (Network Containment)

**Objective:** Prevent the endpoint from communicating with internal/external hosts (except EDR management channel, depending on vendor).

| Item | Guidance |
|---|---|
| Use When | Active malware/C2, lateral movement, ransomware suspected |
| Risk | Business disruption; may break remote access tools |
| Evidence Impact | May prevent further telemetry, but usually preserves current data |
| Approval | SOC Lead for workstations; IRT Lead for servers (per matrix) |

**Execution Checklist**

| Check | Done |
|---|---|
| Host identity confirmed (hostname/device ID) | ☐ |
| Business owner notified if required | ☐ |
| Evidence exported (minimum set) | ☐ |
| Ticket updated with approval | ☐ |
| Isolation executed | ☐ |
| Post-isolation validation performed | ☐ |

---

## 8.2 Kill Process / Terminate Malicious Execution

| Item | Guidance |
|---|---|
| Use When | Active encryption process, suspicious scripting, known malicious process |
| Risk | Can destroy volatile evidence; attacker may restart via persistence |
| Evidence Impact | Capture command line/process tree first if possible |
| Approval | SOC Lead / IRT Lead depending on severity |

**Recommended Practice**
- Prefer **isolation first**, then process kill (if ransomware spreading, kill immediately).
- Always document the **PID**, process name, command line, and parent process.

---

## 8.3 Quarantine / Remove File

| Item | Guidance |
|---|---|
| Use When | Known malicious payload identified (hash confirmed) |
| Risk | Removing wrong file can break systems |
| Evidence Impact | Preserve a copy/hash before quarantine (if allowed) |
| Approval | SOC Lead / IRT Lead depending on system criticality |

---

## 8.4 Block Hash / IOC (Prevent Re-Execution)

| Item | Guidance |
|---|---|
| Use When | Confirmed malware hash observed; outbreak control |
| Risk | False positives can cause widespread disruption |
| Evidence Impact | Strong; supports prevention and fleet containment |
| Approval | Detection Engineering Lead / IRT Lead recommended |

**Required Inputs**
- SHA-256 (preferred)
- File name and path
- Prevalence (how many hosts)
- Business application exception check

---

## 8.5 Collect Investigation Package / Live Response Artifacts

| Item | Guidance |
|---|---|
| Use When | Need endpoint artifacts for deeper analysis |
| Risk | May increase load on endpoint; may take time |
| Evidence Impact | Improves forensic depth |
| Approval | L2/L3 (per tool access policy) |

Typical artifacts:
- Running processes
- Network connections
- Autoruns/persistence items
- Event logs
- Memory capture (if supported/approved)

---

## 8.6 Bulk Containment (Multiple Hosts)

| Item | Guidance |
|---|---|
| Use When | Outbreak detected (worm/ransomware spread) |
| Risk | Broad business disruption |
| Evidence Impact | Ensure at least one representative host fully preserved for forensics |
| Approval | IRT Lead + SOC Manager recommended; CISO for critical environments |

**Bulk Actions Examples**
- Isolate all hosts with IOC match
- Quarantine file across fleet
- Block hash globally
- Enforce network restrictions on affected group

---

# 9. Platform-Specific Command Examples (Reference Only)

> These examples are provided to standardize intent and documentation. Exact commands and UI labels vary by platform/version/role. Always follow your organization’s tool access policy and change controls.

---

## 9.1 CrowdStrike Falcon (RTR/Console) — Common Actions (Example)

| Action | Example Command / UI Action | Notes |
|---|---|---|
| Isolate host | **Network Contain** (UI) / `contain` (RTR) | Confirms network containment |
| Release isolation | **Lift Containment** / `uncontain` | Validate first |
| Kill process | `kill <pid>` | Capture PID + cmdline first |
| Get file | `get <path>` | Store evidence securely |
| Run script | `runscript -Raw=<script>` | Use only approved scripts |
| List processes | `ps` | Useful for quick triage |
| List network | `netstat` / `connections` (tool-dependent) | Validate C2 |

**Documentation requirement:** record host ID, action time (UTC), operator, result.

---

## 9.2 Microsoft Defender for Endpoint (MDE) — Common Actions (Example)

| Action | Console Feature | Notes |
|---|---|---|
| Isolate device | **Isolate device** | Choose full vs selective isolation as available |
| Release isolation | **Release from isolation** | Validate remediation first |
| Collect package | **Collect investigation package** | Preserves artifacts |
| Live response | **Live response** | Execute read-only commands where possible |
| Restrict app execution | (Policy-dependent) | Requires governance |

**Documentation requirement:** device name/ID, isolation type, reason, evidence link.

---

## 9.3 SentinelOne — Common Actions (Example)

| Action | Console Feature | Notes |
|---|---|---|
| Disconnect from network | **Disconnect** | Similar to isolation |
| Reconnect | **Reconnect** | Validate first |
| Kill process | **Kill** | Capture process lineage first |
| Quarantine | **Quarantine** | Ensure correct file |
| Remediate | **Remediate/Rollback** | Use with IRT approval |

**Documentation requirement:** site/group, endpoint ID, action, outcome.

---

## 9.4 Cortex XDR / Carbon Black / Other EDRs

Use the same operational mapping:

| Operational Intent | Typical Feature Name |
|---|---|
| Isolate host | Isolate / Quarantine network |
| Kill process | Terminate / Kill |
| Remove file | Quarantine / Delete |
| Collect triage | Live response / Triage package |
| Block IOC | Prevention policy / IOC management |
| Release | Unisolate / Restore connectivity |

---

# 10. Containment Validation (Mandatory)

After containment, validate:

| Validation | How |
|---|---|
| Host communications stopped (except EDR channel) | Network telemetry / EDR status |
| Ransomware encryption stopped | File event rate drop |
| C2 beacon stopped | Firewall/proxy/EDR network events |
| No new suspicious child processes | EDR process timeline |
| No further lateral movement | NetFlow/auth logs |

If containment is ineffective:
- Escalate immediately to IR Team
- Consider network-level isolation
- Consider credential resets and segmentation

---

# 11. Rollback / Release Procedures (Unisolate / Restore)

Release actions must be controlled.

---

## 11.1 Release Preconditions (All Required)

| Condition | Completed |
|---|---|
| Root cause identified (or mitigated with acceptable risk) | ☐ |
| Persistence mechanisms removed | ☐ |
| Malware removed/quarantined | ☐ |
| Credentials reset (if compromise suspected) | ☐ |
| Patching/hardening applied | ☐ |
| Post-remediation scan completed | ☐ |
| Stakeholder approval documented | ☐ |

---

## 11.2 Release Documentation

| Field | Requirement |
|---|---|
| Release reason | Mandatory |
| Approver | Mandatory |
| Validation performed | Mandatory |
| Time (UTC) | Mandatory |
| Residual risk statement | Recommended |

---

# 12. Documentation Requirements (Ticket Standard)

Every containment action must be recorded as:

---

## 12.1 Containment Action Log Table

| Timestamp (UTC) | Endpoint | Action | Executed By | Approval By | Reason | Outcome | Evidence Ref |
|---|---|---|---|---|---|---|---|
| | | | | | | | |

---

## 12.2 Common Reason Codes (Recommended)

| Code | Meaning |
|---|---|
| CONTAIN-C2 | Active C2 communication |
| CONTAIN-RAN | Ransomware suspected/confirmed |
| CONTAIN-LMOV | Lateral movement suspected |
| CONTAIN-CRED | Credential dumping suspected |
| CONTAIN-IOC | IOC match outbreak |
| CONTAIN-TAMPER | EDR tampering detected |

---

# 13. MSSP-Specific Requirements

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Confirm correct tenant/site | Prevent cross-client action |
| Follow client containment authority | Contract compliance |
| Notify client for high impact actions | SLA compliance |
| Preserve evidence per client | Legal/audit needs |
| Document approvals with client references | Audit readiness |

References:
- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
- `03_SOC-TIER-PROCEDURES/03.4_SOC-Lead-Procedures/SOCLead-Client-Communication-MSSP.md`

---

# 14. Common Mistakes

| Mistake | Risk |
|---|---|
| Isolating wrong host | Operational disruption |
| Killing process without capturing command line | Lost evidence |
| Blocking hash without validation | Business outage |
| Forgetting to unisolate after remediation | Prolonged disruption |
| Executing bulk actions without approval | Governance failure |
| Missing ticket documentation | Audit failure |

---

# 15. Related Documents

| Document | Path |
|---|---|
| EDR Alert Handling Guide | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Alert-Handling-Guide.md` |
| EDR Investigation Queries | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Investigation-Queries.md` |
| L2 EDR Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-EDR-Deep-Investigation.md` |
| L2 Evidence Handling SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md` |
| IRT Containment Authority Matrix | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md` |
| Network Isolation Procedure | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Isolation-Procedure.md` |

---

# 16. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | Endpoint Security Lead | Initial version |

---

# 17. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**