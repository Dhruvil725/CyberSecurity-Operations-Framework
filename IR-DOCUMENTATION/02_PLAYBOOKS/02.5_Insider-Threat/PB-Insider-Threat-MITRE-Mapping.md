# Playbook: Insider Threat – MITRE ATT&CK Mapping

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Insider Threat (MITRE ATT&CK Mapping) |
| Document ID | IR-PB-INS-007 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | Threat Intelligence Lead / L3 Lead |
| Approved By | IR Team Lead |
| Classification | Strictly Confidential |
| Review Cycle | Quarterly and after major insider threat incidents |

---

## 2. Purpose

This document maps insider threat activity to the MITRE ATT&CK framework.

The objectives are to:
- standardize insider threat investigations
- align insider activity with ATT&CK tactics and techniques
- improve detection engineering
- improve UEBA and DLP monitoring
- support threat hunting
- improve executive and technical reporting
- support legal and HR evidence analysis

Unlike external attacks, insider threat ATT&CK mapping often focuses on:
- legitimate account abuse
- authorized access misuse
- data collection and exfiltration
- privilege misuse
- defense evasion by trusted users

---

## 3. Scope

Applies to:
- malicious insider activity
- privileged misuse
- data theft
- sabotage
- cloud sharing abuse
- unauthorized data transfers
- insider-assisted compromise
- employee misuse of legitimate tools

Includes:
- endpoint activity
- cloud and SaaS abuse
- email and collaboration misuse
- privilege abuse
- removable media usage
- data staging and exfiltration

---

## 4. How to Use This Mapping

During insider threat investigations:
1. Identify observed user actions and artifacts.
2. Map activity to ATT&CK techniques.
3. Record:
   - ATT&CK Technique ID
   - Technique Name
   - Evidence Source
   - Confidence Level
4. Use mappings to:
   - expand scope
   - improve detections
   - improve DLP and UEBA rules
   - support investigations and reporting

---

## 5. Insider Threat Attack Lifecycle

Typical insider threat activity often follows this progression:

1. Discovery
2. Collection
3. Privilege Abuse
4. Data Staging
5. Exfiltration
6. Concealment or Sabotage
7. Persistence or Re-access Attempts

Not every incident contains every phase.

---

# 6. MITRE ATT&CK Mapping Table

| Tactic | Technique ID | Technique Name | Common Insider Threat Evidence | Primary Data Sources |
|--------|--------------|----------------|--------------------------------|----------------------|
| Initial Access | T1078 | Valid Accounts | legitimate employee login | IAM logs |
| Initial Access | T1078.004 | Valid Accounts: Cloud Accounts | cloud account misuse | cloud audit logs |
| Execution | T1059 | Command and Scripting Interpreter | PowerShell or shell usage | endpoint logs |
| Execution | T1204 | User Execution | manual execution of tools/scripts | EDR telemetry |
| Persistence | T1098 | Account Manipulation | permission or group changes | IAM logs |
| Persistence | T1136 | Create Account | unauthorized account creation | directory logs |
| Persistence | T1078 | Valid Accounts | continued use of legitimate credentials | authentication logs |
| Privilege Escalation | T1068 | Exploitation for Privilege Escalation | local admin abuse | endpoint telemetry |
| Privilege Escalation | T1548 | Abuse Elevation Control Mechanism | unauthorized elevation | EDR logs |
| Defense Evasion | T1070 | Indicator Removal on Host | log deletion | Windows event logs |
| Defense Evasion | T1562 | Impair Defenses | disabling security tools | endpoint telemetry |
| Defense Evasion | T1036 | Masquerading | misleading filenames/processes | endpoint telemetry |
| Discovery | T1087 | Account Discovery | user and group enumeration | IAM logs |
| Discovery | T1018 | Remote System Discovery | internal host discovery | network logs |
| Discovery | T1083 | File and Directory Discovery | searching for sensitive data | endpoint telemetry |
| Discovery | T1217 | Browser Information Discovery | browser credential/data review | endpoint telemetry |
| Collection | T1005 | Data from Local System | local file collection | endpoint telemetry |
| Collection | T1213 | Data from Information Repositories | SharePoint/database access | cloud/database logs |
| Collection | T1119 | Automated Collection | scripted bulk collection | process telemetry |
| Collection | T1560 | Archive Collected Data | ZIP/RAR creation | endpoint telemetry |
| Collection | T1025 | Data from Removable Media | USB file access | USB logs |
| Credential Access | T1555 | Credentials from Password Stores | browser credential access | browser artifacts |
| Credential Access | T1539 | Steal Web Session Cookie | session theft | browser telemetry |
| Lateral Movement | T1021 | Remote Services | RDP/SMB/WinRM | Windows logs |
| Exfiltration | T1020 | Automated Exfiltration | automated uploads/transfers | DLP/CASB logs |
| Exfiltration | T1041 | Exfiltration Over C2 Channel | malware-assisted exfiltration | proxy logs |
| Exfiltration | T1567 | Exfiltration Over Web Service | cloud storage uploads | cloud logs |
| Exfiltration | T1052 | Exfiltration Over Physical Medium | USB storage usage | USB telemetry |
| Impact | T1485 | Data Destruction | file deletion/sabotage | endpoint logs |
| Impact | T1491 | Defacement | internal content manipulation | collaboration logs |
| Impact | T1489 | Service Stop | disabling services | service logs |

---

# 7. Data Theft and Exfiltration Mapping

Data theft is one of the most common insider threat objectives.

---

## 7.1 Common Exfiltration Techniques

| ATT&CK Technique | Evidence | Detection Opportunity |
|------------------|----------|-----------------------|
| T1567 Exfiltration Over Web Service | cloud uploads | CASB/DLP alerts |
| T1052 Exfiltration Over Physical Medium | USB transfers | removable media monitoring |
| T1560 Archive Collected Data | ZIP/RAR staging | archive creation alerts |
| T1020 Automated Exfiltration | scripted transfers | UEBA anomalies |

---

## 7.2 Cloud Sharing Abuse Mapping

| ATT&CK Technique | Common Evidence | Detection Focus |
|------------------|----------------|----------------|
| T1567 Web Service Exfiltration | external OneDrive sharing | cloud audit monitoring |
| T1213 Data from Information Repositories | SharePoint access | unusual downloads |
| T1020 Automated Exfiltration | sync client abuse | upload spikes |

---

# 8. Privileged Misuse Mapping

Privileged insider activity carries elevated organizational risk.

---

## 8.1 Privileged Abuse Techniques

| ATT&CK Technique | Evidence | Detection |
|------------------|----------|----------|
| T1098 Account Manipulation | permission changes | IAM alerts |
| T1548 Abuse Elevation Control Mechanism | unauthorized elevation | endpoint logs |
| T1070 Indicator Removal | log deletion | SIEM monitoring |
| T1562 Impair Defenses | disabling EDR/DLP | security logs |

---

## 8.2 High-Risk Privileged Indicators

| Indicator | Meaning |
|-----------|---------|
| Security tool disablement | Defense evasion |
| Unauthorized group membership | Privilege escalation |
| New admin accounts | Persistence |
| Access outside maintenance windows | Suspicious admin activity |

---

# 9. Discovery and Collection Mapping

Insiders often perform discovery before exfiltration.

---

## 9.1 Discovery Techniques

| ATT&CK Technique | Example |
|------------------|---------|
| T1083 File and Directory Discovery | searching shared drives |
| T1087 Account Discovery | user/group review |
| T1018 Remote System Discovery | internal network scanning |

---

## 9.2 Collection Indicators

| Indicator | Meaning |
|-----------|---------|
| Large directory traversal | Bulk discovery |
| Sequential file access | Data staging |
| Repeated database queries | Structured data collection |
| Archive creation | Packaging data |

---

# 10. Concealment and Anti-Forensics Mapping

Insiders may attempt to conceal activity.

---

## 10.1 Anti-Forensics Techniques

| ATT&CK Technique | Evidence |
|------------------|----------|
| T1070 Indicator Removal | log clearing |
| T1036 Masquerading | misleading filenames |
| T1562 Impair Defenses | disabling security tools |

---

## 10.2 Concealment Indicators

| Indicator | Meaning |
|-----------|---------|
| Log deletion | Evidence tampering |
| Temporary file wiping | Concealment |
| Archive encryption | Hidden exfiltration |
| Renamed tools/scripts | Masquerading |

---

# 11. Insider Sabotage Mapping

Some insider threats focus on operational disruption.

---

## 11.1 Sabotage Techniques

| ATT&CK Technique | Evidence |
|------------------|----------|
| T1485 Data Destruction | mass deletion |
| T1489 Service Stop | service shutdown |
| T1491 Defacement | internal content manipulation |

---

## 11.2 Sabotage Indicators

| Indicator | Meaning |
|-----------|---------|
| Mass file deletion | Destructive activity |
| Service shutdowns | Operational sabotage |
| Unauthorized configuration changes | Service disruption |

---

# 12. Technique Confirmation Guidance

Use confidence levels consistently.

| Confidence Level | Meaning | Documentation Requirement |
|------------------|---------|---------------------------|
| Confirmed | Direct evidence exists | Logs and timestamps required |
| Likely | Strong indicators exist | Supporting evidence required |
| Possible | Weak indicators | Additional review needed |

---

# 13. Detection and Monitoring Recommendations

---

## 13.1 Endpoint Monitoring Recommendations

| Monitoring Area | Purpose |
|-----------------|---------|
| Archive creation | Detect staging |
| USB activity | Detect exfiltration |
| PowerShell usage | Detect automation |
| Privilege changes | Detect abuse |

---

## 13.2 Cloud Monitoring Recommendations

| Monitoring Area | Purpose |
|-----------------|---------|
| External sharing links | Detect exposure |
| Large uploads | Detect exfiltration |
| Guest account creation | Detect sharing abuse |
| OAuth grants | Detect persistence |

---

## 13.3 Identity Monitoring Recommendations

| Monitoring Area | Purpose |
|-----------------|---------|
| Privileged logins | Detect misuse |
| Group membership changes | Detect escalation |
| Login anomalies | Detect unusual activity |
| After-hours access | Behavioral anomaly detection |

---

# 14. Threat Hunting Recommendations

| Hunt Area | Purpose |
|-----------|---------|
| Archive creation followed by upload | Exfiltration detection |
| USB insertion after large file access | Data theft |
| Large cloud uploads | Exfiltration |
| Privileged changes outside maintenance windows | Misuse |
| Bulk file access patterns | Collection activity |

---

# 15. Detection Engineering Recommendations

Every insider threat investigation should improve:
- DLP visibility
- UEBA tuning
- cloud monitoring
- privileged activity monitoring
- exfiltration detection

---

## 15.1 Recommended Detection Improvements

| Improvement | Purpose |
|-------------|---------|
| DLP rule tuning | Detect sensitive transfers |
| UEBA baselines | Detect anomalies |
| USB monitoring alerts | Detect removable media abuse |
| Cloud sharing alerts | Detect external sharing |
| Privileged access alerts | Detect misuse |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 16. Reporting Requirements

Final reports should include:
- ATT&CK technique mappings
- timeline of activity
- data accessed or exfiltrated
- privilege misuse details
- concealment activity
- impact assessment
- recommended control improvements

Reference:
`07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`

---

# 17. MSSP Client Handling Notes

For MSSP-managed environments:
- insider threat mappings remain client-scoped
- maintain confidentiality
- avoid cross-client ATT&CK intelligence sharing
- follow client-approved reporting standards

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 18. Related Documents

| Document | Path |
|---------|------|
| Insider Threat Master | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Master.md` |
| Insider Threat L1 Triage | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L1-Triage.md` |
| Insider Threat L2 Investigation | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L2-Investigation.md` |
| Insider Threat L3 Forensics | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L3-Forensics.md` |
| Insider Threat Containment | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Containment.md` |
| HR and Legal Coordination | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md` |
| MITRE ATT&CK Quick Reference | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATTCK-Quick-Reference.md` |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |

---

## 19. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | Threat Intelligence Lead / L3 Lead | Initial version |

---

## 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**