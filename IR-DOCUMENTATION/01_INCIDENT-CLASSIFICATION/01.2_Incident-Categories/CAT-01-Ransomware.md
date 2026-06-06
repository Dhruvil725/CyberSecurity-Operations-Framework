# CAT-01 – Ransomware Incident Category

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Incident Category – Ransomware |
| Document ID | IR-CAT-001 |
| Version | 1.0 |
| Effective Date | 14-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Category Overview

| Field | Details |
|-------|---------|
| Category ID | CAT-01 |
| Default Severity | P1 – Critical |
| Escalation Priority | Immediate |
| Attack Goal | Encrypt or destroy data for financial extortion |
| Threat Actors | Cybercriminal groups, RaaS operators, nation-state affiliates |
| Playbook Reference | 02_PLAYBOOKS/02.1_Ransomware/ |

---

## 3. What is Ransomware?

Ransomware is malicious software designed to:

- Encrypt files on victim systems making them inaccessible
- Demand payment (usually cryptocurrency) for decryption keys
- Threaten to leak stolen data if ransom is not paid
- Disrupt business operations to maximize pressure on victims

Modern ransomware attacks follow a structured kill chain:

Initial Access
	|
	v
Establish Foothold
	|
	v
Privilege Escalation
	|
	v
Lateral Movement
	|
	v
Data Exfiltration (double extortion)
	|
	v
Encryption / Impact
	|
	v
Ransom Demand


---

## 4. Ransomware Types

| Type | Description |
|------|-------------|
| Crypto Ransomware | Encrypts files and demands key for decryption |
| Locker Ransomware | Locks user out of entire system |
| Double Extortion | Encrypts AND exfiltrates; threatens to publish stolen data |
| Triple Extortion | Adds DDoS or direct customer notification threats |
| RaaS (Ransomware-as-a-Service) | Ransomware toolkit sold or leased to criminal affiliates |
| Wiper / Pseudo-Ransomware | Destroys data with no intention to restore |

---

## 5. Attack Vectors – Initial Access

| Vector | Description |
|--------|-------------|
| Phishing Email | Malicious attachment or link delivered via email |
| RDP Exploitation | Brute-force or vulnerability exploitation of exposed RDP (port 3389) |
| VPN / Remote Access | Compromised or stolen credentials for VPN or remote access |
| Supply Chain | Compromise via vendor software, updates, or managed service providers |
| Web Application Exploit | Vulnerability in public-facing web application |
| Malvertising | Drive-by download via malicious advertisement |
| Exposed Services | Unpatched internet-facing services (SMB, FTP, RDP) |

---

## 6. Indicators of Compromise (IoCs)

### 6.1 Host-Based Indicators

| Indicator Type | Examples / Details |
|---------------|-------------------|
| File Extensions | .locked / .encrypted / .WNCRY / .ryuk / .conti / .hive / .blackcat |
| Ransom Notes | README.txt / DECRYPT_INSTRUCTIONS.html / HOW_TO_DECRYPT.txt |
| Shadow Copy Deletion | vssadmin.exe delete shadows / wbadmin delete catalog |
| Boot Recovery Disabled | bcdedit /set recoveryenabled no |
| Mass File Rename | High volume file rename events in short time window |
| Suspicious Processes | taskill.exe / net stop (stopping security services) |
| New Scheduled Tasks | Encoded tasks set to persist or execute payload |
| New Services Created | Services with random names or system32 impersonation |

### 6.2 Network Indicators

| Indicator Type | Examples / Details |
|---------------|-------------------|
| C2 Communication | Beaconing to Tor nodes or known RaaS infrastructure |
| Data Exfiltration | Large outbound HTTPS / FTP / SFTP transfers |
| SMB Lateral Movement | Unusual SMB traffic between internal hosts (port 445) |
| Cobalt Strike Beacons | Known C2 communication patterns from post-exploitation |
| DNS Anomalies | High-frequency DNS requests to newly registered domains |
| Port Scanning | Internal host scanning other hosts (pre-lateral movement) |

### 6.3 Log-Based Indicators

| Log Source | Indicator / Event |
|------------|-------------------|
| Windows Event Log | Event ID 4688 – suspicious process creation |
| Windows Event Log | Event ID 7045 – new service installed |
| Windows Event Log | Event ID 4698/4702 – scheduled task created or modified |
| SIEM Alert | vssadmin delete shadows command detected |
| SIEM Alert | bcdedit /set recoveryenabled no command detected |
| EDR Alert | Mass file rename or encryption activity on endpoint |
| Firewall Log | Outbound traffic to Tor exit nodes or known C2 IPs |
| Proxy Log | Large outbound data transfers to cloud storage or unknown hosts |

---

## 7. Severity Classification

| Scenario | Severity |
|----------|----------|
| Active file encryption detected on endpoints or file shares | P1 – Critical |
| Ransom note dropped on file systems or shares | P1 – Critical |
| Shadow copies or backups being deleted | P1 – Critical |
| Ransomware operator tools detected (pre-encryption stage) | P2 – High |
| Cobalt Strike or post-exploitation beacon detected | P2 – High |
| Suspicious script or LOLBin activity (no ransom payload yet) | P3 – Medium |

---

## 8. Immediate Response Actions

### Phase 1 – First 15 Minutes

- [ ] Declare P1 immediately in ticketing system
- [ ] Activate bridge call and war room
- [ ] Notify SOC Lead, CISO, and Management within 15 minutes
- [ ] Isolate affected endpoints via EDR network containment
- [ ] Block known IoCs at firewall, DNS, and proxy level
- [ ] Capture volatile memory evidence if safe to do so
- [ ] Disable affected user accounts and revoke active sessions
- [ ] Notify MSSP client immediately (if applicable)

### Phase 2 – First 1 Hour

- [ ] Map full scope of affected systems and users
- [ ] Identify initial access vector
- [ ] Isolate and segment affected network segments
- [ ] Verify backup integrity (do NOT access from potentially infected system)
- [ ] Check if shadow copies and backups are intact
- [ ] Document full timeline in real time
- [ ] Notify GRC and Compliance for regulatory assessment
- [ ] Assess regulatory reporting obligations (RBI / CERT-In)

### Phase 3 – 1 to 4 Hours

- [ ] Confirm containment of encryption activity
- [ ] Begin eradication planning
- [ ] Identify and preserve forensic evidence (disk images if required)
- [ ] Assess feasibility of decryption (NoMoreRansom.org check)
- [ ] Assess backup restoration readiness
- [ ] Prepare executive summary for management
- [ ] Initiate regulatory reporting if required

---

## 9. MITRE ATT&CK Mapping

| Tactic | Technique Name | Technique ID |
|--------|---------------|-------------|
| Initial Access | Phishing | T1566 |
| Initial Access | Exploit Public-Facing Application | T1190 |
| Initial Access | Valid Accounts (External Remote Services) | T1078 |
| Execution | User Execution | T1204 |
| Execution | Command and Scripting Interpreter | T1059 |
| Persistence | Scheduled Task / Job | T1053 |
| Persistence | Boot or Logon Autostart Execution | T1547 |
| Privilege Escalation | Exploitation for Privilege Escalation | T1068 |
| Defense Evasion | Indicator Removal | T1070 |
| Defense Evasion | Obfuscated Files or Information | T1027 |
| Credential Access | OS Credential Dumping | T1003 |
| Discovery | Network Share Discovery | T1135 |
| Discovery | Remote System Discovery | T1018 |
| Lateral Movement | SMB / Windows Admin Shares | T1021.002 |
| Lateral Movement | Remote Services | T1021 |
| Exfiltration | Exfiltration Over Web Service | T1567 |
| Exfiltration | Exfiltration Over Alternative Protocol | T1048 |
| Impact | Data Encrypted for Impact | T1486 |
| Impact | Inhibit System Recovery | T1490 |
| Impact | Service Stop | T1489 |

---

## 10. Key Investigation Questions

The following questions must be answered during the investigation:

**When did encryption begin? (first encrypted file timestamp)**
**Which systems, shares, and users are confirmed affected?**
**Is encryption still actively in progress?**
**Was data exfiltrated before encryption? (double extortion risk)**
**What was the confirmed initial access vector?**
**Are domain administrator credentials compromised?**
**Are backups intact, isolated, and unaffected?**
**Have shadow copies been deleted?**
**Has C2 communication been severed?**
**Is the ransomware strain identified? (known decryptor available?)**
**How far has lateral movement progressed?**
**Are any cloud environments or SaaS platforms impacted?**


---

## 11. Critical Do's and Do Not's

### Do

- Isolate affected systems immediately via EDR containment
- Preserve encrypted files in case a decryptor becomes available
- Capture memory dumps if safe and before shutdown
- Use known-clean systems for all investigation activity
- Notify management and GRC immediately
- Check NoMoreRansom.org for known decryptors before any payment discussion
- Follow chain-of-custody for all evidence

### Do Not

- Pay ransom without explicit CISO and Legal approval
- Reboot affected systems unless directed (destroys memory evidence)
- Run antivirus scans that may overwrite forensic artifacts
- Access backups from a potentially compromised system
- Delete or modify logs or artifacts
- Assume backups are clean without verification
- Make any public statements without Legal and PR approval

---

## 12. Regulatory Reporting Requirements

| Regulator / Framework | Requirement |
|-----------------------|------------|
| RBI Cyber Security Framework | Report cyber incident to RBI within defined circular timeline |
| CERT-In | Mandatory notification for ransomware affecting critical sectors |
| ISO 27001 (Annex A.5.26) | Log and manage as major information security incident |
| MSSP Client SLA | Notify client as per contractual notification timeline |
| Legal / Law Enforcement | Engage if criminal prosecution or insurance claim required |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 13. Escalation Path
L1 Analyst (alert detected)

​	|
​	v (less than or equal to 5 minutes)

L2 Analyst (investigation begins)

​	|
​	v (less than or equal to 10 minutes)

L3 Analyst + SOC Lead (P1 declared)

​	|
​	v (less than or equal to 30 minutes)

IR Team Activated (Incident Commander assigned)

​	|
​	v (immediately)

CISO + Management notified

​	|
​	v (if regulatory trigger confirmed)

GRC / Compliance initiates regulatory reporting


---

## 14. Evidence Collection Requirements

The following evidence must be collected for all ransomware incidents:

| Evidence Type | Priority | Notes |
|--------------|---------|-------|
| Memory dump (affected hosts) | Critical | Before any reboot |
| Disk image (affected hosts) | Critical | Triage image acceptable if full not possible |
| SIEM log export | Critical | 48 hours prior to first encrypted file |
| EDR telemetry export | Critical | Process tree, file activity, network connections |
| Network capture (PCAP) | High | If available from time of activity |
| Active Directory / authentication logs | Critical | Identify compromised accounts |
| Firewall and proxy logs | High | Identify C2 and exfiltration channels |
| Backup system status report | Critical | Verify integrity before restore |
| Ransom note copy | Medium | Preserve for strain identification |
| Encrypted file sample | Medium | Preserve for potential decryptor |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 15. Related Documents

| Document | Path |
|---------|------|
| Ransomware Master Playbook | 02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Master.md |
| L1 Triage Playbook | 02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L1-Triage.md |
| L2 Investigation Playbook | 02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L2-Investigation.md |
| L3 Forensics Playbook | 02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L3-Forensics.md |
| Containment Playbook | 02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md |
| Eradication Playbook | 02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Eradication.md |
| Recovery Playbook | 02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Recovery.md |
| MITRE ATT&CK Mapping | 02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-MITRE-Mapping.md |
| P1 Critical Definition | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md |
| Emergency Escalation P1 | 05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md |
| Evidence Collection SOP | 06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md |
| RBI Incident Reporting SOP | 05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md |

---

## 16. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Manager | Initial version |

---

## 17. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**