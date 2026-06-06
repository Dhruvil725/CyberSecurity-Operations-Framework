# CAT-11 – Network Intrusion Incident Category

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Incident Category – Network Intrusion |
| Document ID | IR-CAT-011 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Category Overview

| Field | Details |
|-------|---------|
| Category ID | CAT-11 |
| Default Severity | P2 – High (confirmed unauthorized access) / P1 – Critical (lateral movement + privileged compromise + business impact) |
| Escalation Priority | High; treat early to prevent spread and data loss |
| Attack Goal | Establish unauthorized access, persistence, lateral movement, data theft, ransomware staging |
| Threat Actors | Cybercriminal groups, APT groups, ransomware affiliates, insider-compromised accounts |
| Primary Systems | AD/Domain Controllers, file servers, application servers, VPN, remote access services, network devices |
| Playbook Reference | `02_PLAYBOOKS/02.11_Network-Intrusion/` |

---

## 3. What is a Network Intrusion?

A network intrusion is an unauthorized presence or unauthorized activity
within an internal network or environment. It typically involves one or
more of the following:

- Unauthorized access to internal hosts (servers/endpoints)
- Unauthorized access to internal network segments
- Lateral movement across systems
- Establishing persistence (accounts, scheduled tasks, services)
- Credential theft and privilege escalation
- Discovery/reconnaissance of internal assets
- Exfiltration of data or staging for ransomware

Network intrusion is often the “middle phase” of a major incident:
phishing or exploit leads to initial access, then intrusion expands
internally toward high-value assets (AD, databases, backups).

---

## 4. Common Intrusion Entry Points (Initial Access)

| Entry Point | Examples |
|------------|----------|
| Remote Access | VPN compromise, exposed RDP, remote admin portals |
| Valid Credentials | Credential stuffing, password spraying success, stolen passwords |
| Public-Facing Exploit | Web application vulnerability leading to foothold |
| Phishing | Compromised user leads to endpoint access and internal pivot |
| Supply Chain | MSP/RMM or vendor access used to enter internal network |
| Misconfiguration | Open shares, weak firewall rules, exposed management ports |

---

## 5. Common Intrusion Techniques (Internal Stage)

| Technique Area | Examples |
|----------------|----------|
| Discovery | Network scanning, host enumeration, AD discovery tools |
| Credential Access | LSASS dumping, browser credential theft, Kerberos attacks |
| Lateral Movement | RDP, SMB, WMI, PsExec, WinRM, SSH |
| Persistence | Scheduled tasks, services, startup items, new user creation |
| Privilege Escalation | Local admin, domain admin escalation, exploitation |
| Defense Evasion | Log clearing, disabling EDR, masquerading binaries |
| Data Collection | File share staging, DB exports, email collection |
| Command and Control | Beaconing to external hosts, proxying through internal servers |

---

## 6. Indicators of Compromise (IoCs) and Observables

### 6.1 Network and Authentication Observables (High Value)

| Indicator | What It May Mean |
|----------|-------------------|
| Successful logins from unusual source subnets | Credential compromise or pivoting |
| Multiple failed logins across many hosts (spray) | Password spraying campaign |
| Sudden increase in RDP/SMB sessions | Lateral movement |
| New admin shares accessed (C$, ADMIN$) | Remote execution/lateral movement |
| Unusual Kerberos requests (high volume) | Kerberoasting or ticket abuse |
| NTLM authentication spikes | Pass-the-hash patterns or legacy fallback abuse |
| New VPN sessions followed by internal host access | External entry → internal pivot |

### 6.2 Host and Endpoint Observables

| Indicator | What It May Mean |
|----------|-------------------|
| Suspicious remote execution tools | PsExec/WMI/WinRM usage outside admin patterns |
| Encoded PowerShell and LOLBins | Post-exploitation activity |
| New services or scheduled tasks | Persistence or lateral execution |
| Security tooling disabled | Defense evasion by attacker |
| Credential dumping indicators | LSASS access, dumper tools |

### 6.3 Network Traffic Observables

| Indicator | What It May Mean |
|----------|-------------------|
| Beaconing pattern to external destination | Command and control |
| Unusual outbound ports from servers | Malware/C2 |
| DNS anomalies to new/rare domains | C2 or staging |
| Internal scanning patterns | Recon prior to lateral movement |
| Large outbound data transfers | Possible exfiltration |

### 6.4 Key Log Sources to Review (Minimum)

| Source | Minimum Checks |
|--------|----------------|
| AD / Domain Controller Logs | 4624/4625, group changes, Kerberos events, admin logons |
| EDR | Process trees, remote execution, credential access, suspicious binaries |
| Firewall / NetFlow | New outbound destinations, unusual internal east-west traffic |
| VPN / Remote Access | New sessions, failed attempts, geo anomalies |
| DNS / Proxy | New domain queries, suspicious web destinations |
| Server Logs | RDP logs, SMB access, service creation, task creation |
| SIEM Correlation | Multi-source sequence: VPN → endpoint → server → DC |

---

## 7. Severity Classification

| Scenario | Severity |
|----------|----------|
| Domain Controller compromise confirmed | P1 – Critical |
| Privileged account compromise with broad access (Domain Admin / Cloud Admin) | P1 – Critical |
| Lateral movement confirmed across multiple servers or segments | P1 – Critical |
| Confirmed data exfiltration or staging during intrusion | P1 – Critical |
| Network intrusion causing outage of business-critical services | P1 – Critical |
| Confirmed unauthorized access to internal host(s) (single segment, contained) | P2 – High |
| Confirmed foothold with C2 on one host (no lateral movement yet) | P2 – High |
| Suspicious internal scanning or enumeration (unconfirmed access) | P3 – Medium |
| Blocked intrusion attempt (IDS/IPS blocked, no evidence of access) | P4 – Low |

---

## 8. Immediate Response Actions (Operational Detail)

### 8.1 First 15 Minutes (Stabilize and Contain Initial Spread)

- Create incident ticket and assign initial severity
- Notify SOC Lead immediately for P2 and above
- Identify initial “patient zero” host and user account (if known)
- Preserve key logs immediately (AD, VPN, EDR telemetry, firewall/NetFlow)
- Determine whether attacker activity is active (ongoing sessions, beaconing)
- Initiate containment approval if compromise is confirmed:
  - EDR isolate affected hosts
  - disable compromised accounts or revoke sessions
  - block known C2 destinations at firewall/proxy/DNS
- Mark suspected hosts for immediate scoping (same subnet, same user, same alert pattern)

### 8.2 First 1 Hour (Scope and Confirm Lateral Movement)

- Confirm intrusion path:
  - how attacker entered (VPN, web exploit, phishing, vendor access)
  - what account was used
  - what systems were accessed
- Identify lateral movement:
  - RDP/SMB/WMI/PsExec/WinRM/SSH activity
  - admin share access
  - remote service/task creation
- Identify privilege escalation:
  - group membership changes
  - credential dumping indicators
  - abnormal Kerberos/NTLM patterns
- Check for persistence:
  - new local users
  - scheduled tasks
  - new services
  - startup/run keys
- Escalate to P1 if domain/privileged compromise or multi-system lateral movement is confirmed

### 8.3 First 4 Hours (Containment Confirmation and Eradication Planning)

- Confirm all attacker sessions terminated (VPN sessions, cloud sessions, RDP sessions)
- Ensure all compromised accounts are reset and tokens revoked
- Ensure network blocks are effective and monitored for bypass attempts
- Identify and preserve artifacts required for forensics and RCA
- Begin eradication planning:
  - patch exploited services
  - harden remote access controls
  - rotate credentials, keys, certificates (as needed)
- Increase monitoring:
  - create temporary hunts for suspicious remote tools and authentication patterns
  - monitor for reinfection or re-entry

---

## 9. Containment Guidance (Decision Support)

| Containment Action | Use When | Notes |
|-------------------|----------|------|
| EDR network isolation | Confirmed compromised endpoint/server | Preferred for fast containment |
| Account disable | Confirmed credential compromise | Requires coordination with IAM/AD and business owner |
| Session/token revocation | Cloud/email compromise or risky sign-ins | Must be paired with password reset |
| Block C2 domains/IPs | Confirmed beaconing destinations | Implement at multiple layers (DNS/proxy/firewall) |
| Segment network | Lateral movement across segments | May require network change approval |
| Disable remote services | RDP/SMB abused | Use carefully; coordinate with IT operations |

Reference: `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 10. MITRE ATT&CK Mapping (Common for Intrusions)

| Tactic | Technique | ID |
|--------|-----------|----|
| Initial Access | External Remote Services | T1133 |
| Initial Access | Exploit Public-Facing Application | T1190 |
| Credential Access | Brute Force / Password Spraying | T1110 / T1110.003 |
| Credential Access | Valid Accounts | T1078 |
| Credential Access | OS Credential Dumping | T1003 |
| Discovery | Network Service Scanning | T1046 |
| Discovery | Account Discovery | T1087 |
| Lateral Movement | Remote Services | T1021 |
| Lateral Movement | SMB/Windows Admin Shares | T1021.002 |
| Lateral Movement | Lateral Tool Transfer | T1570 |
| Persistence | Create Account | T1136 |
| Persistence | Scheduled Task/Job | T1053 |
| Defense Evasion | Indicator Removal on Host | T1070 |
| Command and Control | Application Layer Protocol | T1071 |
| Exfiltration | Exfiltration Over C2 Channel | T1041 |
| Impact | Data Encrypted for Impact | T1486 |

---

## 11. Key Investigation Questions (Visibility-Focused)

1. What is the suspected initial access vector (VPN, RDP, exploit, phishing, vendor access)?
2. Which account(s) were used, and are they privileged?
3. What is the earliest confirmed malicious activity timestamp?
4. Which systems were accessed (first host, pivot hosts, target hosts)?
5. Is lateral movement confirmed (which protocol/tool was used)?
6. Is there evidence of credential dumping or ticket abuse?
7. Are there C2 communications (domains/IPs, timing, protocol)?
8. Are there signs of data staging or exfiltration?
9. Are backups, hypervisors, or management systems targeted?
10. What persistence mechanisms exist (accounts, tasks, services)?
11. Have any security controls been disabled or tampered with?
12. What containment actions are required and what approvals are needed?
13. Is this incident connected to ransomware precursor activity?

---

## 12. Critical Do's and Do Not's

### Do

- Prioritize stopping spread: isolate, disable compromised accounts, block C2
- Preserve logs before major changes where feasible
- Confirm and document scope continuously; intrusion scope changes quickly
- Use a single timeline source in the incident ticket
- Coordinate with IT/network/IAM for high-impact containment actions
- Run targeted hunts across environment for same TTPs and indicators
- Consider this category a precursor to data breach or ransomware unless proven otherwise

### Do Not

- Assume a single compromised host is the full scope without validation
- Reset passwords without revoking sessions/tokens
- Apply broad network blocks without business impact review
- Remove suspicious artifacts before evidence capture and logging
- Close the incident without verifying persistence removal and monitoring for re-entry

---

## 13. Escalation Path

| Stage | Action |
|-------|--------|
| L1 Triage | Detect, validate, create ticket, notify SOC Lead if suspicious activity confirmed |
| L2 Investigation | Confirm intrusion, scope affected hosts/accounts, recommend containment |
| SOC Lead | Approve severity, coordinate response tasks, manage communications |
| L3 / IR Team | Perform advanced analysis, forensics, root cause and persistence checks |
| Network Team | Implement segmentation, blocks, routing changes, logging enhancements |
| IAM / AD Team | Execute disables, resets, group membership rollback, token revocations |
| Management / CISO | Engage for P1 and major business risk decisions |
| GRC / Compliance | Engage if breach/regulatory reporting is likely |
| MSSP SDM / Client Owner | Notify and coordinate actions for client environments |

---

## 14. Regulatory and Client Reporting Considerations

| Trigger | Action |
|--------|--------|
| Privileged identity compromise | Treat as major incident; assess reporting obligations |
| Sensitive data access/exfiltration suspected | Engage Compliance and Legal immediately |
| Critical service disruption | Assess customer/client notification requirements |
| MSSP client affected | Notify per SLA and include scope and containment status |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 15. Evidence Collection Requirements

| Evidence Type | Priority | Notes |
|--------------|----------|-------|
| AD/DC security logs export | Critical | Auth events, group changes, Kerberos/NTLM indicators |
| VPN/remote access logs | Critical | Session history, source IPs, MFA results |
| EDR telemetry export | Critical | Process trees, remote execution tools, suspicious binaries |
| Network flow logs (NetFlow/sFlow) | High | East-west movement and external C2 patterns |
| Firewall/proxy logs | High | C2 destinations and exfil signals |
| DNS logs | High | Suspicious domains and tunneling indicators |
| Host artifacts (tasks/services/autoruns) | High | Persistence evidence |
| Memory capture (selected hosts) | As needed | For fileless malware and injection analysis |
| Disk image/triage image (selected hosts) | As needed | For forensic reconstruction |
| Timeline and communications log | Critical | For incident report and audits |
| Chain-of-custody forms | As needed | Required if forensic evidence is collected |

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 16. Related Documents

| Document | Path |
|---------|------|
| Network Intrusion Master Playbook | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Master.md` |
| L1 Triage Playbook | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L1-Triage.md` |
| L2 Investigation Playbook | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L2-Investigation.md` |
| L3 Forensics Playbook | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L3-Forensics.md` |
| Containment Playbook | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Containment.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-MITRE-Mapping.md` |
| Credential Attack Category | `01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/CAT-07-Credential-Attack.md` |
| Malware Category | `01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/CAT-03-Malware-Trojan.md` |
| P1 Critical Definition | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |

---

## 17. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Manager | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**