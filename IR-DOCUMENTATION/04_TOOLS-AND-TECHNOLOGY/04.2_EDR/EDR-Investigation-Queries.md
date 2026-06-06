# REFERENCE: EDR Investigation Queries

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | REFERENCE – EDR Investigation Queries |
| Document ID | TOOL-EDR-005 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Endpoint Security Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Monthly |

---

# 2. Purpose

This document provides a centralized library of **approved endpoint investigation queries and filters** for Endpoint Detection and Response (EDR/XDR) platforms.

These queries support:

- L2/L3 investigations and scoping
- Threat hunting on endpoints
- Evidence collection preparation
- Rapid validation of alerts (true vs false positive)
- Identification of lateral movement and persistence
- Ransomware precursor detection
- Credential access and privilege abuse investigation
- MSSP tenant-safe hunting and triage (where applicable)

This library ensures:

- Consistent investigations across analysts and shifts
- Faster time-to-scope for endpoint incidents
- Higher documentation quality (queries are reproducible)
- Safer standardized investigative workflows
- Reduced “random searching” and missed pivots

---

# 3. Scope

Applies to endpoint investigations for:

| Incident Type | Examples |
|---|---|
| Malware / Trojan | Loader activity, persistence |
| Ransomware | Encryption precursors, propagation |
| Credential attacks | LSASS access, token abuse indicators |
| Lateral movement | PsExec/WMI/WinRM, RDP fan-out |
| Insider threat | Unauthorized tools, abnormal access |
| Web/app compromise pivoting to endpoint | Webserver spawning shells |
| EDR tampering | Sensor disable/kill attempts |
| Data staging | Archiving tools, rclone usage |
| Cloud-connected endpoints | Hybrid identity compromise evidence |
| MSSP incidents | Client-specific scoping |

---

# 4. Query Usage Standards (IMPORTANT)

---

## 4.1 Mandatory Rules

| Rule | Requirement |
|---|---|
| Always set a time window | Mandatory (do not run open-ended queries) |
| Use UTC timestamps | Mandatory |
| Validate endpoint scope/tenant first (MSSP) | Mandatory |
| Prefer high-signal pivots | Start from alert host/user/process/hash and expand |
| Document queries used in the ticket | Mandatory for P1/P2/P3 |
| Preserve evidence when required | Export results for P1/P2 and legal/regulatory cases |
| Queries must be read-only | No execution/remediation commands in this document |

---

## 4.2 MSSP Tenant Safety Controls

For MSSP operations:

- Confirm correct **client tenant/site/group**
- Confirm correct **device scope** and **policy group**
- Do not hunt across tenants using global wildcards
- Document the tenant identifier in the ticket

**MSSP Pre-Query Checklist**

| Validation Item | Completed |
|---|---|
| Correct client tenant selected | ☐ |
| Correct device group/site selected | ☐ |
| Time range defined | ☐ |
| Query reviewed for cross-tenant exposure | ☐ |
| Ticket reference present | ☐ |

---

## 4.3 Evidence Export Guidance (When Required)

If results are used as evidence:

- Export in platform-supported original format (CSV/JSON where possible)
- Record:
  - Query text and filters
  - Time window
  - Execution timestamp (UTC)
  - Analyst name
  - Case/ticket ID
- Hash exported files (SHA-256 recommended)
- Store per evidence policy

Reference:
- `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md`
- `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 5. Query Catalog & Naming Convention

---

## 5.1 Query ID Format

**Format:** `EDR-Q-<CATEGORY>-<NNN>`

Categories:
- `PROC` = Process execution
- `FILE` = File events
- `NET` = Network events
- `PERS` = Persistence
- `CRED` = Creden-tial access
- `LMOV` = Lateral movement
- `RAN` = Ransomware indicators
- `EVA` = Defense evasion / tampering
- `WEB` = Web/server compromise pivots
- `OPS` = EDR operational checks

Example: `EDR-Q-PROC-003`

---

## 5.2 Common Pivot Fields (EDR)

Use these pivots in most EDRs:

| Pivot | Examples |
|---|---|
| Device | hostname, device_id, agent_id |
| User | account name / UPN |
| Process | process name, PID, parent process |
| Command line | arguments, encoded content |
| File | path, hash (SHA-256), signer |
| Network | remote IP/domain, port, protocol |
| Time | first_seen, last_seen (UTC) |

---

## 5.3 Platform Notes (EDR Query Languages)

EDR platforms differ. This library provides:

- **Microsoft Defender for Endpoint (MDE) Advanced Hunting (KQL)** queries (commonly adopted)
- **Vendor-agnostic filters** (what to search for in any EDR)
- Guidance to translate logic into your EDR’s hunting language (XQL/FQL/Deep Visibility/etc.)

If your platform uses different field names, map them consistently (DeviceName/Hostname, AccountName/User, etc.).

---

# 6. Process Execution Queries (EDR-Q-PROC)

---

## EDR-Q-PROC-001 — Recent Process Activity on a Host (Baseline View)

| Field | Value |
|---|---|
| Objective | List recent process activity for a specific host in a defined time window |
| Primary Use | Investigation pivot |
| Notes | Use for quick context; refine with user/process filters |

### MDE (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated between (ago(24h) .. now())
| where DeviceName == "<HOST>"
| project TimeGenerated, DeviceName, AccountName,
          InitiatingProcessAccountName, InitiatingProcessFileName, InitiatingProcessCommandLine,
          FileName, FolderPath, ProcessCommandLine, ProcessId, InitiatingProcessId
| order by TimeGenerated desc
```

### Vendor-agnostic EDR Filters
- Device = `<HOST>`
- Time range = last 24h
- View = “Process Timeline” / “Process Tree”
- Export = include command line + parent/child relationships

---

## EDR-Q-PROC-002 — Office Spawning Script Engines (Macro/Phishing Indicator)

| Field | Value |
|---|---|
| Objective | Detect Office apps spawning PowerShell/cmd/wscript/mshta (common initial access chain) |
| Primary Use | Phishing/BEC + initial access investigation |
| Notes | High-signal; validate parent-child lineage and user context |

### MDE (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(7d)
| where InitiatingProcessFileName in~ ("winword.exe","excel.exe","powerpnt.exe","outlook.exe")
| where FileName in~ ("powershell.exe","cmd.exe","wscript.exe","cscript.exe","mshta.exe","rundll32.exe","regsvr32.exe")
| project TimeGenerated, DeviceName, AccountName,
          InitiatingProcessFileName, InitiatingProcessCommandLine,
          FileName, ProcessCommandLine
| order by TimeGenerated desc
```

---

## EDR-Q-PROC-003 — Encoded / Obfuscated PowerShell

| Field | Value |
|---|---|
| Objective | Identify encoded PowerShell or common obfuscation patterns |
| Primary Use | Malware / fileless investigation |
| Notes | Correlate with network events and file drops |

### MDE (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(7d)
| where FileName =~ "powershell.exe"
| where ProcessCommandLine has_any ("-enc","EncodedCommand","IEX","Invoke-Expression","FromBase64String")
| project TimeGenerated, DeviceName, AccountName, InitiatingProcessFileName, ProcessCommandLine
| order by TimeGenerated desc
```

### Vendor-agnostic EDR Filters
- Process = `powershell.exe`
- Command line contains: `-enc`, `EncodedCommand`, `IEX`, `FromBase64String`
- Parent process = Office/browser/archive tool is higher risk

---

## EDR-Q-PROC-004 — Common LOLBins (Living-off-the-land)

| Field | Value |
|---|---|
| Objective | Detect execution of common LOLBins used in attacks |
| Primary Use | Threat hunting |
| Notes | Validate against IT automation; focus on command line and origin |

### MDE (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(7d)
| where FileName in~ ("rundll32.exe","regsvr32.exe","mshta.exe","certutil.exe","bitsadmin.exe","wmic.exe","schtasks.exe","net.exe","nltest.exe")
| project TimeGenerated, DeviceName, AccountName, InitiatingProcessFileName, FileName, ProcessCommandLine
| order by TimeGenerated desc
```

---

## EDR-Q-PROC-005 — Native Download/Dropper Techniques

| Field | Value |
|---|---|
| Objective | Identify common download behaviors (certutil/BITS/PowerShell web) |
| Primary Use | Malware staging investigation |
| Notes | Pivot to file creation and subsequent execution |

### MDE (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(7d)
| where ProcessCommandLine has_any ("certutil -urlcache","bitsadmin /transfer","Invoke-WebRequest","Start-BitsTransfer","curl ","wget ")
| project TimeGenerated, DeviceName, AccountName, FileName, ProcessCommandLine, InitiatingProcessFileName
| order by TimeGenerated desc
```

---

# 7. Credential Access Queries (EDR-Q-CRED)

---

## EDR-Q-CRED-001 — LSASS Access / Dumping Tools (Heuristic)

| Field | Value |
|---|---|
| Objective | Identify potential credential dumping attempts |
| Primary Use | P1/P2 investigation |
| Notes | Escalate if server/DC; validate against sanctioned tools |

### MDE (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(7d)
| where ProcessCommandLine has_any ("lsass","sekurlsa","comsvcs.dll","procdump","rundll32.exe C:\\Windows\\System32\\comsvcs.dll")
| project TimeGenerated, DeviceName, AccountName, FileName, ProcessCommandLine, InitiatingProcessFileName
| order by TimeGenerated desc
```

---

## EDR-Q-CRED-002 — Access to SAM/SECURITY/NTDS (If File Telemetry Available)

| Field | Value |
|---|---|
| Objective | Identify access to credential stores (high risk) |
| Primary Use | Investigation |
| Notes | Highly sensitive on DCs; depends on file telemetry availability |

### MDE (KQL)
```kql
DeviceFileEvents
| where TimeGenerated > ago(7d)
| where FolderPath has_any ("\\Windows\\System32\\config\\SAM",
                           "\\Windows\\System32\\config\\SECURITY",
                           "\\Windows\\NTDS\\ntds.dit")
| project TimeGenerated, DeviceName, AccountName, ActionType, FolderPath, FileName,
          InitiatingProcessFileName, InitiatingProcessCommandLine
| order by TimeGenerated desc
```

---

# 8. Persistence Queries (EDR-Q-PERS)

---

## EDR-Q-PERS-001 — New Service Installation (Persistence)

| Field | Value |
|---|---|
| Objective | Detect new service creation (persistence or lateral movement) |
| Primary Use | Investigation |
| Notes | Validate signer/path; check actor account and parent process |

### MDE (KQL) (platform schema-dependent; may require DeviceEvents)
```kql
DeviceEvents
| where TimeGenerated > ago(14d)
| where ActionType has_any ("ServiceInstalled","ServiceCreated","WindowsServiceInstalled")
| project TimeGenerated, DeviceName, AccountName, ActionType, AdditionalFields
| order by TimeGenerated desc
```

> If `DeviceEvents` does not include service install events in your environment, use Windows logs via SIEM (Event ID 7045) and pivot back into EDR timeline for affected hosts.

---

## EDR-Q-PERS-002 — Scheduled Task Creation / Modification (Process Proxy)

| Field | Value |
|---|---|
| Objective | Identify scheduled task creation/modification via schtasks execution |
| Primary Use | Investigation |
| Notes | Validate task name, author, path, trigger; look for odd paths |

### MDE (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(14d)
| where FileName in~ ("schtasks.exe")
| project TimeGenerated, DeviceName, AccountName, ProcessCommandLine, InitiatingProcessFileName
| order by TimeGenerated desc
```

---

## EDR-Q-PERS-003 — Startup Folder Writes (Common Persistence)

| Field | Value |
|---|---|
| Objective | Identify files written into Startup folders |
| Primary Use | Investigation / Hunting |
| Notes | Validate signer and origin; suspicious if paired with script engines |

### MDE (KQL)
```kql
DeviceFileEvents
| where TimeGenerated > ago(14d)
| where FolderPath has_any ("\\Microsoft\\Windows\\Start Menu\\Programs\\Startup",
                           "\\ProgramData\\Microsoft\\Windows\\Start Menu\\Programs\\Startup")
| project TimeGenerated, DeviceName, AccountName, ActionType, FolderPath, FileName,
          InitiatingProcessFileName, InitiatingProcessCommandLine
| order by TimeGenerated desc
```

---

# 9. Network Activity Queries (EDR-Q-NET)

---

## EDR-Q-NET-001 — New/Rare External Connections by Host

| Field | Value |
|---|---|
| Objective | Identify unusual external connections from a host |
| Primary Use | C2 investigation |
| Notes | Tune by environment; validate against known SaaS/CDNs |

### MDE (KQL)
```kql
DeviceNetworkEvents
| where TimeGenerated > ago(7d)
| where DeviceName == "<HOST>"
| where RemoteIPType == "Public"
| summarize connections=count(), firstSeen=min(TimeGenerated), lastSeen=max(TimeGenerated)
          by RemoteIP, RemotePort, InitiatingProcessFileName
| order by connections desc
```

---

## EDR-Q-NET-002 — Suspicious Ports (Heuristic)

| Field | Value |
|---|---|
| Objective | Identify connections using high-risk ports (heuristic) |
| Primary Use | Hunting |
| Notes | Not definitive; use with process context and destination reputation |

### MDE (KQL)
```kql
DeviceNetworkEvents
| where TimeGenerated > ago(7d)
| where RemoteIPType == "Public"
| where RemotePort in (4444, 1337, 2222, 3389, 445, 5985, 5986)
| project TimeGenerated, DeviceName, AccountName, RemoteIP, RemotePort, Protocol,
          InitiatingProcessFileName, InitiatingProcessCommandLine
| order by TimeGenerated desc
```

---

# 10. Lateral Movement Queries (EDR-Q-LMOV)

---

## EDR-Q-LMOV-001 — Remote Execution Indicators (PsExec/WMI/WinRM/PowerShell Remoting)

| Field | Value |
|---|---|
| Objective | Detect tools and command lines often used for lateral movement and remote execution |
| Primary Use | Investigation / Hunting |
| Notes | Correlate with authentication logs and network flows |

### MDE (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(14d)
| where FileName in~ ("psexec.exe","wmic.exe","winrs.exe","powershell.exe","cmd.exe")
| where ProcessCommandLine has_any ("\\\\","/node:","process call create","winrm","Invoke-Command","Enter-PSSession")
| project TimeGenerated, DeviceName, AccountName, FileName, ProcessCommandLine, InitiatingProcessFileName
| order by TimeGenerated desc
```

---

## EDR-Q-LMOV-002 — Admin Share / Remote Service Creation (EDR Pivot Guidance)

| Field | Value |
|---|---|
| Objective | Identify remote service creation and admin share usage signals via endpoint behavior |
| Primary Use | Investigation |
| Notes | Often detected better via Windows logs; use EDR to validate target endpoints |

### Vendor-agnostic EDR Filters (Pivot Guidance)
- Look for:
  - `services.exe` spawning unusual child processes
  - Remote tool processes running as `SYSTEM`
  - New service installed with odd binary path (Temp/AppData/Public)
  - New executable dropped shortly before service creation
- Correlate:
  - Authentication spikes (4624/4625)
  - SMB fan-out in NetFlow/firewall logs

---

# 11. Ransomware Indicators (EDR-Q-RAN)

---

## EDR-Q-RAN-001 — Shadow Copy Deletion / Recovery Inhibition Commands

| Field | Value |
|---|---|
| Objective | Detect common ransomware precursor commands |
| Primary Use | P1 response |
| Notes | High-confidence indicator; escalate immediately if confirmed |

### MDE (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(7d)
| where ProcessCommandLine has_any ("vssadmin delete shadows","wmic shadowcopy delete","bcdedit /set","wbadmin delete catalog","wevtutil cl")
| project TimeGenerated, DeviceName, AccountName, FileName, ProcessCommandLine, InitiatingProcessFileName
| order by TimeGenerated desc
```

---

## EDR-Q-RAN-002 — High Volume File Modification (Encryption Heuristic)

| Field | Value |
|---|---|
| Objective | Identify potential encryption behavior via file event spikes |
| Primary Use | Investigation |
| Notes | Requires file telemetry; tune thresholds per endpoint type and workload |

### MDE (KQL)
```kql
DeviceFileEvents
| where TimeGenerated > ago(6h)
| summarize fileEvents=count() by DeviceName, AccountName, bin(TimeGenerated, 10m)
| where fileEvents > 2000
| order by fileEvents desc
```

---

## EDR-Q-RAN-003 — Execution from High-Risk User-Writeable Paths

| Field | Value |
|---|---|
| Objective | Detect execution from common malware staging locations |
| Primary Use | Investigation |
| Notes | Validate signer and origin; not all executions are malicious |

### MDE (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(14d)
| where FolderPath has_any ("\\AppData\\Local\\Temp\\","\\AppData\\Roaming\\","\\Users\\Public\\","\\ProgramData\\")
| project TimeGenerated, DeviceName, AccountName, FolderPath, FileName, ProcessCommandLine, InitiatingProcessFileName
| order by TimeGenerated desc
```

---

# 12. Defense Evasion / Tampering (EDR-Q-EVA)

---

## EDR-Q-EVA-001 — Attempts to Disable Security Tools (Heuristic)

| Field | Value |
|---|---|
| Objective | Detect commands frequently used to weaken security controls |
| Primary Use | Investigation |
| Notes | Validate against authorized IT activity; treat as high risk when paired with malware indicators |

### MDE (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(14d)
| where ProcessCommandLine has_any ("DisableRealtimeMonitoring","Set-MpPreference","sc stop","taskkill /f","net stop","wevtutil cl")
| project TimeGenerated, DeviceName, AccountName, FileName, ProcessCommandLine, InitiatingProcessFileName
| order by TimeGenerated desc
```

---

## EDR-Q-EVA-002 — Sensor Tamper / Agent Disable Indicators (Platform-Specific)

| Field | Value |
|---|---|
| Objective | Identify sensor tampering, disablement, policy downgrade, or uninstall indicators |
| Primary Use | P1/P2 response |
| Notes | Use EDR platform event categories (tamper protection, sensor disabled/uninstalled, policy changed) |

### Vendor-agnostic EDR Filters
- Event categories: agent uninstall, sensor stop, tamper alert, policy downgrade
- Scope: all endpoints in last 7 days
- Escalate immediately if:
  - tamper events coincide with suspicious process activity
  - tamper occurs on servers or admin endpoints

---

# 13. Web / Server Compromise Pivots (EDR-Q-WEB)

---

## EDR-Q-WEB-001 — Web Server Worker Spawning Shells (Webshell Indicator)

| Field | Value |
|---|---|
| Objective | Detect IIS/Apache/Nginx processes spawning cmd/powershell and admin discovery |
| Primary Use | Web compromise investigation |
| Notes | High signal on web servers; confirm with web logs/WAF |

### MDE (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(14d)
| where InitiatingProcessFileName in~ ("w3wp.exe","httpd.exe","nginx.exe","php-cgi.exe")
| where FileName in~ ("cmd.exe","powershell.exe","wscript.exe","cscript.exe","net.exe","whoami.exe")
| project TimeGenerated, DeviceName, AccountName, InitiatingProcessFileName, FileName, ProcessCommandLine
| order by TimeGenerated desc
```

---

# 14. Operational EDR Checks (EDR-Q-OPS)

---

## EDR-Q-OPS-001 — Devices Not Seen Recently (Coverage / Health)

| Field | Value |
|---|---|
| Objective | Identify endpoints that have not checked in recently |
| Primary Use | Ops / coverage tracking |
| Notes | Prioritize Tier 0/1 assets (DCs, servers, admin endpoints) |

### Vendor-agnostic EDR Filters
- Filter devices by “Last Seen” > 24 hours
- Group by criticality (servers/DCs/admin endpoints first)
- Open remediation tickets for offline sensors

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Deployment-Coverage-Check.md`

---

# 15. Investigation Play Patterns (How to Use Queries)

---

## 15.1 Standard Pivot Flow (Recommended)

| Step | Pivot | Goal |
|---|---|---|
| 1 | Alert host + timestamp | Establish starting point |
| 2 | Process tree around event | Identify execution chain |
| 3 | Command line inspection | Identify intent and tooling |
| 4 | File hash/path | Determine payload and prevalence |
| 5 | Network events for that process | Identify C2/exfil |
| 6 | Persistence checks | Determine reinfection risk |
| 7 | Scope expansion to other endpoints | Determine blast radius |
| 8 | Escalate if thresholds met | IR/L3 engagement |

---

## 15.2 Scope Expansion Guidance

When you find one confirmed malicious indicator, expand by:

| Indicator | Expand To |
|---|---|
| SHA-256 hash | Search across endpoints for same hash |
| Domain/IP | Search for other endpoints communicating with it |
| Command line pattern | Search for similar patterns fleet-wide |
| Persistence artifact | Search for same service/task name elsewhere |
| User account | Search endpoints where account executed suspicious commands |

---

# 16. Escalation Guidance (From Query Findings)

Escalate immediately to IR Team if queries confirm:

| Finding | Typical Severity | Escalation Target |
|---|---|---|
| Ransomware precursors + file modification spike | P1 | IR Team |
| Credential dumping on server/DC | P1 | IR Team |
| Multiple endpoints with same payload | P1/P2 | IR Team |
| EDR tampering + suspicious execution | P1 | IR Team |
| Data staging tools (archive + rclone) with outbound spikes | P1 | IR Team + Legal/Compliance |

Reference:
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Escalation-Criteria.md`

---

# 17. Change Control & Review

All changes to this query library must be logged.

## 17.1 Change Log

| Date | Version | Change Summary | Author | Approved By |
|---|---|---|---|---|
| 22-May-2026 | 1.0 | Initial version | Endpoint Security Lead | IR Team Lead |

---

# 18. Related Documents

| Document | Path |
|---|---|
| EDR Alert Handling Guide | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Alert-Handling-Guide.md` |
| EDR Containment Commands | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Containment-Commands.md` |
| EDR Deployment Coverage Check | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Deployment-Coverage-Check.md` |
| L2 EDR Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-EDR-Deep-Investigation.md` |
| SIEM Query Library | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md` |
| Evidence Handling SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md` |

---

# 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**