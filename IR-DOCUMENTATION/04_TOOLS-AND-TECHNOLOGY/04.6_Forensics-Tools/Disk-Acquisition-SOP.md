# SOP: Disk Acquisition (Forensic Imaging)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Disk Acquisition (Forensic Imaging) |
| Document ID | TOOL-FOR-001 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | IR Team Lead / Digital Forensics Lead |
| Approved By | CISO (or SOC Manager – delegated) |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the approved method for performing **forensically sound disk acquisition** (imaging) of endpoints and servers during investigations and incident response.

Disk acquisition is critical because:

- Disk images preserve evidence for root cause analysis, attribution, and scope validation
- Improper acquisition can alter evidence and invalidate findings
- Audit and regulatory reviews may require defensible forensic processes and chain-of-custody
- MSSP environments require strict tenant segregation and evidence handling controls
- Acquisition must be repeatable, documented, and verifiable via cryptographic hashes

This SOP ensures:

- Evidence integrity (minimal alteration + hash verification)
- Repeatable, standardized acquisition steps
- Documented chain-of-custody and evidence logs
- Secure transfer and storage of forensic images
- Clear approvals and authority for high-impact actions (e.g., shutdown, disk removal)
- Audit-ready records aligned to IR governance

---

# 3. Scope

This SOP applies to disk acquisition for:

| System Type | Examples |
|---|---|
| Endpoints | Windows/macOS/Linux workstations, laptops |
| Servers | Physical servers, virtual machines, critical application servers |
| Storage media | HDD/SSD/NVMe, removable media, external drives |
| Cloud workloads (where possible) | Volume snapshots, managed disk exports (provider-dependent) |

In scope acquisition outcomes:

- Full disk image (preferred for deep forensic work)
- Partition image (when full disk is not feasible and approved)
- Targeted acquisition (restricted scope; requires justification and approval)

Out of scope:

- Memory acquisition (see `Memory-Acquisition-SOP.md`)
- Log-only evidence collection (see `Log-Collection-SOP.md`)
- Malware reverse engineering (covered under L3 procedures)

---

# 4. Definitions

| Term | Definition |
|---|---|
| Forensic image | Bit-for-bit copy of storage media |
| Write blocker | Hardware/software control preventing writes to evidence media |
| Hash | Cryptographic checksum used to verify integrity (SHA256 preferred) |
| E01 | EnCase evidence file format (supports compression/metadata) |
| RAW/DD | Raw bitstream image format |
| CoC | Chain of Custody documentation |
| Evidence custodian | Person/team responsible for secure evidence storage and access |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L2 Analyst | Requests acquisition, provides incident context, identifies target systems |
| L3 Analyst / Forensics Analyst | Executes acquisition, validates integrity, documents results |
| IR Team Lead | Authorizes acquisition actions during P1/P2 incidents; ensures CoC compliance |
| SOC Lead | Coordinates operational impact, bridge call coordination for P1/P2 |
| IT Ops / System Owner | Provides access, maintenance window, credentials (where needed) |
| Evidence Custodian | Ensures secure storage, access control, retention, and transfers |
| MSSP Service Delivery | Coordinates client approvals and evidence handling requirements |

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

# 6. Forensic Acquisition Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Do no harm | Minimize changes to the target system and evidence |
| Repeatability | Steps must be consistent and documented |
| Integrity verification | Pre/post hashes must be recorded and matched |
| Chain-of-custody | Required for P1/P2 and any legal/regulatory-sensitive case |
| Least necessary scope | Full disk preferred; targeted acquisition only with justification |
| Secure handling | Encrypt evidence transfers; restrict access |
| Time accuracy | All timestamps recorded in UTC |

---

# 7. Acquisition Triggers (When Disk Imaging is Required)

Disk acquisition is recommended/required when:

| Scenario | Examples |
|---|---|
| Confirmed compromise | Malware infection, persistence suspected, unauthorized access |
| Ransomware event | Encryption activity, ransom note, suspected staging |
| Data breach investigation | Suspected exfil tools, staging directories |
| Insider threat | Evidence preservation for HR/legal actions (follow approvals) |
| Incident scope unclear | Need to validate timeline, lateral movement artifacts |
| Regulatory/audit requirements | Evidence preservation per incident reporting obligations |

---

# 8. Approvals and Authority

Disk acquisition may require downtime, system reboot, or physical access. Approvals depend on criticality and scope.

## 8.1 Minimum Approval Matrix (Guidance)

| Action | Minimum Approval |
|---|---|
| Acquire disk image of standard endpoint | IR Team Lead or SOC Lead |
| Acquire disk image of critical server | IR Team Lead + System Owner + SOC Manager |
| Power-off/shutdown to protect evidence | IR Team Lead + System Owner (best effort in P1) |
| Physical disk removal | IR Team Lead + System Owner + Data Center/IT Ops |
| Targeted acquisition instead of full image | Forensics Lead approval + justification in ticket |

## 8.2 MSSP Client Approvals

For client systems:

- Confirm contractual authority to collect forensic images
- Obtain client approval where required
- Ensure evidence storage is **client-segregated**
- Follow client escalation matrix if present

Reference:  
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

---

# 9. Ticketing and Evidence Documentation Requirements (Mandatory)

Every acquisition must be linked to an incident ticket.

Minimum ticket fields:

| Field | Requirement |
|---|---|
| Incident/Ticket ID | Mandatory |
| Target system details | Hostname, IP, asset tag, owner, role/criticality |
| Acquisition rationale | Why disk imaging is required |
| Acquisition scope | Full disk / partitions / targeted (with justification) |
| Acquisition method | Live / offline / snapshot |
| Start/end time (UTC) | Mandatory |
| Tools used | Name + version (where possible) |
| Image format | E01/RAW and compression settings |
| Hash algorithm | SHA256 (preferred) |
| Storage location | Evidence repository path/reference |
| CoC requirement | Yes/No with rationale |
| Approvals | Names + timestamps (UTC) |

References:  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`

---

# 10. Pre-Acquisition Checklist (Mandatory)

Before collecting a disk image:

| Check | Requirement |
|---|---|
| Confirm incident priority and urgency | Mandatory |
| Confirm system identification (no wrong-host imaging) | Mandatory |
| Confirm access method (onsite/remote/cloud) | Mandatory |
| Confirm whether system must remain powered | Mandatory |
| Confirm encryption status (BitLocker/FileVault/LUKS) | Mandatory |
| Confirm storage capacity for image | Mandatory |
| Confirm write-blocking approach (hardware preferred for offline) | Mandatory |
| Confirm evidence storage destination prepared | Mandatory |
| Confirm CoC forms prepared (if required) | Mandatory |
| Confirm data sensitivity and handling restrictions | Mandatory |

---

# 11. Acquisition Methods (Standard)

Choose the method based on scenario, feasibility, and evidence requirements.

## 11.1 Method A — Offline Acquisition (Preferred When Feasible)

**Best for forensic soundness.** Typically requires powering down and imaging via write blocker.

Use when:

- System can be safely taken offline
- Physical access is available
- Evidence integrity requirements are strict (legal/regulatory)

High-level steps:

1. Obtain approvals and schedule downtime (unless emergency)
2. Power down system gracefully (or as directed by IR Team Lead)
3. Remove disk (if required) and connect via **hardware write blocker**
4. Acquire full disk image (E01 or RAW)
5. Compute and record hashes
6. Securely store image + logs
7. Complete CoC records

---

## 11.2 Method B — Live Acquisition (Use When Downtime Not Possible)

Live imaging may introduce changes (system writes). It is acceptable when:

- Business cannot tolerate downtime
- Immediate evidence preservation is required
- Cloud/virtual environment snapshotting is not available

Mandatory controls:

- Document that acquisition was live and why
- Minimize system interactions
- Prefer read-only methods and limit additional tools installed
- Capture critical artifacts promptly (logs, triage) alongside imaging

---

## 11.3 Method C — Virtual/Cloud Snapshot Acquisition (Preferred for Cloud/VMs)

Use when:

- The system is a VM with snapshot capability
- Cloud provider supports volume snapshots/export

Controls:

- Document snapshot ID(s), time (UTC), and scope
- Ensure snapshots are copied to secure, access-controlled evidence storage
- Validate integrity via provider checksums + local hashing after export (where possible)
- Ensure tenant segregation (MSSP)

---

# 12. Acquisition Procedure (Minimum Standard Steps)

> Exact tool commands differ by environment. The steps below define mandatory outcomes and documentation requirements.

## 12.1 Step 1 — Identify and Record Target Details

Record in ticket/evidence log:

- Hostname, IP, asset tag
- Device type (endpoint/server)
- OS and disk type (HDD/SSD/NVMe)
- Disk size and partitions (if known)
- Encryption status (enabled/disabled/unknown)
- Current state (powered on/off)
- Location (site/DC/cloud region)

---

## 12.2 Step 2 — Prepare Destination Storage

| Requirement | Standard |
|---|---|
| Storage must be approved evidence repository | Mandatory |
| Storage must be access-controlled | Mandatory |
| Storage must be encrypted at rest | Mandatory |
| Sufficient capacity available | Mandatory |
| Folder naming standard applied | Mandatory |

Recommended folder naming:

`/evidence/INC-[ID]/disk/[HOSTNAME]-[YYYYMMDD]/`

---

## 12.3 Step 3 — Acquire Image

Mandatory requirements during acquisition:

| Requirement | Standard |
|---|---|
| Acquire full disk unless approved otherwise | Mandatory |
| Record tool name/version | Mandatory |
| Record image format and settings | Mandatory |
| Record start and end time (UTC) | Mandatory |
| Capture acquisition logs | Mandatory |
| Avoid writing to evidence disk (use write blocker where feasible) | Mandatory |

---

## 12.4 Step 4 — Integrity Verification (Hashing)

Hashing requirements:

| Item | Requirement |
|---|---|
| Hash algorithm | SHA256 preferred (MD5/SHA1 optional as secondary) |
| Hash of source media | Where feasible (especially offline imaging) |
| Hash of acquired image file(s) | Mandatory |
| Hash match verification | Mandatory |
| Record hashes in ticket and evidence log | Mandatory |

If hashes do not match:

- Stop processing
- Escalate to Forensics Lead / IR Team Lead
- Repeat acquisition if possible
- Document discrepancy and actions taken

---

## 12.5 Step 5 — Secure Transfer and Storage

- Transfer evidence using approved secure method
- Encrypt during transfer (where applicable)
- Store in designated evidence repository
- Restrict access to approved personnel only
- Update CoC and evidence log with storage location and custodian

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`

---

# 13. Evidence Log Requirements (Mandatory)

For each disk image, maintain an evidence log entry including:

| Field | Requirement |
|---|---|
| Evidence ID | Mandatory |
| Incident ID | Mandatory |
| Device/Host | Mandatory |
| Collector | Mandatory |
| Date/time acquired (UTC) | Mandatory |
| Method | Offline/Live/Snapshot |
| Tool + version | Mandatory |
| Image format | E01/RAW |
| Size | Mandatory |
| Hashes | SHA256 required |
| Storage location | Mandatory |
| Access restrictions | Mandatory |
| CoC reference | Mandatory if CoC used |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`

---

# 14. Chain of Custody (CoC) Requirements

CoC is mandatory when:

- P1/P2 incidents
- Potential legal action / law enforcement
- Insider threat cases involving HR/legal
- Client contract requires forensic-grade handling

Minimum CoC actions:

1. Complete CoC form at collection time
2. Record every transfer (who/when/why)
3. Store evidence in secure evidence storage
4. Maintain integrity (hash verification as needed)

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`

---

# 15. Special Considerations

## 15.1 Encrypted Disks (BitLocker/FileVault/LUKS)

- Record encryption status in ticket
- If live and decrypted, acquisition may capture accessible content
- If offline and encrypted, coordinate with system owner/IR lead on key availability
- Do not attempt unauthorized decryption
- Document limitations clearly in the final report

## 15.2 SSD/NVMe and TRIM

- SSD TRIM may reduce recoverability of deleted artifacts
- Prefer immediate acquisition once incident is detected
- Document storage type and any limitations

## 15.3 Critical Systems

For critical servers:

- Coordinate with IT Ops for downtime
- Consider snapshot method if feasible
- Ensure rollback/BCP considerations are addressed
- Maintain continuous monitoring during acquisition planning

---

# 16. MSSP Client Requirements (Mandatory)

For MSSP forensic imaging:

| Requirement | Standard |
|---|---|
| Client ID recorded in ticket and evidence log | Mandatory |
| Evidence storage segregated by client | Mandatory |
| Client approvals documented | Mandatory (contract-dependent) |
| Client data handling restrictions respected | Mandatory |
| No cross-client tooling contamination | Mandatory (use clean acquisition media/tooling) |
| Secure transfer method agreed | Mandatory |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 17. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Imaging wrong host/disk | Investigation failure | Pre-check system identity + asset tag |
| No hashes recorded | Evidence integrity failure | SHA256 mandatory |
| No acquisition logs | Audit failure | Tool logs required |
| Storing images on local machine | Evidence loss | Approved evidence repository only |
| No CoC for P1/P2 | Legal/audit exposure | CoC mandatory triggers |
| Broad access to evidence | Data leakage | Access control + encryption |
| Targeted acquisition without justification | Missed artifacts | Require approval + rationale |

---

# 18. Related Documents

| Document | Path |
|---|---|
| Forensics Toolkit Reference | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Forensics-Toolkit-Reference.md` |
| Memory Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md` |
| Log Collection SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Log-Collection-SOP.md` |
| Tool Chain of Custody | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Tool-Chain-of-Custody.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| CoC Digital Evidence | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |

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