# Attack Technique Reference

---

# 1. Document Control

| Field          | Value                                               |
| -------------- | --------------------------------------------------- |
| Document Name  | Attack Technique Reference                          |
| Document ID    | MSSP-TRN-KB-001                                     |
| Version        | 1.0                                                 |
| Effective Date | 30-May-2026                                         |
| Owner          | MSSP Threat Intel Lead / Detection Engineering Lead |
| Approved By    | MSSP CISO                                           |
| Classification | Confidential – MSSP Internal                        |
| Review Cycle   | Quarterly (or upon major TTP update)                |

---

# 2. Purpose

This document defines the standardized **Attack Technique Reference** providing SOC analysts (L1/L2/L3), IR Team members, Threat Intelligence analysts, and Detection Engineers with a consolidated, operationally-focused reference for understanding, detecting, investigating, and responding to the most prevalent adversary techniques observed across the MSSP multi-tenant client portfolio — bridging detailed MITRE ATT&CK framework knowledge with practical SOC application.

A formal Attack Technique Reference is critical because:

- SOC analysts need rapid access to technique details during alert triage
- inconsistent technique understanding across tiers leads to mis-classification and missed attacks
- new analysts require structured reference to learn TTPs efficiently
- L1 analysts often lack time to research techniques during high-volume triage
- L2/L3 analysts need investigation patterns aligned to specific techniques
- IR Team members need response playbook linkage per technique
- Detection Engineers need consistent technique-to-detection mapping
- Threat Intel analysts need standard terminology for cross-tenant correlation
- ISO 27001 A.5.7 (threat intelligence) and NIST CSF DE.AE (event analysis) require structured threat knowledge
- RBI Cyber Security Framework expects demonstrable threat awareness
- without consolidated reference, analysts rely on inconsistent external sources
- multi-tenant MSSPs need consistent technique application across all clients
- detection engineering depends on technique-driven rule development
- this reference is the operational backbone for technique-driven SOC operations

This reference ensures:

- consolidated technique catalog for SOC operational use
- consistent technique terminology aligned to MITRE ATT&CK
- per-technique detection guidance for analysts
- per-technique investigation patterns
- per-technique response actions
- linkage to MSSP playbooks and SOPs
- multi-tenant applicability per technique
- audit-ready threat knowledge documentation
- quarterly update cycle aligned to threat landscape

**Reference alignment:**

- `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`
- `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Common-IoC-Reference.md`
- `02_PLAYBOOKS/` (all playbooks)
- `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md`

---

# 3. Scope

This reference covers:

| Scope Element                          | Coverage             |
| -------------------------------------- | -------------------- |
| Top adversary techniques by prevalence | Yes                  |
| MITRE ATT&CK Enterprise techniques     | Most relevant subset |
| Detection guidance per technique       | Yes                  |
| Investigation guidance per technique   | Yes                  |
| Response guidance per technique        | Yes                  |
| Multi-tenant considerations            | Yes                  |
| Playbook linkage                       | Yes                  |
| Tool-specific detection queries        | Reference only       |
| Cloud-specific techniques              | Yes                  |
| Identity-specific techniques           | Yes                  |
| Endpoint-specific techniques           | Yes                  |
| Network-specific techniques            | Yes                  |

Out of scope:

- Full MITRE ATT&CK framework documentation (use external reference)
- Specific actor profiles (covered by `08_POST-INCIDENT/08.4_Threat-Intel-Output/`)
- Specific IoCs (covered by `Common-IoC-Reference.md`)
- Detailed forensic procedures (covered by `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/`)
- Detection rule code (covered by Detection Engineering repository)

---

# 4. Definitions

| Term                  | Definition                                       |
| --------------------- | ------------------------------------------------ |
| TTP                   | Tactic, Technique, Procedure                     |
| Tactic                | Adversary's tactical goal (e.g., Initial Access) |
| Technique             | How adversary achieves tactical goal             |
| Sub-technique         | More specific technique variant                  |
| MITRE ATT&CK          | Standard framework for adversary behavior        |
| Detection Guidance    | What to look for in tools                        |
| Investigation Pattern | How to investigate once detected                 |
| Response Action       | Immediate actions to contain/mitigate            |
| Data Source           | Where evidence lives (logs, telemetry)           |
| Procedure             | Specific implementation of a technique           |

---

# 5. Roles and Responsibilities

| Role                                | Responsibilities                      |
| ----------------------------------- | ------------------------------------- |
| **MSSP Threat Intel Lead**          | Document ownership; quarterly updates |
| **MSSP Detection Engineering Lead** | Detection mapping per technique       |
| **MSSP IR Team Lead**               | Response action mapping per technique |
| **MSSP SOC Manager**                | Operational use validation            |
| **MSSP L1/L2/L3 Analysts**          | Reference users; feedback providers   |
| **MSSP Compliance Lead**            | Audit evidence                        |
| **All SOC Personnel**               | Apply reference in operations         |

---

# 6. Reference Structure (Mandatory)

Each technique entry contains:

| Element                   | Content                       |
| ------------------------- | ----------------------------- |
| Technique ID              | MITRE ATT&CK identifier       |
| Technique name            | Standard name                 |
| Tactic(s)                 | Goal(s) addressed             |
| Description               | Brief operational description |
| Prevalence (MSSP context) | High / Medium / Low           |
| Data sources              | Where to detect               |
| Detection guidance        | What to look for              |
| Investigation pattern     | How to investigate            |
| Response actions          | Immediate containment         |
| Linked playbooks          | Path references               |
| Multi-tenant note         | Cross-client considerations   |

---

# 7. MITRE ATT&CK Tactics (Operational Order)

| #   | Tactic               | Code   | Goal                                 |
| --- | -------------------- | ------ | ------------------------------------ |
| 1   | Reconnaissance       | TA0043 | Gather information about target      |
| 2   | Resource Development | TA0042 | Establish infrastructure             |
| 3   | Initial Access       | TA0001 | Gain entry into environment          |
| 4   | Execution            | TA0002 | Run malicious code                   |
| 5   | Persistence          | TA0003 | Maintain access                      |
| 6   | Privilege Escalation | TA0004 | Gain higher permissions              |
| 7   | Defense Evasion      | TA0005 | Avoid detection                      |
| 8   | Credential Access    | TA0006 | Steal credentials                    |
| 9   | Discovery            | TA0007 | Learn the environment                |
| 10  | Lateral Movement     | TA0008 | Move through environment             |
| 11  | Collection           | TA0009 | Gather target data                   |
| 12  | Command and Control  | TA0011 | Communicate with compromised systems |
| 13  | Exfiltration         | TA0010 | Steal data                           |
| 14  | Impact               | TA0040 | Damage / extort                      |

---

# 8. Top Techniques by MSSP Prevalence (Detailed Reference)

## 8.1 Initial Access Tactics

### T1566 – Phishing (T1566.001/.002/.003)

| Element               | Detail                                                                                                                                                                                                           |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tactic                | Initial Access                                                                                                                                                                                                   |
| Prevalence            | **Very High**                                                                                                                                                                                                    |
| Sub-techniques        | .001 Spearphishing Attachment, .002 Spearphishing Link, .003 Spearphishing via Service                                                                                                                           |
| Description           | Sending emails with malicious attachments, links, or via service messaging                                                                                                                                       |
| Data sources          | Email security gateway logs, mail server logs, EDR (file execution), proxy logs, URL filtering                                                                                                                   |
| Detection guidance    | Suspicious sender domains, attachment types (.exe, .scr, .js, macro-enabled docs), links to lookalike domains, language patterns, urgency cues, executions of attachments from email folders                     |
| Investigation pattern | 1) Identify all recipients of similar email; 2) Check link/attachment hash reputation; 3) Track click/execution events; 4) Identify any subsequent process executions; 5) Check for credential prompts triggered |
| Response actions      | Quarantine email org-wide; block sender domain; block URL; isolate hosts with execution; force password reset for credential-prompted users                                                                      |
| Linked playbooks      | `02_PLAYBOOKS/02.2_Phishing-BEC/`                                                                                                                                                                                |
| Multi-tenant note     | Per-client phishing campaigns common; sanitized IoCs shareable across MSSP portfolio                                                                                                                             |

### T1190 – Exploit Public-Facing Application

| Element               | Detail                                                                                                                                                                                        |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tactic                | Initial Access                                                                                                                                                                                |
| Prevalence            | **High**                                                                                                                                                                                      |
| Description           | Exploitation of vulnerabilities in internet-exposed applications (web apps, VPN, RDP, etc.)                                                                                                   |
| Data sources          | WAF logs, web server logs, IDS/IPS, VPN logs, vulnerability scanner output                                                                                                                    |
| Detection guidance    | Exploitation patterns (SQLi, RCE, SSRF), unusual POST requests with payloads, server-side errors after suspicious input, post-exploit shells/processes                                        |
| Investigation pattern | 1) Identify exploited CVE/component; 2) Check application logs around exploit time; 3) Identify any shells/backdoors planted; 4) Check for lateral movement attempts; 5) Confirm patch status |
| Response actions      | Patch vulnerability; deploy WAF rule; isolate compromised application server; rotate any exposed credentials                                                                                  |
| Linked playbooks      | `02_PLAYBOOKS/02.8_Web-Application-Attack/`, `02_PLAYBOOKS/02.12_Zero-Day-Exploit/`                                                                                                           |
| Multi-tenant note     | Mass-exploitation campaigns affect multiple clients; CCIC trigger likely                                                                                                                      |

### T1078 – Valid Accounts (T1078.001/.002/.003/.004)

| Element               | Detail                                                                                                                                                                          |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tactic                | Initial Access / Persistence / Defense Evasion                                                                                                                                  |
| Prevalence            | **Very High**                                                                                                                                                                   |
| Sub-techniques        | .001 Default Accounts, .002 Domain Accounts, .003 Local Accounts, .004 Cloud Accounts                                                                                           |
| Description           | Use of legitimate credentials obtained via phishing, leaks, brokers, or insider                                                                                                 |
| Data sources          | IdP logs (Azure AD, Okta), SIEM auth events, VPN logs, EDR login events, UEBA                                                                                                   |
| Detection guidance    | Impossible travel, unusual login times, login from suspicious ASN/country, sudden privilege use, new device sign-in for sensitive accounts, MFA fatigue patterns                |
| Investigation pattern | 1) Verify legitimacy with user; 2) Check authentication source/IP/device; 3) Look at session activities; 4) Identify if MFA was used or bypassed; 5) Check for lateral movement |
| Response actions      | Disable account; force password reset; revoke active sessions; investigate session activities; review recent permission changes                                                 |
| Linked playbooks      | `02_PLAYBOOKS/02.7_Credential-Attack/`, `02_PLAYBOOKS/02.10_Cloud-Security-Incident/`                                                                                           |
| Multi-tenant note     | Credential reuse across SaaS apps common; per-tenant investigation strict                                                                                                       |

### T1195.002 – Supply Chain Compromise (Software Supply Chain)

| Element               | Detail                                                                                                                                        |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Tactic                | Initial Access                                                                                                                                |
| Prevalence            | **Medium-Rising**                                                                                                                             |
| Description           | Trojanized software updates from compromised vendors                                                                                          |
| Data sources          | EDR (post-install behaviors), SIEM (network beacons), vendor advisories, threat intel feeds                                                   |
| Detection guidance    | Unusual post-install network beacons, hash matches to known compromised updates, anomalous behavior post-software-update                      |
| Investigation pattern | 1) Identify affected software/version; 2) Check vendor advisory; 3) Inventory all installations; 4) Check for IoCs; 5) Coordinate with vendor |
| Response actions      | Isolate affected systems; coordinate vendor response; deploy hunt for IoCs across portfolio; consider portfolio-wide rollback                 |
| Linked playbooks      | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/`                                                                                                      |
| Multi-tenant note     | **Highest CCIC priority** — affects multiple clients simultaneously                                                                           |

---

## 8.2 Execution Tactics

### T1059 – Command and Scripting Interpreter (T1059.001/.003/.004/.005/.006/.007)

| Element               | Detail                                                                                                                                                                   |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Tactic                | Execution                                                                                                                                                                |
| Prevalence            | **Very High**                                                                                                                                                            |
| Sub-techniques        | .001 PowerShell, .003 Windows CMD, .004 Unix Shell, .005 Visual Basic, .006 Python, .007 JavaScript                                                                      |
| Description           | Use of command interpreters to execute commands, scripts                                                                                                                 |
| Data sources          | EDR (process creation), Windows event logs (4688, PowerShell logs 4103/4104), shell history (Unix), SIEM                                                                 |
| Detection guidance    | Encoded PowerShell, downloading/executing via IEX, suspicious cmd parameters, base64-decoded payloads, parent-child relationships (Word → cmd → PowerShell)              |
| Investigation pattern | 1) Decode any encoded commands; 2) Identify parent process chain; 3) Check for downloaded files; 4) Identify network connections initiated; 5) Track persistence created |
| Response actions      | Kill malicious process; isolate host; collect memory for forensics; rotate exposed credentials                                                                           |
| Linked playbooks      | `02_PLAYBOOKS/02.3_Malware-Trojan/`, all major playbooks                                                                                                                 |
| Multi-tenant note     | Per-tenant; common across all tenants                                                                                                                                    |

### T1204 – User Execution

| Element               | Detail                                                                                                                             |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| Tactic                | Execution                                                                                                                          |
| Prevalence            | **High**                                                                                                                           |
| Description           | User-initiated execution (clicking, opening, running)                                                                              |
| Data sources          | EDR, email logs, browser history, user interaction logs                                                                            |
| Detection guidance    | Suspicious file types opened from email/downloads, macro execution from documents, shortcut files executing scripts                |
| Investigation pattern | 1) Identify source of file; 2) Identify file hash/reputation; 3) Track subsequent process activity; 4) Check for persistence or C2 |
| Response actions      | Isolate host; quarantine file; user training note                                                                                  |
| Linked playbooks      | `02_PLAYBOOKS/02.2_Phishing-BEC/`, `02_PLAYBOOKS/02.3_Malware-Trojan/`                                                             |
| Multi-tenant note     | Per-tenant; user-driven                                                                                                            |

---

## 8.3 Persistence Tactics

### T1547 – Boot or Logon Autostart Execution

| Element               | Detail                                                                                                                                                           |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tactic                | Persistence / Privilege Escalation                                                                                                                               |
| Prevalence            | **High**                                                                                                                                                         |
| Description           | Persistence via registry run keys, startup folders, services, scheduled tasks at boot/logon                                                                      |
| Data sources          | EDR, Windows registry monitoring, Sysmon (event ID 12/13), event logs                                                                                            |
| Detection guidance    | New entries in Run/RunOnce registry keys, new files in startup folders, new services with suspicious names/paths                                                 |
| Investigation pattern | 1) Identify persistence artifact; 2) Identify executable referenced; 3) Identify creator process; 4) Check execution history; 5) Remove persistence + executable |
| Response actions      | Remove persistence; quarantine executable; check for additional persistence mechanisms                                                                           |
| Linked playbooks      | All major playbooks                                                                                                                                              |
| Multi-tenant note     | Per-tenant; common technique                                                                                                                                     |

### T1053.005 – Scheduled Task/Job: Scheduled Task

| Element               | Detail                                                                                                                        |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Tactic                | Persistence / Privilege Escalation / Execution                                                                                |
| Prevalence            | **High**                                                                                                                      |
| Description           | Scheduled tasks for persistence and recurring execution                                                                       |
| Data sources          | Windows event logs (4698, 4702), EDR, scheduled task auditing                                                                 |
| Detection guidance    | New scheduled tasks with suspicious commands, tasks created by unusual users, tasks invoking PowerShell with encoded commands |
| Investigation pattern | 1) Identify task XML/details; 2) Identify task creator; 3) Identify execution history; 4) Identify referenced executable      |
| Response actions      | Disable/delete task; quarantine executable; check for similar tasks elsewhere                                                 |
| Linked playbooks      | Multiple                                                                                                                      |
| Multi-tenant note     | Per-tenant                                                                                                                    |

---

## 8.4 Privilege Escalation Tactics

### T1068 – Exploitation for Privilege Escalation

| Element               | Detail                                                                                                                  |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Tactic                | Privilege Escalation                                                                                                    |
| Prevalence            | **Medium**                                                                                                              |
| Description           | Exploitation of OS or application vulnerabilities to gain elevated privileges                                           |
| Data sources          | EDR, Windows event logs, OS logs                                                                                        |
| Detection guidance    | Known exploit signatures, kernel-mode exploitation patterns, sudden privilege escalations                               |
| Investigation pattern | 1) Identify exploit CVE; 2) Verify patch status; 3) Check for post-exploitation activity; 4) Identify privileges gained |
| Response actions      | Patch vulnerability; revoke session; investigate post-exploit activity                                                  |
| Linked playbooks      | Multiple                                                                                                                |
| Multi-tenant note     | Per-tenant; patch portfolio awareness                                                                                   |

---

## 8.5 Defense Evasion Tactics

### T1027 – Obfuscated Files or Information

| Element               | Detail                                                                                            |
| --------------------- | ------------------------------------------------------------------------------------------------- |
| Tactic                | Defense Evasion                                                                                   |
| Prevalence            | **Very High**                                                                                     |
| Description           | Obfuscation of malicious code to evade detection                                                  |
| Data sources          | EDR, file analysis, decoders                                                                      |
| Detection guidance    | High-entropy files, base64-encoded scripts, packed/encrypted payloads, suspicious string patterns |
| Investigation pattern | 1) Decode/deobfuscate; 2) Identify decoded payload; 3) Analyze behavior                           |
| Response actions      | Quarantine; analyze; update detections                                                            |
| Linked playbooks      | Multiple                                                                                          |
| Multi-tenant note     | Per-tenant; sanitized findings shareable                                                          |

### T1562 – Impair Defenses

| Element               | Detail                                                                                                                                               |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tactic                | Defense Evasion                                                                                                                                      |
| Prevalence            | **High**                                                                                                                                             |
| Description           | Disabling AV/EDR, log clearing, blocking telemetry                                                                                                   |
| Data sources          | EDR (own state), Windows event logs (1102 log clear), security tool admin logs                                                                       |
| Detection guidance    | EDR/AV service stoppage, security log clearing events, GPO changes affecting security                                                                |
| Investigation pattern | 1) Identify which defense was impaired; 2) Identify the actor/credential used; 3) Re-enable defenses; 4) Check for activity during impairment window |
| Response actions      | Restore defenses; isolate host; investigate gap window                                                                                               |
| Linked playbooks      | `02_PLAYBOOKS/02.1_Ransomware/`, `02_PLAYBOOKS/02.13_APT-Campaign/`                                                                                  |
| Multi-tenant note     | Per-tenant; serious indicator                                                                                                                        |

---

## 8.6 Credential Access Tactics

### T1003 – OS Credential Dumping (T1003.001/.002/.003/.006)

| Element               | Detail                                                                                                                           |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Tactic                | Credential Access                                                                                                                |
| Prevalence            | **High**                                                                                                                         |
| Sub-techniques        | .001 LSASS Memory, .002 SAM, .003 NTDS, .006 DCSync                                                                              |
| Description           | Extracting credentials from OS (Mimikatz-like)                                                                                   |
| Data sources          | EDR (LSASS access, process behavior), Windows event logs (4662 DCSync), Sysmon                                                   |
| Detection guidance    | Mimikatz signatures, LSASS read/process access by non-system processes, NTDS.dit access, DCSync replication from non-DC sources  |
| Investigation pattern | 1) Identify dumping tool/technique; 2) Identify accounts exposed; 3) Force credential rotation; 4) Investigate downstream access |
| Response actions      | Rotate ALL exposed credentials (especially KRBTGT, admin); isolate host; investigate session activity                            |
| Linked playbooks      | `02_PLAYBOOKS/02.7_Credential-Attack/`, multiple                                                                                 |
| Multi-tenant note     | Per-tenant; high-impact                                                                                                          |

### T1110 – Brute Force (T1110.001/.002/.003/.004)

| Element               | Detail                                                                                                                                       |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Tactic                | Credential Access                                                                                                                            |
| Prevalence            | **High**                                                                                                                                     |
| Sub-techniques        | .001 Password Guessing, .002 Password Cracking, .003 Password Spraying, .004 Credential Stuffing                                             |
| Description           | Repeated authentication attempts                                                                                                             |
| Data sources          | IdP logs, SIEM, VPN logs, application logs                                                                                                   |
| Detection guidance    | Multiple failed logons across accounts (spraying), failed → success patterns, credential stuffing from known leaked credentials              |
| Investigation pattern | 1) Identify scope (accounts targeted); 2) Identify source IPs; 3) Identify successful logons; 4) Block source; 5) Reset compromised accounts |
| Response actions      | Block source IPs; reset compromised accounts; enforce MFA; lockout policies review                                                           |
| Linked playbooks      | `02_PLAYBOOKS/02.7_Credential-Attack/`                                                                                                       |
| Multi-tenant note     | Cross-tenant spraying campaigns observed; CCIC may trigger                                                                                   |

---

## 8.7 Discovery Tactics

### T1018 – Remote System Discovery

| Element               | Detail                                                                                        |
| --------------------- | --------------------------------------------------------------------------------------------- |
| Tactic                | Discovery                                                                                     |
| Prevalence            | **High**                                                                                      |
| Description           | Network/system enumeration (net view, nltest, etc.)                                           |
| Data sources          | EDR, command execution logs                                                                   |
| Detection guidance    | Suspicious enumeration commands by non-IT users, large-scale system discovery                 |
| Investigation pattern | 1) Identify enumeration scope; 2) Correlate with prior/subsequent activity; 3) Identify actor |
| Response actions      | Investigate actor context; check for lateral movement                                         |
| Linked playbooks      | Multiple                                                                                      |
| Multi-tenant note     | Per-tenant                                                                                    |

### T1087 – Account Discovery

| Element               | Detail                                                                                            |
| --------------------- | ------------------------------------------------------------------------------------------------- |
| Tactic                | Discovery                                                                                         |
| Prevalence            | **High**                                                                                          |
| Description           | Enumeration of accounts (net user, AzureAD enumeration)                                           |
| Data sources          | EDR, IdP audit logs, Azure AD logs                                                                |
| Detection guidance    | Bulk account enumeration, AzureAD list user operations from suspicious context                    |
| Investigation pattern | 1) Identify enumeration tool/method; 2) Correlate with other discovery; 3) Identify actor account |
| Response actions      | Investigate actor; check for credential compromise                                                |
| Linked playbooks      | Multiple                                                                                          |
| Multi-tenant note     | Per-tenant                                                                                        |

---

## 8.8 Lateral Movement Tactics

### T1021 – Remote Services (T1021.001/.002/.006)

| Element               | Detail                                                                                                                                |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Tactic                | Lateral Movement                                                                                                                      |
| Prevalence            | **High**                                                                                                                              |
| Sub-techniques        | .001 RDP, .002 SMB/Admin Shares, .006 WinRM                                                                                           |
| Description           | Using remote services for lateral movement                                                                                            |
| Data sources          | Windows event logs (4624 logon type 3/10), EDR, network logs                                                                          |
| Detection guidance    | RDP from non-jump-server sources, SMB admin share access from unusual sources, WinRM from suspicious contexts                         |
| Investigation pattern | 1) Identify source and destination; 2) Identify credential used; 3) Check for tool transfer; 4) Track command execution post-movement |
| Response actions      | Disable account used; isolate source/destination; investigate full session                                                            |
| Linked playbooks      | Multiple                                                                                                                              |
| Multi-tenant note     | Per-tenant                                                                                                                            |

### T1570 – Lateral Tool Transfer

| Element               | Detail                                                                                                      |
| --------------------- | ----------------------------------------------------------------------------------------------------------- |
| Tactic                | Lateral Movement                                                                                            |
| Prevalence            | **High**                                                                                                    |
| Description           | Transferring tools to other systems for lateral execution                                                   |
| Data sources          | EDR (file writes), SMB logs, network logs                                                                   |
| Detection guidance    | Tool file transfers via SMB/admin shares, execution of newly-transferred files                              |
| Investigation pattern | 1) Identify transferred tool; 2) Identify destinations; 3) Identify executions; 4) Quarantine + investigate |
| Response actions      | Quarantine tool; investigate executions; remove                                                             |
| Linked playbooks      | Multiple                                                                                                    |
| Multi-tenant note     | Per-tenant                                                                                                  |

---

## 8.9 Collection Tactics

### T1005 – Data from Local System

| Element               | Detail                                                                            |
| --------------------- | --------------------------------------------------------------------------------- |
| Tactic                | Collection                                                                        |
| Prevalence            | **High**                                                                          |
| Description           | Collection of files from local system                                             |
| Data sources          | EDR, file access logs, DLP                                                        |
| Detection guidance    | Bulk file access by non-typical users/processes, staging archives (zip, rar)      |
| Investigation pattern | 1) Identify files accessed; 2) Identify staging location; 3) Track exfil attempts |
| Response actions      | Block exfil; preserve evidence; rotate credentials                                |
| Linked playbooks      | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`                                     |
| Multi-tenant note     | Per-tenant                                                                        |

---

## 8.10 Command and Control Tactics

### T1071 – Application Layer Protocol (T1071.001/.004)

| Element               | Detail                                                                                                                              |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Tactic                | Command and Control                                                                                                                 |
| Prevalence            | **Very High**                                                                                                                       |
| Sub-techniques        | .001 Web Protocols (HTTP/HTTPS), .004 DNS                                                                                           |
| Description           | C2 over HTTP/HTTPS/DNS                                                                                                              |
| Data sources          | NDR, proxy logs, DNS logs, EDR network telemetry                                                                                    |
| Detection guidance    | Beaconing patterns (regular intervals), suspicious user-agents, low-and-slow C2, DNS tunneling, traffic to newly-registered domains |
| Investigation pattern | 1) Identify C2 domain/IP; 2) Identify infected hosts; 3) Identify communication patterns; 4) Block C2; 5) Investigate hosts         |
| Response actions      | Block C2 IoCs; isolate infected hosts; investigate scope                                                                            |
| Linked playbooks      | `02_PLAYBOOKS/02.13_APT-Campaign/`, multiple                                                                                        |
| Multi-tenant note     | C2 IoCs sanitized for cross-tenant defense                                                                                          |

### T1573 – Encrypted Channel

| Element               | Detail                                                                      |
| --------------------- | --------------------------------------------------------------------------- |
| Tactic                | Command and Control                                                         |
| Prevalence            | **High**                                                                    |
| Description           | Encrypted C2 (TLS, custom encryption)                                       |
| Data sources          | NDR, JA3/JA3S fingerprints, TLS metadata                                    |
| Detection guidance    | Suspicious JA3 fingerprints, self-signed certs, atypical TLS patterns       |
| Investigation pattern | 1) Identify TLS fingerprint; 2) Identify destination; 3) Correlate with EDR |
| Response actions      | Block destination; investigate host                                         |
| Linked playbooks      | Multiple                                                                    |
| Multi-tenant note     | Per-tenant                                                                  |

---

## 8.11 Exfiltration Tactics

### T1567 – Exfiltration Over Web Service (T1567.001/.002)

| Element               | Detail                                                                                                                      |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Tactic                | Exfiltration                                                                                                                |
| Prevalence            | **Very High**                                                                                                               |
| Sub-techniques        | .001 Code Repository, .002 Cloud Storage                                                                                    |
| Description           | Exfiltration to legitimate cloud services (Dropbox, Google Drive, GitHub, Rclone, MEGA)                                     |
| Data sources          | DLP, proxy logs, NDR, CASB                                                                                                  |
| Detection guidance    | Large uploads to cloud storage from non-typical users, Rclone usage, unusual cloud SaaS data flows                          |
| Investigation pattern | 1) Identify destination service; 2) Identify volume + data type; 3) Identify source user/host; 4) Block + preserve evidence |
| Response actions      | Block destination; preserve evidence; legal hold; investigate data scope                                                    |
| Linked playbooks      | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`                                                                               |
| Multi-tenant note     | Per-tenant; cross-tenant cloud destinations possible                                                                        |

### T1041 – Exfiltration Over C2 Channel

| Element               | Detail                                                                                    |
| --------------------- | ----------------------------------------------------------------------------------------- |
| Tactic                | Exfiltration                                                                              |
| Prevalence            | **High**                                                                                  |
| Description           | Data exfiltration via existing C2 channel                                                 |
| Data sources          | NDR, EDR, C2 destination volume                                                           |
| Detection guidance    | Unusual outbound volume to C2 destinations, large POST requests to suspicious domains     |
| Investigation pattern | 1) Identify C2 destination; 2) Identify exfil volume; 3) Identify data accessed pre-exfil |
| Response actions      | Block C2; preserve evidence; investigate scope                                            |
| Linked playbooks      | Multiple                                                                                  |
| Multi-tenant note     | Per-tenant                                                                                |

---

## 8.12 Impact Tactics

### T1486 – Data Encrypted for Impact

| Element               | Detail                                                                                                                                                       |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Tactic                | Impact                                                                                                                                                       |
| Prevalence            | **Very High**                                                                                                                                                |
| Description           | Ransomware encryption of victim data                                                                                                                         |
| Data sources          | EDR (mass file modification), file integrity monitoring, SIEM                                                                                                |
| Detection guidance    | Rapid file modification across many files, file extension changes, ransom note file creation, encryption process patterns                                    |
| Investigation pattern | 1) Identify ransomware family; 2) Identify scope of encryption; 3) Check for exfiltration pre-encryption (double-extortion); 4) Activate ransomware playbook |
| Response actions      | Isolate; activate BCP/DR; activate ransomware playbook; legal/Compliance engagement                                                                          |
| Linked playbooks      | `02_PLAYBOOKS/02.1_Ransomware/` (all)                                                                                                                        |
| Multi-tenant note     | Cross-client ransomware campaigns common; CCIC likely                                                                                                        |

### T1490 – Inhibit System Recovery

| Element               | Detail                                                                                |
| --------------------- | ------------------------------------------------------------------------------------- |
| Tactic                | Impact                                                                                |
| Prevalence            | **High** (paired with ransomware)                                                     |
| Description           | Deleting backups, shadow copies, recovery features                                    |
| Data sources          | EDR, Windows event logs (vssadmin commands)                                           |
| Detection guidance    | `vssadmin delete shadows`, `wbadmin delete`, backup service tampering                 |
| Investigation pattern | 1) Identify deletion command; 2) Correlate with ransomware; 3) Check backup integrity |
| Response actions      | Verify backup state; activate BCP/DR; isolate                                         |
| Linked playbooks      | `02_PLAYBOOKS/02.1_Ransomware/`                                                       |
| Multi-tenant note     | Per-tenant; paired with ransomware                                                    |

---

# 9. Cloud-Specific Techniques (Quick Reference)

| Technique      | Tactic                       | Brief                                        |
| -------------- | ---------------------------- | -------------------------------------------- |
| T1078.004      | Initial Access / Persistence | Cloud account abuse (compromised IAM, OAuth) |
| T1530          | Collection                   | Data from cloud storage (S3, Blob)           |
| T1098.001/.003 | Persistence                  | Cloud account / OAuth app manipulation       |
| T1496          | Impact                       | Resource hijacking (cryptomining)            |
| T1098.005      | Persistence                  | Device registration in IdP                   |

**Detailed cloud playbook:** `02_PLAYBOOKS/02.10_Cloud-Security-Incident/`

---

# 10. Identity-Specific Techniques (Quick Reference)

| Technique | Tactic                              | Brief                                                  |
| --------- | ----------------------------------- | ------------------------------------------------------ |
| T1556     | Credential Access / Defense Evasion | Modify authentication (MFA bypass)                     |
| T1621     | Credential Access                   | MFA request generation (MFA fatigue)                   |
| T1606     | Credential Access                   | Forge web credentials (Golden SAML, OAuth token theft) |
| T1098.005 | Persistence                         | Additional device registration                         |
| T1606.001 | Credential Access                   | Forged Kerberos tickets (Golden/Silver Ticket)         |

---

# 11. Multi-Tenant Considerations (Mandatory)

| Aspect                               | Application                      |
| ------------------------------------ | -------------------------------- |
| Per-tenant detection rules           | Standard                         |
| Sanitized TTP findings               | Cross-portfolio applicable       |
| Cross-client TTP correlation         | Via Threat Intel + Detection Eng |
| CCIC triggers per technique          | Documented per-technique above   |
| Tenant-specific detection variations | Per client environment           |

**Reference:**

- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`

---

# 12. How to Use This Reference (Mandatory)

## 12.1 L1 Analyst Usage

| Situation                        | Action                                                           |
| -------------------------------- | ---------------------------------------------------------------- |
| Alert references MITRE technique | Look up technique → use detection guidance + escalation criteria |
| Unfamiliar technique seen        | Reference → apply detection guidance                             |
| Triage decision needed           | Reference response actions                                       |

## 12.2 L2/L3 Analyst Usage

| Situation                    | Action                          |
| ---------------------------- | ------------------------------- |
| Investigation begins         | Reference investigation pattern |
| Multiple techniques observed | Map to attack chain             |
| Detection gap identified     | Feed Detection Engineering      |

## 12.3 IR Team Usage

| Situation               | Action               |
| ----------------------- | -------------------- |
| Incident classification | Map to techniques    |
| Playbook selection      | Use linked playbooks |
| Response prioritization | Use response actions |

## 12.4 Detection Engineering Usage

| Situation               | Action                                      |
| ----------------------- | ------------------------------------------- |
| New rule development    | Reference detection guidance + data sources |
| Coverage gap analysis   | Cross-reference to ATT&CK                   |
| Purple team preparation | Select techniques for validation            |

---

# 13. Quarterly Update Process (Mandatory)

| Step | Action                                     | Owner              | Cadence   |
| ---- | ------------------------------------------ | ------------------ | --------- |
| 1    | Review new MITRE ATT&CK updates            | Threat Intel Lead  | Quarterly |
| 2    | Review threat landscape changes            | Threat Intel Lead  | Quarterly |
| 3    | Review recent incidents for new techniques | IR Team Lead       | Quarterly |
| 4    | Update detection guidance per new tools    | Detection Eng Lead | Quarterly |
| 5    | Update playbook linkage                    | IR Team Lead       | Quarterly |
| 6    | Publish updated version                    | Training Lead      | Quarterly |
| 7    | Communicate updates to SOC                 | Training Lead      | Quarterly |

---

# 14. Quality Checklist (Per Update)

- [ ] All MITRE ATT&CK changes reviewed
- [ ] New high-prevalence techniques added
- [ ] Deprecated techniques removed/flagged
- [ ] Detection guidance current
- [ ] Investigation patterns current
- [ ] Response actions current
- [ ] Playbook linkages accurate
- [ ] Multi-tenant notes maintained
- [ ] Version updated
- [ ] CISO + IR Team Lead approval
- [ ] SOC communication issued

---

# 15. Related Documents

| Document                        | Path                                                                               |
| ------------------------------- | ---------------------------------------------------------------------------------- |
| MITRE ATT&CK Quick Reference    | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`    |
| Tool Command Reference          | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Tool-Command-Reference.md`          |
| Common IoC Reference            | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Common-IoC-Reference.md`            |
| All Playbooks                   | `02_PLAYBOOKS/`                                                                    |
| SIEM Use Cases Master           | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md`                       |
| SIEM Query Library              | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md`                          |
| EDR Investigation Queries       | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Investigation-Queries.md`                    |
| TI Feed Management              | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md`           |
| Threat Actor Profile Template   | `08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md`       |
| TTP Intelligence Report         | `08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md`             |
| IoC Output Register             | `08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md`                 |
| Detection Improvement Log       | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`          |
| L2 Threat Hunting Procedures    | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md`        |
| L3 Threat Intel Integration     | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Threat-Intel-Integration.md`         |
| Purple Team Exercise Guide      | `10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`              |
| Red Team IR Integration SOP     | `10_TRAINING-AND-EXERCISES/10.3_Drills/Red-Team-IR-Integration-SOP.md`             |
| Cross-Client Incident Procedure | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md` |

---

# 16. Revision History

| Version | Date        | Author                                              | Changes         |
| ------- | ----------- | --------------------------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP Threat Intel Lead / Detection Engineering Lead | Initial version |

---

# 17. Approval

Approved by:

| Role                            | Name | Signature | Date |
| ------------------------------- | ---- | --------- | ---- |
| MSSP Threat Intel Lead          |      |           |      |
| MSSP Detection Engineering Lead |      |           |      |
| MSSP IR Team Lead               |      |           |      |
| MSSP CISO                       |      |           |      |

---

**End of Document**
