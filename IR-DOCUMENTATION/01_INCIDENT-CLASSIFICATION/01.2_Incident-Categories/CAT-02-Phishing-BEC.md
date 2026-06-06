# CAT-02 – Phishing and Business Email Compromise (BEC)

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Incident Category – Phishing and BEC |
| Document ID | IR-CAT-002 |
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
| Category ID | CAT-02 |
| Default Severity | P2 – High (user interaction confirmed) / P4 – Low (blocked) |
| Escalation Priority | High if credentials entered, mailbox compromised, or malware executed |
| Attack Goal | Credential theft, financial fraud, malware delivery, mailbox compromise |
| Threat Actors | Cybercriminal groups, nation-state actors, opportunistic attackers |
| Playbook Reference | `02_PLAYBOOKS/02.2_Phishing-BEC/` |

---

## 3. What is Phishing and BEC?

### 3.1 Phishing

Phishing is a social engineering attack in which threat actors send deceptive communications, usually by email, to trick users into performing unsafe actions.

Common attacker objectives include:

- Stealing usernames and passwords
- Delivering malware through attachments or links
- Harvesting MFA tokens or session cookies
- Redirecting users to fake login portals
- Gaining initial access for follow-on attacks

### 3.2 Business Email Compromise (BEC)

Business Email Compromise (BEC) is a targeted email fraud attack in which attackers impersonate or compromise a trusted business account in order to manipulate employees, vendors, or partners.

Common BEC objectives include:

- Unauthorized wire transfers
- Payment redirection
- Invoice fraud
- Sensitive business data theft
- Internal account takeover for further phishing

### 3.3 Common Phishing / BEC Attack Flow

1. Threat actor prepares phishing lure or impersonation email
2. Email is delivered to one or more recipients
3. User opens, clicks, replies, or submits credentials
4. Attacker gains access to mailbox, endpoint, or credentials
5. Attacker uses access for fraud, internal phishing, malware delivery, or persistence

---

## 4. Types of Phishing and BEC

| Type | Description |
|------|-------------|
| Spear Phishing | Targeted phishing using personalized details about the victim |
| Whaling | Phishing aimed at senior executives or high-value individuals |
| Clone Phishing | Copy of a legitimate email with malicious links or attachments |
| Credential Phishing | Fake login page used to steal credentials |
| Malware Phishing | Email designed to deliver malicious payloads |
| BEC – CEO Fraud | Impersonation of leadership to request payments or sensitive actions |
| BEC – Vendor Fraud | Vendor email impersonation to redirect invoices or payment details |
| Account Takeover | Use of a compromised legitimate mailbox for malicious activity |
| OAuth Phishing | Malicious consent requests to access cloud resources |
| QR Phishing | Use of QR codes in emails to bypass URL scanning and trick users |

---

## 5. Attack Vectors

| Vector | Description |
|--------|-------------|
| Email Attachment | Macro documents, PDFs, archives, shortcut files, HTML attachments |
| Malicious Link | Link to credential harvesting site or malware download |
| Lookalike Domain | Domain visually similar to legitimate business domain |
| Display Name Spoofing | Trusted sender name with unrelated email address |
| Compromised Internal Account | Legitimate account used to send phishing internally |
| Compromised Vendor Account | Trusted third-party account used to send malicious requests |
| Adversary-in-the-Middle | MFA bypass through real-time phishing proxy |
| OAuth Consent Abuse | User authorizes malicious cloud application access |

---

## 6. Indicators of Compromise (IoCs)

### 6.1 Email Indicators

| Indicator Type | Details |
|---------------|---------|
| Sender Anomaly | Mismatch between display name and email address |
| Reply-To Mismatch | Reply address differs from visible sender |
| SPF / DKIM / DMARC Failure | Email authentication checks fail |
| Domain Similarity | Lookalike or typosquatted sender domain |
| Suspicious Language | Urgency, secrecy, payment pressure, account lockout threat |
| Unusual Attachment | HTML, ISO, ZIP, RAR, LNK, macro-enabled Office files |
| Suspicious URL | Newly registered, shortened, or IP-based links |
| Unusual Conversation Pattern | Sudden invoice or payment request with changed banking details |

### 6.2 Account / Cloud Indicators

| Indicator Type | Details |
|---------------|---------|
| Impossible Travel | Login from distant locations within impossible time window |
| Unusual MFA Activity | Unexpected MFA pushes, repeated denial prompts |
| New Inbox Rules | Forwarding rules, delete rules, hide-from-view rules |
| External Forwarding | Mailbox auto-forwarding to external address |
| OAuth App Consent | New consent granted to unknown or risky application |
| Session Anomalies | Multiple simultaneous sessions from different locations |
| Mass Mail Activity | Compromised account sending phishing emails internally or externally |

### 6.3 Endpoint / User Interaction Indicators

| Indicator Type | Details |
|---------------|---------|
| Browser Visit | Access to known phishing domain |
| Credential Submission | User submitted credentials to external site |
| Attachment Execution | User opened malicious document or HTML attachment |
| Child Process Spawn | Office launching PowerShell, cmd.exe, mshta, wscript |
| Downloaded Payload | Suspicious file written to Downloads, Temp, or AppData |
| Reported User Behavior | User reports suspicious login page, email, or MFA prompt |

---

## 7. Severity Classification

| Scenario | Severity |
|----------|----------|
| Confirmed BEC with successful fraudulent transaction | P1 – Critical |
| Mass mailbox compromise or mass credential compromise | P1 – Critical |
| Confirmed credential entry on phishing page | P2 – High |
| Confirmed mailbox takeover | P2 – High |
| Confirmed malware execution from phishing email | P2 – High |
| OAuth consent to malicious application | P2 – High |
| Phishing click confirmed, no credential entry yet | P3 – Medium |
| Suspicious phishing email delivered, no interaction | P4 – Low |
| Phishing email blocked by secure mail gateway | P4 – Low |

---

## 8. Immediate Response Actions

### 8.1 First 15 Minutes

- Create incident ticket and assign preliminary severity
- Preserve original email and full headers
- Determine whether the email was delivered, blocked, or clicked
- Check whether other users received the same email
- Block sender, sender domain, URLs, and hashes where applicable
- Notify SOC Lead if user interaction is confirmed
- Begin mailbox and login activity review for impacted user

### 8.2 First 1 Hour

- Confirm whether credentials were submitted
- Force password reset if credentials are suspected compromised
- Revoke active sessions and refresh tokens
- Review mailbox audit logs
- Review Azure AD / Entra ID sign-ins and MFA events
- Check for inbox rules, forwarding rules, and delegate access
- Remove phishing email from all user mailboxes if campaign confirmed
- Notify management and client if severity is P2 or above

### 8.3 First 4 Hours

- Validate whether mailbox compromise occurred
- Check for internal phishing from compromised mailbox
- Review financial fraud exposure in BEC scenarios
- Review OAuth consents and remove malicious apps
- Assess whether incident must be escalated to P1
- Preserve all evidence and communication records

---

## 9. MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|--------|-----------|----|
| Initial Access | Phishing: Spearphishing Attachment | T1566.001 |
| Initial Access | Phishing: Spearphishing Link | T1566.002 |
| Initial Access | Phishing: Spearphishing via Service | T1566.003 |
| Execution | User Execution: Malicious Link | T1204.001 |
| Execution | User Execution: Malicious File | T1204.002 |
| Credential Access | Phishing for Information | T1598 |
| Credential Access | Steal or Forge Authentication Tokens | T1528 |
| Credential Access | Adversary-in-the-Middle | T1557 |
| Collection | Email Collection | T1114 |
| Persistence | Email Forwarding Rule | T1114.003 |
| Persistence | Account Manipulation | T1098 |
| Defense Evasion | Use Alternate Authentication Material | T1550 |

---

## 10. Key Investigation Questions

The following questions must be answered during every phishing or BEC investigation:

1. What is the original sender address and domain?
2. Did the email pass SPF, DKIM, and DMARC checks?
3. How many users received the email?
4. How many users opened, clicked, replied, or submitted credentials?
5. Was any malware executed from the email or attachment?
6. Were credentials entered into a phishing page?
7. Was MFA challenged, bypassed, or abused?
8. Has the mailbox been accessed from unusual locations or devices?
9. Were inbox rules, forwarding rules, or delegates added?
10. Was OAuth consent granted to any unknown application?
11. Was the compromised mailbox used to send additional emails?
12. Was any financial fraud attempted or completed?
13. Has the malicious email been purged from all impacted mailboxes?

---

## 11. Critical Do's and Do Not's

### Do

- Preserve the original email with full headers
- Block sender, domain, and malicious URLs quickly
- Revoke sessions and reset credentials if compromise is suspected
- Review mailbox rules and forwarding configurations
- Check cloud identity logs for suspicious sign-in patterns
- Coordinate with finance immediately if BEC is suspected
- Remove malicious OAuth consents where applicable
- Notify affected users and stakeholders according to severity

### Do Not

- Delete the original phishing email before evidence is preserved
- Assume MFA prevents all phishing outcomes
- Ignore user reports of unusual MFA prompts
- Close the ticket without checking for mailbox manipulation
- Delay finance notification in BEC payment fraud scenarios
- Trust display names without checking actual sender addresses

---

## 12. BEC-Specific Investigation Checklist

| Check | Required |
|------|----------|
| Review mailbox audit logs | Yes |
| Review inbox rules and forwarding rules | Yes |
| Review delegate permissions | Yes |
| Review OAuth app consents | Yes |
| Revoke active sessions | Yes |
| Validate recent payment instructions | Yes |
| Validate vendor banking changes | Yes |
| Notify finance and procurement teams | Yes |
| Review sent items and deleted items | Yes |
| Check for further impersonation attempts | Yes |

---

## 13. Escalation Path

| Stage | Action |
|------|--------|
| L1 Triage | Validate phishing email, identify impacted users, preserve evidence |
| L2 Investigation | Confirm interaction, account risk, malware execution, or mailbox compromise |
| SOC Lead | Approve severity escalation, client and management communication |
| IR Team | Engage for mailbox takeover, large-scale phishing, or BEC fraud |
| GRC / Compliance | Engage if regulatory reporting is required |
| Legal / Finance | Engage immediately for confirmed BEC payment fraud |

---

## 14. Regulatory Reporting Considerations

| Trigger | Action |
|--------|--------|
| Customer or regulated data exposed | Notify Compliance and assess reporting obligations |
| Confirmed fraud affecting regulated client or BFSI operations | Assess RBI / CERT-In reporting |
| Material business disruption or financial fraud | Notify Legal, Management, and Compliance |
| MSSP client impacted | Notify client per SLA and contract terms |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 15. Evidence Collection Requirements

| Evidence Type | Priority | Notes |
|--------------|----------|-------|
| Original email with full headers | Critical | Export as EML or MSG |
| Mail gateway logs | Critical | Delivery, block, click, and attachment activity |
| Proxy / Web logs | Critical | URL visits and phishing page access |
| Azure AD / Entra ID logs | Critical | Sign-ins, MFA events, risky sign-ins |
| Mailbox audit logs | Critical | Inbox rule changes, delegates, sends, deletes |
| Inbox rules / forwarding config | High | Preserve before remediation |
| OAuth consent logs | High | Review new or suspicious app grants |
| Attachment sample | High | Preserve for malware analysis |
| SIEM correlated events | High | Include timeline of user and mailbox activity |
| Financial system records | High | If BEC payment fraud suspected |

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 16. Related Documents

| Document | Path |
|---------|------|
| Phishing Master Playbook | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Master.md` |
| L1 Triage Playbook | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L1-Triage.md` |
| L2 Investigation Playbook | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L2-Investigation.md` |
| L3 Forensics Playbook | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L3-Forensics.md` |
| BEC Detection and Analysis | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-BEC-Detection-Analysis.md` |
| Containment Playbook | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Containment.md` |
| Eradication Playbook | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Eradication.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-MITRE-Mapping.md` |
| P2 High Definition | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P2-High-Definition.md` |
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