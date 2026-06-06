# Incident Category Master List

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Incident Category Master List |
| Document ID | IR-CAT-000 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Purpose

This document provides the authoritative master list of incident categories used by the SOC and Incident Response program for:

- consistent incident classification and reporting
- playbook selection and execution
- SLA/SLO measurement and trend analysis
- MSSP client reporting and multi-tenant operations
- audit support (ISO 27001 / NIST / RBI)

---

## 3. Scope

Applies to:
- all incidents detected via SIEM/EDR/Network/Cloud tooling
- internal enterprise incidents
- MSSP client incidents (where contracted and applicable)

---

## 4. Category List (Authoritative)

| Category ID | Category Name | Primary Description | Default Severity (Typical) | Upgrade Triggers (Examples) | Primary Playbook Folder | Category Document |
|:----------:|---------------|---------------------|----------------------------|-----------------------------|-------------------------|:-----------------|
| CAT-01 | Ransomware | Encryption/wiper activity; extortion operations | P1 | active encryption; ransom note on shares; backup tampering; DC compromise | `02_PLAYBOOKS/02.1_Ransomware/` | `CAT-01-Ransomware.md` |
| CAT-02 | Phishing and BEC | Email social engineering, credential theft, mailbox compromise, fraud | P2 (interaction) / P4 (blocked) | creds entered; mailbox takeover; OAuth abuse; malware executed; fraud confirmed | `02_PLAYBOOKS/02.2_Phishing-BEC/` | `CAT-02-Phishing-BEC.md` |
| CAT-03 | Malware and Trojan | Malware execution, trojans, RATs, infostealers, loaders | P2 (execution) / P4 (blocked) | lateral movement; credential dumping; privileged compromise; ransomware precursor | `02_PLAYBOOKS/02.3_Malware-Trojan/` | `CAT-03-Malware-Trojan.md` |
| CAT-04 | DDoS | Availability attacks on network/app services | P1 (down) / P2 (degraded) | outage of critical services; diversion with intrusion indicators; extortion | `02_PLAYBOOKS/02.4_DDoS/` | `CAT-04-DDoS.md` |
| CAT-05 | Insider Threat | Malicious/negligent insider actions; compromised insider accounts | P2 / P3 | confirmed sensitive data theft; sabotage; privileged abuse; fraud | `02_PLAYBOOKS/02.5_Insider-Threat/` | `CAT-05-Insider-Threat.md` |
| CAT-06 | Data Breach and Exfiltration | Unauthorized access/exposure/exfiltration of sensitive data | P1 (confirmed) / P2 (suspected) | confirmed exfiltration; public exposure; regulated data impacted | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/` | `CAT-06-Data-Breach-Exfiltration.md` |
| CAT-07 | Credential Attack | Brute force, spraying, stuffing, MFA abuse, token theft | P2 (success) / P3 (suspicious) | privileged compromise; MFA bypass; widespread takeover; persistence found | `02_PLAYBOOKS/02.7_Credential-Attack/` | `CAT-07-Credential-Attack.md` |
| CAT-08 | Web Application Attack | Exploits against web apps/APIs (SQLi, RCE, auth bypass) | P2 / P3 / P4 | web shell/RCE; data access/exfiltration; admin takeover | `02_PLAYBOOKS/02.8_Web-Application-Attack/` | `CAT-08-Web-Application-Attack.md` |
| CAT-09 | Supply Chain Attack | Compromise via vendor software, updates, MSP tools, dependencies | P1 / P2 | malicious update deployed; RMM abuse; cross-client impact; breach confirmed | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/` | `CAT-09-Supply-Chain-Attack.md` |
| CAT-10 | Cloud Security Incident | Cloud identity/resource compromise; misconfig exposure; SaaS compromise | P1 / P2 / P3 | cloud admin takeover; logging tampering; data exfiltration; public exposure | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/` | `CAT-10-Cloud-Security-Incident.md` |
| CAT-11 | Network Intrusion | Unauthorized internal access; lateral movement; persistence | P2 / P1 | DC compromise; privileged compromise; multi-host lateral movement; exfiltration | `02_PLAYBOOKS/02.11_Network-Intrusion/` | `CAT-11-Network-Intrusion.md` |
| CAT-12 | Zero-Day Exploit | Exploitation of unknown/unpatched vulnerabilities; emergency mitigations | P1 / P2 / P3 | active exploitation; web shell; privileged compromise; data exposure | `02_PLAYBOOKS/02.12_Zero-Day-Exploit/` | `CAT-12-Zero-Day-Exploit.md` |
| CAT-13 | APT Campaign | Persistent targeted intrusion with advanced tradecraft | P1 / P2 | confirmed persistence; long-term access; data theft; re-entry attempts | `02_PLAYBOOKS/02.13_APT-Campaign/` | `CAT-13-APT-Campaign.md` |
| CAT-14 | Physical Security Incident | Theft/tampering/unauthorized physical access affecting information security | P2 / P3 / P1 | data center compromise; theft of unencrypted device; sabotage outage | Cross-functional | `CAT-14-Physical-Security-Incident.md` |

---

## 5. How to Use Categories (Operational Rules)

### 5.1 Category Selection
- Select the category based on the primary attack type or primary risk driver.
- If multiple categories apply, select the primary driver and reference secondary categories in the ticket notes.

### 5.2 Category vs Severity
- Category indicates the incident type.
- Severity (P1–P4) indicates urgency and response level.

Severity is governed by:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

### 5.3 Escalation and Communications
Follow escalation and communications SOPs:
`05_ESCALATION-AND-COMMUNICATION/`

---

## 6. Reporting and Metrics Alignment

Incident categories are used for:
- daily and weekly SOC reporting
- monthly trend analysis and KPI tracking
- MSSP client monthly reporting
- audit evidence and incident logs

Reference:
`07_REPORTING/`

---

## 7. Review and Maintenance

This category list must be reviewed:
- quarterly
- after major incidents (P1/P2) to incorporate new patterns
- upon onboarding major new platforms (cloud, SaaS, endpoints)
- upon regulatory or contractual changes

Changes must be approved by the SOC Manager and CISO.

---

## 8. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Manager | Initial version |

---

## 9. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**