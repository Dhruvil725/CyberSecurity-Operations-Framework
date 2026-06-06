# Playbook: Phishing and BEC – L3 Forensics and Advanced Analysis

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Phishing and BEC (L3 Forensics) |
| Document ID | IR-PB-PHB-004 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | L3 Forensics Lead / Threat Intel Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 phishing or BEC incident |

---

## 2. Purpose

This document defines the Level 3 (L3) advanced forensic procedure for complex Phishing and Business Email Compromise (BEC) incidents escalated from L2. 

L3 involvement is required when standard L2 scoping is insufficient, specifically involving:
- **AiTM (Adversary-in-the-Middle)** attacks and token/session theft.
- Advanced endpoint execution (e.g., obfuscated macros, LOLBins, zero-day payloads).
- Complex identity persistence (hidden inbox rules, Graph API abuse, rogue OAuth apps).
- Elaborate BEC financial fraud requiring timeline reconstruction for legal/law enforcement.
- Attribution, Threat Intelligence pivoting, and advanced threat hunting.

L3's objective is to provide definitive, legally defensible root cause analysis and technical depth.

---

## 3. Scope

Applies to:
- P1 and major P2 phishing/BEC incidents.
- Suspicion of MFA bypass, token theft, or session hijacking.
- Targeted spear-phishing or whaling campaigns.
- Malware payloads requiring reverse engineering or memory forensics.
- Enterprise and MSSP client environments (strict evidence handling required).

---

## 4. Inputs Required from L2 (Preconditions)

L3 expects the following packaged from L2 before commencing deep forensics. 

| L2 Input / Artifact | Description | Status Check |
|---------------------|-------------|--------------|
| **Original Evidence** | Preserved `.eml`/`.msg`, headers, and exact URLs. | ☐ Present |
| **Confirmed Scope** | List of known affected users, endpoints, and compromised accounts. | ☐ Present |
| **L2 IOC List** | Initial domains, IPs, and hashes identified. | ☐ Present |
| **Log Exports** | Proxy logs, email gateway logs, and initial Azure AD / IAM sign-in logs. | ☐ Present |
| **Escalation Reason** | Specific technical question L2 could not answer (e.g., "Did the malware run?", "Was a token stolen?"). | ☐ Present |

---

## 5. L3 Forensics Objectives and Outputs

### 5.1 Objectives
1. Prove or disprove session/token theft (AiTM) definitively.
2. Unearth hidden or advanced persistence mechanisms in cloud identity and mailboxes.
3. Reverse engineer malicious payloads to extract advanced IOCs and C2 configurations.
4. Construct an authoritative, second-by-second timeline of the BEC/compromise lifecycle.
5. Identify the threat actor (Attribution) and map to MITRE ATT&CK.

### 5.2 Required Outputs (Deliverables)

| Output Item | Description |
|-------------|-------------|
| **Authoritative Timeline** | Second-by-second reconstruction of the attack. |
| **Forensic IOC Package** | Advanced indicators (JA3 hashes, SSL certs, C2 domains, decoded scripts). |
| **Root Cause Analysis (RCA)** | Technical explanation of how MFA was bypassed or the payload executed. |
| **Data Exfiltration Report** | Confirmation of exactly what data was accessed/stolen (`MailItemsAccessed`). |
| **Containment Validation** | Confirmation that all advanced persistence has been eradicated. |

---

## 6. Step-by-Step L3 Forensic Procedure

---

### Step 1: Advanced Identity & Token Forensics (AiTM Focus)

Standard phishing steals passwords; advanced phishing (AiTM) steals session cookies to bypass MFA.

**Actions:**
- Analyze Identity/Azure AD Sign-in logs for token anomalies:

| Forensic Indicator | What to Look For | Significance |
|--------------------|------------------|--------------|
| **Session Cookie Theft** | `SessionLifetimePolicies` anomalies; login without a new MFA prompt shortly after a phishing click. | Attacker injected a stolen cookie into their browser. |
| **Device & Browser Mismatch** | Same `SessionID` or `TokenID` used across different OS/Browser strings or completely different ASNs. | Session token was moved from victim device to attacker device. |
| **Attacker Infrastructure** | IP address belongs to known VPN/Proxy networks (Mullvad, ExpressVPN, Tor) or VPS providers (DigitalOcean, Linode). | Evasion technique to mask true location. |
| **Token Refresh Spikes** | High volume of token refresh requests within a short timeframe. | Attacker automating data scraping via APIs. |

**Outputs:**
- Definitive ruling on MFA bypass / token theft.
- List of all attacker IPs and User-Agents used via the stolen session.

---

### Step 2: Deep Mailbox & Cloud App Forensics

Attackers hide their tracks using methods invisible to standard GUI checks.

**Actions:**
- Execute advanced Exchange/O365 PowerShell queries:

| Forensic Check | Command / Tool | Malicious Indicator |
|----------------|----------------|---------------------|
| **Hidden Inbox Rules** | `Get-InboxRule -Mailbox [User] -IncludeHidden` | Rules created with `PR_RULE_MSG_STATE` flag set to hidden (via MAPI/MFCMAPI). |
| **Data Access Audit** | `Search-MailboxAuditLog -Operations MailItemsAccessed` (Requires E5/Audit Premium) | Proves exactly which emails the attacker opened or downloaded. |
| **Rogue OAuth Apps** | `Get-AzureADServicePrincipal` / `Get-AzureADUserOAuth2PermissionGrant` | Applications granted `Mail.ReadWrite`, `Mail.Send`, or `offline_access`. |
| **Mailbox Forwarding** | `Get-MailboxForwardingSmtpAddress` | External SMTP forwarding at the tenant or mailbox level. |
| **Suspicious Delegates** | `Get-MailboxPermission` / `Get-RecipientPermission` | "Full Access" or "Send As" granted to compromised or unknown accounts. |

**Outputs:**
- List of all hidden persistence mechanisms.
- Confirmed list of accessed/exfiltrated emails.

---

### Step 3: Payload Reverse Engineering & Endpoint Forensics

If an attachment was executed and L2 could not determine the impact.

**Actions:**
- **Static Analysis:**
  - Deobfuscate macros (VBA), PowerShell, or JavaScript payloads using tools like `CyberChef`, `ViperMonkey`, or `Oledump`.
  - Extract embedded URLs, C2 IP addresses, and secondary payload drop paths.
- **Dynamic / Memory Analysis:**
  - If EDR memory dumps are available, analyze for injected threads or hollowed processes (e.g., Cobalt Strike beacons).
- **EDR Telemetry Deep-Dive:**
  - Trace the execution tree: `outlook.exe` -> `winword.exe` -> `cmd.exe` -> `powershell.exe` (base64 encoded).

| Execution Artifact | Check | Action / Result |
|--------------------|-------|-----------------|
| **Living off the Land (LOLBins)** | Use of `certutil.exe`, `bitsadmin.exe`, `wmic.exe` to download payloads. | Create advanced threat hunting queries. |
| **Persistence Mechanisms** | Registry Run keys, Scheduled Tasks (`schtasks`), WMI Event Subscriptions. | Add to IOC package for eradication. |

**Outputs:**
- Deobfuscated scripts and extracted C2 configurations.
- Endpoint persistence list.

---

### Step 4: BEC / Financial Fraud Timeline Reconstruction

For legal and law enforcement escalation, BEC requires rigorous timeline mapping.

**Actions:**
- Correlate email headers, sign-in logs, and mailbox audit logs to build a unified timeline.

| Timeline Component | Evidence Source | Requirement for Legal/Finance |
|--------------------|-----------------|-------------------------------|
| **Point of Entry** | Phishing Email + Sign-in log | Exact UTC timestamp of compromise. |
| **Reconnaissance** | `MailItemsAccessed` logs | Proof the attacker searched for "invoice", "bank", "wire". |
| **Impersonation** | Sent Items / SMTP logs | Exact copy of the email requesting the wire transfer/bank change. |
| **Evasion** | `Update Inbox Rules` log | Exact timestamp the attacker hid the victim's replies. |

**Outputs:**
- Authoritative BEC timeline document (formatted for non-technical stakeholders/Legal).

---

### Step 5: Attacker Infrastructure & Threat Intel Pivoting

**Actions:**
- Pivot on L2 indicators to find the broader campaign infrastructure.
- Check SSL certificate hashes, WHOIS registrants, and HTML DOM structures using tools like `Censys`, `Shodan`, or `RiskIQ`.
- Identify the Phishing Kit used (e.g., EvilProxy, Tycoon, Modlishka).

**Outputs:**
- Enriched threat actor profile.
- Proactive blocklist for firewall and DNS.

---

## 7. Escalation & Handoff to IR Team

L3 must brief the Incident Response (IR) Team if:

| Trigger | IR Team Action Required |
|---------|-------------------------|
| **Data Exfiltration Confirmed** | Legal notification, breach disclosure process activation. |
| **Financial Loss Confirmed** | Law enforcement engagement, banking fraud coordination. |
| **Widespread Network Intrusion** | Transition from Phishing Playbook to Ransomware/Network Intrusion Playbooks. |
| **Executive VIP Compromise** | Crisis communication and VIP executive protection protocols. |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L3-to-IR-Team-Escalation.md`

---

## 8. L3 Deliverables (Standard Templates)

L3 must attach these tables to the incident ticket or final report.

### 8.1 Authoritative Timeline Table
| Time (UTC) | Source IP | User/Account | Action / Event | Evidence Ref |
|------------|-----------|--------------|----------------|--------------|
| | | | | |

### 8.2 Advanced IOC Package
| IOC Type (JA3, C2, Hash) | Value | Context / Tool | Recommended Action |
|--------------------------|-------|----------------|--------------------|
| | | | |

### 8.3 Exfiltration / Access Summary
| Mailbox | Search Query Used by Attacker | Sensitive Items Accessed (Yes/No) | Confidence |
|---------|-------------------------------|-----------------------------------|------------|
| | | | |

---

## 9. Common L3 Mistakes to Avoid

| Mistake | Risk | Correct Approach |
|---------|------|------------------|
| **Relying only on GUI for Mailbox Rules** | Missing hidden persistence | Always use PowerShell (`-IncludeHidden`). |
| **Assuming MFA prevents account takeover** | Missing AiTM attacks | Always check for session cookie theft and token anomalies. |
| **Failing to document time zones** | Timeline corruption for Legal | **ALL logs and timelines MUST be in UTC.** |
| **Executing malware outside a secure lab** | Lab/Prod contamination | Only detonate payloads in isolated, air-gapped sandboxes. |

---

## 10. MSSP Client Handling Notes

- **Evidence Handling:** Advanced artifacts (memory dumps, decoded scripts) must be stored in encrypted, client-segregated vaults.
- **Reporting:** L3 technical findings must be summarized into business risk language for the client executive briefing.
- **Attribution:** Do not make definitive APT attribution claims to the client without threat intelligence validation and IR Team approval.

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Digital-Evidence-Handling.md`

---

## 11. Related Documents

| Document | Path |
|----------|------|
| **Phishing Master** | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Master.md` |
| **L2 Investigation**| `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L2-Investigation.md` |
| **BEC Detection** | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-BEC-Detection-Analysis.md` |
| **Containment** | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Containment.md` |
| **Eradication** | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Eradication.md` |
| **MITRE Mapping** | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-MITRE-Mapping.md` |

---

## 12. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | L3 Forensics Lead | Initial version |

---

## 13. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**