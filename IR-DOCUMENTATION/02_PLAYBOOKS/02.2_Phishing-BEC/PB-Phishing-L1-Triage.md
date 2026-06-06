# Playbook: Phishing and BEC – L1 Triage

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Phishing and BEC (L1 Triage) |
| Document ID | IR-PB-PHB-002 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | SOC Lead / SOC Manager |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 phishing or BEC incident |

---

## 2. Purpose

This document defines the L1 SOC Analyst procedure for triaging phishing
and BEC alerts and user reports. It covers:

- alert validation and qualification (alert vs incident)
- evidence preservation (email artifacts and headers)
- user interaction verification (click/open/credential entry)
- severity recommendation (P1–P4) and escalation triggers
- ticket creation standards and required fields
- MSSP client attribution requirements (if applicable)

L1’s objective is to rapidly determine:
- is this phishing/BEC?
- did any user interact?
- is compromise suspected?
- who must be engaged immediately?

---

## 3. Scope

Applies to:
- secure email gateway alerts (quarantine/delivery)
- user-reported suspicious emails
- SIEM alerts derived from email, proxy, DNS, IAM, and SaaS logs
- BEC impersonation reports from finance/procurement
- OAuth consent suspicious alerts (where visible at L1)

---

## 4. L1 Safety Rules

1. Do not delete the email before preserving evidence.
2. Do not click suspicious links from corporate endpoints.
3. Do not open attachments outside approved sandbox workflows.
4. Do not contact external senders or reply to the phishing email.
5. Do not notify clients directly in MSSP context; escalate to SOC Lead/SDM.

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

---

## 5. L1 SLA Targets (Phishing/BEC)

| Severity (likely) | L1 Triage Target | Escalation Target |
|-------------------|------------------|-------------------|
| P1 | 5 minutes | SOC Lead immediately |
| P2 | 10 minutes | SOC Lead immediately; L2 within 15 minutes |
| P3 | 15 minutes | L2 within 30 minutes if needed |
| P4 | 30 minutes | close or batch per SOP |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 6. Inputs to Collect at L1 (Minimum Required)

### 6.1 Email Artifact Data (Mandatory)
- subject, sender address, display name
- recipient(s) and delivery time
- email gateway disposition (blocked/quarantined/delivered)
- any URLs, domains, and attachment names
- preserve the email in EML/MSG or copy full headers

### 6.2 User Interaction Data (Mandatory)
Confirm one of the following (record explicitly):
- no interaction (delivered only)
- opened only
- clicked link
- downloaded attachment
- attachment opened/executed
- credentials entered (confirmed)
- MFA prompt received (unexpected)
- user unsure (treat as suspicious and escalate to L2)

### 6.3 User and Asset Context (Mandatory)
- impacted user name and email address
- user role (finance/executive/admin/high-risk user)
- endpoint used (if known) for click/open
- whether endpoint is managed and has EDR agent

### 6.4 BEC Context (If Reported)
- impersonated person (CEO/CFO/vendor)
- requested action (wire transfer, banking change, gift card, data request)
- amount and urgency (if financial)
- whether any funds were transferred or pending

---

## 7. Step-by-Step L1 Triage Procedure

### Step 1: Validate Alert Type and Source
Classify the report as one of:
- phishing (generic)
- credential phishing (login lure)
- malware phishing (attachment)
- BEC impersonation (payment or business request)
- suspected mailbox takeover (internal phishing from real account)
- OAuth consent / token abuse indicator (if observed)

If unclear, proceed with phishing category and escalate to L2.

---

### Step 2: Preserve Evidence Immediately
Required actions:
- capture full email headers
- preserve the email sample (EML/MSG if possible)
- record all URLs and attachment names
- capture screenshots only if they do not expose other users/tenants

If MSSP:
- ensure client attribution is correct before saving artifacts
- store evidence only in client-approved evidence location

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

### Step 3: Determine Delivery Scope (Campaign vs Single Target)
Check:
- how many recipients received the email
- whether similar emails exist in the last 24 hours
- whether the sender domain is targeting multiple users

Output required in ticket:
- initial recipient count (known)
- whether it appears to be a campaign (yes/no/unknown)

---

### Step 4: Determine Interaction Status (Most Important Decision Point)
Use available telemetry:
- email gateway click/open tracking (if enabled)
- proxy logs for URL access
- user confirmation
- endpoint telemetry (if available)

Record one interaction outcome (Section 6.2).

---

### Step 5: Apply Severity Recommendation
Use this standard mapping:

| Condition | Severity Recommendation |
|----------|--------------------------|
| confirmed funds transferred or confirmed fraud executed | P1 |
| confirmed mailbox takeover of privileged user / widespread campaign compromise | P1 or P2 (SOC Lead decides) |
| credentials entered on phishing page confirmed | P2 |
| suspicious OAuth consent granted or token abuse suspected | P2 |
| attachment executed or malware suspected | P2 |
| click confirmed but no credential entry confirmed | P3 |
| delivered only, no interaction confirmed | P4 |
| blocked/quarantined before delivery | P4 |

L1 must include justification: “Recommended severity due to: …”.

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

### Step 6: Create/Update Ticket (Mandatory Fields)
Ticket must include:
- incident category: CAT-02
- severity recommendation
- email evidence and interaction evidence
- affected user and role
- actions taken (L1 actions only)
- escalation actions taken and timestamps

Use Section 10 ticket template.

---

### Step 7: Escalate Appropriately
Escalation rules:

- any P2 or above: notify SOC Lead immediately and assign to L2
- any suspected mailbox takeover: escalate to L2 and SOC Lead
- any BEC payment request: notify SOC Lead and Finance (via approved path) immediately
- any confirmed credential entry: escalate immediately to L2 (account compromise risk)
- any suspected malware execution: escalate to L2 and endpoint team

For MSSP:
- SOC Lead/SDM triggers client notification per SLA

---

## 8. L1 Allowed Actions (Without Additional Approval)

L1 may perform:
- evidence preservation and enrichment
- IOC extraction (URLs, domains, sender details, hashes if available)
- blocking request submission (sender/domain/URL) following SOP
- initiating mail purge request (through email admin) via SOC Lead
- notifying affected user to stop interaction (via approved process)

L1 must not:
- reset passwords directly (unless explicitly authorized in environment)
- revoke tokens directly (unless explicitly authorized)
- disable accounts without approval
- instruct finance/vendor actions directly; route via SOC Lead

---

## 9. Evidence to Capture at L1 (Minimum Set)

Attach or reference in ticket:
- email headers (full)
- preserved email sample (EML/MSG) if possible
- URLs and attachment names extracted
- email gateway disposition and delivery details
- user interaction statement (written)
- any proxy log confirming click (if available)

If BEC:
- email chain showing payment request and banking change details

---

## 10. Ticket Notes Template (Copy-Paste Standard)

Title:
- Phishing/BEC suspected – [User/Dept] – [Sender/Domain] – [Severity Recommendation]

Required fields:
- Alert Source:
- Detection/Report Time (UTC):
- Reporter (user/system):
- Sender Address / Display Name:
- Subject:
- Recipient(s):
- Delivery Status (blocked/quarantined/delivered):
- URLs Extracted:
- Attachments (names/hashes if available):
- Interaction Status (none/open/click/credentials entered/attachment executed/unknown):
- Affected User Role (finance/executive/admin/standard):
- Initial Recipient Scope (single/multiple/unknown):
- Recommended Severity and Justification:
- Recommended Category: CAT-02 Phishing/BEC
- Evidence Captured (headers, EML/MSG, logs):
- Escalations Made (SOC Lead/L2/Finance/Email Admin):
- Actions Taken (L1):
- Actions Requested:

---

## 11. L1 Communication Templates (Internal Use)

### 11.1 SOC Lead Escalation Message (P2+)
Subject:
- Phishing/BEC – interaction confirmed – [User] – [Severity]

Body:
- user and role:
- interaction status:
- sender and subject:
- IOC summary (URLs/domains/attachments):
- recipient scope:
- ticket link:

### 11.2 Finance Escalation Message (BEC)
Subject:
- Suspected BEC payment request – finance action required – [Severity]

Body:
- impersonated party:
- requested action:
- any funds transferred/pending:
- deadline/urgency in email:
- ticket link:

---

## 12. Common L1 Mistakes to Avoid

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| closing as P4 without confirming click or credential entry | missed compromise | confirm via logs or user statement |
| failing to preserve email headers | weak evidence | preserve headers and EML/MSG early |
| clicking link to “verify” | infection risk | use sandbox or safe tools only |
| delaying escalation to collect more info | SLA breach | escalate early; L2 can deepen |
| not treating finance BEC as urgent | financial loss | escalate to SOC Lead/Finance immediately |
| mixing client evidence (MSSP) | confidentiality breach | verify tenant attribution first |

---

## 13. MSSP Notes (Client Handling)

For MSSP operations:
- confirm correct tenant/client attribution before evidence capture
- use client-specific notification and severity rules (if defined)
- do not store evidence in shared locations
- do not include any cross-client details in ticket notes

Reference:
`01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Multi-Client-Triage-MSSP.md`

---

## 14. Related Documents

| Document | Path |
|---------|------|
| Phishing Master | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Master.md` |
| L2 Investigation | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L2-Investigation.md` |
| Containment | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Containment.md` |
| BEC Detection Analysis | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-BEC-Detection-Analysis.md` |
| Severity Guide | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md` |
| Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Client Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md` |

---

## 15. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Lead / SOC Manager | Initial version |

---

## 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document