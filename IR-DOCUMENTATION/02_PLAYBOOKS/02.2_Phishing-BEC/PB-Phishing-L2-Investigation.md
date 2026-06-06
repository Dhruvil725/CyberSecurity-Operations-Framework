# Playbook: Phishing and BEC – L2 Investigation

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Phishing and BEC (L2 Investigation) |
| Document ID | IR-PB-PHB-003 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | L2 SOC Analyst / SOC Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 phishing or BEC incident |

---

## 2. Purpose

This document defines the L2 SOC Analyst procedure for investigating
phishing and Business Email Compromise (BEC) incidents escalated from L1.

L2 investigation covers:
- confirmation of scope (single user vs campaign)
- credential and session compromise determination
- mailbox compromise and persistence identification
- BEC financial fraud assessment and urgent escalation
- endpoint execution confirmation (if attachment-based)
- IOC enrichment and blocking recommendations
- escalation decision to L3 or IR Team with documented justification

L2's objective is to definitively determine:
- what happened and to which users/systems
- whether credentials, sessions, or mailboxes are compromised
- whether financial fraud is active, completed, or not detected
- what immediate containment actions are required
- whether L3 or IR Team must be engaged

---

## 3. Scope

Applies to:
- confirmed phishing with user interaction escalated from L1
- suspected or confirmed credential compromise via phishing
- BEC incidents involving financial fraud, payment redirection, or vendor impersonation
- bulk phishing campaigns targeting multiple users
- OAuth consent abuse and token theft indicators
- enterprise and MSSP client environments (client evidence segregation required)

---

## 4. L2 Safety Rules

1. Do not detonate attachments or click URLs outside approved sandbox workflows.
2. Do not reset credentials or revoke tokens without SOC Lead approval or defined authorization.
3. Do not contact finance, legal, or external parties directly; route via SOC Lead.
4. Do not store evidence in shared or cross-client locations in MSSP environments.
5. Do not make containment changes in client environments without documented approval.

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

---

## 5. L2 SLA Targets (Phishing/BEC)

| Severity | L2 Investigation Start | First Finding Update | Escalation Target |
|----------|------------------------|----------------------|-------------------|
| P1 | Immediately on receipt | 15 minutes | IR Team + SOC Lead immediately |
| P2 | Within 15 minutes | 30 minutes | SOC Lead immediately; L3 if required |
| P3 | Within 30 minutes | 60 minutes | L3 or SOC Lead if scope expands |
| P4 | Within 2 hours | End of shift | Close or downgrade with justification |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 6. Inputs Required from L1 (Minimum Before L2 Begins)

L2 must confirm the following data is present in the ticket before starting.
If missing, request from L1 immediately and note the gap.

### 6.1 Email Evidence (Mandatory)

| Evidence Item | Expected Detail | Present in Ticket |
|---------------|-----------------|-------------------|
| Full email headers | Raw headers including Received, Return-Path, Reply-To | Yes / No |
| Preserved email sample | EML or MSG format preferred | Yes / No |
| Sender address and display name | Exact values, not summarized | Yes / No |
| All URLs extracted | Including rewritten or gateway-modified URLs | Yes / No |
| Attachment names and hashes | If applicable | Yes / No / NA |
| Email gateway disposition | Blocked / Quarantined / Delivered | Yes / No |
| Recipient list | All known recipients | Yes / No |

### 6.2 User Interaction Status (Mandatory)

| Interaction Level | Confirmed by L1 | Notes |
|-------------------|-----------------|-------|
| No interaction (delivered only) | Yes / No | |
| Opened only | Yes / No | |
| Clicked link | Yes / No | |
| Downloaded attachment | Yes / No | |
| Attachment executed | Yes / No | |
| Credentials entered | Yes / No | |
| MFA prompt received unexpectedly | Yes / No | |
| User unsure / unknown | Yes / No | Treat as suspicious; escalate scope |

### 6.3 User and Asset Context (Mandatory)

- affected user name and email address
- user role (finance / executive / admin / privileged / standard)
- endpoint name and IP (if known)
- whether endpoint has EDR agent (yes / no / unknown)
- initial severity recommendation from L1 and justification

### 6.4 BEC Context (If Reported)

- impersonated party (CEO / CFO / vendor / other)
- requested action (wire transfer / banking change / gift card / data request)
- financial amount and stated urgency (if present)
- whether funds were transferred, pending, or not yet initiated

---

## 7. L2 Investigation Objectives and Required Outputs

### 7.1 Objectives

1. Confirm phishing campaign scope (single user vs multiple targets)
2. Determine if credentials were harvested or sessions were hijacked
3. Determine if BEC financial activity occurred or is actively pending
4. Identify malicious payload behavior and endpoint execution (if attachment-based)
5. Map attacker infrastructure including URLs, domains, IPs, and redirect chains
6. Assess mailbox compromise indicators (rules, forwarding, delegates, OAuth grants)
7. Enrich IOC list for containment team
8. Provide documented escalation decision to L3 or IR Team

### 7.2 Required Outputs (Minimum)

| Output Item | Required For | Notes |
|-------------|--------------|-------|
| Confirmed scope (users, systems, accounts) | All incidents | |
| Credential and session compromise determination | All P2+ incidents | |
| BEC financial fraud status | All BEC incidents | Active / Completed / Not Detected |
| Enriched IOC list with blocking recommendations | All incidents | |
| Mailbox persistence assessment | All P2+ incidents | |
| Escalation decision with justification | All incidents | |
| Updated incident timeline | All incidents | |
| Containment recommendations documented in ticket | All P2+ incidents | |

---

## 8. Step-by-Step L2 Investigation Procedure

---

### Step 1: Email Header and Infrastructure Analysis

Actions:
- obtain full email headers in raw format
- analyze the following:

| Header Field | What to Check | Indicator of Concern |
|-------------|---------------|----------------------|
| Return-Path vs From | Mismatch between return and display | Spoofing indicator |
| Reply-To | Points to different domain | Classic BEC indicator |
| Received headers | Trace the actual sending path | Unusual relay chains |
| X-Originating-IP | Verify alignment with sender org | Third-party send platform abuse |
| SPF / DKIM / DMARC | Check pass/fail/softfail results | Fail or softfail indicates spoofing |
| Message-ID / X-Mailer | Generic or mismatched values | Bulk sender or phishing kit indicator |

- perform domain and IP enrichment:
  - WHOIS registration date (newly registered domains are high risk)
  - hosting provider and ASN
  - MX record alignment check
  - domain similarity to legitimate domains (typosquatting check)
- verify email gateway logs for delivery confirmation and full recipient list

Outputs:
- sending infrastructure profile documented in ticket
- domain and IP reputation assessment
- confirmed full recipient list

---

### Step 2: URL and Link Analysis

Actions:
- extract all URLs including any gateway-rewritten versions
- use approved sandbox or URL analysis tools (do not click directly)
- analyze the full redirect chain:

| Step | What to Record |
|------|----------------|
| Initial URL | As received in email |
| Intermediate redirects | Each hop in the chain |
| Final landing page | Domain, category, content type |
| Credential harvest indicators | Login form, brand impersonation, certificate status |

- check URL reputation against threat intelligence platforms
- review proxy and web gateway logs for user click history and access timestamp

Key questions to answer:
- did any user access the URL?
- is the phishing kit still active at time of investigation?
- did the user reach a credential harvesting page?

Outputs:
- full URL redirect chain documented
- click confirmation with user list and timestamps
- landing page characterization

---

### Step 3: Attachment Analysis (If Applicable)

Actions:
- obtain attachment sample safely from email gateway quarantine
- record file hash (SHA256 and MD5)
- check hash against threat intelligence sources
- submit to approved sandbox for detonation
- review sandbox output:

| Sandbox Indicator | Significance |
|-------------------|--------------|
| Files dropped and paths | Identifies persistence mechanisms |
| Processes spawned | Identifies execution chain |
| Registry or scheduled task changes | Identifies host persistence |
| Network connections initiated | Identifies C2 destinations |
| C2 domains or IPs contacted | Identifies attacker infrastructure |

- cross-reference with EDR telemetry to confirm execution on user endpoint

Outputs:
- attachment behavior profile documented
- execution confirmation (yes / no / unknown)
- additional IOCs from attachment analysis added to IOC list

---

### Step 4: User and Credential Compromise Assessment

Actions:
- identify all users who received the phishing email
- identify users who clicked the link using proxy and gateway logs
- identify users who submitted credentials where detectable
- review identity and sign-in logs for:

| Log Indicator | What to Look For | Significance |
|---------------|------------------|--------------|
| Successful login after phishing delivery | New IP or geolocation | Possible credential use by attacker |
| Sign-in from new device or browser | Device not seen before | New access method |
| Impossible travel | Legitimate location then attacker location within minutes | High confidence compromise |
| MFA prompt anomalies | MFA push sent at unusual time without user initiating | MFA fatigue attempt |
| Token-based sign-in after credential submission window | Refresh token use without MFA | AiTM session hijacking indicator |

- check for Adversary-in-the-Middle indicators:
  - session cookie theft patterns
  - attacker IP matching known phishing kit hosting infrastructure
  - simultaneous sign-ins from user location and attacker location

Outputs:
- confirmed compromised accounts list
- suspected compromised accounts list
- credential and session compromise confidence level (Confirmed / Likely / Possible)

---

### Step 5: Mailbox Compromise Assessment

For any confirmed or suspected compromised account:

Actions:
- review mailbox audit logs and check:

| Mailbox Area | What to Check | Malicious Indicator |
|--------------|---------------|---------------------|
| Inbox rules | New rules created after compromise window | Forwarding to external address; delete or move rules hiding security replies |
| Sent items | Emails sent from compromised account | Internal phishing; vendor fraud; payment requests |
| Deleted items | Evidence of tampering or cleanup | Deleted security emails or warnings |
| OAuth and application consent | New consents granted | Suspicious app with mail read or send permissions |
| Mailbox delegation | New delegates added | Unauthorized access granted |
| External forwarding | Active forwarding rules | Data exfiltration path |

- check for transport rules or connectors modified at tenant level (admin-level compromise indicator)

Outputs:
- mailbox compromise indicators documented (Confirmed / Suspected / Not Detected)
- forwarding rule details and removal status
- OAuth consent anomalies and revocation status

---

### Step 6: BEC Financial Fraud Assessment

If BEC indicators are present:

Actions:
- identify the impersonated party (executive / finance lead / vendor)
- review sent items and email chain for:
  - payment redirection requests
  - invoice modification
  - wire transfer instructions
  - vendor banking detail changes
- coordinate with SOC Lead to engage Finance team:
  - confirm whether any payment instructions were received from the affected account
  - confirm whether any payments are processed or still pending
  - confirm whether banking details were changed for any vendor
- check BEC email chain for:
  - urgency and secrecy language
  - domain lookalike in Reply-To
  - thread hijacking indicators

| BEC Status | Definition | Required Action |
|-----------|-----------|-----------------|
| Confirmed fraud completed | Funds transferred | P1; escalate immediately to management, finance, and legal |
| Fraud pending | Payment instruction pending; not yet executed | Stop payment immediately; escalate to management and finance |
| Fraud attempted | Instructions sent; no payment yet | Escalate to SOC Lead; document fully |
| Not detected | No financial request found | Continue investigation; document and close BEC thread |

Outputs:
- BEC fraud status documented
- financial impact assessment
- urgent escalation flag raised if payment is pending or completed

---

### Step 7: Scope Expansion Check

Actions:
- search email gateway for other emails from the same sender or infrastructure within previous 72 hours
- check if phishing email was forwarded internally by any user
- search SIEM for other users with similar sign-in anomalies in the same window
- check proxy logs for other users who accessed the same phishing URL or destination
- check EDR for payload execution on other endpoints

Outputs:
- confirmed total scope (number of users, systems, accounts affected)
- additional IOCs discovered during scope expansion
- updated ticket with expanded scope confirmed

---

### Step 8: IOC Enrichment and Blocking Recommendations

Compile the full enriched IOC list for the containment team:

| IOC Type | Value | Source | Confidence | Recommended Blocking Action |
|---------|-------|--------|-----------|---------------------------|
| Sender email domain | | Email header | | Block in email gateway |
| Phishing URL | | Email body | | Block in proxy and DNS |
| Hosting IP address | | URL resolution | | Block in firewall |
| Attachment file hash | | Sandbox analysis | | Block in EDR |
| Reply-To address | | Email header | | Block or monitor in gateway |
| C2 domain or IP | | Sandbox or EDR output | | Block in DNS and firewall |
| Redirect domain | | URL chain analysis | | Block in proxy |

Submit blocking requests via:
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md`

---

## 9. Escalation Decision Criteria

### 9.1 Escalate to L3 if:

| Condition | Reason |
|-----------|--------|
| Confirmed credential compromise with active attacker session | Advanced token and session analysis required |
| AiTM session hijacking suspected | Specialized protocol and log analysis required |
| Confirmed mailbox compromise with evidence of lateral phishing | Multi-account scope; complex forensics |
| Payload execution confirmed on endpoint | Host forensics and malware analysis required |
| Cloud environment compromise suspected | Cloud-specific forensic capability required |
| Multiple accounts compromised across the organization | Scope and hunting beyond L2 capacity |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L2-to-L3-Escalation.md`

### 9.2 Escalate to IR Team if:

| Condition | Reason |
|-----------|--------|
| BEC financial fraud confirmed (payment processed) | Major incident; legal and financial response required |
| Executive or privileged account confirmed compromised | High impact; IR Team coordination required |
| Mass phishing campaign with significant confirmed compromise | Incident command required |
| Evidence of intrusion extending beyond email compromise | Cross-domain response required |
| Regulatory notification trigger likely | Compliance and legal engagement required |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L2-to-L3-Escalation.md`
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L3-to-IR-Team-Escalation.md`

---

## 10. Containment Recommendations (L2 Output to SOC Lead)

L2 documents and submits recommendations; execution authority per approval matrix.

| Finding | Containment Recommendation | Approval Required |
|--------|---------------------------|-------------------|
| Credentials confirmed compromised | Reset password and revoke all sessions immediately | SOC Lead |
| Active attacker session detected | Revoke all tokens and sessions; disable account temporarily | SOC Lead |
| Mailbox forwarding rule found | Remove forwarding rule immediately | IAM or Email Admin |
| OAuth consent granted to suspicious app | Revoke application consent | IAM Team |
| Endpoint payload executed | Isolate endpoint via EDR containment | SOC Lead + IT Ops |
| BEC payment pending | Escalate to management and Finance immediately; do not delay | SOC Lead + Management |
| Active phishing kit | Block URL and domain in proxy and DNS | SOC Lead |
| Campaign confirmed multi-user | Purge email from all mailboxes | Email Admin via SOC Lead |

Reference:
`02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Containment.md`

---

## 11. Investigation Documentation Requirements

The following must be documented in the incident ticket before handoff or closure:

| Documentation Item | Status |
|-------------------|--------|
| Investigation timeline with all actions and timestamps | ☐ Complete |
| Email header analysis summary and findings | ☐ Complete |
| URL and attachment analysis results | ☐ Complete |
| User click and credential submission confirmation | ☐ Complete |
| Identity log analysis findings | ☐ Complete |
| Mailbox compromise assessment results | ☐ Complete |
| BEC fraud assessment (if applicable) | ☐ Complete |
| Enriched IOC table with blocking recommendations | ☐ Complete |
| Confirmed scope (users, systems, accounts) | ☐ Complete |
| Escalation decision and justification documented | ☐ Complete |
| Containment recommendations submitted to SOC Lead | ☐ Complete |

---

## 12. Common L2 Mistakes to Avoid

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Stopping investigation after confirming one compromised account | Missing full scope | Always perform scope expansion check |
| Missing mailbox rule and OAuth checks | Attacker persistence remains | Always check rules, delegates, and app consents |
| Confirming click without checking credential entry | Underestimating severity | Always validate credential submission via logs |
| Failing to check for AiTM indicators | Session hijack missed | Always check for impossible travel and token anomalies |
| Not documenting escalation justification | Audit gap; decision unclear | Always document reason for escalation or no escalation |
| Mixing MSSP client evidence | Confidentiality breach | Verify tenant attribution before saving any evidence |
| Delaying BEC financial fraud escalation | Financial loss not stopped | Escalate to SOC Lead and Finance immediately on any payment indicator |

---

## 13. MSSP Client Handling Notes

For MSSP client incidents:
- all evidence must remain scoped to the specific client case only
- client notification must follow client-specific SLA timelines
- financial fraud findings must be escalated to client SDM immediately
- regulatory notification triggers must be communicated to SDM and compliance
- document client approval for any containment actions that have business impact

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`

---

## 14. Related Documents

| Document | Path |
|---------|------|
| Phishing Master | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Master.md` |
| L1 Triage | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L1-Triage.md` |
| L3 Forensics | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L3-Forensics.md` |
| BEC Detection Analysis | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-BEC-Detection-Analysis.md` |
| Containment | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Containment.md` |
| Eradication | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Eradication.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-MITRE-Mapping.md` |
| L2 Investigation SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |
| Firewall Block Request | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md` |
| Escalation Paths | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/` |
| MSSP Multi-Client Handling | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md` |

---

## 15. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | L2 SOC Analyst / SOC Lead | Initial version |

---

## 16. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**