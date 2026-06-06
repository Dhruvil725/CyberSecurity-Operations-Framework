# MITRE ATT&CK Quick Reference

---

# 1. Document Control

| Field          | Value                                               |
| -------------- | --------------------------------------------------- |
| Document Name  | MITRE ATT&CK Quick Reference                        |
| Document ID    | MSSP-TRN-KB-002                                     |
| Version        | 1.0                                                 |
| Effective Date | 30-May-2026                                         |
| Owner          | MSSP Threat Intel Lead / Detection Engineering Lead |
| Approved By    | MSSP CISO                                           |
| Classification | Confidential – MSSP Internal                        |
| Review Cycle   | Quarterly (or upon MITRE ATT&CK framework update)   |

---

# 2. Purpose

This document defines the standardized **MITRE ATT&CK Quick Reference** providing SOC analysts (L1/L2/L3), IR Team members, Threat Intelligence analysts, and Detection Engineers with a single-page operational summary of the MITRE ATT&CK framework — enabling rapid lookup of tactics, techniques, sub-techniques, and procedures during alert triage, investigations, threat hunting, and detection engineering across the MSSP multi-tenant environment.

A formal MITRE ATT&CK Quick Reference is critical because:

- SOC analysts need instant tactical lookups during triage without browsing full ATT&CK website
- consistent ATT&CK terminology is the global standard for adversary behavior description
- MITRE ATT&CK is referenced in nearly all modern threat intelligence, vendor reports, and tools
- detection engineering, purple teaming, and threat hunting all map to ATT&CK
- L1 analysts encountering alert ATT&CK tags need rapid context
- L2/L3 analysts building investigation timelines need consistent technique mapping
- IR Team members briefing executives need plain-language ATT&CK translation
- Threat Intel analysts producing reports need consistent reference
- Detection Engineers measuring coverage need standardized framework
- ISO 27001 A.5.7 (threat intelligence) and NIST CSF DE.AE (event analysis) leverage ATT&CK
- RBI Cyber Security Framework and BFSI clients reference ATT&CK in vendor reports
- without quick reference, analysts spend valuable triage time on external research
- multi-tenant MSSPs need consistent ATT&CK application across all clients
- ATT&CK Navigator coverage matrices depend on consistent framework knowledge
- this reference is the operational quick-lookup companion to the detailed Attack Technique Reference

This reference ensures:

- single-page operational summary of ATT&CK Enterprise framework
- tactic and technique lookup tables
- sub-technique mapping
- common procedure examples per technique
- platform applicability (Windows, Linux, macOS, cloud, identity, etc.)
- data source mapping for detection
- linkage to Attack-Technique-Reference for deep dives
- linkage to ATT&CK Navigator usage
- multi-tenant operational consistency
- quarterly update cycle aligned to ATT&CK framework releases

**Reference alignment:**

- `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Attack-Technique-Reference.md`
- `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Tool-Command-Reference.md`
- `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Common-IoC-Reference.md`
- `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md`

---

# 3. Scope

This reference covers:

| Scope Element                                                              | Coverage       |
| -------------------------------------------------------------------------- | -------------- |
| MITRE ATT&CK Enterprise Matrix                                             | All 14 tactics |
| Key techniques (most prevalent)                                            | Yes            |
| Sub-techniques                                                             | Yes (key ones) |
| Platform mapping (Win, Linux, macOS, cloud, identity, network, containers) | Yes            |
| Data source mapping                                                        | Yes            |
| Detection considerations                                                   | Brief          |
| Investigation considerations                                               | Brief          |
| ATT&CK Navigator usage                                                     | Yes            |
| Multi-tenant operational use                                               | Yes            |

Out of scope:

- MITRE ATT&CK Mobile Matrix (separate doc if needed)
- MITRE ATT&CK ICS Matrix (separate doc if needed)
- Full technique deep-dives (covered by `Attack-Technique-Reference.md`)
- Specific detection rule code (covered by Detection Engineering repository)
- Specific actor profiles (covered by `08_POST-INCIDENT/08.4_Threat-Intel-Output/`)
- Specific IoCs (covered by `Common-IoC-Reference.md`)

---

# 4. Definitions

| Term             | Definition                                            |
| ---------------- | ----------------------------------------------------- |
| ATT&CK           | Adversarial Tactics, Techniques, and Common Knowledge |
| Tactic           | Adversary's tactical goal (the "why")                 |
| Technique        | How adversary achieves tactic (the "how")             |
| Sub-technique    | More specific technique variant                       |
| Procedure        | Specific implementation of a technique                |
| TTP              | Tactic, Technique, Procedure                          |
| ATT&CK Navigator | Visualization tool for ATT&CK coverage                |
| Data Source      | Telemetry source for detection                        |
| Platform         | OS/environment where technique applies                |
| Mitigation       | Defense against technique                             |
| Coverage Matrix  | Detection capability mapped to ATT&CK                 |
| Coverage Heatmap | Visual representation of coverage                     |

---

# 5. Roles and Responsibilities

| Role                                | Responsibilities                        |
| ----------------------------------- | --------------------------------------- |
| **MSSP Threat Intel Lead**          | Document ownership; quarterly updates   |
| **MSSP Detection Engineering Lead** | Coverage mapping; Navigator maintenance |
| **MSSP IR Team Lead**               | Operational use validation              |
| **MSSP SOC Manager**                | SOC tier adoption                       |
| **MSSP L1/L2/L3 Analysts**          | Reference users; feedback providers     |
| **All SOC Personnel**               | Apply ATT&CK consistently               |

---

# 6. ATT&CK Enterprise Matrix Overview (Mandatory)

## 6.1 The 14 Tactics

| #   | Tactic                   | Code   | Adversary Goal                               |
| --- | ------------------------ | ------ | -------------------------------------------- |
| 1   | **Reconnaissance**       | TA0043 | Gather information for planning              |
| 2   | **Resource Development** | TA0042 | Build/acquire/compromise infrastructure      |
| 3   | **Initial Access**       | TA0001 | Get into the target network                  |
| 4   | **Execution**            | TA0002 | Run malicious code                           |
| 5   | **Persistence**          | TA0003 | Maintain foothold across reboots/credentials |
| 6   | **Privilege Escalation** | TA0004 | Gain higher-level permissions                |
| 7   | **Defense Evasion**      | TA0005 | Avoid detection                              |
| 8   | **Credential Access**    | TA0006 | Steal account credentials                    |
| 9   | **Discovery**            | TA0007 | Learn about the environment                  |
| 10  | **Lateral Movement**     | TA0008 | Move through the environment                 |
| 11  | **Collection**           | TA0009 | Gather data of interest                      |
| 12  | **Command and Control**  | TA0011 | Communicate with compromised systems         |
| 13  | **Exfiltration**         | TA0010 | Steal data from the network                  |
| 14  | **Impact**               | TA0040 | Manipulate, interrupt, destroy               |

## 6.2 Visual Flow

┌──────────────────────────────────────────────────────────┐
│ RECONNAISSANCE → RESOURCE DEVELOPMENT │
│ (Pre-Compromise) │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ INITIAL ACCESS │
│ (Foothold) │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ EXECUTION → PERSISTENCE → PRIVILEGE ESCALATION │
│ (Establish + Elevate) │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ DEFENSE EVASION → CREDENTIAL ACCESS → DISCOVERY │
│ (Operate + Expand Knowledge) │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ LATERAL MOVEMENT → COLLECTION │
│ (Expand + Gather) │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ COMMAND AND CONTROL │
│ (Maintain Communications) │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ EXFILTRATION → IMPACT │
│ (Achieve Objectives) │
└──────────────────────────────────────────────────────────┘

---

# 7. Tactic-by-Tactic Quick Lookup (Mandatory)

## 7.1 TA0043 – Reconnaissance

| Technique ID | Name                               | Brief                                |
| ------------ | ---------------------------------- | ------------------------------------ |
| T1595        | Active Scanning                    | Scanning IPs, ports, vulnerabilities |
| T1592        | Gather Victim Host Information     | OS, software, hardware               |
| T1589        | Gather Victim Identity Information | Emails, names                        |
| T1591        | Gather Victim Org Information      | Business relationships               |
| T1593        | Search Open Websites/Domains       | OSINT                                |
| T1597        | Search Closed Sources              | Dark web, paid intel                 |

**Data sources:** Network traffic, web logs, DNS, OSINT monitoring

---

## 7.2 TA0042 – Resource Development

| Technique ID | Name                      | Brief                                  |
| ------------ | ------------------------- | -------------------------------------- |
| T1583        | Acquire Infrastructure    | Domains, servers, accounts             |
| T1584        | Compromise Infrastructure | Hijack legitimate infrastructure       |
| T1585        | Establish Accounts        | Social media, email                    |
| T1586        | Compromise Accounts       | Hijack existing accounts               |
| T1588        | Obtain Capabilities       | Malware, exploits, tools               |
| T1608        | Stage Capabilities        | Upload tools to staging infrastructure |

**Data sources:** Internet scan data, certificate transparency, domain registration

---

## 7.3 TA0001 – Initial Access

| Technique ID | Name                                     | Brief                        |
| ------------ | ---------------------------------------- | ---------------------------- |
| T1566        | Phishing (.001/.002/.003)                | Email-based attack           |
| T1190        | Exploit Public-Facing Application        | Web/app vulnerability        |
| T1078        | Valid Accounts (.001/.002/.003/.004)     | Legitimate credentials       |
| T1133        | External Remote Services                 | RDP/VPN/SSH access           |
| T1195        | Supply Chain Compromise (.001/.002/.003) | Hardware/software/dependency |
| T1199        | Trusted Relationship                     | Trusted 3rd-party access     |
| T1091        | Replication Through Removable Media      | USB/external media           |
| T1189        | Drive-by Compromise                      | Malicious website            |
| T1200        | Hardware Additions                       | Physical access              |

**Data sources:** Email, IdP logs, web proxy, EDR, vulnerability scanners, USB monitoring

---

## 7.4 TA0002 – Execution

| Technique ID | Name                                          | Brief                             |
| ------------ | --------------------------------------------- | --------------------------------- |
| T1059        | Command and Scripting Interpreter (.001-.008) | PowerShell, cmd, bash, Python, JS |
| T1204        | User Execution (.001/.002/.003)               | User clicks/opens                 |
| T1053        | Scheduled Task/Job (.005)                     | Persistence via scheduled task    |
| T1569        | System Services (.002)                        | Service execution                 |
| T1106        | Native API                                    | Direct API calls                  |
| T1129        | Shared Modules                                | DLL loading                       |
| T1203        | Exploitation for Client Execution             | Browser/document exploit          |
| T1559        | Inter-Process Communication                   | COM/IPC                           |
| T1648        | Serverless Execution                          | Lambda, Cloud Functions           |

**Data sources:** EDR process creation, command-line logs, Sysmon, Windows event logs (4688, 4103/4104)

---

## 7.5 TA0003 – Persistence

| Technique ID | Name                                            | Brief                          |
| ------------ | ----------------------------------------------- | ------------------------------ |
| T1547        | Boot/Logon Autostart Execution (.001/.004/.009) | Registry run keys, services    |
| T1053        | Scheduled Task/Job (.005)                       | Scheduled tasks                |
| T1543        | Create or Modify System Process (.003)          | New services                   |
| T1078        | Valid Accounts                                  | Persistent credentials         |
| T1136        | Create Account (.001/.002/.003)                 | New local/domain/cloud account |
| T1098        | Account Manipulation (.001/.003/.005)           | Modify accounts                |
| T1505        | Server Software Component (.003)                | Web shells                     |
| T1525        | Implant Internal Image                          | Trojanized images              |
| T1546        | Event Triggered Execution (.003/.008)           | WMI, accessibility features    |
| T1574        | Hijack Execution Flow (.001/.002/.007)          | DLL hijacking                  |

**Data sources:** Registry monitoring, file integrity monitoring, EDR, event logs (4697, 4698)

---

## 7.6 TA0004 – Privilege Escalation

| Technique ID | Name                                     | Brief                      |
| ------------ | ---------------------------------------- | -------------------------- |
| T1548        | Abuse Elevation Control Mechanism (.002) | UAC bypass, sudo abuse     |
| T1068        | Exploitation for Privilege Escalation    | OS/app vulnerability       |
| T1078        | Valid Accounts                           | Already-elevated creds     |
| T1055        | Process Injection (.001/.012)            | Code in another process    |
| T1134        | Access Token Manipulation (.001)         | Token theft/impersonation  |
| T1547        | Autostart Execution                      | Persistence with privilege |
| T1543        | System Process                           | Service privilege          |
| T1484        | Domain Policy Modification               | GPO abuse                  |

**Data sources:** EDR, Windows event logs (4672, 4673), Sysmon

---

## 7.7 TA0005 – Defense Evasion

| Technique ID | Name                                           | Brief                        |
| ------------ | ---------------------------------------------- | ---------------------------- |
| T1027        | Obfuscated Files or Information                | Encoded payloads             |
| T1562        | Impair Defenses (.001/.002/.004)               | Disable AV, firewall         |
| T1070        | Indicator Removal (.001/.002/.003/.004/.006)   | Clear logs, files, artifacts |
| T1112        | Modify Registry                                | Registry tampering           |
| T1055        | Process Injection                              | Code in legit process        |
| T1140        | Deobfuscate/Decode Files                       | Decode payload at runtime    |
| T1218        | System Binary Proxy Execution (.005/.010/.011) | LOLBins (rundll32, msbuild)  |
| T1036        | Masquerading (.005)                            | Filename impersonation       |
| T1497        | Virtualization/Sandbox Evasion                 | Anti-analysis                |
| T1620        | Reflective Code Loading                        | In-memory loading            |
| T1556        | Modify Authentication Process (.006/.007)      | MFA bypass                   |

**Data sources:** EDR, file integrity, registry monitoring, Sysmon, event log clearing (1102)

---

## 7.8 TA0006 – Credential Access

| Technique ID | Name                                           | Brief                                 |
| ------------ | ---------------------------------------------- | ------------------------------------- |
| T1003        | OS Credential Dumping (.001/.002/.003/.006)    | LSASS, SAM, NTDS, DCSync              |
| T1110        | Brute Force (.001/.002/.003/.004)              | Password guessing, spraying, stuffing |
| T1555        | Credentials from Password Stores (.003/.004)   | Browser/keychain                      |
| T1056        | Input Capture (.001/.002)                      | Keylogging                            |
| T1187        | Forced Authentication                          | NTLM relay, responder                 |
| T1606        | Forge Web Credentials (.001/.002)              | Golden SAML, OAuth tokens             |
| T1621        | Multi-Factor Authentication Request Generation | MFA fatigue/bombing                   |
| T1558        | Steal/Forge Kerberos Tickets (.003/.004)       | Kerberoasting, Golden Ticket          |
| T1552        | Unsecured Credentials (.001/.004)              | Files, registry, GPO                  |
| T1212        | Exploitation for Credential Access             | Vulnerability for creds               |

**Data sources:** EDR (LSASS access), IdP logs, Windows event logs (4624/4625/4662/4769), Sysmon

---

## 7.9 TA0007 – Discovery

| Technique ID | Name                                         | Brief                     |
| ------------ | -------------------------------------------- | ------------------------- |
| T1018        | Remote System Discovery                      | Network enumeration       |
| T1087        | Account Discovery (.001/.002/.004)           | User/group enumeration    |
| T1082        | System Information Discovery                 | OS, hardware info         |
| T1083        | File and Directory Discovery                 | Filesystem walk           |
| T1057        | Process Discovery                            | Running processes         |
| T1016        | System Network Configuration Discovery       | IP, routing               |
| T1049        | System Network Connections Discovery         | netstat                   |
| T1135        | Network Share Discovery                      | SMB enumeration           |
| T1069        | Permission Groups Discovery (.001/.002/.003) | Group membership          |
| T1518        | Software Discovery (.001)                    | Installed software        |
| T1046        | Network Service Discovery                    | Port scanning             |
| T1538        | Cloud Service Dashboard                      | Cloud console access      |
| T1526        | Cloud Service Discovery                      | Cloud service enumeration |

**Data sources:** EDR, command-line logs, IdP, cloud audit logs

---

## 7.10 TA0008 – Lateral Movement

| Technique ID | Name                                              | Brief                          |
| ------------ | ------------------------------------------------- | ------------------------------ |
| T1021        | Remote Services (.001/.002/.004/.006)             | RDP, SMB, SSH, WinRM           |
| T1570        | Lateral Tool Transfer                             | Move tools between hosts       |
| T1080        | Taint Shared Content                              | Malicious files in shares      |
| T1550        | Use Alternate Authentication Material (.002/.003) | Pass-the-hash, pass-the-ticket |
| T1563        | Remote Service Session Hijacking (.002)           | RDP/SSH session hijack         |
| T1534        | Internal Spearphishing                            | Phishing within network        |
| T1210        | Exploitation of Remote Services                   | Vulnerability for lateral      |

**Data sources:** Windows event logs (4624 type 3/10), EDR, network logs, SMB logs

---

## 7.11 TA0009 – Collection

| Technique ID | Name                                                | Brief                              |
| ------------ | --------------------------------------------------- | ---------------------------------- |
| T1005        | Data from Local System                              | Local file collection              |
| T1039        | Data from Network Shared Drive                      | SMB collection                     |
| T1213        | Data from Information Repositories (.001/.002/.003) | SharePoint, Confluence, code repos |
| T1530        | Data from Cloud Storage                             | S3, Blob, GCS                      |
| T1114        | Email Collection (.001/.002/.003)                   | Mail data                          |
| T1056        | Input Capture                                       | Keylogging                         |
| T1113        | Screen Capture                                      | Screenshots                        |
| T1125        | Video Capture                                       | Camera capture                     |
| T1115        | Clipboard Data                                      | Clipboard content                  |
| T1560        | Archive Collected Data (.001/.002/.003)             | Zip/rar staging                    |
| T1119        | Automated Collection                                | Scripted collection                |

**Data sources:** EDR, DLP, file access logs, email logs

---

## 7.12 TA0011 – Command and Control

| Technique ID | Name                                             | Brief                           |
| ------------ | ------------------------------------------------ | ------------------------------- |
| T1071        | Application Layer Protocol (.001/.002/.003/.004) | HTTP/HTTPS, FTP, DNS, mail      |
| T1573        | Encrypted Channel (.001/.002)                    | Symmetric/asymmetric encryption |
| T1090        | Proxy (.001/.002/.003)                           | Internal/external/multi-hop     |
| T1132        | Data Encoding (.001/.002)                        | Base64, custom                  |
| T1568        | Dynamic Resolution (.002)                        | DGA                             |
| T1102        | Web Service (.001/.002/.003)                     | Legit services for C2           |
| T1095        | Non-Application Layer Protocol                   | Custom protocols                |
| T1219        | Remote Access Software                           | TeamViewer, AnyDesk             |
| T1572        | Protocol Tunneling                               | Tunnel over allowed protocols   |
| T1008        | Fallback Channels                                | Backup C2                       |
| T1665        | Hide Infrastructure                              | Hide C2 location                |

**Data sources:** NDR, proxy logs, DNS, JA3/JA3S, EDR network telemetry

---

## 7.13 TA0010 – Exfiltration

| Technique ID | Name                                                    | Brief                                   |
| ------------ | ------------------------------------------------------- | --------------------------------------- |
| T1041        | Exfiltration Over C2 Channel                            | Through existing C2                     |
| T1567        | Exfiltration Over Web Service (.001/.002/.003/.004)     | Cloud storage, code repos, text storage |
| T1048        | Exfiltration Over Alternative Protocol (.001/.002/.003) | DNS, ICMP                               |
| T1029        | Scheduled Transfer                                      | Timed exfil                             |
| T1020        | Automated Exfiltration (.001)                           | Scripted                                |
| T1052        | Exfiltration Over Physical Medium (.001)                | USB                                     |
| T1011        | Exfiltration Over Other Network Medium                  | Bluetooth, WiFi                         |
| T1030        | Data Transfer Size Limits                               | Chunked transfer                        |

**Data sources:** DLP, NDR, CASB, EDR, cloud API logs

---

## 7.14 TA0040 – Impact

| Technique ID | Name                               | Brief                               |
| ------------ | ---------------------------------- | ----------------------------------- |
| T1486        | Data Encrypted for Impact          | Ransomware encryption               |
| T1490        | Inhibit System Recovery            | Delete backups, shadow copies       |
| T1485        | Data Destruction                   | Wipe data                           |
| T1561        | Disk Wipe (.001/.002)              | Disk content/structure wipe         |
| T1565        | Data Manipulation (.001/.002/.003) | Modify stored, transmitted, runtime |
| T1491        | Defacement (.001/.002)             | Internal/external defacement        |
| T1496        | Resource Hijacking                 | Cryptomining                        |
| T1499        | Endpoint DoS (.001/.002/.003/.004) | DoS at endpoint                     |
| T1498        | Network DoS (.001/.002)            | DoS at network                      |
| T1531        | Account Access Removal             | Lock out users                      |
| T1657        | Financial Theft                    | Fraudulent transactions             |

**Data sources:** EDR, SIEM, file integrity, backup logs, transaction logs

---

# 8. Platform Mapping (Mandatory)

| Platform                  | Most Relevant Tactics                                                                     |
| ------------------------- | ----------------------------------------------------------------------------------------- |
| **Windows**               | All tactics (full Enterprise coverage)                                                    |
| **Linux**                 | Initial Access, Execution, Persistence, Privilege Escalation, Lateral Movement            |
| **macOS**                 | Initial Access, Execution, Persistence, Defense Evasion                                   |
| **Cloud (AWS/Azure/GCP)** | Initial Access, Persistence, Defense Evasion, Discovery, Collection, Exfiltration, Impact |
| **Identity (IdP)**        | Initial Access, Persistence, Credential Access, Defense Evasion                           |
| **Network**               | C2, Exfiltration, Lateral Movement                                                        |
| **Containers**            | Initial Access, Execution, Persistence, Privilege Escalation, Lateral Movement            |
| **SaaS**                  | Initial Access, Persistence, Collection, Exfiltration                                     |
| **Office 365**            | Initial Access, Persistence, Collection, Exfiltration                                     |
| **Azure AD**              | Initial Access, Persistence, Credential Access, Defense Evasion                           |
| **Google Workspace**      | Initial Access, Persistence, Collection, Exfiltration                                     |

---

# 9. Data Source Quick Mapping (Mandatory)

| Data Source                                | Tactics Supported                              |
| ------------------------------------------ | ---------------------------------------------- |
| **EDR (process, file, network telemetry)** | All except Recon, Resource Dev                 |
| **SIEM (aggregated logs)**                 | All                                            |
| **Email Security Gateway**                 | Initial Access (Phishing), Collection          |
| **Web Proxy / SWG**                        | Initial Access, C2, Exfiltration               |
| **NDR / Network Monitoring**               | Lateral Movement, C2, Exfiltration, Discovery  |
| **IdP Logs (Azure AD, Okta, AD)**          | Credential Access, Initial Access, Persistence |
| **Cloud Audit Logs**                       | All cloud-relevant tactics                     |
| **DLP / CASB**                             | Collection, Exfiltration                       |
| **Vulnerability Scanner**                  | Initial Access (vuln awareness)                |
| **DNS Logs**                               | C2, Discovery                                  |
| **WAF Logs**                               | Initial Access (T1190)                         |
| **File Integrity Monitoring**              | Persistence, Defense Evasion, Impact           |
| **Threat Intel Feed**                      | Pre-compromise + IoCs across all               |

---

# 10. ATT&CK Navigator Usage (Mandatory)

## 10.1 Purpose

ATT&CK Navigator is the visualization tool for tracking:

- Current detection coverage (per technique)
- Coverage gaps
- Adversary group overlap
- Detection priority

## 10.2 MSSP ATT&CK Navigator Layers

| Layer                          | Purpose                         | Owner               |
| ------------------------------ | ------------------------------- | ------------------- |
| **Master Coverage Layer**      | Current MSSP detection coverage | Detection Eng Lead  |
| **Per-Client Coverage Layer**  | Coverage per tenant             | Detection Eng + SDM |
| **Threat Actor Layer**         | Per-actor TTP overlay           | Threat Intel Lead   |
| **Purple Team Findings Layer** | Recent purple team coverage     | Detection Eng Lead  |
| **Red Team Findings Layer**    | Recent red team gaps            | Detection Eng Lead  |
| **Industry-Specific Layer**    | BFSI / Healthcare / etc.        | Threat Intel Lead   |

## 10.3 Color Coding Standard

| Color       | Meaning                             |
| ----------- | ----------------------------------- |
| Dark Green  | Detection mature + tuned            |
| Light Green | Detection exists but needs tuning   |
| Yellow      | Partial detection / data source gap |
| Orange      | Detection planned, not deployed     |
| Red         | No detection capability             |
| Grey        | Not applicable to environment       |

---

# 11. Operational Use Patterns (Mandatory)

## 11.1 L1 Analyst Quick Lookup

| Situation                                     | Action                                                       |
| --------------------------------------------- | ------------------------------------------------------------ |
| Alert tagged with technique (e.g., T1059.001) | Look up technique → understand context → triage per playbook |
| Unfamiliar technique                          | Read brief → escalate to L2 if uncertain                     |
| Multiple techniques in alert                  | Map to attack chain → escalate severity                      |

## 11.2 L2/L3 Analyst Investigation

| Situation            | Action                                                                |
| -------------------- | --------------------------------------------------------------------- |
| Investigation begins | Map observed activity to ATT&CK techniques                            |
| Build timeline       | Sequence techniques per tactic order                                  |
| Identify gaps        | Note missing techniques (e.g., persistence not observed but expected) |
| Hunt expansion       | Use ATT&CK to identify related techniques to hunt                     |

## 11.3 IR Team Briefing

| Situation          | Action                             |
| ------------------ | ---------------------------------- |
| Executive briefing | Translate ATT&CK to plain language |
| Client briefing    | Use ATT&CK as standard reference   |
| Regulatory report  | Map incident to ATT&CK for clarity |

## 11.4 Detection Engineering

| Situation            | Action                           |
| -------------------- | -------------------------------- |
| New rule development | Map rule to ATT&CK technique     |
| Coverage measurement | Update Navigator per new rule    |
| Gap analysis         | Identify untouched techniques    |
| Purple team prep     | Select techniques for validation |

## 11.5 Threat Intel

| Situation                   | Action                            |
| --------------------------- | --------------------------------- |
| Actor profile               | Document actor TTPs via ATT&CK    |
| Campaign analysis           | Map campaign to ATT&CK techniques |
| External report consumption | Standardize via ATT&CK            |
| Cross-tenant correlation    | Use ATT&CK as common reference    |

---

# 12. Multi-Tenant Considerations (Mandatory)

| Aspect                                       | Application       |
| -------------------------------------------- | ----------------- |
| Per-tenant ATT&CK coverage tracked           | Standard          |
| Sanitized cross-tenant ATT&CK findings       | Portfolio defense |
| ATT&CK as common language across tenants     | Mandatory         |
| ATT&CK Navigator per tenant + portfolio      | Standard          |
| Cross-client campaign correlation via ATT&CK | Via Threat Intel  |
| Detection coverage variance across tenants   | Tracked quarterly |

**Reference:**

- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`

---

# 13. Common Pitfalls (Avoid These)

| Pitfall                                  | Correct Behavior                                           |
| ---------------------------------------- | ---------------------------------------------------------- |
| Using ATT&CK technique names without IDs | Always include ID for clarity (e.g., T1059.001 PowerShell) |
| Confusing tactic vs technique            | Tactic = goal; technique = how                             |
| Inventing custom technique IDs           | Use only MITRE-defined IDs                                 |
| Over-mapping (every alert = T1059)       | Be precise; map to specific sub-technique when possible    |
| Ignoring sub-techniques                  | Sub-techniques (e.g., .001) often essential for detection  |
| Static ATT&CK knowledge                  | Framework updates regularly; review quarterly              |
| Single-source ATT&CK                     | Cross-reference vendor-reported ATT&CK to confirm          |

---

# 14. Quarterly Update Process (Mandatory)

| Step | Action                                                         | Owner              | Cadence   |
| ---- | -------------------------------------------------------------- | ------------------ | --------- |
| 1    | Review MITRE ATT&CK quarterly release                          | Threat Intel Lead  | Quarterly |
| 2    | Identify new/changed techniques                                | Threat Intel Lead  | Quarterly |
| 3    | Update this reference document                                 | Threat Intel Lead  | Quarterly |
| 4    | Update Attack-Technique-Reference for new prevalent techniques | Threat Intel Lead  | Quarterly |
| 5    | Update Detection Eng coverage matrix                           | Detection Eng Lead | Quarterly |
| 6    | Update Navigator layers                                        | Detection Eng Lead | Quarterly |
| 7    | Communicate updates to SOC                                     | Training Lead      | Quarterly |

---

# 15. Quality Checklist (Per Update)

- [ ] MITRE ATT&CK quarterly release reviewed
- [ ] All 14 tactics still current
- [ ] Tactic-by-tactic tables updated
- [ ] New high-relevance techniques added
- [ ] Deprecated techniques flagged
- [ ] Platform mapping current
- [ ] Data source mapping current
- [ ] Navigator coverage updated
- [ ] Multi-tenant notes maintained
- [ ] Version updated
- [ ] CISO + IR Team Lead approval
- [ ] SOC communication issued

---

# 16. External Reference

- **MITRE ATT&CK Website:** `https://attack.mitre.org/`
- **ATT&CK Navigator:** `https://mitre-attack.github.io/attack-navigator/`
- **CTI Repository:** `https://github.com/mitre/cti`

---

# 17. Related Documents

| Document                            | Path                                                                               |
| ----------------------------------- | ---------------------------------------------------------------------------------- |
| Attack Technique Reference          | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Attack-Technique-Reference.md`      |
| Tool Command Reference              | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Tool-Command-Reference.md`          |
| Common IoC Reference                | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Common-IoC-Reference.md`            |
| All Playbooks (with MITRE Mappings) | `02_PLAYBOOKS/`                                                                    |
| SIEM Use Cases Master               | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md`                       |
| SIEM Query Library                  | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md`                          |
| EDR Investigation Queries           | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Investigation-Queries.md`                    |
| TI Feed Management                  | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md`           |
| Detection Improvement Log           | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`          |
| Threat Actor Profile Template       | `08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md`       |
| TTP Intelligence Report             | `08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md`             |
| L2 Threat Hunting Procedures        | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md`        |
| L3 Threat Intel Integration         | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Threat-Intel-Integration.md`         |
| Purple Team Exercise Guide          | `10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`              |
| Red Team IR Integration SOP         | `10_TRAINING-AND-EXERCISES/10.3_Drills/Red-Team-IR-Integration-SOP.md`             |
| Cross-Client Incident Procedure     | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md` |
| L1 Onboarding Program               | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L1-Onboarding-Program.md`               |
| L2 Onboarding Program               | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L2-Onboarding-Program.md`               |
| L3 Onboarding Program               | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L3-Onboarding-Program.md`               |

---

# 18. Revision History

| Version | Date        | Author                                              | Changes         |
| ------- | ----------- | --------------------------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP Threat Intel Lead / Detection Engineering Lead | Initial version |

---

# 19. Approval

Approved by:

| Role                            | Name | Signature | Date |
| ------------------------------- | ---- | --------- | ---- |
| MSSP Threat Intel Lead          |      |           |      |
| MSSP Detection Engineering Lead |      |           |      |
| MSSP IR Team Lead               |      |           |      |
| MSSP CISO                       |      |           |      |

---

**End of Document**
