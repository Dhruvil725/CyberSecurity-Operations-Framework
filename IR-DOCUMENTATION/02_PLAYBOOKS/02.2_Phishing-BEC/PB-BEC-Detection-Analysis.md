# Playbook: Business Email Compromise – Detection and Analysis

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – BEC Detection and Analysis |
| Document ID | IR-PB-PHB-005 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | L2 SOC Lead / Threat Intelligence Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 BEC incident |

---

## 2. Purpose

This document defines the detection and analysis procedures specifically
for Business Email Compromise (BEC) incidents. While the L1, L2, and L3
playbooks cover the full phishing and BEC response lifecycle, this document
provides dedicated, in-depth detection logic, behavioral indicators, and
analysis methodology focused specifically on BEC scenarios.

BEC differs from standard phishing in that:
- it does not always require malware or malicious links
- it relies on trust, impersonation, and social engineering
- it can originate from a legitimately compromised account (not a spoofed one)
- it targets business processes (payments, HR data, vendor relationships)
- financial losses can occur within hours of initial compromise

This document is used alongside:
- `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L2-Investigation.md`
- `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L3-Forensics.md`

---

## 3. Scope

Applies to:
- BEC incidents involving financial fraud (wire transfer, invoice fraud, payroll diversion)
- BEC involving vendor or supply chain impersonation
- executive impersonation (CEO fraud, CFO fraud)
- internal account takeover used to commit BEC internally
- BEC targeting MSSP-managed client environments (with strict segregation)

---

## 4. BEC Classification and Scenario Types

Understanding the BEC scenario type is critical because each type
has different detection signals, urgency levels, and required actions.

| BEC Type | Description | Primary Target | Urgency |
|----------|-------------|----------------|---------|
| CEO / Executive Fraud | Attacker impersonates CEO/CFO/COO to request urgent payment or gift cards | Finance team / Executive assistants | Critical |
| Vendor / Supplier Impersonation | Attacker impersonates a known vendor to change banking details or send fraudulent invoices | Accounts Payable / Procurement | Critical |
| Payroll Diversion | Attacker impersonates employee and requests payroll bank account change | HR / Payroll team | Critical |
| Attorney / Legal Impersonation | Attacker impersonates a legal representative to demand confidential transfer or data | Finance / Executives | High |
| Internal Account Takeover BEC | Legitimate compromised account sends BEC emails from inside the organization | Finance / HR / Vendor contacts | Critical |
| Data Theft BEC | BEC used to request sensitive data (W2s, employee PII, IP) rather than money | HR / Finance / Legal | High |

---

## 5. BEC Detection Sources and Signals

BEC detection requires correlation across multiple sources simultaneously.
Relying on a single source will result in missed incidents.

### 5.1 Email Gateway Detection Signals

| Signal | Description | Confidence |
|--------|-------------|------------|
| Display Name Spoofing | From name matches executive but email domain is external or lookalike | High |
| Reply-To Mismatch | Reply-To header points to a different domain than the From address | High |
| Lookalike Domain | Domain uses typosquatting such as micros0ft.com or company-finance.com | High |
| SPF / DKIM / DMARC Fail | Email fails authentication checks for the claimed sending domain | Medium-High |
| New Sending Domain | Domain registered within the last 30 days | Medium |
| No Prior Communication | Sender has never communicated with the recipient before | Medium |
| Language and Urgency Patterns | Keywords present: urgent, confidential, do not discuss, wire today | Medium |

### 5.2 Identity and IAM Detection Signals

| Signal | Description | Confidence |
|--------|-------------|------------|
| Impossible Travel | Successful login from two geographically distant locations within an impossible timeframe | High |
| Unfamiliar Device or Browser | Login from device or client app not previously associated with user | High |
| New MFA Device Enrolled | MFA device registered immediately after or during suspicious login period | High |
| Sign-in from Attacker Infrastructure | Login from known VPN/Proxy/VPS provider such as DigitalOcean, Mullvad, or Tor | High |
| OAuth App Consent Granted | New application granted Mail.ReadWrite, Mail.Send, or Calendars.Read permissions | High |
| Password Reset Initiated | Self-service or admin password reset outside normal patterns | Medium |

### 5.3 Mailbox Behavioral Detection Signals

| Signal | Description | Confidence |
|--------|-------------|------------|
| Inbox Rule Created | New rule that forwards, deletes, or moves emails matching specific keywords | High |
| External Forwarding Active | All incoming or outgoing emails forwarded to external address | Critical |
| Mass Outbound Emails | Large volume of emails sent from account in short window | High |
| Sensitive Keyword Search | Attacker searched mailbox for invoice, payment, wire, bank using MailItemsAccessed audit log | High |
| Sent Emails Not in Sent Folder | Attacker deleted sent items or used Graph API to send without creating a sent items trace | High |
| Delegate Permission Added | New mailbox delegate or Send As permission granted without authorization | High |

### 5.4 Financial Process Detection Signals

| Signal | Description | Confidence |
|--------|-------------|------------|
| Sudden Bank Account Change Request | Vendor requests change of banking details via email only with no secondary verification | High |
| Payment Urgency Outside Normal Process | Payment request bypasses normal approval workflow | High |
| Duplicate Invoice with Changed Account | Same invoice number submitted but with different banking details | High |
| Out-of-Hours Payment Request | Wire transfer requested on weekend or public holiday | Medium |
| Unusual Payee or Country | Payment to new payee or unusual country not previously transacted with | High |

---

## 6. BEC Detection Use Cases (SIEM Rules and Alert Logic)

These represent the core SIEM or email security platform detection logic
that should be configured to detect BEC scenarios. Each use case includes
the rule logic written in plain-language pseudocode format for implementation
across any SIEM platform.

### 6.1 Use Case BEC-001: Reply-To Domain Mismatch

| Field | Detail |
|-------|--------|
| Alert Name | BEC-001 Reply-To Domain Mismatch Detected |
| Severity | Medium |
| Action | L1 Review |

Detection Logic:

- Condition 1: email.from_domain matches a known internal or trusted domain
- Condition 2: email.reply_to_domain does not match email.from_domain
- Condition 3: email.reply_to_domain is not in the approved external domains list
- Result: Generate alert BEC-001

Investigation Focus:
- confirm whether the Reply-To domain is a lookalike or attacker-controlled domain
- check if the recipient replied to the email
- if recipient replied, escalate immediately to L2

---

### 6.2 Use Case BEC-002: Impossible Travel Detection

| Field | Detail |
|-------|--------|
| Alert Name | BEC-002 Impossible Travel Detected |
| Severity | High |
| Action | L2 Review Immediately |

Detection Logic:

- Condition 1: user has a successful login from location A at timestamp 1
- Condition 2: user has a successful login from location B at timestamp 2
- Condition 3: geographic distance between location A and location B exceeds 500 km
- Condition 4: time difference between timestamp 1 and timestamp 2 is less than 60 minutes
- Result: Generate alert BEC-002

Investigation Focus:
- confirm whether both logins belong to the same user
- identify the IP addresses and hosting providers for both logins
- determine whether MFA was satisfied for both logins or bypassed
- revoke suspicious session pending investigation

---

### 6.3 Use Case BEC-003: Suspicious Inbox Rule Created

| Field | Detail |
|-------|--------|
| Alert Name | BEC-003 Suspicious Inbox Rule Created |
| Severity | High |
| Action | L2 Review Immediately; disable rule pending investigation |

Detection Logic:

- Condition 1: mailbox_audit_log.operation equals New-InboxRule or UpdateInboxRule
- Condition 2 (any one of the following must match):
  - rule condition contains any of: invoice, payment, bank, wire, transfer, security, alert
  - rule action is ForwardTo with an external email address
  - rule action is Delete or MoveToFolder with deletion destination
- Result: Generate alert BEC-003

Investigation Focus:
- identify when the rule was created and from which IP and device
- determine if the rule creation coincides with a suspicious login event
- disable the rule immediately pending investigation
- run full mailbox audit to check for additional persistence mechanisms

---

### 6.4 Use Case BEC-004: Suspicious OAuth Application Consent

| Field | Detail |
|-------|--------|
| Alert Name | BEC-004 Suspicious OAuth Consent Granted |
| Severity | High |
| Action | L2 Review; revoke consent pending investigation |

Detection Logic:

- Condition 1: azure_ad_audit.operation equals Consent to application
- Condition 2: application.permissions contains any of: Mail.ReadWrite, Mail.Send, offline_access, Calendars.ReadWrite
- Condition 3: application.publisher is not in the approved vendor application list
- Result: Generate alert BEC-004

Investigation Focus:
- identify which user consented and from which session
- check if the session was suspicious (new IP, new device, post-phishing click)
- review what data the application has accessed since consent was granted
- revoke consent immediately and monitor for continued access attempts

---

### 6.5 Use Case BEC-005: External Mail Forwarding Enabled

| Field | Detail |
|-------|--------|
| Alert Name | BEC-005 External Mail Forwarding Enabled |
| Severity | Critical |
| Action | Disable forwarding immediately; L2 escalation |

Detection Logic:

- Condition 1: mailbox_audit_log.operation equals Set-Mailbox
- Condition 2: modified parameter is ForwardingSMTPAddress
- Condition 3: new value is an external email address not in approved list
- Result: Generate alert BEC-005

Investigation Focus:
- identify who made the forwarding change and from which session
- determine how long forwarding has been active and what emails were forwarded
- disable the forwarding rule immediately
- review MailItemsAccessed audit log to assess what data was exfiltrated

---

### 6.6 Use Case BEC-006: Mass Outbound Email from Single Account

| Field | Detail |
|-------|--------|
| Alert Name | BEC-006 Mass Outbound Email Detected |
| Severity | High |
| Action | L1 Triage; SOC Lead notification |

Detection Logic:

- Condition 1: outbound email count from a single user account exceeds 50 emails
- Condition 2: all emails sent within a 30-minute window
- Condition 3: recipient list includes external domains
- Result: Generate alert BEC-006

Investigation Focus:
- review content of sent emails to determine if they are phishing or BEC lures
- confirm whether the account holder initiated the sending or if the account is compromised
- if compromise suspected, revoke session and escalate to L2 immediately

---

### 6.7 Use Case BEC-007: Sign-in from Known Attacker Infrastructure

| Field | Detail |
|-------|--------|
| Alert Name | BEC-007 Login from Attacker Infrastructure |
| Severity | High |
| Action | L2 Immediate; revoke session pending investigation |

Detection Logic:

- Condition 1: user has a successful login event
- Condition 2: source IP address is present in threat intelligence feed for VPS, Proxy, or Tor exit nodes
- Condition 3: MFA challenge was not re-issued (session token reused indicating possible AiTM)
- Result: Generate alert BEC-007

Investigation Focus:
- identify all actions taken during the suspicious session
- check for inbox rule creation, mail forwarding, OAuth consent, and data access
- revoke all active sessions and tokens immediately
- escalate to L3 if AiTM token theft is suspected

---

## 7. BEC Investigation Decision Tree

Use this decision tree when any BEC alert fires or a BEC report is received.
Follow each branch in order and document the outcome at each decision point in the ticket.

**Start: BEC Alert or User Report Received**

| Step | Question | Yes Path | No Path |
|------|----------|----------|---------|
| 1 | Is the email from an external domain impersonating an internal person? | Confirm spoofing via header analysis. Block sender and domain. Check if user replied or took action. If action taken proceed to Step 3. | Proceed to Step 2 |
| 2 | Is the email from a legitimate but compromised internal account? | Escalate to L2 immediately. Begin mailbox forensics. Revoke sessions pending investigation. Proceed to Step 3. | Proceed to Step 3 |
| 3 | Did the target user take any action (reply, approve payment, change banking details, share data)? | Escalate IMMEDIATELY to SOC Lead, Finance, and Management. Proceed to Step 4. | Continue monitoring. Document and educate user. Close or downgrade severity. |
| 4 | Has money already moved (wire transfer completed or payment processed)? | Declare P1 Major Incident. Engage Legal and Bank Fraud Team. Preserve all evidence. Notify CISO. | Place immediate hold on pending payment. Escalate to Finance Controller. Document payment details. |
| 5 | Is there evidence of mailbox access from an unusual IP or device? | Treat as confirmed Account Takeover BEC. L2 investigation mandatory. Full mailbox audit required. Proceed to Phase 3 analysis. | Lower risk profile. Document all findings. Continue monitoring for 72 hours. |

---

## 8. BEC Analysis Workflow (Detailed)

### Phase 1: Confirm BEC Type and Entry Point

Actions:
- classify the BEC scenario type using Section 4 of this document
- determine whether the origin is one of the following:
  - External spoofed account: no actual compromise; attacker only impersonates the person
  - Lookalike domain: threat actor registered a visually similar domain
  - Legitimate compromised internal account: highest risk scenario; treat as full account takeover

| Entry Point Type | Key Evidence | Required Action |
|-----------------|--------------|-----------------|
| External Spoofed | SPF/DKIM fail; Reply-To mismatch confirmed | Block sender and domain; no credential reset needed for victim |
| Lookalike Domain | WHOIS shows new domain registration; visual similarity to legitimate domain | Block domain; submit to gateway blocklist; user awareness |
| Compromised Internal Account | Successful login from unusual IP; inbox rules created; session anomalies | Full L2 mailbox and identity investigation; revoke sessions immediately |

---

### Phase 2: Financial Impact Triage (Time-Critical)

This phase must happen in parallel with the technical investigation for any
BEC incident involving a payment request, invoice, or banking change.
Do not wait for technical investigation to complete before engaging Finance.
Every minute of delay increases the risk of irreversible financial loss.

Actions:
- contact Finance Controller or Accounts Payable team immediately via phone only (not email)
- confirm answers to the following questions and document in the ticket:

| Question | Answer Required | If Yes - Immediate Action Required |
|---------|-----------------|-----------------------------------|
| Was a wire transfer or payment already processed? | Yes / No / Unknown | Declare P1; attempt wire recall via bank; engage Legal immediately |
| Is a payment currently pending approval or in queue? | Yes / No | Place immediate hold; escalate to Finance Controller and Management |
| Were banking details changed for any vendor or employee account? | Yes / No | Revert change immediately; verify all recent payments to that account number |
| Was sensitive data requested and sent (W2 forms, employee PII, IP)? | Yes / No | Assess data exposure; activate regulatory notification assessment immediately |

---

### Phase 3: Mailbox and Identity Deep Analysis

Performed by L2 or L3 depending on incident severity and technical complexity.

Actions:
- run full mailbox audit log review covering the 72 hours prior to incident detection

| Audit Operation | What It Reveals | Investigation Priority |
|----------------|-----------------|------------------------|
| MailItemsAccessed | Exactly which emails the attacker read; requires E5 or Audit Premium license | Critical |
| UpdateInboxRules | When rules were created, conditions set, and actions configured | Critical |
| SendAs or Send on Behalf | Whether attacker sent emails while impersonating the victim | Critical |
| AddMailboxPermission | Delegate access granted by attacker to maintain persistent access | High |
| Set-Mailbox ForwardingSMTPAddress | External SMTP forwarding configured to exfiltrate emails | Critical |
| New-InboxRule | Full rule creation details including filter conditions and action details | Critical |

- review Azure AD or identity platform sign-in logs for the compromise window:
  - identify exact attacker session start time and total session duration
  - identify all attacker IPs, geographic locations, devices, and user-agents used
  - determine whether MFA was bypassed through AiTM token theft or was simply not enforced
  - identify all Graph API calls made during attacker session to detect automated data scraping
  - check for new MFA device registrations or authentication method changes made by attacker

- review OAuth application grants for the compromise window:
  - identify all applications consented to during the compromise window
  - check permissions scope including read, send, delete, and offline access
  - check whether the app publisher is verified and appears in known vendor list
  - revoke any unrecognized or suspicious application consents immediately

---

### Phase 4: Scope and Lateral BEC Assessment

Actions:
- determine whether the compromised mailbox was used by the attacker to:
  - send additional BEC emails to other internal employees targeting Finance or HR
  - contact external vendors or clients while impersonating the victim
  - access shared calendars or SharePoint sites to gather targeting intelligence
  - access shared mailboxes via delegate permissions added during the compromise window
- search outbound email gateway logs for unusual sending patterns from the compromised account
- check whether the attacker pivoted to additional accounts using information gathered from the compromised mailbox

| Scope Indicator | Evidence Source | Action Required |
|----------------|-----------------|-----------------|
| Emails sent to Finance from compromised account | Sent items and mail flow logs | Notify Finance immediately; verify no action taken on any request |
| Emails sent to vendors from compromised account | Outbound gateway logs | Notify vendor immediately using a verified phone number; not email |
| Access to shared Finance or HR mailboxes detected | Audit logs for shared mailboxes | Extend scope of full investigation to all shared mailboxes accessed |
| Calendar access indicating attacker reconnaissance | Calendar audit logs | Assess what scheduling and meeting information was gathered for targeting |

---

## 9. Evidence Requirements for BEC Incidents

BEC incidents frequently carry legal, regulatory, and financial consequences.
Evidence must be collected and preserved to the highest standard from the
earliest possible point in the investigation.

### 9.1 Minimum Evidence for All BEC Incidents

| Evidence Item | Source | Preservation Method |
|--------------|--------|---------------------|
| Original email with full headers | Email gateway or affected mailbox | Export as .eml format; do not forward as forwarding alters headers |
| Sender domain WHOIS records | WHOIS lookup tool | Screenshot and export with investigation timestamp |
| Email gateway delivery logs | Gateway admin console | Full log export covering the complete date range of the incident |
| User interaction confirmation | User statement and proxy logs | Written user statement and log export both required |

### 9.2 Additional Evidence for P1 and P2 BEC Incidents

| Evidence Item | Source | Preservation Method |
|--------------|--------|---------------------|
| Full mailbox audit log export | Compliance Center or PowerShell | Export CSV with all operations for the full investigation window |
| Sign-in logs for compromised account | Azure AD or IAM Platform | Export with IP address, device ID, timestamp, and MFA status for each event |
| Wire transfer or payment request emails | Mailbox and Finance records | Preserve complete email chain; do not delete any related emails |
| Banking change request documentation | AP and Vendor records | Preserve original account records and any changed account details |
| OAuth consent grant records | Azure AD Audit Logs | Export with timestamps, application names, and full permission scopes |
| Chain of custody form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md` | Complete for every evidence item collected in P1 incidents |

---

## 10. Containment Actions (BEC-Specific)

| Finding | Containment Action | Urgency | Approver |
|--------|-------------------|---------|---------|
| External forwarding rule active | Disable forwarding rule immediately | Immediate | SOC Lead |
| Inbox rules hiding security alerts or replies | Remove all suspicious rules | Immediate | SOC Lead |
| Compromised account with active session | Revoke all active sessions and refresh tokens | Immediate | SOC Lead |
| OAuth app with mail read or send permissions | Revoke OAuth consent for suspicious application | Immediate | IAM Team |
| Known attacker IP identified | Block IP at firewall and proxy layers | Within 30 minutes | SOC Lead |
| Vendor banking details changed by attacker | Revert to verified details via phone confirmation only | Immediate | Finance and SOC Lead |
| Payment pending in approval queue | Place immediate hold on payment | Immediate | Finance Controller |
| Payment already completed and funds transferred | Notify bank fraud department and legal counsel | Within 1 hour | Finance and Legal |
| Unauthorized delegate permission added | Remove delegate access | Immediate | Email Admin |
| Suspicious OAuth application still active | Revoke consent and disable application | Immediate | IAM Team |

Reference:
`02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Containment.md`

---

## 11. Regulatory and Legal Notification Triggers

BEC incidents may trigger mandatory regulatory or legal obligations.
GRC and Legal must be engaged as early as possible for all P1 and P2 incidents.
Do not wait for investigation completion before making initial regulatory contact.

| Trigger Condition | Notification Required | Timeframe |
|------------------|----------------------|-----------|
| Confirmed financial loss from BEC | Legal Counsel and Management | Immediately |
| Customer or vendor PII accessed or exfiltrated | GRC / Compliance and Legal | Within 4 hours of confirmation |
| Regulatory-covered data involved such as banking or healthcare PII | Compliance Team and Legal | As per applicable regulatory SLA |
| Law enforcement referral required for large financial loss | Legal Counsel decision and direction | Legal-directed timeline |
| RBI-regulated client or environment impacted | RBI incident reporting SOP activation | Per RBI circular timelines |
| ISO 27001 notifiable security event | ISO 27001 incident log update and notification | Per ISMS incident management procedure |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/ISO27001-Incident-Notification.md`

---

## 12. Common BEC Detection and Analysis Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Treating BEC as low priority because no malware is involved | Active financial fraud missed or delayed | BEC carries highest financial impact; treat with P1 urgency whenever any payment is involved |
| Only reviewing the reported email without checking sent items | Missing attacker activity conducted from the compromised account | Always review full sent items and outbound mail logs for minimum 72 hours prior to detection |
| Not checking for hidden inbox rules | Ongoing persistence and email forwarding missed entirely | Always use PowerShell with -IncludeHidden flag; the GUI does not surface hidden rules |
| Assuming MFA fully protects against BEC | AiTM token theft scenarios completely missed | Always verify sign-in logs for session anomalies even when MFA was reportedly enforced |
| Delaying Finance notification to complete full technical investigation first | Payment completed and funds transferred before hold is placed | Contact Finance immediately in parallel with investigation; never wait for technical closure |
| Not preserving original email in EML format for legal proceedings | Headers altered; weak or inadmissible legal evidence | Always export as EML format; forwarding an email permanently alters the original headers |
| Revoking sessions without coordinating with IT Ops | Legitimate users locked out causing operational disruption | Always coordinate with SOC Lead and IT Ops before executing any mass session revocation |
| Not auditing OAuth consents during investigation | Attacker retains persistent mailbox access via rogue application | Always audit all OAuth application consents granted during the full compromise window |

---

## 13. MSSP Client Handling Notes

For BEC incidents occurring in MSSP-managed client environments:
- financial fraud findings must be escalated to the client SDM immediately without any delay
- do not contact client finance teams directly; all communication must be routed via SDM
- regulatory notification obligations rest with the client organization; SOC provides evidence and timeline support only
- all evidence must remain strictly client-scoped and stored in client-designated secure locations
- BEC financial loss is always treated as client P1 regardless of the MSSP internal severity classification
- document all client communications, approvals, and decisions formally in the incident ticket
- provide the client with a business-language summary of technical findings suitable for their executive team

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

---

## 14. Related Documents

| Document | Path |
|---------|------|
| Phishing Master | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Master.md` |
| L1 Triage | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L1-Triage.md` |
| L2 Investigation | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L2-Investigation.md` |
| L3 Forensics | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L3-Forensics.md` |
| Containment | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Containment.md` |
| Eradication | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Eradication.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-MITRE-Mapping.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Chain of Custody Master Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md` |
| RBI Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md` |
| Legal Counsel Engagement | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| ISO 27001 Incident Notification | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/ISO27001-Incident-Notification.md` |
| MSSP Multi-Client Handling | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md` |
| MSSP Client Responsibility Matrix | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md` |

---

## 15. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | L2 SOC Lead / Threat Intel Lead | Initial version |

---

## 16. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**