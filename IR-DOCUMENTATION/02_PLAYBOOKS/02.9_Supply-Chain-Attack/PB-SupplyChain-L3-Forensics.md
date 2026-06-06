# Playbook: Supply Chain Attack – L3 Forensics and Advanced Analysis

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Supply Chain Attack (L3 Forensics and Advanced Analysis) |
| Document ID    | IR-PB-SC-004                                                 |
| Version        | 1.0                                                          |
| Effective Date | 19-May-2026                                                  |
| Owner          | L3 Lead / IR Team Lead                                       |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 supply chain incident          |

---

## 2. Purpose

This document defines the Level 3 (L3) forensic and advanced analysis procedures for supply chain attacks.

L3 involvement is required when:

- Malicious functionality execution is **confirmed or highly likely** across one or more systems
- **Lateral movement** has been detected or suspected beyond the initial supply chain entry point
- **Persistence mechanisms** have been identified requiring forensic confirmation and removal validation
- **Data exfiltration** is confirmed or suspected requiring forensic reconstruction of what was taken
- The **dwell time appears significant** (weeks or months) requiring extended timeline reconstruction
- **CI/CD pipeline compromise** is confirmed and deployed code integrity must be forensically validated
- **Legal or regulatory evidence** requirements necessitate forensic-grade collection and chain-of-custody
- The incident may overlap with a broader **APT campaign** requiring advanced attribution analysis
- **Cloud infrastructure** has been compromised through the supply chain vector

L3 objectives:

- Reconstruct the **full attack chain** from initial supply chain entry through all attacker activity
- Identify **patient zero** — the first system where malicious functionality executed
- Confirm all **persistence mechanisms** and provide validated eradication guidance
- Confirm **data access and exfiltration scope** with forensic-grade evidence
- Validate **CI/CD pipeline and build artifact integrity** if pipeline compromise occurred
- Generate a **defensible evidence package** for legal, regulatory, and executive use
- Produce **IOC and TTP packages** for detection engineering and threat intelligence
- Provide **eradication criteria** that IR Team and platform teams can execute with confidence

---

## 3. Scope

Applies to L3 forensic investigation of:

- Software update supply chain attacks with confirmed or likely execution on internal systems
- Malicious package or dependency attacks with confirmed installation and execution in production
- CI/CD pipeline compromises with potential backdoored code deployed to production
- MSP/MSSP compromise with confirmed or suspected pivot into managed environments
- Open-source library attacks with active exploitation confirmed in application runtime
- Cloud infrastructure compromise originating from supply chain vector
- Hardware supply chain incidents where digital forensic evidence supports investigation

Includes:

- On-premises servers and workstations
- Cloud VMs, containers, serverless, and PaaS environments
- CI/CD infrastructure and build servers
- Development environments (if connected to production)
- MSSP-managed client environments (strict evidence segregation required)

---

## 4. Preconditions (Inputs from L2 and SOC Lead)

L3 begins after L2 has:

- Confirmed or assessed execution likelihood with supporting evidence
- Completed scope identification (affected systems inventory)
- Completed IoC search across extended time window (90+ days)
- Performed lateral movement and persistence preliminary assessments
- Completed data breach trigger assessment
- Obtained necessary access approvals for forensic collection on production systems
- Ensured operations teams are not applying updates or making changes to affected systems

Minimum required inputs from L2:

| Input                           | Minimum Content                                              |
| ------------------------------- | ------------------------------------------------------------ |
| Incident summary                | Attack type, affected software/vendor, severity, timeline    |
| Affected systems inventory      | Full list with hostname, IP, environment, version, priority  |
| IoC match results               | All IoC types searched, results, evidence references         |
| Execution confidence level      | Confirmed / Highly Likely / Possible with evidence basis     |
| Lateral movement assessment     | Confirmed / Suspected / Not confirmed with evidence          |
| Persistence assessment          | Confirmed / Suspected / Not confirmed with evidence          |
| Data breach trigger decision    | Yes / No / Unknown with documentation                        |
| Containment actions taken       | What has been blocked/isolated/revoked so far                |
| Access approvals                | Approvals for forensic collection on production systems      |
| Evidence preserved by L2        | References to all evidence captured at L1/L2 stages          |

Reference: `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L2-Investigation.md`

---

## 5. L3 Required Outputs (Deliverables)

L3 must deliver the following to IR Team, SOC Lead, and Legal/Compliance as applicable:

| Deliverable                          | Description                                                  |
| ------------------------------------ | ------------------------------------------------------------ |
| Authoritative Attack Timeline        | UTC timeline from initial supply chain compromise through all attacker activity |
| Patient Zero Identification          | First system where malicious functionality executed with evidence |
| Full Scope Confirmation              | Forensically confirmed list of all compromised systems       |
| Persistence Confirmation             | All persistence mechanisms identified with locations and removal guidance |
| Lateral Movement Map                 | Complete map of attacker movement through the environment    |
| Data Access and Exfiltration Report  | Confirmed/estimated data accessed, collected, and exfiltrated |
| CI/CD Integrity Report               | Build artifact hash verification results; backdoored code identification |
| IOC Package                          | Hashes, paths, domains, IPs, process names, registry keys    |
| TTP / MITRE Mapping                  | Technique mapping for report and threat intelligence         |
| Eradication Guidance                 | What to remove, rebuild, rotate; validation criteria         |
| Detection and Hunt Recommendations   | SIEM/EDR queries, alert gaps, coverage improvements          |
| Evidence Package                     | Hashed artifacts with chain-of-custody documentation         |

---

## 6. Forensic Principles and Evidence Rules

### 6.1 Evidence Integrity Requirements

| Rule                    | Requirement                                                  |
| ----------------------- | ------------------------------------------------------------ |
| Preserve before analyze | Acquire forensic images and memory captures before any analysis that may alter state |
| Hash all artifacts      | Compute SHA-256 hash for all collected evidence files and disk images |
| Chain-of-custody        | Maintain transfer records for all P1/P2 evidence and any evidence with legal implications |
| Minimize footprint      | Use read-only forensic techniques where possible; avoid writing to evidence media |
| UTC timestamps          | Normalize all event timestamps to UTC; document timezone conversions |
| Document everything     | Record every action taken during forensic collection with timestamps |
| Least disruption        | Coordinate with business owners before taking systems offline for forensic collection |

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

### 6.2 Supply Chain Forensics Specific Considerations

Supply chain forensics has unique challenges that differ from standard forensic investigations:

**Long dwell time implications:**
- Log retention may be insufficient to cover the full dwell period
- Attacker artifacts may have been cleaned up or overwritten
- Multiple rounds of legitimate software updates may have overwritten malicious files
- Forensic reconstruction may require correlation across many systems simultaneously

**Trusted software complications:**
- Malicious code runs under a trusted, signed process making behavioral analysis complex
- Standard malware signatures will not detect supply chain backdoors initially
- Code signing certificates make file integrity checks more complex
- Standard EDR behavioral rules may be tuned to allow vendor software behavior

**Evidence confidentiality:**
- Forensic artifacts may contain customer data requiring careful handling
- Evidence must be strictly segregated per client in MSSP environments
- Some artifacts may be subject to legal hold and cannot be deleted

---

## 7. L3 Investigation Workflow Overview

| Phase    | Focus                                                   | Output                                    |
| -------- | ------------------------------------------------------- | ----------------------------------------- |
| Phase 1  | Evidence acquisition plan and collection                | Evidence manifest with hashes             |
| Phase 2  | Malicious component analysis (binary/package/script)    | Malware analysis report                   |
| Phase 3  | System-level forensics (disk and memory)                | Host compromise confirmation              |
| Phase 4  | Attack timeline reconstruction                          | Authoritative UTC timeline                |
| Phase 5  | Lateral movement forensic confirmation                  | Lateral movement map with evidence        |
| Phase 6  | Persistence forensic confirmation                       | Persistence inventory with removal steps  |
| Phase 7  | Data access and exfiltration forensics                  | Data scope report with volume estimates   |
| Phase 8  | CI/CD and build artifact integrity analysis             | Integrity validation report               |
| Phase 9  | Cloud and IAM forensics                                 | Cloud compromise assessment               |
| Phase 10 | IOC and TTP package generation                          | Threat intelligence output package        |
| Phase 11 | Eradication guidance and clean state definition         | Eradication checklist                     |

---

## 8. Phase 1 – Evidence Acquisition Plan

### 8.1A Evidence Priority by System Classification

| System Classification          | Evidence to Acquire                              | Priority | Method                          |
| ------------------------------ | ------------------------------------------------ | -------- | ------------------------------- |
| Patient zero (first execution) | Full disk image + memory capture + all logs      | Critical | Forensic workstation; read-only |
| Systems with IoC matches       | Full disk image + memory capture + all logs      | Critical | Forensic workstation; read-only |
| Lateral movement targets       | Memory capture + targeted disk artifacts + logs  | High     | EDR + targeted collection       |
| All other affected systems     | Targeted artifact collection + logs              | Medium   | EDR + log export                |
| Build servers / CI/CD          | Full disk image + all pipeline logs + artifacts  | Critical | Forensic workstation; read-only |
| Cloud instances                | Snapshot + cloud audit logs + runtime logs       | High     | Cloud provider forensic tools   |

### 8.1B Evidence Acquisition Checklist (Per System)

For each priority system, collect:

| Evidence Item                    | Method                          | Hash Required | Chain of Custody | Status |
| -------------------------------- | ------------------------------- | ------------- | ---------------- | ------ |
| Full disk image                  | dd / FTK Imager / Velociraptor  | Yes (SHA-256) | Yes              | ☐      |
| Memory capture (RAM)             | WinPmem / LiME / EDR            | Yes (SHA-256) | Yes              | ☐      |
| System event logs (Windows)      | Export from EDR / SIEM / wevtutil | Yes         | Yes              | ☐      |
| Syslog / auth logs (Linux)       | Export from /var/log/           | Yes (SHA-256) | Yes              | ☐      |
| Vendor software logs             | Application-specific log paths  | Yes (SHA-256) | Yes              | ☐      |
| Network connection state         | netstat capture via EDR         | Yes           | Yes              | ☐      |
| Running process list             | EDR / tasklist / ps aux         | Yes           | Yes              | ☐      |
| Scheduled tasks / cron           | Export via EDR / schtasks       | Yes           | Yes              | ☐      |
| Registry hives (Windows)         | Export HKLM/HKCU via forensic tools | Yes       | Yes              | ☐      |
| Installed software list          | EDR / registry / dpkg           | Yes           | Yes              | ☐      |
| Browser artifacts (if relevant)  | Targeted extraction             | Yes           | Yes              | ☐      |

### 8.1C Evidence ID Standard

Use consistent evidence reference IDs for all collected artifacts:

Format: `EV-[INC-ID]-[HOSTNAME]-[SOURCE]-[YYYYMMDD]-[SEQ]`

Example: `EV-INC2026-0519-WEBSRV01-DISK-20260519-001`

---

## 9. Phase 2 – Malicious Component Analysis

### 9.1A Analysis Objectives

L3 must analyze the malicious component (backdoored binary, malicious package, injected script) to understand:

- **What it does** — capabilities, C2 mechanisms, data collection, lateral movement features
- **How it evades detection** — obfuscation, anti-analysis techniques, living-off-the-land usage
- **What it accesses** — files, credentials, network, registry
- **What it leaves behind** — persistence mechanisms, dropped files, registry keys

### 9.1B Static Analysis Steps

| Step | Action                                                       | Tools                              | Output                          |
| ---- | ------------------------------------------------------------ | ---------------------------------- | ------------------------------- |
| 1    | Hash the malicious component and compare against known threat databases | VirusTotal / MISP / internal TI | Attribution and known status |
| 2    | Identify file type, architecture, and compilation details    | file / PE-bear / Detect-It-Easy    | File metadata                   |
| 3    | Extract strings from binary for IoCs and capabilities        | strings / FLOSS / BinText          | String artifacts                |
| 4    | Identify imported libraries and functions                    | PE-bear / IDA / Ghidra             | Capability map                  |
| 5    | Extract network indicators (URLs, IPs, domains)              | FLOSS / manual analysis            | Network IoCs                    |
| 6    | Identify obfuscation and packing techniques                  | Detect-It-Easy / DIE / PEiD        | Obfuscation method              |
| 7    | Decompile or disassemble for code-level analysis             | Ghidra / IDA Pro / Binary Ninja    | Code analysis report            |
| 8    | Extract configuration (if applicable)                       | Custom scripts / manual            | C2 config / capabilities        |

### 9.1C Dynamic Analysis Steps (Isolated Environment Only)

**CRITICAL: All dynamic analysis must be performed in an isolated, non-networked analysis environment.**

| Step | Action                                                       | Tools                              | Output                          |
| ---- | ------------------------------------------------------------ | ---------------------------------- | ------------------------------- |
| 1    | Set up isolated sandbox environment (no network access to real infrastructure) | Cuckoo / Any.run / custom sandbox | Isolated environment |
| 2    | Execute malicious component and monitor all system activity  | Procmon / API Monitor / Cuckoo     | Behavioral report               |
| 3    | Monitor network activity (use simulated C2 if needed)        | FakeNet-NG / INetSim               | Network behavior                |
| 4    | Monitor file system changes                                  | Procmon / FIM in sandbox           | File artifacts                  |
| 5    | Monitor registry changes (Windows)                          | Procmon / RegShot                  | Registry persistence            |
| 6    | Monitor process creation and injection                       | Procmon / API Monitor              | Execution chain                 |
| 7    | Capture memory during execution for in-memory artifact extraction | Volatility / WinPmem + Volatility | Memory artifacts |
| 8    | Document all observed behaviors with timestamps              | Manual documentation               | Behavioral timeline             |

### 9.1D Package and Script Analysis (For Package Supply Chain Attacks)

For malicious npm, PyPI, or similar packages:

| Step | Action                                                       | Output                          |
| ---- | ------------------------------------------------------------ | ------------------------------- |
| 1    | Extract and review all package files (do not execute)        | File listing and content        |
| 2    | Review install scripts (preinstall, postinstall, setup.py)   | Malicious install behavior      |
| 3    | Review main module code for malicious functionality          | Code analysis                   |
| 4    | Identify obfuscated code sections (base64, eval, exec)       | Deobfuscated payload            |
| 5    | Extract all network endpoints referenced in code             | Network IoCs                    |
| 6    | Identify what environment variables or files the package accesses | Data theft scope            |
| 7    | Determine when malicious code executes (install, import, runtime) | Execution trigger              |
| 8    | Compare against legitimate package version (if available)    | Diff report of changes          |

---

## 10. Phase 3 – System-Level Forensics (Disk and Memory)

### 10.1A Disk Forensics (Priority Systems)

#### File System Analysis

| Analysis Task                           | What to Look For                                             | Tools                        |
| --------------------------------------- | ------------------------------------------------------------ | ---------------------------- |
| Timeline analysis (MAC times)           | File creation/modification/access times correlating to attack timeline | Autopsy / Plaso / log2timeline |
| Deleted file recovery                   | Attacker-deleted tools or staging files                      | Autopsy / Sleuth Kit         |
| Prefetch analysis (Windows)             | Evidence of program execution (attacker tools run)           | WinPrefetchView / Autopsy    |
| LNK file analysis                       | Shortcuts pointing to attacker tools or staging areas        | LECmd / Autopsy              |
| Browser history (if relevant)           | Attacker activity if using browser-based access              | Hindsight / Autopsy          |
| Shellbag analysis (Windows)             | Evidence of directory browsing by attacker                   | ShellBagsExplorer            |
| USN journal analysis (Windows)          | File system change history                                   | MFTECmd / Autopsy            |
| MFT analysis (Windows)                 | Complete file system metadata including deleted files        | MFTECmd / Autopsy            |
| Temp and staging directories            | Data staging before exfiltration                             | Manual + Autopsy             |
| Vendor software directories             | Malicious modifications to vendor files                      | Manual + hash comparison     |

#### Registry Forensics (Windows)

| Registry Location                    | What to Look For                                 | Tools                   |
| ------------------------------------ | ------------------------------------------------ | ----------------------- |
| HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run | Persistence via run keys          | RegRipper / Autopsy     |
| HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run | User-level persistence            | RegRipper / Autopsy     |
| HKLM\SYSTEM\CurrentControlSet\Services | Malicious services installed by attacker      | RegRipper / Autopsy     |
| HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options | IFEO hijacking | RegRipper      |
| ShimCache / AppCompatCache           | Evidence of program execution                    | RegRipper / AppCompatCacheParser |
| Amcache.hve                          | Application execution history                    | AmcacheParser / Autopsy  |
| UserAssist                           | GUI program execution history                    | RegRipper               |
| MRU lists                            | Recently accessed files and commands             | RegRipper               |

### 10.2A Memory Forensics

Memory forensics is critical for supply chain attacks because:
- Backdoors may be **fileless** (existing only in memory)
- C2 configuration may be **stored only in memory** (not on disk)
- **Injected code** into legitimate processes appears only in memory
- **Encryption keys** for encrypted C2 communications may be in memory

#### Memory Analysis Steps

| Step | Action                                                       | Tools                          | Output                          |
| ---- | ------------------------------------------------------------ | ------------------------------ | ------------------------------- |
| 1    | Acquire memory image using appropriate acquisition tool      | WinPmem / LiME / EDR           | Raw memory image                |
| 2    | Identify OS profile for memory image                         | Volatility imageinfo           | OS profile                      |
| 3    | List running processes at time of capture                    | Volatility pslist / pstree     | Process list                    |
| 4    | Identify hidden or suspicious processes                      | Volatility psscan vs pslist    | Hidden process list             |
| 5    | Analyze process memory for injected code                     | Volatility malfind             | Injected code segments          |
| 6    | Extract network connections from memory                      | Volatility netscan / netstat   | Network connections             |
| 7    | Identify loaded DLLs and detect DLL injection                | Volatility dlllist / ldrmodules | Injected DLL list             |
| 8    | Extract strings from suspicious process memory               | Volatility strings + grep      | Memory string artifacts         |
| 9    | Recover C2 configuration from memory                         | Custom Volatility plugins / YARA | C2 configuration               |
| 10   | Identify registry hives loaded in memory                     | Volatility hivelist            | Registry context                |
| 11   | Extract credentials from memory (LSASS)                      | Volatility hashdump / lsadump  | Credential exposure assessment  |
| 12   | Scan memory with YARA rules for known supply chain indicators | Volatility yarascan            | YARA match results              |

---

## 11. Phase 4 – Attack Timeline Reconstruction

### 11.1A Timeline Anchor Points (Establish First)

| Anchor Point                            | Evidence Source                        | Why Critical                              |
| --------------------------------------- | -------------------------------------- | ----------------------------------------- |
| Vendor-side compromise date (if known)  | Vendor advisory / threat intelligence  | Defines maximum possible dwell start date |
| Affected software installation date     | OS install logs / software manager     | Organization's exposure start date        |
| Affected software update date           | Windows Update / package manager logs  | Specific version introduction date        |
| First network connection to C2          | Firewall / proxy / DNS logs            | First execution indicator                 |
| First malicious process execution       | EDR / OS audit logs                    | Execution confirmed timestamp             |
| First lateral movement event            | AD logs / EDR / firewall               | Spread start timestamp                    |
| First data collection or staging        | EDR file system / DLP                  | Data theft start timestamp                |
| First exfiltration event                | Proxy / firewall / NetFlow             | Data loss start timestamp                 |
| Containment start                       | Firewall change logs / EDR isolation   | Stop point for active compromise          |
| Last confirmed attacker activity        | All sources                            | Confirms containment effectiveness        |

### 11.1B Timeline Construction Table (Authoritative Output)

All events must be recorded in UTC:

| Timestamp (UTC)     | System / Source | Event Type            | Event Detail                              | Evidence Reference   | Attacker Action? |
| ------------------- | --------------- | --------------------- | ----------------------------------------- | -------------------- | ---------------- |
| 2026-02-14 03:22:11 | WEBSRV01 / EDR  | Software update       | Affected vendor software v3.2.1 installed | EV-INC-WEBSRV01-001  | No (legitimate)  |
| 2026-02-14 03:25:44 | WEBSRV01 / Proxy| Network connection    | Outbound HTTPS to C2 domain confirmed IoC | EV-INC-WEBSRV01-002  | Yes              |
| 2026-02-14 03:26:01 | WEBSRV01 / EDR  | Process creation      | cmd.exe spawned by vendor software process | EV-INC-WEBSRV01-003 | Yes              |
|                     |                 |                       |                                           |                      |                  |

### 11.1C Multi-System Timeline Correlation

For supply chain attacks affecting multiple systems:

- Create a **master timeline** that incorporates events from all affected systems
- Identify **sequence patterns** — which system was compromised first, second, and so on
- Map **propagation speed** — how quickly the attacker moved from initial system to others
- Identify **gaps in attacker activity** — periods of dormancy that may indicate waiting for opportunity
- Identify **acceleration points** — periods of increased activity that may indicate specific objectives being executed

---

## 12. Phase 5 – Lateral Movement Forensic Confirmation

### 12.1A Forensic Evidence of Lateral Movement

| Movement Type                  | Forensic Evidence                                            | Tools / Sources                |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------ |
| RDP lateral movement           | Windows Event 4624 (logon type 10) on destination; RDP bitmap cache | Windows Event Logs / Autopsy |
| SMB/Pass-the-Hash              | Windows Event 4624 (logon type 3) + NTLM auth; no Kerberos  | Windows Event Logs / SIEM      |
| WMI lateral movement           | WMI activity logs; process creation on remote system         | Windows Event Logs / EDR       |
| PsExec lateral movement        | ADMIN$ share access; service creation on remote system       | Windows Event Logs / EDR       |
| SSH lateral movement (Linux)   | auth.log entries; known_hosts modifications                  | Auth logs / FIM                |
| Scheduled task remote creation | Windows Event 4698 on destination system                     | Windows Event Logs             |
| Service installation remotely  | Windows Event 7045 on destination system                     | Windows Event Logs             |
| Kerberoasting / Golden Ticket  | Unusual Kerberos TGS requests; Event 4769                    | AD logs / SIEM                 |

### 12.1B Lateral Movement Map (Required Deliverable)

Document the complete attacker movement map:

| Source System | Destination System | Movement Method | Timestamp (UTC) | Credential Used | Evidence Reference |
| ------------- | ------------------ | --------------- | --------------- | --------------- | ------------------ |
|               |                    |                 |                 |                 |                    |

---

## 13. Phase 6 – Persistence Forensic Confirmation

### 13.1A Persistence Mechanism Investigation by Category

**Windows Persistence Locations:**

| Persistence Location                     | Forensic Check Method                        | Evidence Source              |
| ---------------------------------------- | -------------------------------------------- | ---------------------------- |
| Run / RunOnce registry keys              | Export and analyze registry hives            | RegRipper / Autopsy          |
| Scheduled tasks                          | Export XML task definitions; check creation timestamps | schtasks export / Autopsy |
| Windows Services                         | Analyze service registry hive; check binaries | RegRipper / SC query         |
| WMI subscriptions                        | Query WMI repository for event subscriptions | Get-WMIObject / forensic tools |
| Startup folders                          | Review all startup directory contents        | File system analysis         |
| DLL hijacking / sideloading              | Compare DLL load order; check non-standard paths | Process Monitor / Autopsy  |
| COM object hijacking                     | Review HKCU COM registrations                | RegRipper                    |
| Boot/pre-OS persistence (bootkit)        | Analyze MBR/VBR; review boot sequence        | Specialized bootkit tools    |

**Linux Persistence Locations:**

| Persistence Location                     | Forensic Check Method                        | Evidence Source              |
| ---------------------------------------- | -------------------------------------------- | ---------------------------- |
| Cron jobs (/etc/cron* and user crontabs) | Review all cron directories and files        | File system analysis         |
| Systemd services and timers              | Review /etc/systemd and /usr/lib/systemd     | File system analysis         |
| /etc/rc.local and init scripts           | Review startup scripts for modifications     | File system / FIM            |
| SSH authorized_keys                      | Review all user ~/.ssh/authorized_keys       | File system analysis         |
| LD_PRELOAD / LD_LIBRARY_PATH hijacking   | Review /etc/ld.so.conf and environment files | File system analysis         |
| PAM module modification                  | Review /etc/pam.d and PAM libraries          | File system + hash comparison |
| Shell profile modifications              | Review .bashrc, .profile, .bash_profile      | File system analysis         |
| Setuid/setgid binaries                   | Find SUID/SGID binaries not in baseline      | find / -perm /4000           |

**Cloud Persistence Mechanisms:**

| Persistence Type                    | Forensic Check Method                        | Evidence Source              |
| ----------------------------------- | -------------------------------------------- | ---------------------------- |
| New IAM users or roles              | Review IAM audit logs for account creation   | Cloud audit logs             |
| New API keys / access keys          | Review key creation events in audit logs     | Cloud audit logs             |
| New OAuth applications              | Review OAuth app registrations               | Identity platform logs       |
| Lambda/Function backdoors           | Review function code and deployment history  | Cloud audit + code repo      |
| New VPC peering or network routes   | Review network configuration changes         | Cloud audit logs             |
| S3 bucket policy changes            | Review bucket policy modification events     | Cloud audit logs             |
| CloudTrail disabling                | Check for CloudTrail stop/disable events     | Cloud audit logs             |

### 13.1B Persistence Confirmation Checklist (Per System)

| System | Persistence Type | Location / Key / Path | Created Timestamp (UTC) | Attacker Created? | Evidence Reference | Removal Confirmed |
| ------ | ---------------- | --------------------- | ----------------------- | ----------------- | ------------------ | ----------------- |
|        |                  |                       |                         |                   |                    | ☐                 |

---

## 14. Phase 7 – Data Access and Exfiltration Forensics

### 14.1A Data Access Forensics Steps

| Step | Action                                                       | Tools                           | Output                          |
| ---- | ------------------------------------------------------------ | ------------------------------- | ------------------------------- |
| 1    | Identify all data stores accessible to compromised software  | Application configs / IAM review | Data access scope map           |
| 2    | Review database audit logs for queries during dwell period   | DB audit / SIEM                 | Query analysis report           |
| 3    | Review file server access logs for large file access         | File server audit / SIEM        | File access patterns            |
| 4    | Review cloud storage access logs for unusual downloads       | Cloud audit logs                | Storage access report           |
| 5    | Review secrets vault access logs for credential access       | Vault audit logs                | Secrets access report           |
| 6    | Review email access logs if email service accessible         | Exchange / O365 audit           | Email access report             |
| 7    | Identify data staging locations on affected systems          | File system forensics           | Staging locations               |
| 8    | Estimate volume of data accessed and potentially collected   | Query result sizes / file sizes  | Volume estimate                 |

### 14.2A Exfiltration Forensics Steps

| Step | Action                                                       | Tools                           | Output                          |
| ---- | ------------------------------------------------------------ | ------------------------------- | ------------------------------- |
| 1    | Analyze proxy/firewall logs for large outbound transfers     | SIEM / proxy export             | Transfer volume analysis        |
| 2    | Analyze DNS logs for DNS exfiltration patterns               | DNS log analysis / SIEM         | DNS exfil assessment            |
| 3    | Analyze NetFlow/IPFIX for volumetric outbound patterns       | NetFlow analyzer                | Traffic volume report           |
| 4    | Review cloud audit logs for large storage uploads/downloads  | Cloud audit logs                | Cloud transfer report           |
| 5    | Identify exfiltration destinations (IPs, domains, services)  | Proxy / firewall correlation    | Destination profiles            |
| 6    | Estimate exfiltration volume per destination                 | Transfer size logs              | Volume per destination          |
| 7    | Determine exfiltration protocol and method                   | PCAP / proxy logs               | Method identification           |
| 8    | Correlate exfiltration timing with data access events        | Timeline correlation            | Exfil chain confirmation        |

### 14.3A Exfiltration Destination Profiling Table (Required)

For each suspected exfiltration destination:

| Destination IP/Domain | ASN / Provider | Protocol | First Seen (UTC) | Last Seen (UTC) | Volume Estimate | Blocked? | Evidence Reference |
| --------------------- | -------------- | -------- | ---------------- | --------------- | --------------- | -------- | ------------------ |
|                       |                |          |                  |                 |                 |          |                    |

### 14.4A Data Breach Scope Report (Required for Regulatory Use)

| Data Category            | Tables/Files/Systems Accessed | Records Accessed (Estimate) | Time Window | Exfiltrated? (Confirmed/Likely/Unknown) |
| ------------------------ | ----------------------------- | --------------------------- | ----------- | --------------------------------------- |
| Customer PII             |                               |                             |             |                                         |
| Financial records        |                               |                             |             |                                         |
| Authentication credentials|                              |                             |             |                                         |
| Cloud IAM credentials    |                               |                             |             |                                         |
| Source code              |                               |                             |             |                                         |
| Internal configuration   |                               |                             |             |                                         |

---

## 15. Phase 8 – CI/CD Pipeline and Build Artifact Integrity Analysis

This phase applies when CI/CD pipeline compromise is confirmed or suspected.

### 15.1A Build Artifact Integrity Verification

| Step | Action                                                       | Output                          |
| ---- | ------------------------------------------------------------ | ------------------------------- |
| 1    | Identify all deployments made during the suspected dwell period | Deployment list with timestamps |
| 2    | Obtain deployed artifact hashes from artifact registry       | Deployed artifact hash list     |
| 3    | Rebuild each identified deployment from the same source commit independently | Independently built hashes |
| 4    | Compare deployed artifact hashes against independently rebuilt hashes | Hash comparison report    |
| 5    | Flag any hash mismatches for detailed code analysis          | Mismatch list                   |
| 6    | Decompile or disassemble mismatched artifacts to identify injected code | Injected code report     |
| 7    | Identify all production environments where backdoored artifacts were deployed | Affected deployment scope |
| 8    | Assess what the backdoored code did and what access it enabled | Backdoor capability report |

### 15.1B Pipeline Forensics Steps

| Step | Action                                                       | Evidence Source                 | Output                          |
| ---- | ------------------------------------------------------------ | ------------------------------- | ------------------------------- |
| 1    | Export all pipeline run logs during dwell period             | CI/CD platform audit            | Pipeline run log export         |
| 2    | Review all code commits for unauthorized changes             | Source control audit            | Unauthorized commit list        |
| 3    | Review all secrets accessed during pipeline runs             | CI/CD secrets audit             | Secrets exposure list           |
| 4    | Review all external network calls during pipeline runs       | CI/CD logs / network logs       | External call list              |
| 5    | Identify any new variables, scripts, or steps introduced     | Pipeline configuration history  | Unauthorized pipeline changes   |
| 6    | Review container images built during dwell period            | Container registry              | Image integrity report          |

### 15.1C Code Injection Analysis

If injected code is identified in build artifacts:

- Extract injected code segment and analyze statically and dynamically (in isolated environment)
- Determine capabilities: C2, credential theft, data collection, backdoor, persistence
- Identify all functions or services where injected code executes
- Determine what runtime privileges the injected code has
- Assess all production environments potentially affected

---

## 16. Phase 9 – Cloud and IAM Forensics

### 16.1A Cloud Audit Log Analysis

| Service / Event Type           | What to Look For                                             | Evidence Source              |
| ------------------------------ | ------------------------------------------------------------ | ---------------------------- |
| IAM user/role creation         | New accounts created during dwell period                     | CloudTrail / Azure Audit     |
| IAM policy modifications       | Privilege escalation via policy changes                      | CloudTrail / Azure Audit     |
| API key creation               | New access keys for lateral movement or persistence          | CloudTrail / Azure Audit     |
| Cross-account role assumption  | Lateral movement to other AWS accounts                       | CloudTrail                   |
| S3 / Blob storage access       | Data access or exfiltration via cloud storage                | Cloud audit logs             |
| Compute instance modifications | New instances, snapshots, or AMIs created by attacker        | Cloud audit logs             |
| VPC / network changes          | New routes, peering, or security group changes               | Cloud audit logs             |
| CloudTrail/logging disabling   | Attacker attempt to disable logging                          | CloudTrail / monitoring      |
| Secrets Manager access         | Credential access during dwell period                        | CloudTrail / Secrets audit   |
| Lambda/Function modifications  | Backdoor injection into serverless functions                 | Cloud audit logs             |

### 16.1B Cloud IAM Compromise Assessment

For every IAM account, role, or key created or modified during the dwell period:

| IAM Entity | Type (User/Role/Key) | Created/Modified (UTC) | Activity During Dwell | Legitimate? | Actions Taken |
| ---------- | -------------------- | ---------------------- | --------------------- | ----------- | ------------- |
|            |                      |                        |                       |             |               |

---

## 17. Phase 10 – IOC and TTP Package Generation

### 17.1A IOC Package (Mandatory Deliverable)

| IOC Type           | Value | Context                   | Confidence | First Seen (UTC) | Recommended Action       |
| ------------------ | ----- | ------------------------- | ---------- | ---------------- | ------------------------ |
| IP Address         |       | C2 server                 |            |                  | Block at firewall/proxy  |
| Domain             |       | C2 domain                 |            |                  | DNS sinkhole + block     |
| File Hash (SHA256) |       | Malicious component       |            |                  | EDR block + FIM alert    |
| File Path          |       | Dropped malware path      |            |                  | Hunt + remove            |
| Process Name       |       | Attacker tool             |            |                  | EDR alert + block        |
| Registry Key       |       | Persistence key           |            |                  | Alert + remove           |
| Package Name/Version|      | Malicious package         |            |                  | Remove + block in repo   |
| User Agent         |       | C2 communication UA       |            |                  | Proxy/WAF detection rule |
| Certificate Hash   |       | Signing cert of malicious code |       |                  | Revoke trust             |

### 17.1B YARA Rules (Develop and Deploy)

For each malicious component identified, develop YARA rules for:

- Static detection based on unique strings, byte patterns, or code structures
- Deploy to EDR and file scanning tools for ongoing detection
- Share through threat intelligence platform for hunting

### 17.1C Sigma Rules (Develop and Deploy)

For each attacker behavior observed, develop Sigma rules for:

- SIEM detection of specific attack patterns
- Process creation patterns from supply chain component
- Network connection patterns to C2 infrastructure
- Lateral movement patterns observed in this campaign
- Persistence mechanism patterns

---

## 18. Phase 11 – Eradication Guidance and Clean State Definition

### 18.1A Eradication Decision Framework (Rebuild vs Clean)

| Scenario                                       | Recommended Approach                                         |
| ---------------------------------------------- | ------------------------------------------------------------ |
| Confirmed persistence with unknown scope        | Full system rebuild — do not attempt clean                   |
| Confirmed webshell or backdoor file only        | Remove file + validate + extended monitoring                 |
| Confirmed malicious scheduled task/service only | Remove + validate + extended monitoring                      |
| Confirmed registry persistence only            | Remove keys + validate + extended monitoring                 |
| Memory-only infection (no disk persistence)    | Reboot + validate + monitoring (infection cleared on reboot) |
| CI/CD pipeline compromised                     | Rebuild pipeline from scratch + re-validate all secrets      |
| Cloud IAM compromised                          | Revoke all affected credentials + audit all actions taken    |
| Confirmed deep multi-layer persistence         | Full system rebuild — highest confidence approach            |

### 18.2A Definition of Clean State (Supply Chain Specific)

Before any affected system is returned to production, L3 must confirm:

| Validation Check                                          | Method                                  | Expected Result          |
| --------------------------------------------------------- | --------------------------------------- | ------------------------ |
| Malicious component removed or replaced with clean version | File hash verification                 | Clean version hash match |
| All persistence mechanisms removed                        | Check all persistence locations         | None found               |
| No active C2 connections from system                      | Network monitoring post-remediation     | No IoC connections       |
| Secrets and credentials rotated                           | IAM audit + vault audit                 | New credentials in use   |
| System integrity verified                                 | Hash comparison of system binaries      | No unexpected changes    |
| EDR agent healthy and monitoring                          | EDR console verification                | Agent active and clean   |
| Logging fully operational                                 | SIEM log flow verification              | Logs flowing normally    |
| Vendor software updated to clean version                  | Version verification                    | Clean version confirmed  |
| CI/CD pipeline rebuilt and validated (if applicable)      | Pipeline run with integrity checks      | Clean build verified     |
| Cloud IAM cleaned and audited (if applicable)             | IAM review + no unauthorized activity   | Clean IAM state          |

---

## 19. Detection and Hunting Improvements (Required Output)

### 19.1A Detection Improvement Recommendations

Add to Detection Improvement Log after incident:

| Improvement                                                         | Owner          | Target Date | Priority | Status |
| ------------------------------------------------------------------- | -------------- | ----------- | -------- | ------ |
| Deploy YARA rules for malicious component to EDR                    | L3/Detection   | +3 days     | Critical | Open   |
| Deploy Sigma rules for observed attack patterns to SIEM             | L3/Detection   | +7 days     | Critical | Open   |
| Implement software inventory alerting for new vendor software versions | Detection   | +30 days    | High     | Open   |
| Deploy package integrity checking in CI/CD pipeline                 | DevSecOps      | +30 days    | High     | Open   |
| Implement SBOM generation for all production applications           | DevSecOps      | +45 days    | High     | Open   |
| Add behavioral detection for vendor software making unusual network connections | Detection | +14 days | High  | Open   |
| Implement cloud audit log alerting for IAM changes                  | Cloud/Detection| +14 days    | High     | Open   |
| Deploy DNS monitoring for supply chain C2 domains                   | Network/Detection | +7 days  | High     | Open   |
| Implement build artifact hash verification in deployment pipeline   | DevSecOps      | +30 days    | High     | Open   |

Reference: `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

## 20. Common L3 Pitfalls to Avoid

| Pitfall                                               | Impact                                     | Prevention                                        |
| ----------------------------------------------------- | ------------------------------------------ | ------------------------------------------------- |
| Starting analysis on live system without imaging first | Evidence alteration or loss               | Always acquire disk and memory image before analysis |
| Using only vendor-provided IoC list                   | Misses attacker TTPs not in advisory       | Perform full behavioral analysis beyond IoC list  |
| Not extending timeline to cover full dwell period     | Miss early attacker activity               | Use full log retention; extend to 12 months if needed |
| Focusing only on initial entry system                 | Miss full lateral movement scope           | Map all attacker activity across all systems      |
| Not analyzing CI/CD pipeline artifacts                | Backdoored code remains in production      | Always verify build artifacts if pipeline is in scope |
| Declaring clean without rebuild when persistence is unclear | Attacker retains access            | Use conservative approach; rebuild if unsure      |
| Not validating eradication with technical checks      | Incomplete remediation                     | Use defined clean state checklist                 |
| Poor timeline documentation                           | Weak evidence for legal/regulatory use     | UTC timestamps + evidence references for every event |
| Not generating YARA/Sigma rules after analysis        | No improved detection for future attacks   | Always generate detection rules as output         |
| Not coordinating with threat intel team               | Misses attribution and related campaigns   | Brief TI team with all technical findings         |

---

## 21. Regulatory and Legal Considerations

| Obligation                                    | When Triggered                              | L3 Responsibility                           |
| --------------------------------------------- | ------------------------------------------- | ------------------------------------------- |
| Evidence preservation for legal proceedings   | Any P1 with data breach or criminal activity | Maintain forensic-grade evidence with CoC   |
| Regulatory breach notification support        | Data breach confirmed                       | Provide technical evidence package to Legal |
| RBI reporting                                 | Financial sector incident with customer data| Support SOC Lead / Legal with technical facts |
| CERT-In reporting                             | Significant cyber incident                  | Provide IoCs and technical summary          |
| Vendor legal coordination                     | Vendor responsible for supply chain compromise | Preserve evidence of vendor-side failure  |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 22. MSSP Client Handling Notes

For MSSP-managed environments:

- Maintain **strict evidence segregation** per client — never mix evidence across client investigations
- Obtain **client approval for forensic collection** on production systems before proceeding
- All evidence transfers must use **encrypted methods** with chain-of-custody documentation
- Client-specific forensic findings must be reported to the **client's designated contact** — not shared with other clients
- If multiple clients are affected by the same supply chain attack, conduct **separate forensic investigations** per client with independent deliverables
- MSSP L3 findings may support client's own **regulatory reporting obligations** — coordinate with SDM and Legal

Reference: `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

## 23. Related Documents

| Document                         | Path                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| Supply Chain Master              | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Master.md` |
| Supply Chain L1 Triage           | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L1-Triage.md` |
| Supply Chain L2 Investigation    | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L2-Investigation.md` |
| Supply Chain Vendor Coordination | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Vendor-Coordination.md` |
| Supply Chain MITRE Mapping       | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-MITRE-Mapping.md` |
| Data Breach Master               | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md` |
| APT Campaign Playbooks           | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md`           |
| Memory Forensics SOP             | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Memory-Forensics-SOP.md` |
| Disk Forensics SOP               | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Disk-Forensics-SOP.md` |
| Malware Analysis SOP             | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Malware-Analysis-SOP.md` |
| Evidence Collection SOP          | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Chain of Custody Master Form     | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md` |
| TTP Intelligence Report          | `08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md` |
| IoC Output Register              | `08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md` |
| Detection Improvement Log        | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |
| Regulatory Communication         | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/` |
| Multi-Client Alert Handling      | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md` |

---

## 24. Revision History

| Version | Date        | Author                    | Changes         |
| ------- | ----------- | ------------------------- | --------------- |
| 1.0     | 19-May-2026 | L3 Lead / IR Team Lead    | Initial version |

---

## 25. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**