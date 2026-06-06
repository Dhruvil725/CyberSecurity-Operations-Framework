# SOP: Memory Acquisition (RAM Capture)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Memory Acquisition (RAM Capture) |
| Document ID | TOOL-FOR-004 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | IR Team Lead / Digital Forensics Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the approved method for performing **memory acquisition (RAM capture)** during incident response and forensic investigations.

Memory acquisition is critical because:

- Many attacker artifacts exist only in memory (in-memory malware, injected code, decrypted payloads)
- Credential material and session tokens may be present in memory during active compromise
- Memory often contains evidence of command execution, network connections, and persistence staging
- Improper collection can destroy volatile evidence or contaminate findings
- Audit and regulatory readiness requires repeatable and documented procedures
- MSSP environments require strict tenant segregation and secure evidence handling

This SOP ensures:

- Consistent, safe, minimally disruptive memory capture procedures
- Evidence integrity via hashing and secure storage
- Clear authorization and coordination (especially for critical systems)
- Proper documentation for audits, RCA, and post-incident reporting
- Alignment with chain-of-custody and evidence retention policies

---

# 3. Scope

This SOP applies to memory acquisition for:

| System Type | Examples |
|---|---|
| Windows endpoints/servers | Workstations, application servers, DCs (special handling) |
| Linux servers | Web servers, application servers |
| macOS endpoints (if supported) | Laptops/desktop endpoints |
| Cloud workloads | Instances/VMs (provider capability dependent) |

Acquisition types:

- Full physical memory capture (preferred)
- Targeted volatile artifact capture (only with approval and documented limitations)

Out of scope:

- Disk imaging (see Disk Acquisition SOP)
- Deep memory analysis methodology (covered under L3 procedures)
- Live response containment actions (covered under playbooks)

---

# 4. Definitions

| Term | Definition |
|---|---|
| Volatile evidence | Evidence lost on reboot/power-off |
| Memory dump | Captured snapshot of RAM content |
| Pagefile/swap | Disk-backed memory extension; may contain useful artifacts |
| Integrity hash | SHA256 checksum for evidence validation |
| CoC | Chain of Custody |
| Minimal footprint | Tools/actions that minimize system changes during acquisition |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L2 Analyst | Identifies need; provides incident context; coordinates access |
| L3 Forensics Analyst | Executes memory capture; validates integrity; documents outputs |
| IR Team Lead | Authorizes memory acquisition for P1/P2; coordinates with containment strategy |
| SOC Lead | Coordinates urgency and operational impact; bridge call for P1 |
| IT Ops / System Owner | Provides access and change window; supports stability considerations |
| Evidence Custodian | Stores evidence securely; manages access and transfers |
| MSSP Service Delivery | Coordinates client approvals and evidence handling requirements |

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Memory-Evidence-SOP.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`

---

# 6. Memory Acquisition Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Capture early | RAM changes rapidly; capture as soon as feasible |
| Avoid reboot/shutdown | Do not reboot before capture unless directed by IR Lead |
| Minimal footprint | Use approved tools; avoid installing unnecessary components |
| Document everything | Tool, version, method, time (UTC), system state |
| Integrity verification | Hash outputs (SHA256) and record |
| Secure handling | Encrypt transfers; restrict access; segregate tenants (MSSP) |
| Safety first | Consider system stability and business impact |

---

# 7. When Memory Acquisition is Required

Memory acquisition is recommended/required when:

| Scenario | Examples |
|---|---|
| Suspected in-memory malware | Fileless malware, PowerShell stagers, injected code |
| Credential theft suspected | LSASS access, token theft, suspicious auth |
| Active C2 beaconing | Need to identify process and network connections |
| Ransomware active | Capture before shutdown to preserve encryption key artifacts (where feasible) |
| Privileged system compromise | DC/identity server suspicious activity |
| APT/long-term intrusion | Need to confirm toolsets, persistence, and lateral movement methods |

---

# 8. Approvals and Authority

Memory capture may require elevated privileges and can impact performance.

## 8.1 Minimum Approval Matrix (Guidance)

| Action | Minimum Approval |
|---|---|
| Capture memory from standard endpoint | SOC Lead or IR Team Lead |
| Capture memory from critical server | IR Team Lead + System Owner |
| Capture from Domain Controller | IR Team Lead + SOC Manager (and notify CISO for P1) |
| Capture requiring endpoint isolation changes | IR Team Lead (per containment authority matrix) |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

## 8.2 MSSP Client Approval

- Obtain client approval if required by contract
- Ensure secure transfer and segregated storage
- Follow client escalation matrix and legal constraints

---

# 9. Ticketing and Evidence Documentation (Mandatory)

Every memory acquisition must be linked to an incident ticket.

Minimum ticket fields:

| Field | Requirement |
|---|---|
| Incident/Ticket ID | Mandatory |
| Target system identifiers | Hostname/IP/asset tag |
| Reason for capture | Mandatory |
| System state | Powered on; user logged in; EDR status |
| Tool + version | Mandatory |
| Start/end time (UTC) | Mandatory |
| Output file name(s) | Mandatory |
| Output size | Recommended |
| Hash algorithm + hash values | SHA256 mandatory |
| Storage location | Evidence repository path |
| CoC required? | Yes/No with rationale |
| Approvals | Names + timestamps (UTC) |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 10. Pre-Acquisition Checklist (Mandatory)

Before starting the capture:

| Check | Requirement |
|---|---|
| Confirm correct target host | Mandatory |
| Confirm time sync and current system time | Recommended |
| Confirm sufficient disk space for output | Mandatory |
| Confirm capture destination (external drive/network share) | Mandatory |
| Confirm tool integrity (known good hash if stored internally) | Recommended |
| Confirm whether encryption or sensitive data concerns exist | Mandatory |
| Confirm CoC forms ready (if required) | Mandatory |
| Confirm containment plan (isolation/kill process) is coordinated | Mandatory |
| Inform system owner (if required) | Mandatory (unless emergency) |

---

# 11. Acquisition Procedure (Standard)

> Specific commands depend on the approved toolset. Follow these required outcomes and documentation steps.

## 11.1 Step 1 — Prepare Capture Location

- Use approved evidence storage or secure temporary staging (as documented)
- Ensure encryption at rest where possible
- Ensure file naming standard is applied

Recommended naming:

`[INC-ID]_[HOSTNAME]_MEM_[YYYYMMDD_HHMM]UTC.raw`

Example:
`INC-2026-0102_FIN-WS-12_MEM_20260525_0415UTC.raw`

---

## 11.2 Step 2 — Execute Memory Capture

Mandatory requirements:

| Requirement | Standard |
|---|---|
| Use approved capture tool | Mandatory |
| Record tool name/version | Mandatory |
| Record start/end time (UTC) | Mandatory |
| Avoid unnecessary system interaction | Mandatory |
| Monitor for system instability | Mandatory |
| Capture is complete and file is not truncated | Mandatory |

If capture fails:

- Document error and partial outputs (if any)
- Re-attempt if safe
- Escalate to Forensics Lead / IR Team Lead

---

## 11.3 Step 3 — Hashing and Integrity Verification

Hashing requirements:

| Item | Requirement |
|---|---|
| Hash algorithm | SHA256 |
| Hash computed for memory dump file | Mandatory |
| Hash recorded in ticket + evidence log | Mandatory |
| Re-hash after transfer (recommended) | Validate integrity |

If the file is split into multiple parts, compute SHA256 for each part and for the final archive (if created).

---

## 11.4 Step 4 — Secure Storage and Access Control

- Transfer memory dump securely to evidence repository
- Restrict access to forensics/IR team only (especially P1/P2)
- Update evidence log and CoC (if required)
- Avoid copying RAM dumps into non-controlled collaboration tools

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`

---

# 12. Additional Volatile Data Collection (Recommended)

When possible (and approved), capture the following volatile context alongside RAM:

| Artifact | Why |
|---|---|
| Active network connections | Identify C2/exfil |
| Running processes and command lines | Identify execution chain |
| Logged-on users / sessions | Identify compromised accounts |
| ARP/DNS cache | Identify recent communications |
| Scheduled tasks/services (snapshot) | Identify persistence staging |
| EDR timeline export | Additional context |

Document all artifacts collected, tools used, and timestamps.

---

# 13. Special Considerations

## 13.1 Domain Controllers / Identity Servers

Extra controls:

- Coordinate carefully with IT Ops
- Avoid actions that disrupt authentication services
- Consider capturing memory during low utilization if possible
- Ensure approvals and CISO notification for P1

## 13.2 High-Availability / Clustered Systems

- Coordinate with application owner
- Capture from replica node where feasible
- Document node roles and failover considerations

## 13.3 Malware Self-Protection / EDR Interactions

- Some malware may detect acquisition tools
- Do not disable EDR without approval
- Coordinate capture with containment actions to avoid losing evidence

---

# 14. Chain of Custody (CoC)

CoC is mandatory for:

- P1/P2 incidents
- Legal/regulatory sensitive cases
- Insider threat investigations (HR/legal)
- Client contractual requirements

CoC requirements:

- Evidence ID and label
- Collector name/time (UTC)
- Hash values
- Storage and transfer records

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`

---

# 15. MSSP Multi-Tenant Requirements (Mandatory)

For MSSP memory captures:

| Requirement | Standard |
|---|---|
| Client ID recorded in ticket/evidence log | Mandatory |
| Secure transfer method agreed | Mandatory |
| Evidence stored in client-specific repository | Mandatory |
| No cross-client tooling contamination | Mandatory (clean kit per client) |
| Client approvals documented | Mandatory (contract-dependent) |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 16. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Rebooting before capture | Volatile evidence lost | Capture early; avoid reboot |
| Using unapproved tools | Contamination/legal risk | Approved toolkit only |
| Not hashing dump | Integrity failure | SHA256 mandatory |
| Saving dump to local desktop | Evidence loss/leak | Evidence repository only |
| Capturing wrong host | Invalid investigation | Pre-check identity |
| No CoC for P1/P2 | Audit/legal risk | CoC triggers enforced |
| Long delays | Evidence changes | SLA-driven capture initiation |

---

# 17. Related Documents

| Document | Path |
|---|---|
| Disk Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md` |
| Log Collection SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Log-Collection-SOP.md` |
| Forensics Toolkit Reference | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Forensics-Toolkit-Reference.md` |
| Tool Chain of Custody | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Tool-Chain-of-Custody.md` |
| Memory Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Memory-Evidence-SOP.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| CoC Digital Evidence | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| L3 Memory Forensics SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Memory-Forensics-SOP.md` |

---

# 18. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | IR Team Lead / Digital Forensics Lead | Initial version |

---

# 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**