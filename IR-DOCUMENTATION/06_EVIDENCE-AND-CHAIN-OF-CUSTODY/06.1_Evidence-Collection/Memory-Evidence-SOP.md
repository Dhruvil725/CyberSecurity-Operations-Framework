# SOP: Memory Evidence (RAM) Collection and Handling

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Memory Evidence Collection and Handling |
| Document ID | EVD-COL-004 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | IR Team Lead / Digital Forensics Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines how **memory evidence (RAM)** is requested, collected, preserved, validated, stored, and referenced during investigations.

Memory evidence is critical because:

- key attacker artifacts may exist only in memory (in-memory malware, injected code)
- credential material, tokens, and active sessions may be present in RAM
- network connections and running processes are observable in volatile state
- mishandling can destroy volatile evidence (reboot/shutdown) or contaminate outputs
- memory dumps are highly sensitive (may contain credentials and PII)
- audit and legal defensibility may require integrity controls and chain-of-custody

This SOP ensures:

- consistent and defensible memory evidence handling
- proper approvals and risk-based decision-making
- integrity verification (SHA256)
- secure storage and strict access control
- MSSP tenant segregation controls

---

# 3. Scope

This SOP applies to memory evidence collection for:

| System Type | Examples |
|---|---|
| Windows | Workstations, servers, domain controllers (special handling) |
| Linux | Application servers, web servers |
| macOS | Endpoints (where supported) |
| Cloud/VM | Instances/VMs (provider dependent) |

In scope memory evidence artifacts:

- full RAM dump files
- acquisition logs produced by capture tool
- associated volatile context (recommended): process list, network connections, logged-on sessions

Out of scope:

- memory analysis methodology (covered under L3 procedures)
- disk acquisition (separate SOP)
- tool custody process (separate SOP)

References:  
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Tool-Chain-of-Custody.md`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Memory evidence | Evidence derived from volatile RAM state |
| Volatile data | Data lost on reboot/power-off |
| Evidence-grade | Evidence requiring hashing and controlled custody |
| Hash | SHA256 checksum validating integrity |
| CoC | Chain-of-custody record for evidence transfers |
| Quarantine | Restricting a host/segment to reduce risk while preserving evidence |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L2 Analyst | Identifies need; requests memory capture; provides incident context |
| L3/Forensics Analyst | Executes memory capture; validates integrity; documents outputs |
| IR Team Lead | Authorizes memory capture scope; coordinates with containment plan |
| SOC Lead | Ensures escalation and SLA alignment for P1/P2; coordinates communications |
| IT Ops / System Owner | Provides access and stability constraints; supports scheduling |
| Evidence Custodian | Stores and controls access; ensures retention and custody records |
| Legal Counsel | Advises on legal hold, external sharing, and privileged handling (if applicable) |
| MSSP SDM | Coordinates client approval and tenant segregation (MSSP) |

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

# 6. Memory Evidence Handling Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Capture early | RAM changes rapidly; collect ASAP for P1/P2 |
| Do not reboot | Avoid reboot/shutdown before capture unless directed by IR Lead |
| Minimal footprint | Use approved tools; minimize system changes |
| Secure handling | Memory dumps are restricted; treat as sensitive by default |
| Integrity verification | SHA256 mandatory for dump and package |
| Document context | Capture what/when/how and system state |
| Tenant segregation (MSSP) | Client evidence must be isolated and access-controlled |

---

# 7. When Memory Evidence Is Required (Triggers)

Memory evidence should be collected when:

| Trigger | Examples |
|---|---|
| In-memory execution suspected | PowerShell stagers, reflective DLL injection |
| Credential theft suspected | LSASS access, token theft, abnormal privileged auth |
| Active attacker session | RDP/remote tool in use; interactive shell suspected |
| Ransomware in progress | Capture before shutdown to preserve keys/context (if safe) |
| Advanced intrusion (APT) | Need to identify toolset/persistence methods |
| Rootkit suspected | Kernel anomalies, hidden processes/drivers |

---

# 8. Approvals and Authorization

Memory capture can impact system performance and may expose sensitive data.

## 8.1 Approval Matrix (Guidance)

| Target | Minimum Approval |
|---|---|
| Standard endpoint | IR Team Lead or SOC Lead |
| Critical server | IR Team Lead + System Owner |
| Domain Controller / IAM | IR Team Lead + SOC Manager (notify CISO if P1) |
| MSSP client system | Client approval (contract dependent) + MSSP SDM + IR Team Lead |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 9. Ticket and Evidence Log Requirements (Mandatory)

Before capture begins, ticket must include:

| Field | Requirement |
|---|---|
| Incident ID | Mandatory |
| Target host identifiers | Hostname/IP/asset tag |
| Reason for capture | Mandatory |
| Current host state | Powered on; user logged in; isolation status |
| Approver + approval time (UTC) | Mandatory |
| Planned capture tool and method | Mandatory |
| Planned storage location | Mandatory |
| CoC required? | Mandatory (Yes/No + rationale) |

After capture, record:

- start/end time (UTC)
- output filenames and sizes
- SHA256 hashes
- storage path reference
- any errors/anomalies

References:  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`

---

# 10. Collection and Packaging Standard (Minimum Outcomes)

> Follow tool-specific acquisition SOP for exact steps. This SOP defines mandatory outcomes.

## 10.1 Required Outputs

| Output | Requirement |
|---|---|
| Memory dump file(s) | Mandatory |
| Acquisition log (tool output) | Mandatory |
| Collector notes (context) | Mandatory |
| Hash file / manifest | Mandatory (SHA256) |

Recommended additional volatile context:

- process list
- network connections
- logged-in sessions
- ARP/DNS cache snapshots (as feasible)

---

## 10.2 File Naming Convention (Recommended)

`[INC-ID]_[HOSTNAME]_MEM_[YYYYMMDD_HHMM]UTC.[ext]`

Example:
`INC-2026-0102_FIN-WS-12_MEM_20260530_0415UTC.raw`

---

## 10.3 Hashing Requirements (Mandatory)

Compute SHA256 for:

- each memory dump file (or each part if split)
- the final packaged archive (if created)

Record hashes in:

- ticket notes
- evidence log
- CoC (if applicable)

If evidence is transferred, re-hash after transfer (recommended) and confirm match.

---

# 11. Storage and Access Control (Mandatory)

Memory evidence is **Restricted** by default.

Storage requirements:

- store only in approved evidence repository
- encrypt at rest
- restrict access to IR/Forensics and Legal (if needed)
- log access for Restricted artifacts (where feasible)
- store per-tenant for MSSP

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

# 12. Chain-of-Custody (CoC)

CoC is required when:

- P1/P2 incidents with legal/regulatory risk
- insider threats (HR/legal)
- law enforcement engagement
- client contract requires forensic-grade handling

CoC requirements:

- evidence ID
- collector identity and time (UTC)
- hashes
- storage location
- transfer records (who/when/why)

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`

---

# 13. MSSP Multi-Tenant Requirements (Mandatory)

| Requirement | Standard |
|---|---|
| Client approval documented | Mandatory (contract-dependent) |
| Evidence stored in client-specific repository/path | Mandatory |
| Access limited to assigned analysts | Mandatory |
| No cross-client tool media reuse without sanitization | Mandatory |
| Client-safe evidence references | Mandatory for client reporting |

References:  
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`  
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Tool-Chain-of-Custody.md`

---

# 14. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Rebooting before capture | Volatile evidence lost | Capture early; avoid reboot |
| Capturing without approval on critical systems | Business/legal risk | Approval matrix enforced |
| Storing dumps on local devices | Data leak | Evidence repository only |
| No SHA256 hashes | Integrity challenge | Hash mandatory |
| Sharing dumps via email | Severe exposure | Secure transfer only |
| Cross-tenant evidence mix (MSSP) | Compliance breach | Tenant segregation controls |

---

# 15. Related Documents

| Document | Path |
|---|---|
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Digital Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Digital-Evidence-Handling.md` |
| Network Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Network-Evidence-SOP.md` |
| Memory Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md` |
| Tool Chain of Custody | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Tool-Chain-of-Custody.md` |
| CoC Digital Evidence | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |

---

# 16. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | IR Team Lead / Digital Forensics Lead | Initial version |

---

# 17. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**