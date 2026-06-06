# Playbook: Phishing and BEC – MITRE ATT&CK Mapping

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Phishing and BEC (MITRE ATT&CK Mapping) |
| Document ID | IR-PB-PHB-008 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | Threat Intelligence Lead / L3 Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after major phishing or BEC incidents |

---

## 2. Purpose

This document maps phishing and Business Email Compromise (BEC) attack
activities to the MITRE ATT&CK framework.

The objective is to:
- standardize attack-chain documentation
- support investigation and scoping
- improve detection engineering
- align reporting with industry-standard ATT&CK terminology
- support threat hunting and proactive monitoring
- improve executive and regulatory reporting quality

This mapping is used during:
- L2 investigations
- L3 forensic analysis
- threat hunting exercises
- incident reporting
- detection tuning and coverage assessments

---

## 3. Scope

Applies to:
- credential phishing attacks
- BEC campaigns
- AiTM phishing attacks
- OAuth consent abuse
- phishing-delivered malware
- mailbox takeover incidents
- cloud identity compromise
- phishing-enabled internal lateral movement

Includes:
- MITRE tactic and technique mapping
- evidence examples
- recommended log sources
- detection and hunting guidance

---

## 4. How to Use This Mapping

During investigations:
1. Identify attacker actions and artifacts.
2. Map observed behavior to ATT&CK tactics and techniques.
3. Record:
   - Technique ID
   - Technique Name
   - Evidence Source
   - Confidence Level
4. Use mapped techniques to:
   - expand scoping
   - identify additional impacted users or systems
   - improve detections
   - support executive reporting
   - improve future hunting

Documentation standard:
- include ATT&CK technique ID
- include evidence reference
- include confidence level:
  - Confirmed
  - Likely
  - Possible

---

## 5. High-Level Phishing and BEC Attack Chain

Typical phishing and BEC operations follow this progression:

1. Reconnaissance
2. Resource Development
3. Initial Access
4. Credential Access
5. Persistence
6. Defense Evasion
7. Discovery
8. Collection
9. Exfiltration
10. Impact / Fraud Execution

Not every incident contains every phase.

---

# 6. MITRE ATT&CK Mapping Table (Detailed)

| Tactic | Technique ID | Technique Name | Common Evidence Examples | Primary Log Sources |
|--------|--------------|----------------|--------------------------|--------------------|
| Reconnaissance | T1592 | Gather Victim Identity Information | attacker researches executives or finance staff | OSINT monitoring, social media analysis |
| Reconnaissance | T1593 | Search Open Websites/Domains | attacker collects vendor or organizational data | web activity, external monitoring |
| Resource Development | T1583 | Acquire Infrastructure | VPS or cloud infrastructure used for phishing | TI feeds, WHOIS |
| Resource Development | T1584 | Compromise Infrastructure | compromised email servers used for phishing | mail headers, TI reports |
| Resource Development | T1585 | Establish Accounts | attacker registers lookalike domains | WHOIS records |
| Initial Access | T1566.001 | Spearphishing Attachment | malicious Office document or PDF attachment | email gateway logs, EDR |
| Initial Access | T1566.002 | Spearphishing Link | phishing URL leading to fake login page | proxy logs, DNS logs |
| Initial Access | T1566.003 | Spearphishing via Service | phishing through Teams, Slack, WhatsApp, etc. | SaaS logs |
| Initial Access | T1078 | Valid Accounts | attacker logs in with stolen credentials | IAM logs, Azure AD logs |
| Initial Access | T1078.004 | Valid Accounts: Cloud Accounts | compromised Microsoft 365 or Google Workspace account | cloud sign-in logs |
| Execution | T1204 | User Execution | user opens malicious attachment or enters credentials | endpoint logs, user reports |
| Execution | T1059 | Command and Scripting Interpreter | PowerShell or script execution from payload | EDR telemetry |
| Persistence | T1098 | Account Manipulation | attacker adds delegate permissions or forwarding | mailbox audit logs |
| Persistence | T1114.003 | Email Collection: Email Forwarding Rule | forwarding rules to attacker-controlled mailbox | mailbox audit logs |
| Persistence | T1136 | Create Account | attacker creates new mailbox or cloud user | IAM logs |
| Persistence | T1528 | Steal Application Access Token | OAuth refresh token theft | Azure AD logs |
| Persistence | T1137 | Office Application Startup | malicious Outlook rules or templates | Outlook logs |
| Defense Evasion | T1114 | Email Collection | hidden mailbox rules and mail deletion | mailbox audit logs |
| Defense Evasion | T1070 | Indicator Removal on Host | deleting sent items or mailbox cleanup | mailbox logs |
| Defense Evasion | T1562 | Impair Defenses | disabling MFA or email alerts | IAM logs |
| Defense Evasion | T1036 | Masquerading | lookalike domains or spoofed executive display names | email headers |
| Credential Access | T1056 | Input Capture | phishing credential harvesting pages | phishing kit analysis |
| Credential Access | T1556 | Modify Authentication Process | MFA bypass or session hijacking | IAM logs |
| Credential Access | T1539 | Steal Web Session Cookie | AiTM session theft | browser telemetry |
| Credential Access | T1528 | Steal Application Access Token | OAuth token theft | Azure AD logs |
| Discovery | T1087 | Account Discovery | attacker reviews org contacts and users | mailbox access logs |
| Discovery | T1016 | System Network Configuration Discovery | internal email or directory reconnaissance | cloud audit logs |
| Discovery | T1082 | System Information Discovery | endpoint reconnaissance after malware execution | EDR telemetry |
| Collection | T1114.001 | Local Email Collection | attacker reads mailbox contents | mailbox audit logs |
| Collection | T1114.002 | Remote Email Collection | attacker accesses cloud mailbox remotely | cloud audit logs |
| Collection | T1213 | Data from Information Repositories | SharePoint or OneDrive access | M365 audit logs |
| Collection | T1005 | Data from Local System | local file collection after payload execution | endpoint telemetry |
| Exfiltration | T1041 | Exfiltration Over C2 Channel | malware-based data exfiltration | EDR and proxy logs |
| Exfiltration | T1567 | Exfiltration Over Web Service | OneDrive, Dropbox, or external mail forwarding | cloud audit logs |
| Exfiltration | T1020 | Automated Exfiltration | automated forwarding or scripted exfiltration | mailbox rules |
| Impact | T1657 | Financial Theft | fraudulent payment or wire transfer | finance records |
| Impact | T1531 | Account Access Removal | attacker changes password or disables user access | IAM logs |
| Impact | T1491 | Defacement | phishing emails sent internally from compromised account | mail flow logs |

---

# 7. BEC-Specific ATT&CK Mapping

BEC operations frequently rely more on social engineering and mailbox abuse
than malware execution.

---

## 7.1 Executive Impersonation Mapping

| ATT&CK Technique | Evidence | Detection Opportunity |
|------------------|----------|-----------------------|
| T1036 Masquerading | CEO display name spoofing | display-name impersonation alert |
| T1585 Establish Accounts | lookalike domain registration | domain similarity monitoring |
| T1566 Spearphishing | urgent payment request email | anti-phishing gateway rules |

---

## 7.2 Mailbox Takeover Mapping

| ATT&CK Technique | Evidence | Detection Opportunity |
|------------------|----------|-----------------------|
| T1078 Valid Accounts | successful login from attacker IP | impossible travel detection |
| T1114 Email Collection | mailbox searched for invoice/payment terms | MailItemsAccessed monitoring |
| T1114.003 Forwarding Rule | forwarding rule created | mailbox audit alerts |
| T1098 Account Manipulation | delegate permission added | mailbox permission monitoring |

---

## 7.3 OAuth Abuse Mapping

| ATT&CK Technique | Evidence | Detection Opportunity |
|------------------|----------|-----------------------|
| T1528 Steal Application Access Token | OAuth consent grant | OAuth monitoring alerts |
| T1098 Account Manipulation | app granted high permissions | admin consent monitoring |
| T1556 Modify Authentication Process | bypassing MFA through token reuse | session anomaly monitoring |

---

# 8. AiTM (Adversary-in-the-Middle) Mapping

AiTM phishing operations require additional ATT&CK mapping due to session theft.

| ATT&CK Technique | Description | Common Evidence |
|------------------|-------------|-----------------|
| T1539 | Steal Web Session Cookie | token replay after phishing |
| T1556 | Modify Authentication Process | MFA bypass through AiTM |
| T1078 | Valid Accounts | successful cloud login after token theft |
| T1528 | Steal Application Access Token | refresh token abuse |
| T1114 | Email Collection | mailbox access after token replay |

Key indicators:
- “MFA already satisfied” login
- token replay from VPS infrastructure
- login from new browser/device immediately after phishing click
- OAuth consent after suspicious login

---

# 9. Technique Confirmation Guidance

Use confidence levels consistently during investigations.

| Confidence Level | Meaning | Documentation Requirement |
|------------------|---------|---------------------------|
| Confirmed | Direct evidence exists | include logs, screenshots, timestamps |
| Likely | Strong indicators but incomplete evidence | explain reasoning |
| Possible | Weak indicators requiring further analysis | assign follow-up action |

---

# 10. Recommended Detection and Hunting Focus Areas

The following areas should receive prioritized monitoring and threat hunting coverage.

---

## 10.1 Identity and Login Monitoring

| Detection Area | Reason |
|----------------|--------|
| Impossible travel | Detect stolen credentials |
| Login from VPS/Tor | Detect attacker infrastructure |
| MFA registration changes | Detect persistence |
| “MFA already satisfied” logins | Detect token replay |

---

## 10.2 Mailbox Monitoring

| Detection Area | Reason |
|----------------|--------|
| Inbox rule creation | Detect persistence |
| External forwarding enabled | Detect exfiltration |
| Mailbox permission changes | Detect lateral mailbox access |
| Mass outbound email | Detect internal phishing |

---

## 10.3 OAuth and Cloud App Monitoring

| Detection Area | Reason |
|----------------|--------|
| OAuth app consent events | Detect rogue applications |
| High-risk permissions granted | Detect mailbox API abuse |
| Unknown enterprise apps | Detect attacker persistence |

---

## 10.4 Endpoint and Malware Monitoring

| Detection Area | Reason |
|----------------|--------|
| Office spawning PowerShell | Detect malicious attachments |
| Browser credential theft | Detect token/session theft |
| Script execution after email open | Detect payload execution |

---

# 11. Mapping Outputs for Incident Reports

The final incident report should include:
- observed ATT&CK tactics and techniques
- confirmed vs likely techniques
- evidence references
- attack progression narrative
- recommended controls mapped to ATT&CK

Reference:
`07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`

---

# 12. Detection Improvement Requirements

Every phishing or BEC incident should produce detection improvement actions.

Examples:
- new SIEM correlation rules
- new mailbox audit alerts
- OAuth consent monitoring
- executive impersonation detections
- inbox rule anomaly detections

All improvements must be tracked in:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 13. MSSP Client Handling Notes

For MSSP-managed environments:
- ATT&CK mappings must remain client-scoped
- do not reference one client’s TTPs in another client’s report
- anonymize cross-client threat intelligence outputs
- provide ATT&CK mapping summaries in executive reports when required

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 14. Related Documents

| Document | Path |
|---------|------|
| Phishing Master | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Master.md` |
| L1 Triage | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L1-Triage.md` |
| L2 Investigation | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L2-Investigation.md` |
| L3 Forensics | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L3-Forensics.md` |
| Containment | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Containment.md` |
| Eradication | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Eradication.md` |
| BEC Detection Analysis | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-BEC-Detection-Analysis.md` |
| MITRE ATT&CK Quick Reference | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATTCK-Quick-Reference.md` |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |

---

## 15. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | Threat Intelligence Lead / L3 Lead | Initial version |

---

## 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document