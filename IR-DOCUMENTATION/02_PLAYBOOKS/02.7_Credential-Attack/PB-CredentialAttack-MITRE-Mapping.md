# Playbook: Credential Attack – MITRE ATT&CK Mapping

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Credential Attack (MITRE ATT&CK Mapping) |
| Document ID | IR-PB-CRA-005 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | Threat Intelligence Lead / L3 Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after major credential attack incidents |

---

## 2. Purpose

This document maps credential-based attack activity to the MITRE ATT&CK
framework to support:
- consistent credential-attack documentation
- identity attack-chain reconstruction
- detection engineering improvements
- threat hunting development
- audit-ready reporting

Credential attacks often represent the earliest stage of compromise and may
precede:
- privilege escalation
- lateral movement
- data breach / exfiltration
- ransomware deployment

Mapping credential attack activity to ATT&CK enables:
- consistent reporting across incidents
- prioritization of detection gaps
- faster correlation between identity and endpoint activities

---

## 3. Scope

Applies to credential attacks including:
- brute force
- password spraying
- credential stuffing
- MFA fatigue
- token/session theft (AiTM outcomes)
- Kerberoasting
- Pass-the-Hash
- Pass-the-Ticket
- credential dumping (if detected)
- unauthorized privilege escalation via credential misuse

Includes:
- on-prem identity (Active Directory)
- cloud identity (Entra ID / IAM platforms)
- VPN authentication
- web application authentication
- MSSP-managed environments

---

## 4. How to Use This Mapping

During investigations:
1. Identify observed behaviors (logins, failures, successes, MFA anomalies).
2. Map behaviors to ATT&CK techniques.
3. Record:
   - Technique ID and name
   - Evidence references (log exports, ticket links)
   - Confidence level (Confirmed/Likely/Possible)
4. Use mapped techniques to:
   - expand scoping
   - prioritize containment
   - improve detections and monitoring
   - guide hunts and follow-on investigations

---

## 5. Credential Attack Lifecycle (Typical)

Credential attacks typically follow this progression:

1. Reconnaissance / Discovery
2. Credential Access Attempts
3. Successful Authentication
4. Privilege Escalation (if possible)
5. Lateral Movement
6. Persistence (token/app consent/service accounts)
7. Impact (data theft / ransomware / sabotage)

Not all attacks reach all stages.

---

# 6. MITRE ATT&CK Mapping Table (Detailed)

| Tactic | Technique ID | Technique Name | Common Credential Attack Evidence | Primary Log Sources |
|--------|--------------|----------------|-----------------------------------|---------------------|
| Reconnaissance | T1592 | Gather Victim Identity Information | targeted user lists; finance/admin targeting | threat intel, audit context |
| Reconnaissance | T1589 | Gather Victim Identity Information | username enumeration | web logs, IAM logs |
| Initial Access | T1078 | Valid Accounts | successful login with stolen creds | AD logs, Entra sign-in logs |
| Initial Access | T1078.004 | Valid Accounts: Cloud Accounts | cloud sign-in from suspicious IP | cloud sign-in logs |
| Credential Access | T1110 | Brute Force | repeated failed logins | AD 4625, VPN logs |
| Credential Access | T1110.003 | Password Spraying | low-and-slow failures across many accounts | SIEM correlation, IAM logs |
| Credential Access | T1110.004 | Credential Stuffing | failures + successes using reused credentials | IAM logs, app logs |
| Credential Access | T1556 | Modify Authentication Process | MFA bypass indications | IAM logs, CA logs |
| Credential Access | T1621 | Multi-Factor Authentication Request Generation | MFA fatigue/push bombing | MFA logs |
| Credential Access | T1539 | Steal Web Session Cookie | token replay patterns | cloud sign-in logs |
| Credential Access | T1528 | Steal Application Access Token | OAuth token misuse | cloud audit logs |
| Credential Access | T1003 | OS Credential Dumping | LSASS access | EDR alerts, memory forensics |
| Credential Access | T1555 | Credentials from Password Stores | browser credential access | endpoint telemetry |
| Credential Access | T1558.003 | Kerberoasting | abnormal TGS requests | DC logs 4769 |
| Discovery | T1087 | Account Discovery | user/group enumeration | AD logs, endpoint logs |
| Discovery | T1069 | Permission Groups Discovery | admin group membership lookups | AD logs |
| Privilege Escalation | T1098 | Account Manipulation | group membership changes | AD logs 4728/4732 |
| Privilege Escalation | T1078.003 | Valid Accounts: Local Accounts | local admin login reuse | endpoint logs |
| Lateral Movement | T1021 | Remote Services | RDP/WinRM/SMB logons | Windows logs 4624 |
| Lateral Movement | T1021.002 | SMB/Windows Admin Shares | admin share usage | file server logs |
| Lateral Movement | T1570 | Lateral Tool Transfer | tools moved between hosts | EDR, SMB logs |
| Defense Evasion | T1070 | Indicator Removal on Host | clearing event logs | Windows logs 1102 |
| Persistence | T1098 | Account Manipulation | adding delegates; password changes | IAM logs |
| Persistence | T1136 | Create Account | new user created | IAM logs |
| Persistence | T1528 | Steal Application Access Token | persistent token access | cloud audit logs |
| Impact | T1486 | Data Encrypted for Impact | credential attack leads to ransomware | EDR + ransomware playbook |
| Impact | T1565 | Data Manipulation | unauthorized changes using valid accounts | app logs |

---

# 7. Credential Attack Type Mapping (Operational)

This section maps common credential attacks to ATT&CK techniques for operational use.

---

## 7.1 Brute Force Mapping

| Attack Type | ATT&CK Technique | Evidence |
|------------|-------------------|----------|
| Brute Force | T1110 Brute Force | repeated 4625 failures on one account |

---

## 7.2 Password Spray Mapping

| Attack Type | ATT&CK Technique | Evidence |
|------------|-------------------|----------|
| Password Spray | T1110.003 Password Spraying | low failures across many users; lockouts |

---

## 7.3 Credential Stuffing Mapping

| Attack Type | ATT&CK Technique | Evidence |
|------------|-------------------|----------|
| Credential Stuffing | T1110.004 Credential Stuffing | mixed success/failure patterns across accounts |

---

## 7.4 MFA Fatigue Mapping

| Attack Type | ATT&CK Technique | Evidence |
|------------|-------------------|----------|
| MFA Fatigue | T1621 MFA Request Generation | repeated push prompts; approval event |

---

## 7.5 Token Replay / AiTM Mapping

| Attack Type | ATT&CK Technique | Evidence |
|------------|-------------------|----------|
| Session Cookie Theft | T1539 Steal Web Session Cookie | “MFA already satisfied” + new device/IP |
| Token Theft | T1528 Steal Application Access Token | refresh token abuse or OAuth activity |

---

## 7.6 Kerberoasting Mapping

| Attack Type | ATT&CK Technique | Evidence |
|------------|-------------------|----------|
| Kerberoasting | T1558.003 Kerberoasting | high TGS requests for service accounts |

---

# 8. Technique Confirmation Guidance

Use consistent confidence levels.

| Confidence Level | Meaning | Requirement |
|------------------|---------|-------------|
| Confirmed | Direct evidence exists | logs + timestamps |
| Likely | Strong indicators exist | supporting evidence |
| Possible | Weak indicators | follow-up actions required |

---

# 9. Recommended Detection and Hunting Focus Areas

Credential attacks are best detected through correlation.

---

## 9.1 Identity Monitoring Priorities

| Focus Area | Reason |
|-----------|--------|
| Impossible travel with success | account takeover |
| Repeated failures across many users | spray attacks |
| Service account ticket anomalies | kerberoasting |
| MFA fatigue patterns | push bombing |
| Login from VPS/Tor ASNs | attacker infrastructure |
| Legacy auth usage | MFA bypass risk |
| Admin group membership changes | escalation |

---

## 9.2 Endpoint and Network Monitoring Priorities

| Focus Area | Reason |
|-----------|--------|
| LSASS access | credential dumping |
| Remote service logons | lateral movement |
| Admin share usage | remote execution |
| Post-login suspicious processes | attacker activity |

---

## 9.3 Hunting Output Expectations

Hunts should produce:
- list of accounts targeted and successful
- list of IPs/ASNs involved
- list of compromised sessions
- list of privilege escalation indicators

Detection gaps must be recorded in:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 10. Reporting Requirements

Final incident reports should include:
- observed ATT&CK techniques
- confirmed vs likely techniques
- evidence references
- attacker progression narrative
- recommended controls mapped to techniques

Reference:
`07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`

---

# 11. MSSP Client Handling Notes

For MSSP-managed environments:
- keep ATT&CK mappings client-scoped
- do not share one client’s identity attack patterns with another
- anonymize shared threat intelligence outputs
- follow client reporting requirements

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 12. Related Documents

| Document | Path |
|---------|------|
| Credential Attack Master | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-Master.md` |
| Credential Attack L1 Triage | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-L1-Triage.md` |
| Credential Attack L2 Investigation | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-L2-Investigation.md` |
| Credential Attack Containment | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-Containment.md` |
| Phishing/BEC Playbooks | `02_PLAYBOOKS/02.2_Phishing-BEC/` |
| Network Intrusion Playbooks | `02_PLAYBOOKS/02.11_Network-Intrusion/` |
| Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |
| MITRE ATT&CK Quick Reference | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATTCK-Quick-Reference.md` |

---

## 13. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | Threat Intelligence Lead / L3 Lead | Initial version |

---

## 14. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**