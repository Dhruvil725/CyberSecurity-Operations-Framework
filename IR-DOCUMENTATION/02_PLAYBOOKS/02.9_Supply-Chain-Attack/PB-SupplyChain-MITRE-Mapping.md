# Playbook: Supply Chain Attack – MITRE ATT&CK Mapping

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Supply Chain Attack (MITRE ATT&CK Mapping)        |
| Document ID    | IR-PB-SC-006                                                 |
| Version        | 1.0                                                          |
| Effective Date | 19-May-2026                                                  |
| Owner          | L3 Lead / IR Team Lead                                       |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 supply chain incident          |

---

## 2. Purpose

This document provides the MITRE ATT&CK framework mapping for supply chain attacks handled under the Supply Chain Attack playbook set. This mapping serves to align detected techniques to the MITRE ATT&CK Enterprise framework, support threat intelligence enrichment during active supply chain investigations, guide detection engineering and SIEM/EDR rule development for supply chain threats, support L2/L3 scoping by identifying likely next-stage techniques after initial supply chain access, provide audit-ready documentation for ISO 27001, NIST CSF, and RBI compliance, enable structured threat hunting across observed supply chain TTPs, support post-incident reporting at technical and executive levels, and identify detection gaps specific to supply chain attack vectors.

This document is a living reference. Analysts must reference it during L2/L3 investigation and update it after major incidents when new techniques are observed.

---

## 3. Scope

Applies to all supply chain attack categories handled under:

- PB-SupplyChain-Master.md
- PB-SupplyChain-L1-Triage.md
- PB-SupplyChain-L2-Investigation.md
- PB-SupplyChain-L3-Forensics.md
- PB-SupplyChain-Vendor-Coordination.md

Attack classes covered:

- Software update supply chain compromise (SolarWinds-style)
- Malicious package in public repository (npm, PyPI, RubyGems, Maven, NuGet)
- Dependency confusion attacks
- CI/CD pipeline compromise
- Managed service provider (MSP/MSSP) compromise
- Open-source library and maintainer account compromise
- Third-party SDK and API compromise
- Container image supply chain compromise
- Hardware supply chain where digital evidence is available

---

## 4. MITRE ATT&CK Framework Reference

| Field              | Value                                                        |
| ------------------ | ------------------------------------------------------------ |
| Framework          | MITRE ATT&CK Enterprise                                      |
| Version Referenced | v14 (verify current at attack.mitre.org)                     |
| Supplementary      | MITRE ATT&CK for ICS if OT/ICS systems involved              |
| Scope              | Enterprise covering on-prem, cloud, CI/CD, containers        |

---

## 5. Supply Chain Attack – Full TTP Matrix

### 5.1 Initial Access

| Technique ID | Technique Name              | Sub-Technique                               | Attack Class                   | Description                                                  |
| ------------ | --------------------------- | ------------------------------------------- | ------------------------------ | ------------------------------------------------------------ |
| T1195        | Supply Chain Compromise     | T1195.001 Compromise Software Dependencies  | Package/library supply chain   | Attacker compromises software dependency used by target organization |
| T1195        | Supply Chain Compromise     | T1195.002 Compromise Software Supply Chain  | Software update supply chain   | Attacker compromises vendor software build or update mechanism |
| T1195        | Supply Chain Compromise     | T1195.003 Compromise Hardware Supply Chain  | Hardware supply chain          | Physical tampering with hardware before delivery             |
| T1199        | Trusted Relationship        | —                                           | MSP/MSSP compromise            | Attacker leverages trusted MSP or vendor relationship to access target |
| T1078        | Valid Accounts              | T1078.002 Domain Accounts                   | MSP credential abuse           | Use of stolen MSP or vendor credentials to access target environment |
| T1566        | Phishing                    | T1566.002 Spearphishing Link                | Vendor/developer compromise    | Phishing used to compromise vendor employee as first step    |

### 5.2 Execution

| Technique ID | Technique Name                    | Sub-Technique                     | Attack Class                    | Description                                                  |
| ------------ | --------------------------------- | --------------------------------- | ------------------------------- | ------------------------------------------------------------ |
| T1059        | Command and Scripting Interpreter | T1059.001 PowerShell              | Post-supply chain execution     | PowerShell execution via backdoored vendor software          |
| T1059        | Command and Scripting Interpreter | T1059.003 Windows Command Shell   | Post-supply chain execution     | CMD execution spawned by malicious vendor component          |
| T1059        | Command and Scripting Interpreter | T1059.004 Unix Shell              | Post-supply chain Linux         | Shell execution via backdoored library or package            |
| T1059        | Command and Scripting Interpreter | T1059.006 Python                  | Package supply chain            | Malicious Python package executing arbitrary code at install |
| T1059        | Command and Scripting Interpreter | T1059.007 JavaScript              | npm package supply chain        | Malicious JavaScript package executing code at install/import |
| T1072        | Software Deployment Tools         | —                                 | CI/CD compromise                | Attacker uses build/deployment tools to execute malicious code |
| T1569        | System Services                   | T1569.002 Service Execution       | Post-compromise execution       | Malicious service created and executed post-supply chain access |
| T1203        | Exploitation for Client Execution | —                                 | SDK/API compromise              | Malicious SDK code exploits client application at runtime    |

### 5.3 Persistence

| Technique ID | Technique Name                    | Sub-Technique                                        | Attack Class                | Description                                                  |
| ------------ | --------------------------------- | ---------------------------------------------------- | --------------------------- | ------------------------------------------------------------ |
| T1547        | Boot or Logon Autostart Execution | T1547.001 Registry Run Keys/Startup Folder           | Post-supply chain Windows   | Persistence via registry run keys after initial supply chain access |
| T1543        | Create or Modify System Process   | T1543.003 Windows Service                            | Post-supply chain Windows   | Malicious service installed for persistence after supply chain entry |
| T1053        | Scheduled Task/Job                | T1053.005 Scheduled Task                             | Post-supply chain Windows   | Scheduled task created for persistence                       |
| T1053        | Scheduled Task/Job                | T1053.003 Cron                                       | Post-supply chain Linux     | Cron job created for persistence on Linux systems            |
| T1505        | Server Software Component         | T1505.003 Web Shell                                  | Post-compromise web servers | Web shell planted after supply chain pivot to web servers    |
| T1078        | Valid Accounts                    | T1078.002 Domain Accounts                            | Post-compromise persistence | New domain accounts created for persistent access            |
| T1136        | Create Account                    | T1136.001 Local Account                              | Post-compromise persistence | New local accounts created on compromised systems            |
| T1136        | Create Account                    | T1136.002 Domain Account                             | Post-compromise persistence | New domain accounts created for long-term access             |
| T1098        | Account Manipulation              | T1098.001 Additional Cloud Credentials               | Cloud persistence           | New cloud API keys or credentials created for persistence    |
| T1546        | Event Triggered Execution         | T1546.003 Windows Management Instrumentation         | Post-compromise Windows     | WMI event subscription for fileless persistence              |

### 5.4 Privilege Escalation

| Technique ID | Technique Name                        | Sub-Technique                             | Attack Class                | Description                                                  |
| ------------ | ------------------------------------- | ----------------------------------------- | --------------------------- | ------------------------------------------------------------ |
| T1068        | Exploitation for Privilege Escalation | —                                         | Post-supply chain           | Local privilege escalation after initial supply chain access |
| T1548        | Abuse Elevation Control Mechanism     | T1548.002 Bypass User Account Control     | Post-supply chain Windows   | UAC bypass to gain elevated privileges                       |
| T1134        | Access Token Manipulation             | T1134.001 Token Impersonation/Theft       | Post-supply chain Windows   | Token manipulation to escalate privileges                    |
| T1484        | Domain Policy Modification            | T1484.001 Group Policy Modification       | Post-compromise domain      | GPO modification for privilege escalation or persistence     |
| T1098        | Account Manipulation                  | T1098.003 Additional Cloud Roles          | Cloud privilege escalation  | New cloud IAM roles attached for privilege escalation        |

### 5.5 Defense Evasion

| Technique ID | Technique Name              | Sub-Technique                                | Attack Class                    | Description                                                  |
| ------------ | --------------------------- | -------------------------------------------- | ------------------------------- | ------------------------------------------------------------ |
| T1036        | Masquerading                | T1036.005 Match Legitimate Name or Location  | Supply chain evasion            | Malicious code named to match legitimate vendor files        |
| T1027        | Obfuscated Files/Info       | T1027.002 Software Packing                   | Malicious package/binary        | Packed or obfuscated malicious component in supply chain     |
| T1027        | Obfuscated Files/Info       | T1027.010 Command Obfuscation                | Post-supply chain execution     | Obfuscated commands executed by backdoored software          |
| T1553        | Subvert Trust Controls      | T1553.002 Code Signing                       | Software update supply chain    | Malicious code signed with legitimate vendor certificate     |
| T1553        | Subvert Trust Controls      | T1553.006 Code Signing Policy Modification   | Post-compromise                 | Code signing policy modified to trust attacker certificates  |
| T1070        | Indicator Removal           | T1070.001 Clear Windows Event Logs           | Post-compromise cleanup         | Attacker clears Windows event logs to remove evidence        |
| T1070        | Indicator Removal           | T1070.003 Clear Command History              | Post-compromise cleanup Linux   | Shell history cleared to remove attacker command evidence    |
| T1070        | Indicator Removal           | T1070.004 File Deletion                      | Artifact removal                | Malicious artifacts deleted after execution                  |
| T1562        | Impair Defenses             | T1562.001 Disable or Modify Tools            | Post-compromise defense evasion | Security tools disabled on compromised systems               |
| T1562        | Impair Defenses             | T1562.006 Indicator Blocking                 | Post-compromise defense evasion | Malicious code suppresses security alerts or detections      |
| T1564        | Hide Artifacts              | T1564.001 Hidden Files and Directories       | Supply chain persistence        | Malicious artifacts hidden in filesystem                     |

### 5.6 Credential Access

| Technique ID | Technique Name                   | Sub-Technique                             | Attack Class                 | Description                                                  |
| ------------ | -------------------------------- | ----------------------------------------- | ---------------------------- | ------------------------------------------------------------ |
| T1003        | OS Credential Dumping            | T1003.001 LSASS Memory                   | Post-supply chain Windows    | LSASS dumped for credential harvesting after supply chain access |
| T1003        | OS Credential Dumping            | T1003.003 NTDS                           | Post-compromise domain       | NTDS.dit dumped for domain credential harvesting             |
| T1552        | Unsecured Credentials            | T1552.001 Credentials in Files           | Supply chain software access | Vendor software reads credential files on system             |
| T1552        | Unsecured Credentials            | T1552.004 Private Keys                   | Supply chain software access | Private keys read from filesystem by compromised software    |
| T1552        | Unsecured Credentials            | T1552.007 Container API                  | Container supply chain       | Container API queried for credentials                        |
| T1528        | Steal Application Access Token   | —                                        | Cloud supply chain           | OAuth and cloud tokens stolen via compromised software       |
| T1539        | Steal Web Session Cookie         | —                                        | SDK/web supply chain         | Session cookies stolen via compromised web SDK               |
| T1606        | Forge Web Credentials            | T1606.002 SAML Tokens                    | Identity supply chain        | SAML tokens forged after identity infrastructure compromise  |
| T1555        | Credentials from Password Stores | T1555.003 Credentials from Web Browsers  | Post-supply chain workstation | Browser credential stores accessed after supply chain entry |

### 5.7 Discovery

| Technique ID | Technique Name                     | Sub-Technique                  | Attack Class                 | Description                                                  |
| ------------ | ---------------------------------- | ------------------------------ | ---------------------------- | ------------------------------------------------------------ |
| T1082        | System Information Discovery       | —                              | Post-supply chain            | System profiling to understand compromised environment       |
| T1083        | File and Directory Discovery       | —                              | Post-supply chain            | File system enumeration to identify high-value targets       |
| T1057        | Process Discovery                  | —                              | Post-supply chain            | Running process enumeration for lateral movement planning    |
| T1046        | Network Service Discovery          | —                              | Post-supply chain            | Internal network scanning from compromised vendor system     |
| T1018        | Remote System Discovery            | —                              | Post-supply chain lateral    | Discovery of other internal systems for lateral movement     |
| T1087        | Account Discovery                  | T1087.001 Local Account        | Post-supply chain            | Local account enumeration on compromised systems             |
| T1087        | Account Discovery                  | T1087.002 Domain Account       | Post-supply chain            | Domain account enumeration via LDAP or net commands          |
| T1069        | Permission Groups Discovery        | T1069.002 Domain Groups        | Post-supply chain            | AD group enumeration to identify high-privilege targets      |
| T1580        | Cloud Infrastructure Discovery     | —                              | Cloud supply chain           | Cloud resource enumeration after supply chain cloud access   |
| T1526        | Cloud Service Discovery            | —                              | Cloud supply chain           | Cloud service enumeration for lateral movement               |
| T1213        | Data from Information Repositories | T1213.003 Code Repositories    | CI/CD supply chain           | Source code repositories accessed after CI/CD compromise     |

### 5.8 Lateral Movement

| Technique ID | Technique Name                         | Sub-Technique                               | Attack Class                | Description                                                  |
| ------------ | -------------------------------------- | ------------------------------------------- | --------------------------- | ------------------------------------------------------------ |
| T1021        | Remote Services                        | T1021.001 Remote Desktop Protocol           | Post-supply chain Windows   | RDP used for lateral movement after supply chain entry       |
| T1021        | Remote Services                        | T1021.002 SMB/Windows Admin Shares          | Post-supply chain Windows   | SMB lateral movement using harvested credentials             |
| T1021        | Remote Services                        | T1021.004 SSH                               | Post-supply chain Linux     | SSH lateral movement with harvested keys or credentials      |
| T1021        | Remote Services                        | T1021.006 Windows Remote Management         | Post-supply chain Windows   | WinRM lateral movement                                       |
| T1550        | Use Alternate Authentication Material  | T1550.002 Pass the Hash                     | Post-supply chain Windows   | Pass-the-Hash lateral movement with dumped NTLM hashes       |
| T1550        | Use Alternate Authentication Material  | T1550.003 Pass the Ticket                   | Post-supply chain Kerberos  | Pass-the-Ticket lateral movement with stolen Kerberos tickets |
| T1210        | Exploitation of Remote Services        | —                                           | Post-supply chain           | Remote service exploitation for lateral movement             |
| T1534        | Internal Spearphishing                 | —                                           | Post-compromise             | Internal phishing from compromised accounts for further spread |
| T1563        | Remote Service Session Hijacking       | T1563.002 RDP Hijacking                     | Post-compromise             | Active RDP session hijacking                                 |

### 5.9 Collection

| Technique ID | Technique Name                     | Sub-Technique                     | Attack Class              | Description                                                  |
| ------------ | ---------------------------------- | --------------------------------- | ------------------------- | ------------------------------------------------------------ |
| T1005        | Data from Local System             | —                                 | Post-supply chain         | Files read from compromised local systems by backdoor        |
| T1039        | Data from Network Shared Drive     | —                                 | Post-supply chain lateral | Data collected from network shares after lateral movement    |
| T1025        | Data from Removable Media          | —                                 | Post-compromise           | Data collection from removable media on compromised systems  |
| T1530        | Data from Cloud Storage            | —                                 | Cloud supply chain        | Cloud storage data accessed after supply chain cloud access  |
| T1213        | Data from Information Repositories | T1213.001 Confluence              | Post-compromise           | Confluence knowledge base accessed for sensitive information |
| T1213        | Data from Information Repositories | T1213.003 Code Repositories       | CI/CD supply chain        | Source code and secrets accessed from code repositories      |
| T1119        | Automated Collection               | —                                 | Supply chain backdoor     | Automated data collection by backdoored vendor software      |
| T1074        | Data Staged                        | T1074.001 Local Data Staging      | Pre-exfiltration          | Collected data staged locally before exfiltration            |
| T1074        | Data Staged                        | T1074.002 Remote Data Staging     | Pre-exfiltration          | Collected data staged on remote system before exfiltration   |
| T1560        | Archive Collected Data             | T1560.001 Archive via Utility     | Pre-exfiltration          | Data compressed before exfiltration to reduce detection      |

### 5.10 Command and Control

| Technique ID | Technique Name              | Sub-Technique                          | Attack Class           | Description                                                  |
| ------------ | --------------------------- | -------------------------------------- | ---------------------- | ------------------------------------------------------------ |
| T1071        | Application Layer Protocol  | T1071.001 Web Protocols HTTPS          | Supply chain C2        | C2 communication over HTTPS to blend with legitimate traffic |
| T1071        | Application Layer Protocol  | T1071.004 DNS                          | Supply chain C2        | DNS-based C2 communication from compromised systems          |
| T1132        | Data Encoding               | T1132.001 Standard Encoding           | C2 obfuscation         | Base64 or other encoding of C2 communications                |
| T1573        | Encrypted Channel           | T1573.002 Asymmetric Cryptography      | Supply chain C2        | Encrypted C2 channel using asymmetric cryptography           |
| T1008        | Fallback Channels           | —                                      | Resilient C2           | Multiple C2 channels for resilience                          |
| T1105        | Ingress Tool Transfer       | —                                      | Post-supply chain      | Additional tools downloaded from C2 after initial access     |
| T1568        | Dynamic Resolution          | T1568.002 Domain Generation Algorithms | C2 resilience          | DGA used for C2 domain rotation to evade blocking            |
| T1090        | Proxy                       | T1090.004 Domain Fronting              | C2 evasion             | Domain fronting used to hide C2 communication destination    |
| T1219        | Remote Access Software      | —                                      | MSP supply chain       | Legitimate remote access tools (RMM) abused for C2          |

### 5.11 Exfiltration

| Technique ID | Technique Name                         | Sub-Technique                                    | Attack Class              | Description                                                  |
| ------------ | -------------------------------------- | ------------------------------------------------ | ------------------------- | ------------------------------------------------------------ |
| T1041        | Exfiltration Over C2 Channel           | —                                                | Supply chain backdoor     | Data exfiltrated through established C2 channel              |
| T1048        | Exfiltration Over Alternative Protocol | T1048.003 Exfil Over Unencrypted Protocol        | Post-supply chain         | Data exfiltrated via non-standard or unencrypted protocol    |
| T1567        | Exfiltration Over Web Service          | T1567.002 Exfiltration to Cloud Storage          | Cloud supply chain        | Data uploaded to attacker-controlled cloud storage           |
| T1020        | Automated Exfiltration                 | —                                                | Supply chain backdoor     | Automated bulk exfiltration by backdoored vendor software    |
| T1030        | Data Transfer Size Limits              | —                                                | Exfil evasion             | Data exfiltrated in small chunks to avoid detection          |
| T1029        | Scheduled Transfer                     | —                                                | Exfil evasion             | Data exfiltrated on schedule to blend with normal traffic    |

### 5.12 Impact

| Technique ID | Technique Name             | Sub-Technique                     | Attack Class                | Description                                                  |
| ------------ | -------------------------- | --------------------------------- | --------------------------- | ------------------------------------------------------------ |
| T1486        | Data Encrypted for Impact  | —                                 | Ransomware post-supply chain | Ransomware deployed across environment after supply chain access |
| T1485        | Data Destruction           | —                                 | Destructive supply chain    | Data destruction payload delivered via supply chain          |
| T1491        | Defacement                 | T1491.001 Internal Defacement     | Post-compromise impact      | Internal systems defaced after supply chain compromise       |
| T1499        | Endpoint Denial of Service | —                                 | Disruptive supply chain     | Service disruption via compromised vendor software           |
| T1565        | Data Manipulation          | T1565.001 Stored Data Manipulation | Integrity attack            | Data modified by backdoored software to corrupt integrity    |
| T1490        | Inhibit System Recovery    | —                                 | Post-ransomware supply chain | Recovery mechanisms disabled after supply chain ransomware  |

---

## 6. Attack Chain Mapping by Scenario

### 6.1 Software Update Supply Chain (SolarWinds-Style) Full Chain

| Stage              | Technique ID  | Technique Name                                    |
| ------------------ | ------------- | ------------------------------------------------- |
| Initial Access     | T1195.002     | Supply Chain Compromise: Software Supply Chain    |
| Execution          | T1059.001     | Command and Scripting: PowerShell                 |
| Persistence        | T1547.001     | Registry Run Keys / Startup Folder                |
| Defense Evasion    | T1553.002     | Code Signing using legitimate vendor cert         |
| Defense Evasion    | T1036.005     | Masquerading: Match Legitimate Name               |
| Credential Access  | T1003.001     | OS Credential Dumping: LSASS Memory               |
| Discovery          | T1082         | System Information Discovery                      |
| Discovery          | T1018         | Remote System Discovery                           |
| Lateral Movement   | T1021.002     | Remote Services: SMB/Windows Admin Shares         |
| Collection         | T1005         | Data from Local System                            |
| Collection         | T1074.001     | Data Staged: Local Data Staging                   |
| C2                 | T1071.001     | Application Layer Protocol: Web Protocols         |
| Exfiltration       | T1041         | Exfiltration Over C2 Channel                      |

### 6.2 Malicious npm/PyPI Package Attack Chain

| Stage              | Technique ID  | Technique Name                                    |
| ------------------ | ------------- | ------------------------------------------------- |
| Initial Access     | T1195.001     | Supply Chain Compromise: Software Dependencies    |
| Execution          | T1059.007     | Command and Scripting: JavaScript npm             |
| Execution          | T1059.006     | Command and Scripting: Python PyPI                |
| Credential Access  | T1552.001     | Unsecured Credentials: Credentials in Files       |
| Discovery          | T1083         | File and Directory Discovery                      |
| Collection         | T1119         | Automated Collection                              |
| C2                 | T1071.001     | Application Layer Protocol: Web Protocols         |
| Exfiltration       | T1041         | Exfiltration Over C2 Channel                      |

### 6.3 MSP/MSSP Compromise Attack Chain

| Stage              | Technique ID  | Technique Name                                    |
| ------------------ | ------------- | ------------------------------------------------- |
| Initial Access     | T1199         | Trusted Relationship via MSP access               |
| Initial Access     | T1078.002     | Valid Accounts: Domain Accounts MSP credentials   |
| Execution          | T1059.001     | Command and Scripting: PowerShell                 |
| Execution          | T1219         | Remote Access Software RMM tools                  |
| Persistence        | T1078.002     | Valid Accounts: Domain Accounts                   |
| Defense Evasion    | T1562.001     | Impair Defenses: Disable or Modify Tools          |
| Credential Access  | T1003.001     | OS Credential Dumping: LSASS                      |
| Lateral Movement   | T1021.001     | Remote Services: RDP                              |
| Collection         | T1039         | Data from Network Shared Drive                    |
| Exfiltration       | T1048         | Exfiltration Over Alternative Protocol            |
| Impact             | T1486         | Data Encrypted for Impact Ransomware              |

### 6.4 CI/CD Pipeline Compromise Attack Chain

| Stage              | Technique ID  | Technique Name                                    |
| ------------------ | ------------- | ------------------------------------------------- |
| Initial Access     | T1195.002     | Supply Chain Compromise: Software Supply Chain    |
| Execution          | T1072         | Software Deployment Tools CI/CD                   |
| Persistence        | T1053.005     | Scheduled Task automated build trigger            |
| Defense Evasion    | T1553.002     | Code Signing build artifacts signed               |
| Credential Access  | T1552.001     | Unsecured Credentials: Credentials in Files CI/CD secrets |
| Collection         | T1213.003     | Data from Code Repositories                       |
| Exfiltration       | T1041         | Exfiltration Over C2 Channel                      |

### 6.5 Open-Source Library Maintainer Compromise Chain

| Stage              | Technique ID  | Technique Name                                    |
| ------------------ | ------------- | ------------------------------------------------- |
| Initial Access     | T1195.001     | Supply Chain Compromise: Software Dependencies    |
| Initial Access     | T1566.002     | Phishing: Spearphishing Link to compromise maintainer |
| Execution          | T1059.006     | Command and Scripting: Python                     |
| Persistence        | T1546         | Event Triggered Execution import hook             |
| Defense Evasion    | T1027.002     | Software Packing obfuscated payload               |
| Credential Access  | T1552.004     | Unsecured Credentials: Private Keys               |
| Collection         | T1119         | Automated Collection                              |
| Exfiltration       | T1567.002     | Exfiltration to Cloud Storage                     |

---

## 7. Detection Coverage Map

| Technique ID  | Technique Name                           | Primary Detection Source              | Secondary Source               | Tool Stack        |
| ------------- | ---------------------------------------- | ------------------------------------- | ------------------------------ | ----------------- |
| T1195.001     | Supply Chain: Software Dependencies      | Package integrity scanning            | Build pipeline monitoring      | DevSecOps + SIEM  |
| T1195.002     | Supply Chain: Software Supply Chain      | Software update integrity check / FIM | Vendor advisory + TI           | FIM + TI + SIEM   |
| T1195.003     | Supply Chain: Hardware Supply Chain      | Physical inspection                   | Firmware integrity scanning    | Manual + FIM      |
| T1199         | Trusted Relationship                     | Anomalous MSP activity alerts         | VPN/access log monitoring      | SIEM + EDR        |
| T1059         | Command and Scripting Interpreter        | EDR process tree analysis             | SIEM command line logging      | EDR + SIEM        |
| T1072         | Software Deployment Tools               | CI/CD pipeline audit logs             | Build artifact hash monitoring | CI/CD + SIEM      |
| T1553.002     | Code Signing subverted                   | Certificate anomaly detection         | Binary signing validation      | EDR + PKI         |
| T1003.001     | OS Credential Dumping LSASS             | EDR LSASS access monitoring           | Windows Event 4656             | EDR + SIEM        |
| T1021.001     | Remote Services RDP                      | Windows Event 4624 type 10           | Network flow monitoring        | SIEM + Firewall   |
| T1021.002     | Remote Services SMB                      | Windows Event 4624 type 3 + NTLM     | Network flow monitoring        | SIEM + EDR        |
| T1550.002     | Pass the Hash                            | NTLM auth without Kerberos            | Event 4624 type 3 patterns     | SIEM              |
| T1119         | Automated Collection                     | EDR file access volume anomaly        | DLP alerts                     | EDR + DLP         |
| T1041         | Exfiltration Over C2 Channel             | Proxy/firewall outbound anomaly       | NetFlow volume analysis        | Proxy + Firewall  |
| T1567.002     | Exfiltration to Cloud Storage            | Proxy cloud storage uploads           | DLP + cloud audit              | Proxy + Cloud     |
| T1486         | Data Encrypted for Impact                | EDR ransomware behavior detection     | Volume shadow copy deletion    | EDR + SIEM        |
| T1562.001     | Impair Defenses: Disable Tools           | EDR agent status monitoring           | Security tool heartbeat        | EDR + SIEM        |
| T1580         | Cloud Infrastructure Discovery           | Cloud audit anomaly detection         | IAM unusual API calls          | Cloud + SIEM      |
| T1098.001     | Additional Cloud Credentials             | Cloud audit new key creation          | IAM anomaly detection          | Cloud + SIEM      |

---

## 8. Hunting Queries Reference (By Technique)

### 8.1 T1195 – Supply Chain Compromise Detection (Software Update)

Objective: Detect when vendor software makes unexpected network connections after update.

Logic:
- source: EDR OR firewall
- event_type: network_connection
- process_name: vendor_software_process
- destination_ip: NOT IN known_vendor_infrastructure
- destination_port: 443 OR 80 OR 53
- timeframe: within 24 hours of software update event

Pivot on:
- New network destinations not seen before the software update
- Connections to IP ranges not in vendor published infrastructure list

### 8.2 T1059 – Unexpected Process Execution from Vendor Software

Objective: Detect command interpreters spawned by vendor software processes.

Logic:
- source: EDR
- event_type: process_create
- parent_process_name: vendor_software_executable
- child_process_name: powershell.exe OR cmd.exe OR bash OR sh OR python OR wscript OR cscript
- timeframe: since affected version installation date

Pivot on:
- Command line arguments of child processes
- Network connections made by child processes
- Files written by child processes

### 8.3 T1199 – MSP/Trusted Relationship Abuse Detection

Objective: Detect anomalous activity from known MSP/vendor accounts or IP ranges.

Logic:
- source: SIEM
- event_type: authentication OR remote_access
- source_ip: IN known_msp_ip_ranges
- user_account: IN known_msp_service_accounts
- action: NOT IN baseline_msp_activity_patterns
- destination: IN sensitive_system_list
- timeframe: last 90 days

Pivot on:
- MSP accounts accessing systems outside normal scope
- MSP accounts active at unusual times
- MSP accounts performing privilege escalation

### 8.4 T1553.002 – Code Signing Anomaly Detection

Objective: Detect software signed with unexpected or newly introduced certificates.

Logic:
- source: EDR OR FIM
- event_type: file_create OR process_create
- signature_status: signed
- signing_certificate: NOT IN known_trusted_certificate_baseline
- file_path: IN vendor_software_directories
- timeframe: since vendor software update

Pivot on:
- New certificates introduced after software update
- Certificates from unusual certificate authorities

### 8.5 T1003.001 – LSASS Credential Dumping Post-Supply Chain

Objective: Detect LSASS access by vendor software or its child processes.

Logic:
- source: EDR
- event_type: process_access
- target_process: lsass.exe
- source_process: vendor_software_process OR child_of_vendor_process
- access_rights: PROCESS_VM_READ OR PROCESS_ALL_ACCESS
- timeframe: since affected version installation

### 8.6 T1119 – Automated Collection by Backdoored Software

Objective: Detect unusual file access patterns by vendor software processes.

Logic:
- source: EDR
- event_type: file_read
- process_name: vendor_software_process
- file_path: NOT IN vendor_normal_access_paths
- volume: greater than baseline_file_read_count_per_hour
- timeframe: since affected version installation

Pivot on:
- Sensitive directories being read including credential stores, config files, user documents
- File access patterns inconsistent with vendor software purpose

### 8.7 T1041 and T1567 – Exfiltration Detection from Vendor Software

Objective: Detect data exfiltration from compromised vendor software processes.

Logic:
- source: proxy OR firewall
- event_type: network_connection
- process_name: vendor_software_process OR child_of_vendor_process
- bytes_out: greater than baseline_threshold_per_session
- destination: NOT IN known_vendor_infrastructure
- timeframe: since affected version installation

### 8.8 T1195.001 – Malicious Package in CI/CD Pipeline

Objective: Detect malicious package installation during build process.

Logic:
- source: CI/CD pipeline logs OR build server network logs
- event_type: package_install OR network_connection
- package_name: IN malicious_package_watchlist OR destination_domain NOT IN approved_package_repository_list
- timeframe: last 90 days of build history

---

## 9. MITRE ATT&CK Navigator Layer Reference

The following technique IDs should be highlighted in an ATT&CK Navigator layer for supply chain incidents:

| Tactic               | Technique IDs to Highlight                                                        |
| -------------------- | --------------------------------------------------------------------------------- |
| Initial Access       | T1195.001, T1195.002, T1195.003, T1199, T1078.002                                 |
| Execution            | T1059.001, T1059.003, T1059.004, T1059.006, T1059.007, T1072, T1569.002           |
| Persistence          | T1547.001, T1543.003, T1053.005, T1053.003, T1505.003, T1078, T1136, T1098.001    |
| Privilege Escalation | T1068, T1548.002, T1134.001, T1484.001, T1098.003                                 |
| Defense Evasion      | T1036.005, T1027.002, T1027.010, T1553.002, T1070.001, T1562.001, T1564.001       |
| Credential Access    | T1003.001, T1003.003, T1552.001, T1552.004, T1528, T1539, T1555.003               |
| Discovery            | T1082, T1083, T1057, T1046, T1018, T1087, T1069.002, T1580, T1213.003             |
| Lateral Movement     | T1021.001, T1021.002, T1021.004, T1550.002, T1550.003, T1210                      |
| Collection           | T1005, T1039, T1530, T1213, T1119, T1074.001, T1074.002, T1560.001                |
| C2                   | T1071.001, T1071.004, T1573.002, T1568.002, T1090.004, T1219                      |
| Exfiltration         | T1041, T1048, T1567.002, T1020, T1030, T1029                                      |
| Impact               | T1486, T1485, T1491.001, T1565.001, T1490                                         |

---

## 10. Analyst Quick Lookup Table

Use this table for fast technique identification during active supply chain investigations:

| If You Observe This…                                       | MITRE Technique    | Priority Action                                          |
| ---------------------------------------------------------- | ------------------ | -------------------------------------------------------- |
| Vendor software making connections to unknown destinations  | T1195.002 + T1071  | Block C2 at firewall; escalate to IR Team immediately    |
| Vendor software spawning cmd/powershell/bash               | T1059              | Isolate system; escalate to L3 immediately               |
| New files created in vendor software directories           | T1195.002          | Hash and analyze; escalate to L3                         |
| Vendor software reading LSASS memory                       | T1003.001          | Isolate system; escalate to IR Team; rotate credentials  |
| MSP account accessing unusual systems                      | T1199              | Revoke MSP access; escalate to SOC Lead                  |
| New scheduled task created by vendor process               | T1053.005          | Document; remove; escalate to L3                         |
| Package hash mismatch in build artifact                    | T1195.001          | Halt deployments; escalate to IR Team; analyze artifact  |
| New cloud IAM key created during dwell period              | T1098.001          | Revoke key immediately; audit all actions taken          |
| NTLM authentication without Kerberos from affected system  | T1550.002          | Investigate lateral movement; escalate                   |
| Large outbound transfer from vendor software process       | T1041 + T1567      | Block egress; escalate to L3; activate breach playbook   |
| CI/CD pipeline making unexpected external network calls    | T1072              | Halt pipeline; escalate to IR Team; analyze build logs   |
| New domain admin account created during dwell period       | T1136.002          | Disable account; escalate to IR Team immediately         |
| Vendor software accessing credential files                 | T1552.001          | Rotate all credentials; isolate system; escalate         |
| CloudTrail logging disabled during dwell period            | T1562.001          | Re-enable logging; escalate; review all actions          |
| DNS queries with high subdomain entropy from affected host  | T1071.004          | DNS sinkhole; block; escalate for DGA analysis           |

---

## 11. Supply Chain-Specific Detection Gaps and Recommendations

Supply chain attacks exploit trust relationships that make many standard detections ineffective. The following gaps are commonly observed:

| Detection Gap                                               | Why It Exists                                              | Recommended Improvement                                      |
| ----------------------------------------------------------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| Signed malicious code bypasses hash-based detection         | Standard AV relies on known-bad hashes; signed code trusted | Implement behavioral detection independent of signature status |
| Vendor software network connections not baselined           | Vendor software often has legitimate network activity      | Establish and monitor baseline for all vendor software network behavior |
| No software bill of materials SBOM                          | Many organizations do not track software dependencies      | Implement SBOM generation for all production applications    |
| Package integrity not verified at install                   | Build tools pull packages without hash verification        | Implement package signing verification in all CI/CD pipelines |
| MSP activity not adequately monitored                       | MSP access treated as inherently trusted                   | Apply same monitoring to MSP accounts as internal privileged accounts |
| Long log retention gaps                                     | Standard retention may not cover supply chain dwell time   | Extend log retention to minimum 12 months for critical systems |
| No build artifact integrity verification                    | Build artifacts not compared against independently built reference | Implement reproducible builds and artifact hash verification |
| Cloud audit logs not monitored for IAM changes              | Cloud audit is configured but alerts not tuned             | Implement real-time alerting for all IAM changes             |

---

## 12. Post-Incident MITRE Mapping Update Requirements

After every P1/P2 supply chain incident, the L3 analyst or IR Team must complete the following:

| Action                                                       | Owner          | Target                            |
| ------------------------------------------------------------ | -------------- | --------------------------------- |
| Review observed techniques against this mapping              | L3 / IR Lead   | Within 5 days of incident close   |
| Add newly observed techniques not covered in this document   | L3 / IR Lead   | Update this document              |
| Update hunting queries with patterns observed in incident     | L3 / Detection | Detection-Improvement-Log.md      |
| Update ATT&CK Navigator layer with confirmed techniques       | L3 / Detection | Internal TI platform              |
| Add new IOCs to IoC output register                          | L3 / TI Team   | IoC-Output-Register.md            |
| Share TTP intelligence with TI team for threat actor profiling | L3 / TI      | TTP-Intelligence-Report.md        |

Reference: 08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md
Reference: 08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md

---

## 13. Regulatory and Compliance Context

This MITRE mapping supports compliance with the following frameworks:

| Framework      | Requirement                                                  | How This Mapping Helps                                       |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| NIST CSF 2.0   | GV.SC Cybersecurity Supply Chain Risk Management             | TTP-based identification of supply chain attack patterns     |
| NIST CSF 2.0   | DE.AE, RS.AN, RS.MI                                          | Structured detection, analysis, and response framework       |
| ISO 27001:2022 | A.5.19 Information security in supplier relationships        | Technique mapping supports vendor risk assessment            |
| ISO 27001:2022 | A.5.24 through A.5.28 Incident management                   | Structured incident classification and IOC output            |
| RBI CSF        | Threat intelligence and incident response capability         | Technique-based hunting and TI enrichment for BFSI sector    |
| NIST SP 800-161 | Supply Chain Risk Management for Federal Information Systems | Comprehensive TTP coverage for supply chain threats         |

---

## 14. Related Documents

| Document                         | Path                                                                   |
| -------------------------------- | ---------------------------------------------------------------------- |
| Supply Chain Master              | 02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Master.md         |
| Supply Chain L1 Triage           | 02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L1-Triage.md      |
| Supply Chain L2 Investigation    | 02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L2-Investigation.md |
| Supply Chain L3 Forensics        | 02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L3-Forensics.md   |
| Supply Chain Vendor Coordination | 02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Vendor-Coordination.md |
| APT Campaign Playbooks           | 02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md                       |
| Network Intrusion Playbooks      | 02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Master.md     |
| MITRE ATT&CK Quick Reference     | 10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md |
| TTP Intelligence Report          | 08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md   |
| IoC Output Register              | 08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md       |
| Detection Improvement Log        | 08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md |
| TI IoC Handling SOP              | 04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md |

---

## 15. Revision History

| Version | Date        | Author                 | Changes         |
| ------- | ----------- | ---------------------- | --------------- |
| 1.0     | 19-May-2026 | L3 Lead / IR Team Lead | Initial version |

---

## 16. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**