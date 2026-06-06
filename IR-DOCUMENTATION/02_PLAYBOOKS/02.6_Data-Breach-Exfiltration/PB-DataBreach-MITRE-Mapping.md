# Playbook: Data Breach and Data Exfiltration – MITRE ATT&CK Mapping

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Data Breach and Data Exfiltration (MITRE ATT&CK Mapping) |
| Document ID | IR-PB-DBR-007 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | Threat Intelligence Lead / L3 Lead |
| Approved By | IR Team Lead |
| Classification | Strictly Confidential |
| Review Cycle | Quarterly and after major data breach incidents |

---

## 2. Purpose

This document maps data breach and data exfiltration attack activity to
the MITRE ATT&CK framework.

The objectives are to:
- standardize data breach investigation documentation
- align breach analysis with ATT&CK terminology
- improve detection engineering and DLP coverage
- support threat hunting activities
- improve regulatory and executive reporting quality
- identify attacker tradecraft and objectives

Data breach and exfiltration incidents span multiple ATT&CK tactics and
often involve a combination of:
- initial access
- credential compromise
- discovery
- collection
- exfiltration techniques

---

## 3. Scope

Applies to:
- external attacker-driven data theft
- insider exfiltration
- cloud storage exposure
- database extraction
- email-based data theft
- API-based data extraction
- ransomware-related exfiltration
- unauthorized sharing incidents

Includes:
- endpoint exfiltration activity
- cloud platform abuse
- database extraction
- network exfiltration
- identity and access abuse

---

## 4. How to Use This Mapping

During data breach investigations:
1. Identify attacker or insider actions.
2. Map activity to ATT&CK techniques.
3. Document:
   - ATT&CK Technique ID
   - Technique Name
   - Evidence Source
   - Confidence Level
4. Use mappings to:
   - expand investigation scope
   - improve DLP and monitoring
   - support hunting
   - improve reporting

---

## 5. Data Breach Attack Lifecycle

Typical data breach operations follow this progression:

1. Initial Access
2. Authentication and Credential Abuse
3. Discovery
4. Collection and Staging
5. Exfiltration
6. Impact

Not every incident includes every phase.

---

# 6. MITRE ATT&CK Mapping Table

| Tactic | Technique ID | Technique Name | Common Evidence | Primary Data Sources |
|--------|--------------|----------------|-----------------|----------------------|
| Initial Access | T1566 | Phishing | phishing delivery of malware | email gateway logs |
| Initial Access | T1190 | Exploit Public-Facing Application | web app exploitation | WAF/web logs |
| Initial Access | T1078 | Valid Accounts | stolen credential usage | IAM logs |
| Initial Access | T1199 | Trusted Relationship | third-party access abuse | VPN/remote access logs |
| Execution | T1059 | Command and Scripting Interpreter | PowerShell/script execution | endpoint telemetry |
| Persistence | T1098 | Account Manipulation | permission changes | IAM logs |
| Persistence | T1078 | Valid Accounts | continued credential usage | authentication logs |
| Privilege Escalation | T1068 | Exploitation for Privilege Escalation | local exploit | EDR telemetry |
| Defense Evasion | T1070 | Indicator Removal on Host | log deletion | Windows event logs |
| Defense Evasion | T1562 | Impair Defenses | disabling DLP/security tools | security logs |
| Credential Access | T1003 | OS Credential Dumping | LSASS access | EDR/memory analysis |
| Credential Access | T1555 | Credentials from Password Stores | browser credential theft | browser artifacts |
| Credential Access | T1528 | Steal Application Access Token | OAuth token theft | IAM logs |
| Discovery | T1083 | File and Directory Discovery | file system enumeration | endpoint telemetry |
| Discovery | T1082 | System Information Discovery | host enumeration | endpoint logs |
| Discovery | T1213 | Data from Information Repositories | SharePoint/database access | cloud/DB logs |
| Discovery | T1087 | Account Discovery | user enumeration | IAM logs |
| Collection | T1005 | Data from Local System | local file collection | endpoint telemetry |
| Collection | T1213 | Data from Information Repositories | cloud data access | cloud audit logs |
| Collection | T1119 | Automated Collection | scripted data gathering | process logs |
| Collection | T1560 | Archive Collected Data | ZIP/RAR staging | endpoint telemetry |
| Collection | T1114 | Email Collection | mailbox access | mail audit logs |
| Collection | T1530 | Data from Cloud Storage Object | S3/Blob access | cloud logs |
| Exfiltration | T1041 | Exfiltration Over C2 Channel | malware-based transfer | proxy/firewall |
| Exfiltration | T1567 | Exfiltration Over Web Service | cloud upload | cloud audit logs |
| Exfiltration | T1567.002 | Exfiltration to Cloud Storage | personal drive upload | CASB logs |
| Exfiltration | T1048 | Exfiltration Over Alternative Protocol | FTP/SFTP | firewall logs |
| Exfiltration | T1052 | Exfiltration Over Physical Medium | USB transfer | USB telemetry |
| Exfiltration | T1020 | Automated Exfiltration | automated scripts | DLP/CASB |
| Impact | T1485 | Data Destruction | deletion after exfiltration | endpoint logs |
| Impact | T1486 | Data Encrypted for Impact | ransomware after theft | EDR |

---

# 7. Cloud Data Exposure Mapping

Cloud misconfigurations frequently enable large-scale data breaches.

---

## 7.1 Cloud Storage Exposure Techniques

| ATT&CK Technique | Evidence | Detection Opportunity |
|------------------|----------|-----------------------|
| T1530 Data from Cloud Storage | S3/Blob access logs | Cloud access monitoring |
| T1567 Exfiltration Over Web Service | upload activity | CASB monitoring |
| T1213 Data from Repositories | SharePoint downloads | Cloud audit alerts |

---

## 7.2 Cloud Configuration Abuse Indicators

| Indicator | Meaning |
|-----------|---------|
| Public bucket ACL | World-readable |
| Anonymous access enabled | No authentication required |
| Sharing link without expiry | Persistent exposure |
| Guest access granted | External exposure |

---

# 8. Database Exfiltration Mapping

Structured database extraction is common in large breaches.

---

## 8.1 Database Extraction Techniques

| ATT&CK Technique | Evidence | Detection |
|------------------|----------|----------|
| T1213 Data from Repositories | large SELECT queries | DB monitoring |
| T1119 Automated Collection | scripted exports | process logs |
| T1005 Data from Local System | local DB dump | endpoint logs |

---

## 8.2 Database Exfiltration Indicators

| Indicator | Meaning |
|-----------|---------|
| Unrestricted SELECT | Mass data access |
| Export commands | Bulk dump |
| After-hours queries | Suspicious activity |
| New credentials used | Compromised account |

---

# 9. Email and Collaboration Exfiltration Mapping

---

## 9.1 Email Exfiltration Techniques

| ATT&CK Technique | Evidence | Detection |
|------------------|----------|----------|
| T1114 Email Collection | mailbox access | mail audit logs |
| T1567 Web Service Exfiltration | external forwarding | DLP alerts |
| T1020 Automated Exfiltration | forwarding rules | mailbox monitoring |

---

## 9.2 Collaboration Platform Exfiltration

| ATT&CK Technique | Evidence | Detection |
|------------------|----------|----------|
| T1213 Data from Repositories | Teams/Slack export | collaboration logs |
| T1567.002 Cloud Storage Exfiltration | OneDrive upload | CASB logs |
| T1530 Cloud Object Access | SharePoint download | cloud audit |

---

# 10. Insider Exfiltration Mapping

---

## 10.1 Insider Exfiltration Techniques

| ATT&CK Technique | Evidence | Detection |
|------------------|----------|----------|
| T1052 Physical Medium | USB transfer | USB telemetry |
| T1567 Web Service | personal cloud upload | CASB alerts |
| T1114 Email Collection | forwarding rules | mail monitoring |
| T1005 Local System | bulk file copy | endpoint logs |

---

## 10.2 Insider Exfiltration Indicators

| Indicator | Meaning |
|-----------|---------|
| USB insertion after bulk access | Data theft |
| Personal cloud upload | Exfiltration |
| Email forwarding to personal account | Unauthorized transfer |
| Archive creation before USB | Staging |

---

# 11. Credential Abuse Mapping

Credential theft often enables data breaches.

---

## 11.1 Credential Access Techniques

| ATT&CK Technique | Evidence | Detection |
|------------------|----------|----------|
| T1003 Credential Dumping | LSASS access | EDR alerts |
| T1555 Password Store | browser credential | endpoint logs |
| T1528 Token Theft | OAuth token abuse | IAM monitoring |
| T1539 Session Cookie Theft | browser session | UEBA alerts |

---

# 12. Technique Confirmation Guidance

| Confidence Level | Meaning | Requirement |
|------------------|---------|-------------|
| Confirmed | Direct evidence | Logs and timestamps |
| Likely | Strong indicators | Supporting evidence |
| Possible | Weak indicators | Further investigation |

---

# 13. Detection and Hunting Recommendations

---

## 13.1 Endpoint Monitoring

| Monitoring Area | Purpose |
|-----------------|---------|
| Archive creation | Detect staging |
| USB activity | Detect exfiltration |
| Bulk file access | Detect collection |
| Credential access | Detect theft |

---

## 13.2 Cloud Monitoring

| Monitoring Area | Purpose |
|-----------------|---------|
| Public bucket access | Detect exposure |
| Large downloads | Detect exfiltration |
| External sharing | Detect unauthorized access |
| API key usage | Detect programmatic access |

---

## 13.3 Network Monitoring

| Monitoring Area | Purpose |
|-----------------|---------|
| Large outbound transfers | Detect exfiltration |
| Unusual protocols | Detect alternative channels |
| DNS anomalies | Detect covert transfer |
| Proxy upload events | Detect cloud exfiltration |

---

## 13.4 Threat Hunting Recommendations

| Hunt Area | Purpose |
|-----------|---------|
| Bulk file access before upload | Exfiltration detection |
| Archive creation before USB | Staging detection |
| Email forwarding to external | Unauthorized transfer |
| Large database queries | Data extraction |
| OAuth consent after phishing | Token abuse |

---

# 14. Detection Engineering Recommendations

Every data breach investigation must improve detection coverage.

---

## 14.1 Recommended Detection Improvements

| Improvement | Purpose |
|-------------|---------|
| DLP rule tuning | Detect sensitive transfers |
| Cloud sharing alerts | Detect public exposure |
| Database export alerts | Detect extraction |
| USB monitoring | Detect physical exfiltration |
| Large outbound traffic alerts | Detect network exfiltration |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 15. Reporting Requirements

Final incident reports should include:
- ATT&CK techniques observed
- exfiltration method confirmed
- data categories impacted
- exposure duration
- detection gaps
- recommended improvements

Reference:
`07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`

---

# 16. MSSP Client Handling Notes

For MSSP-managed environments:
- maintain client-specific ATT&CK mappings
- anonymize cross-client intelligence outputs
- maintain evidence segregation
- provide client-specific technical briefings

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 17. Related Documents

| Document | Path |
|---------|------|
| Data Breach Master | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md` |
| Data Breach L1 Triage | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L1-Triage.md` |
| Data Breach L2 Investigation | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L2-Investigation.md` |
| Data Breach L3 Forensics | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L3-Forensics.md` |
| Legal Notification | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Legal-Notification.md` |
| Regulatory Reporting | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Regulatory-Reporting.md` |
| MITRE ATT&CK Quick Reference | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATTCK-Quick-Reference.md` |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |

---

## 18. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | Threat Intelligence Lead / L3 Lead | Initial version |

---

## 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**