# Playbook: Network Intrusion – MITRE ATT&CK Mapping

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Network Intrusion (MITRE ATT&CK Mapping)          |
| Document ID    | IR-PB-NI-MITRE-006                                           |
| Version        | 1.0                                                          |
| Effective Date | 21-May-2026                                                  |
| Owner          | L3 Lead / Threat Detection Lead                              |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 network intrusion incident     |

---

## 2. Purpose

This document provides the MITRE ATT&CK Enterprise framework mapping for network intrusion incidents handled under the Network Intrusion playbook set.

Network intrusion incidents frequently involve multi-stage attacker behavior including exploitation, credential abuse, lateral movement, covert command-and-control (C2), and data exfiltration. Mapping observed activity to MITRE ATT&CK techniques enables the organization to:

- Standardize documentation of attacker tradecraft
- Improve detection engineering for network-based threats
- Guide structured threat hunting across network telemetry
- Support L2/L3 scoping and hypothesis-driven investigation
- Identify control and monitoring gaps in firewall, IDS, DNS, proxy, and endpoint logging
- Provide audit-ready documentation aligned to ISO 27001, NIST CSF, RBI CSF
- Support purple team simulations and adversary emulation
- Improve executive reporting clarity by translating technical findings into recognized ATT&CK tactics

This mapping must be reviewed and updated after every major (P1/P2) network intrusion incident.

---

## 3. Scope

Applies to network intrusion categories handled under:

- PB-NetworkIntrusion-Master.md
- PB-NetworkIntrusion-L1-Triage.md
- PB-NetworkIntrusion-L2-Investigation.md
- PB-NetworkIntrusion-L3-Forensics.md
- PB-NetworkIntrusion-Containment.md

Attack classes covered:

- External perimeter compromise
- Exploit-based entry
- VPN compromise
- Credential-based intrusion
- Lateral movement within internal network
- Pass-the-Hash / Pass-the-Ticket attacks
- Internal reconnaissance
- DNS/HTTP/HTTPS tunneling
- Command and control traffic
- Data staging and exfiltration
- Domain controller compromise
- Network-assisted ransomware propagation
- Hybrid cloud/on-prem intrusion

---

## 4. MITRE ATT&CK Framework Reference

| Field              | Value                                    |
| ------------------ | ---------------------------------------- |
| Framework          | MITRE ATT&CK Enterprise                  |
| Version Referenced | v14 (verify at attack.mitre.org)         |
| Scope              | Enterprise network, endpoint, identity   |
| Supplementary      | ATT&CK for Containers if applicable      |

---

## 5. Network Intrusion – Full TTP Matrix

---

### 5.1 Reconnaissance

Reconnaissance activity may occur before and after initial compromise. External scanning is typically followed by internal discovery once access is gained.

| Technique ID | Technique Name                     | Description |
|--------------|-----------------------------------|-------------|
| T1595        | Active Scanning                   | External scanning of IP ranges, ports, and exposed services |
| T1046        | Network Service Discovery         | Internal port scanning to identify accessible services |
| T1018        | Remote System Discovery           | Identifying reachable hosts within internal network |
| T1082        | System Information Discovery      | OS, hostname, and system profiling |
| T1069.002    | Permission Groups Discovery       | Enumerating domain groups for privilege targets |
| T1589        | Gather Victim Identity Information| Collecting usernames and email structures |
| T1596        | Search Open Technical Databases   | Identifying exposed services via Shodan/Censys |
| T1613        | Container and Resource Discovery  | Discovering internal containerized workloads |

Network telemetry often reveals reconnaissance through abnormal connection attempts, rapid port sweeps, or large-scale authentication failures.

---

### 5.2 Initial Access

Network intrusions commonly begin via exploitation of exposed services or misuse of valid credentials.

| Technique ID | Technique Name                           | Description |
|--------------|-------------------------------------------|-------------|
| T1190        | Exploit Public-Facing Application         | Exploiting web servers, VPN gateways, or exposed services |
| T1133        | External Remote Services                  | Abuse of VPN, RDP, SSH for initial access |
| T1078        | Valid Accounts                            | Stolen credentials used for access |
| T1078.002    | Valid Accounts: Domain Accounts           | Domain account compromise |
| T1566        | Phishing                                  | Credential harvesting or malware delivery |
| T1199        | Trusted Relationship                      | Third-party/vendor network access abuse |
| T1552        | Unsecured Credentials                     | Credentials discovered in config files |

Indicators include anomalous VPN logins, unusual RDP source IPs, and IDS exploit alerts.

---

### 5.3 Execution

After access, attackers execute commands to establish control.

| Technique ID | Technique Name                            | Description |
|--------------|--------------------------------------------|-------------|
| T1059.001    | PowerShell                                 | Remote PowerShell command execution |
| T1059.003    | Windows Command Shell                      | CMD-based execution |
| T1059.004    | Unix Shell                                 | Bash execution on Linux hosts |
| T1021        | Remote Services                            | Execution over RDP, SMB, SSH |
| T1569.002    | Service Execution                          | Creating malicious services |
| T1105        | Ingress Tool Transfer                      | Downloading attacker toolkits |

Execution frequently leaves traces in process creation logs (Event ID 4688) and EDR telemetry.

---

### 5.4 Persistence

Persistence ensures attacker access survives reboots or remediation attempts.

| Technique ID | Technique Name                          | Description |
|--------------|------------------------------------------|-------------|
| T1053.005    | Scheduled Task                           | Creating scheduled tasks for persistence |
| T1547.001    | Registry Run Keys                        | Startup registry modifications |
| T1543.003    | Windows Service                          | Installing malicious service |
| T1078        | Valid Accounts                           | Maintaining access via legitimate credentials |
| T1136        | Create Account                           | Creating new domain or local accounts |
| T1546        | Event Triggered Execution                | WMI or event-based persistence |

Persistence detection relies heavily on log review and baseline comparison.

---

### 5.5 Privilege Escalation

Privilege escalation allows attacker movement toward high-value systems.

| Technique ID | Technique Name                             | Description |
|--------------|---------------------------------------------|-------------|
| T1068        | Exploitation for Privilege Escalation       | Local privilege exploit |
| T1548.002    | Bypass UAC                                  | User Account Control bypass |
| T1134        | Access Token Manipulation                   | Token impersonation |
| T1484.001    | Domain Policy Modification                  | GPO abuse |
| T1098        | Account Manipulation                        | Assigning elevated privileges |

Privilege escalation often precedes domain controller access.

---

### 5.6 Defense Evasion

Network attackers attempt to conceal their activity.

| Technique ID | Technique Name                              | Description |
|--------------|----------------------------------------------|-------------|
| T1562.001    | Disable or Modify Tools                      | Disabling security controls |
| T1562.008    | Disable Logging                              | Tampering with logs |
| T1027        | Obfuscated Files or Information              | Encoded PowerShell scripts |
| T1036        | Masquerading                                 | Renaming malicious files |
| T1070.001    | Clear Windows Event Logs                     | Log clearing |
| T1070.003    | Clear Command History                        | Removing shell history |

Defense evasion often correlates with unexpected service restarts or logging gaps.

---

### 5.7 Credential Access

Credential harvesting enables lateral movement.

| Technique ID | Technique Name                           | Description |
|--------------|-------------------------------------------|-------------|
| T1003.001    | LSASS Memory Dumping                     | Dumping LSASS for credentials |
| T1555        | Credentials from Password Stores         | Extracting browser credentials |
| T1552        | Unsecured Credentials                    | Harvesting from config files |
| T1550.002    | Pass-the-Hash                            | NTLM replay |
| T1550.003    | Pass-the-Ticket                          | Kerberos replay |

Credential theft is often identified via abnormal authentication patterns.

---

### 5.8 Lateral Movement

Lateral movement spreads attacker control.

| Technique ID | Technique Name                              | Description |
|--------------|----------------------------------------------|-------------|
| T1021.001    | Remote Desktop Protocol                      | RDP movement |
| T1021.002    | SMB / Admin Shares                           | File share exploitation |
| T1021.004    | SSH                                          | Linux pivoting |
| T1550.002    | Pass-the-Hash                                | Credential replay |
| T1550.003    | Pass-the-Ticket                              | Kerberos replay |
| T1210        | Exploitation of Remote Services              | Internal exploit |

Network logs often reveal lateral movement through abnormal internal traffic.

---

### 5.9 Collection

Collection precedes exfiltration.

| Technique ID | Technique Name                          | Description |
|--------------|------------------------------------------|-------------|
| T1005        | Data from Local System                   | Accessing local files |
| T1039        | Data from Network Shared Drive           | Accessing shared drives |
| T1119        | Automated Collection                     | Script-based harvesting |
| T1074        | Data Staging                             | Preparing data for transfer |
| T1560        | Archive Collected Data                   | Compressing data |

---

### 5.10 Command and Control

C2 communication maintains attacker control.

| Technique ID | Technique Name                             | Description |
|--------------|---------------------------------------------|-------------|
| T1071.001    | Web Protocols (HTTPS)                      | Encrypted C2 |
| T1071.004    | DNS                                        | DNS tunneling |
| T1573.002    | Encrypted Channel                          | TLS-based C2 |
| T1090        | Proxy                                      | Proxy or domain fronting |
| T1102        | Web Service                                | Cloud-based C2 relay |

---

### 5.11 Exfiltration

| Technique ID | Technique Name                               | Description |
|--------------|-----------------------------------------------|-------------|
| T1041        | Exfiltration Over C2 Channel                  | C2 exfiltration |
| T1048        | Exfiltration Over Alternative Protocol        | FTP/SMTP exfiltration |
| T1020        | Automated Exfiltration                        | Script-based exfiltration |
| T1030        | Data Transfer Size Limits                     | Chunked exfil |
| T1029        | Scheduled Transfer                            | Timed data transfer |

---

### 5.12 Impact

| Technique ID | Technique Name                          | Description |
|--------------|------------------------------------------|-------------|
| T1486        | Data Encrypted for Impact                | Ransomware deployment |
| T1485        | Data Destruction                         | Deleting critical data |
| T1496        | Resource Hijacking                       | Cryptomining |
| T1499        | Endpoint Denial of Service               | Service disruption |
| T1490        | Inhibit System Recovery                  | Backup deletion |

---

## 6. Detection Coverage Map (Expanded)

| Technique ID | Primary Detection Source | Secondary Source | Tool Stack |
|--------------|-------------------------|------------------|-----------|
| T1190 | IDS/IPS | Firewall logs | IDS + SIEM |
| T1078 | Authentication logs | VPN logs | SIEM |
| T1059 | EDR process telemetry | Windows logs | EDR + SIEM |
| T1003 | EDR LSASS detection | Event ID 4656 | EDR |
| T1021 | Windows Event 4624 | NetFlow | SIEM |
| T1071 | Proxy logs | DNS logs | Proxy + SIEM |
| T1562 | EDR agent heartbeat | Syslog | EDR |
| T1041 | Firewall egress logs | DLP | Firewall + DLP |
| T1496 | Monitoring alerts | CPU telemetry | EDR + Monitoring |

---

## 7. Hunting Examples

### Beaconing Detection (T1071)

- Identify outbound HTTPS sessions
- Same destination IP
- Fixed interval pattern
- Similar packet sizes

### Pass-the-Hash Detection (T1550.002)

- NTLM authentication without Kerberos
- Same source host authenticating to multiple hosts
- Event ID 4624 type 3 anomalies

### Internal Recon Detection (T1046)

- High number of connection attempts from one internal host
- Sequential port scanning behavior
- NetFlow abnormal spike

---

## 8. Detection Gaps and Recommendations

| Gap | Recommendation |
|-----|---------------|
| No DNS logging | Enable DNS logging enterprise-wide |
| Short log retention | Extend to minimum 12 months |
| No east-west traffic visibility | Deploy NDR |
| VPN logs not centralized | Integrate with SIEM |
| No EDR on servers | Deploy EDR across critical servers |

---

## 9. Post-Incident Update Requirements

After P1/P2 incident:

- Update MITRE mapping with confirmed techniques
- Add new hunting queries
- Update detection improvement log
- Share TTP profile with Threat Intelligence team

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/`

---

## 10. Regulatory Context

Supports:

- NIST CSF (DE.AE, RS.AN, RS.MI)
- ISO 27001 Incident Management Controls
- RBI CSF Threat Detection Requirements
- NIST SP 800-61

---

## 11. Related Documents

| Document | Path |
|----------|------|
| Network Intrusion Master | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Master.md` |
| Network Intrusion L2 | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L2-Investigation.md` |
| Network Intrusion L3 | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L3-Forensics.md` |
| Network Intrusion Containment | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Containment.md` |
| MITRE ATT&CK Quick Reference | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/` |

---

## 12. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 21-May-2026 | L3 Lead / Threat Detection Lead | Initial version |

---

## 13. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**