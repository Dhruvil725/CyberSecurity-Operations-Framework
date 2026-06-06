# Forensics Toolkit Reference

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Reference – Forensics Toolkit |
| Document ID | TOOL-FOR-002 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | IR Team Lead / Digital Forensics Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This document defines the standard forensic tools approved for use by the SOC/IR team to support:

- Evidence acquisition (disk, memory, logs)
- Forensic analysis (timeline, artifacts, malware triage)
- Integrity verification (hashing)
- Reporting and evidence packaging

Standardization is critical because:

- Tool consistency improves repeatability and defensibility of forensic findings
- Unapproved tools may contaminate evidence or violate licensing constraints
- Audit and regulatory reviews require documented toolchains and versions
- MSSP operations require controlled tool usage to prevent cross-client data leakage
- Forensics requires integrity verification and secure handling at every step

This reference ensures:

- Approved tool inventory for acquisition and analysis
- Minimum usage rules and constraints per tool category
- Version and licensing tracking requirements
- Standard outputs and evidence expectations
- Alignment with chain-of-custody requirements

---

# 3. Scope

This reference applies to:

| Area | Included |
|---|---|
| Acquisition | Disk imaging, memory capture, log collection, cloud snapshot exports |
| Analysis | Host-based artifacts, timeline building, browser/email artifacts, malware triage |
| Network forensics | PCAP review tools (where used by forensics team) |
| Integrity | Hashing and verification |
| Reporting | Evidence packaging and final report support |

Out of scope:

- Exploit development tooling
- Offensive security tooling (except where explicitly approved for malware analysis sandbox)

---

# 4. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| Digital Forensics Lead | Owns the toolkit reference, approves new tools, manages quarterly review |
| L3 Forensics Analyst | Uses tools according to SOPs; records tool versions used per case |
| L2 Analyst | Uses approved triage tools for scoped tasks when authorized |
| IR Team Lead | Ensures correct tool usage in P1/P2 investigations; approves deviations |
| SOC Manager | Approves procurement and licensing; ensures governance compliance |
| Evidence Custodian | Ensures tool media integrity for offline kits and secure storage |

---

# 5. Tool Governance Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Approved tools only | Use only tools listed here unless emergency exception approved |
| Record versions | Tool name + version must be documented in tickets/reports for evidence-grade work |
| Licensing compliance | Follow licensing restrictions and client contract constraints |
| Clean media | Use clean, validated acquisition media; prevent cross-case contamination |
| Minimal footprint | Prefer portable/read-only tools for live acquisition |
| Integrity validation | Hash evidence outputs where applicable |
| Secure storage | Store tool installers/scripts in controlled repository with hashes |

---

# 6. Tool Categories and Approved Tools

> Tool names below are examples of common industry tooling. Replace/adjust to your organization's actual toolset. Document exact versions in case tickets.

## 6.1 Acquisition Tools (Disk)

| Tool | Purpose | Supported Output | Notes / Controls |
|---|---|---|---|
| FTK Imager (or equivalent) | Disk imaging (live/offline) | RAW/E01 | Preferred for Windows acquisition |
| dd / dc3dd | Linux-based imaging | RAW | Use with write blockers where possible |
| Guymager | Linux imaging GUI | RAW/E01 | Useful for offline imaging |
| Hardware write blockers | Prevent disk writes | N/A | Preferred for offline disk imaging |

Reference SOP:
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md`

---

## 6.2 Acquisition Tools (Memory)

| Tool | Purpose | Output | Notes / Controls |
|---|---|---|---|
| WinPmem / Magnet RAM Capture (or equivalent) | Memory acquisition | RAW | Prefer minimal footprint |
| LiME (Linux) | Linux memory capture | RAW | Requires kernel module; document impact |
| macOS memory tools (approved) | macOS RAM capture | RAW | Limited; follow vendor guidance |

Reference SOP:
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md`

---

## 6.3 Log and Artifact Collection Tools

| Tool | Purpose | Output | Notes / Controls |
|---|---|---|---|
| KAPE (Windows) | Rapid artifact collection | ZIP/Folder | Use targeted collections; document modules used |
| Velociraptor (if deployed) | Remote collection/hunting | VQL results | Ensure tenant segregation for MSSP |
| Sysmon export tooling | Collect Sysmon logs | EVTX/JSON | Follow log retention and integrity rules |
| Native OS utilities | Collect logs and artifacts | EVTX, TXT | Document commands and paths |

Reference SOP:
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Log-Collection-SOP.md`

---

## 6.4 Integrity / Hashing Tools

| Tool | Purpose | Output | Notes |
|---|---|---|---|
| sha256sum / shasum | Hash verification | SHA256 | Preferred standard |
| certutil (Windows) | Hash calculation | SHA256 | Widely available on Windows |
| md5sum / sha1sum | Legacy hashes | MD5/SHA1 | Optional secondary only |

Mandatory:
- SHA256 required for evidence-grade validation.

---

## 6.5 Disk and File System Analysis Tools

| Tool | Purpose | Notes |
|---|---|---|
| Autopsy / Sleuth Kit | Disk image analysis and timelines | Suitable for broad analysis |
| X-Ways Forensics (or equivalent) | Deep Windows forensic analysis | Commercial; record license usage |
| Plaso / log2timeline | Timeline generation | Useful for multi-source artifacts |
| Registry analysis tools | Windows registry parsing | Document hive sources |
| Prefetch/Amcache parsers | Execution evidence analysis | Validate time zones and timestamps |

---

## 6.6 Malware Triage and Analysis Tools (Controlled Use)

| Tool | Purpose | Controls |
|---|---|---|
| Static analysis tools (strings, pefile, etc.) | Malware triage | Run only in isolated sandbox |
| Dynamic sandbox (approved) | Behavioral analysis | No production network access |
| YARA scanning tools | Malware detection/classification | Use curated rules; record rule set version |

Mandatory controls:

- Use dedicated isolated analysis environment
- Do not run samples on production endpoints
- Maintain sample custody and hashing

Reference:
`03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Malware-Analysis-SOP.md`

---

## 6.7 Network Forensics Tools (If Used by Forensics Team)

| Tool | Purpose | Notes |
|---|---|---|
| Wireshark / tshark | PCAP analysis | Use filters; preserve original PCAP |
| Zeek (if available) | Network metadata extraction | Useful for large captures |
| Flow analysis tools | Identify exfil patterns | Align with SIEM evidence |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md`

---

# 7. Tool Selection Guidance (When to Use What)

## 7.1 Disk Acquisition Decision Guidance

| Scenario | Recommended Tooling |
|---|---|
| Offline imaging with physical access | Hardware write blocker + imaging tool (E01 preferred) |
| Live endpoint imaging (downtime not possible) | Live imaging tool + hashing + logs |
| VM/cloud disk evidence | Snapshot export + hashing where feasible |
| Large disks/time constraint | Targeted acquisition only with approval |

---

## 7.2 Memory Acquisition Decision Guidance

| Scenario | Recommended Tooling |
|---|---|
| Suspected in-memory malware | Memory capture tool + volatility-based analysis |
| Credential dumping suspected | Capture memory quickly before reboot/shutdown |
| Server cannot be rebooted | Live memory capture with minimal footprint |

---

# 8. Tool Integrity and Storage

## 8.1 Tool Repository Requirements (Mandatory)

All tools/scripts used for forensics must be stored in a controlled repository:

| Control | Requirement |
|---|---|
| Access control | Limited to IR/Forensics team |
| Versioning | Mandatory |
| Hashes of installers/scripts | Mandatory |
| Change tracking | Mandatory |
| Malware sample separation | Mandatory (do not store with tools) |

## 8.2 Offline Kit Management (If Applicable)

Offline acquisition kits must include:

- Clean storage drives
- Write blockers
- Verified tool media
- Chain-of-custody forms
- Evidence labels

Kits must be:

- Sealed or logged when issued/returned
- Checked quarterly for completeness and tool updates

---

# 9. Licensing and Compliance Requirements

| Requirement | Standard |
|---|---|
| Use tools within license terms | Mandatory |
| Record commercial tool usage per case | Recommended |
| Do not install unlicensed tools on client systems | Mandatory (MSSP) |
| Follow client restrictions for tooling | Mandatory (MSSP) |
| Avoid exporting restricted intel/tool outputs | Mandatory |

---

# 10. Standard Output and Documentation Requirements

For evidence-grade work, document:

| Item | Requirement |
|---|---|
| Tool name and version | Mandatory |
| Acquisition method (live/offline/snapshot) | Mandatory |
| Hash algorithm and values | Mandatory |
| Output file names and paths | Mandatory |
| Analyst name and timestamp (UTC) | Mandatory |
| Any errors/warnings encountered | Mandatory |
| Validation performed | Mandatory |

---

# 11. Tool Exceptions Process

If a tool not listed here must be used:

| Step | Requirement |
|---|---|
| Create exception request ticket | Mandatory |
| Justify why approved tools are insufficient | Mandatory |
| Validate tool safety and licensing | Mandatory |
| IR Team Lead approval | Mandatory |
| Document tool usage and outputs | Mandatory |
| Add tool to toolkit reference if permanently adopted | Recommended |

Reference:
`00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`

---

# 12. Related Documents

| Document | Path |
|---|---|
| Disk Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md` |
| Memory Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md` |
| Log Collection SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Log-Collection-SOP.md` |
| Tool Chain of Custody | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Tool-Chain-of-Custody.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |
| L3 Malware Analysis SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Malware-Analysis-SOP.md` |

---

# 13. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | IR Team Lead / Digital Forensics Lead | Initial version |

---

# 14. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**