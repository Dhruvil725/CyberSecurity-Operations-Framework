# Playbook: Ransomware – MITRE ATT&CK Mapping

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Ransomware (MITRE ATT&CK Mapping) |
| Document ID | IR-PB-RAN-008 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | L3 Lead / Threat Intelligence Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after major ransomware incidents |

---

## 2. Purpose

This document maps common ransomware operations to MITRE ATT&CK tactics and
techniques to support:

- consistent incident documentation
- investigation structure (attack chain reconstruction)
- detection engineering improvements
- threat hunting development
- reporting alignment for audits and executive communication

This mapping is intended to be used with:
- L2 and L3 investigation outputs
- threat intel enrichment
- SOC detection rule tuning and coverage assessments

---

## 3. Scope

Applies to:
- ransomware execution incidents
- ransomware precursor incidents (pre-encryption)
- ransomware operations including double extortion

Includes:
- technique mapping across tactics
- evidence examples (what to look for)
- logging sources commonly used to confirm technique usage
- suggested detection and hunting focus areas

---

## 4. How to Use This Mapping

During investigation:
1. Identify observed behaviors and artifacts.
2. Map each behavior to tactic and technique.
3. Record technique IDs and evidence references in the incident ticket.
4. Use identified technique set to:
   - expand scoping (find additional hosts/identities)
   - prioritize containment actions
   - guide eradication and recovery safeguards
   - propose detection improvements and hunts

Documentation standard:
- include technique ID and name
- include evidence reference (log export, EDR event, query, file artifact)
- include confidence level (Confirmed / Likely / Possible)

---

## 5. Ransomware Attack Chain Mapping (High-Level)

Ransomware operations typically follow this progression:

1. Initial Access
2. Execution and Foothold
3. Persistence
4. Privilege Escalation
5. Defense Evasion
6. Credential Access
7. Discovery
8. Lateral Movement
9. Collection and Staging
10. Exfiltration (double extortion)
11. Impact (encryption and disruption)

Not all incidents include all stages; confirm based on evidence.

---

## 6. MITRE ATT&CK Mapping Table (Detailed)

| Tactic | Technique ID | Technique Name | Common Ransomware Evidence Examples | Primary Log / Data Sources |
|:-------|--------------|----------------|-------------------------------------|----------------------------|
| Initial Access | T1566 | Phishing | user opened attachment; link click; payload executed | email gateway logs, endpoint logs, proxy logs |
| Initial Access | T1190 | Exploit Public-Facing Application | exploit traffic to vulnerable endpoint; web shell drop | WAF logs, web logs, EDR server telemetry |
| Initial Access | T1133 | External Remote Services | VPN compromise; RDP access; remote admin portal use | VPN logs, firewall logs, RDP logs |
| Initial Access | T1078 | Valid Accounts | successful login from unusual source; reused credentials | AD logs, IAM logs, cloud sign-in logs |
| Execution | T1059 | Command and Scripting Interpreter | PowerShell/cmd execution; encoded scripts; batch runs | EDR process trees, Windows event 4688 |
| Execution | T1204 | User Execution | user executes downloaded file; macro execution | EDR telemetry, office logs |
| Execution | T1106 | Native API | suspicious execution patterns; in-memory loaders | EDR telemetry, memory analysis |
| Persistence | T1053 | Scheduled Task/Job | new scheduled task created/modified | Windows event 4698/4702, EDR persistence view |
| Persistence | T1547 | Boot or Logon Autostart Execution | run keys, startup folder, services | registry logs, EDR, autoruns |
| Persistence | T1543 | Create or Modify System Process | new service installed; service binary suspicious | Windows event 7045, EDR service creation |
| Privilege Escalation | T1068 | Exploitation for Priv Esc | local privilege escalation exploit | EDR telemetry, exploit artifacts |
| Privilege Escalation | T1078.003 | Valid Accounts: Local Accounts | local admin used to pivot | EDR, Windows event logs |
| Defense Evasion | T1562 | Impair Defenses | EDR disabled, services stopped, exclusions added | EDR console logs, Windows events |
| Defense Evasion | T1070 | Indicator Removal on Host | log clearing; deletion of artifacts | Windows event 1102, 104; EDR events |
| Defense Evasion | T1027 | Obfuscated Files or Information | base64 encoded commands; packed binaries | EDR process command lines, file analysis |
| Defense Evasion | T1036 | Masquerading | payload named like system file; placed in system paths | file system, EDR telemetry |
| Credential Access | T1003 | OS Credential Dumping | LSASS access; dump tools; suspicious handle opens | EDR alerts, Windows security logs, memory analysis |
| Credential Access | T1110 | Brute Force | repeated failed logins followed by success | AD logs 4625/4624, VPN logs |
| Credential Access | T1555 | Credentials from Password Stores | browser credential theft | EDR, browser logs, file artifacts |
| Credential Access | T1558.003 | Kerberoasting | high volume service ticket requests | DC logs, SIEM correlation |
| Discovery | T1082 | System Information Discovery | host enumeration commands | EDR command lines, Windows events |
| Discovery | T1018 | Remote System Discovery | scanning for hosts; net view; arp scans | EDR, network logs |
| Discovery | T1135 | Network Share Discovery | enumeration of shares; net use | EDR, Windows logs, file server logs |
| Discovery | T1046 | Network Service Scanning | internal scanning patterns | IDS/IPS, NetFlow |
| Lateral Movement | T1021 | Remote Services | RDP/WMI/WinRM use | Windows logs, EDR telemetry |
| Lateral Movement | T1021.002 | SMB/Windows Admin Shares | use of admin shares C$/ADMIN$ | Windows logs, EDR, file server logs |
| Lateral Movement | T1570 | Lateral Tool Transfer | payload copied to other hosts | EDR file transfer telemetry, SMB logs |
| Collection | T1005 | Data from Local System | access to sensitive files, repositories | EDR, file server logs |
| Collection | T1213 | Data from Information Repositories | DB exports, share access | DB logs, file share logs |
| Collection | T1560 | Archive Collected Data | zip/rar/7z creation | EDR telemetry, file system artifacts |
| Exfiltration | T1041 | Exfiltration Over C2 Channel | data transfer over same C2 channel | proxy/firewall logs, EDR net connections |
| Exfiltration | T1567 | Exfiltration Over Web Service | uploads to cloud storage | proxy logs, cloud audit logs |
| Exfiltration | T1048 | Exfiltration Over Alternative Protocol | SFTP/FTP exfiltration | firewall logs, server logs |
| Impact | T1486 | Data Encrypted for Impact | mass encryption; ransom note; extension changes | EDR, file server logs |
| Impact | T1490 | Inhibit System Recovery | vssadmin delete shadows; bcdedit changes | Windows logs, EDR command line telemetry |
| Impact | T1489 | Service Stop | stopping services to unlock files | Windows logs, service logs |
| Impact | T1485 | Data Destruction | deletion of backups or data | backup logs, file server logs |

---

## 7. Technique Confirmation Guidance (Confidence Levels)

When documenting technique usage, use:

| Level | Meaning | Documentation Requirement |
|------|---------|---------------------------|
| Confirmed | Direct evidence in logs/artifacts | include evidence reference ID and timestamp |
| Likely | Strong indicators but missing direct log | include reasoning and supporting signals |
| Possible | Weak indicators; needs confirmation | assign follow-up investigation action |

---

## 8. Recommended Detection and Hunting Focus Areas

Based on ransomware operations, prioritize coverage for:

1. Credential dumping indicators (LSASS access)
2. Remote execution tools and lateral movement (PsExec, WMI, SMB)
3. Backup destruction and shadow copy deletion commands
4. Abnormal privileged account activity (group changes, admin logons)
5. Data staging and archive creation in unusual paths
6. Unusual outbound traffic from servers (C2 or exfil)
7. New services/scheduled tasks created at scale

Output expectation:
- detection gaps should be logged as improvements under:
  `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

## 9. Mapping Outputs for Incident Report (Standard)

The final incident report should include:
- observed tactics and techniques
- confirmed vs likely techniques
- evidence references
- mapping narrative (how attacker progressed)
- recommended controls mapped to techniques

Reference:
`07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`

---

## 10. Related Documents

| Document | Path |
|---------|------|
| Ransomware Master | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Master.md` |
| L2 Investigation | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L2-Investigation.md` |
| L3 Forensics | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L3-Forensics.md` |
| Containment | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md` |
| Eradication | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Eradication.md` |
| Threat Intel Output | `08_POST-INCIDENT/08.4_Threat-Intel-Output/` |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |
| MITRE Quick Reference | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATTCK-Quick-Reference.md` |

---

## 11. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | L3 Lead / Threat Intel Lead | Initial version |

---

## 12. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document