# Playbook: Phishing and BEC – Containment

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Phishing and BEC (Containment) |
| Document ID | IR-PB-PHB-006 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | SOC Lead / IR Team Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 phishing or BEC incident |

---

## 2. Purpose

This document defines the containment procedures for phishing and Business
Email Compromise (BEC) incidents. Containment is the set of actions taken
to stop the attack from progressing further while preserving evidence and
minimizing business disruption.

Containment for phishing and BEC differs from other incident types because:
- the primary attack surface is email, identity, and cloud applications
- the attacker may already have persistent access via forwarding rules or OAuth tokens
- financial fraud may be active or pending at the time of containment
- containment actions must be carefully sequenced to avoid alerting the attacker
- evidence must be preserved before any destructive containment actions are taken

Containment must occur only after sufficient evidence has been preserved
and the scope of compromise has been assessed by L2 or L3.

---

## 3. Scope

Applies to:
- phishing campaigns with confirmed user interaction
- confirmed or suspected credential compromise via phishing
- BEC incidents with active or pending financial fraud
- confirmed mailbox takeover with attacker persistence
- OAuth consent abuse and token theft scenarios
- enterprise and MSSP client environments

---

## 4. Containment Principles

1. Preserve Evidence First: Do not delete emails, rules, or accounts before evidence is captured.
2. Sequence Actions Carefully: Revoking sessions before preserving audit logs may alert the attacker.
3. Parallel Workstreams: Financial containment and technical containment must run simultaneously for BEC.
4. Document Every Action: Every containment action must be timestamped and logged in the ticket.
5. Coordinate Before Acting: High-impact containment actions require approval per authority matrix.
6. Confirm Effectiveness: Every containment action must be verified as effective before closing the workstream.

---

## 5. Containment Priority Order

| Priority | Objective | Actions |
|----------|-----------|---------|
| P0 | Stop active financial fraud | Place hold on pending payments; notify Finance immediately |
| P1 | Revoke attacker active session | Revoke all tokens and sessions for compromised accounts |
| P2 | Remove attacker persistence | Remove inbox rules, forwarding, delegates, OAuth consents |
| P3 | Block attacker infrastructure | Block sender domains, phishing URLs, IPs across all controls |
| P4 | Purge malicious emails | Remove phishing emails from all recipient mailboxes |
| P5 | Harden identity controls | Enforce MFA; remove unknown MFA devices; apply conditional access |
| P6 | Contain endpoint (if malware) | Isolate endpoint via EDR if payload was executed |

---

## 6. Preconditions Before Containment Begins

Containment begins only when the following conditions are confirmed:

| Precondition | Confirmed By | Notes |
|-------------|--------------|-------|
| Evidence preserved (email headers, audit logs, sign-in logs) | L2 or L3 | Do not begin destructive containment before this |
| Scope of affected users and accounts confirmed | L2 | Partial scope is acceptable; containment can proceed in phases |
| BEC financial status assessed | L2 and SOC Lead | Finance team must be engaged if any payment is involved |
| Severity confirmed and approved | SOC Lead | Drives approval requirements for containment actions |
| Client notification initiated (MSSP) | SOC Lead / SDM | Client must be informed before high-impact actions |

---

## 7. Detailed Containment Procedures

---

### Phase 1: Financial Containment (BEC Incidents Only)

This phase is time-critical and must run immediately in parallel with all
other containment workstreams. Do not delay financial containment waiting
for technical investigation to complete.

Actions:
- contact Finance Controller or Accounts Payable via phone immediately (not email)
- determine payment status and take the following actions:

| Payment Status | Immediate Action | Escalation Required |
|---------------|-----------------|---------------------|
| Payment already processed and funds transferred | Contact bank fraud department immediately to attempt wire recall; notify Legal | CISO, Legal, Management immediately |
| Payment pending in approval queue | Place immediate hold; do not approve under any circumstances | Finance Controller, SOC Lead, Management |
| Payment instructions changed but no payment yet | Revert banking details to verified originals; verify via phone with vendor | Finance, SOC Lead |
| No payment involved | Document and continue technical containment | SOC Lead notification only |

- document all financial containment actions in the incident ticket with timestamps
- do not communicate payment details or investigation status via the affected email account

---

### Phase 2: Identity and Session Containment

This phase stops the attacker's active access to the environment.

#### 7.1 Session and Token Revocation

Actions:
- revoke all active sessions for confirmed and suspected compromised accounts
- revoke all refresh tokens to prevent session persistence

| Platform | Revocation Method | Notes |
|---------|-------------------|-------|
| Microsoft 365 / Azure AD | Revoke-AzureADUserAllRefreshTokens via PowerShell or Entra ID portal | Invalidates all active sessions immediately |
| Google Workspace | Admin Console: Users > Account > Sign out of all sessions | |
| VPN Platform | Kill active VPN sessions for affected accounts | Coordinate with IT Ops |
| SaaS Applications | Revoke sessions from application admin console | Prioritize Finance and HR applications |
| On-premises AD | Force logoff and disable account temporarily if required | Coordinate with IAM team |

#### 7.2 Password Reset

Actions:
- reset passwords for all confirmed compromised accounts immediately
- reset passwords for all suspected compromised accounts within the same window
- enforce password reset at next logon for all users who received and interacted with phishing emails
- reset sequence recommendation:

| Account Category | Reset Priority | Notes |
|-----------------|----------------|-------|
| Privileged admin accounts | Immediate | Domain admin, cloud admin, security admin |
| Finance and HR accounts | Immediate | High BEC risk; prioritize above standard users |
| Executive accounts | Immediate | High impersonation and BEC risk |
| Service accounts (if affected) | Coordinated with IT Ops | Plan downtime window if required |
| Standard user accounts (confirmed interaction) | Within 1 hour | |
| Standard user accounts (suspected interaction) | Within 4 hours | |

#### 7.3 MFA Remediation

Actions:
- review MFA devices registered to compromised accounts
- remove any MFA devices registered during or after the suspicious login window
- re-register MFA only through a verified and secure channel
- enforce MFA for all accounts in the affected scope if not already enabled
- for accounts with MFA fatigue indicators: review and disable push notification MFA temporarily if approved

---

### Phase 3: Mailbox and Persistence Containment

This phase removes the attacker's persistence mechanisms within the email
and cloud environment to prevent continued access after session revocation.

#### 7.4 Inbox Rules Removal

Actions:
- run the following to identify all rules including hidden rules:
  - Get-InboxRule -Mailbox [username] -IncludeHidden
- identify and remove all rules matching the following criteria:

| Rule Characteristic | Malicious Indicator | Action |
|--------------------|---------------------|--------|
| ForwardTo external email address | Data exfiltration path | Remove immediately |
| Delete messages matching keywords | Hiding security alerts and replies | Remove immediately |
| MoveToFolder with unusual destination | Hiding incoming detection notifications | Remove immediately |
| Rule name appears blank or generic | Attacker-created hidden rule | Remove immediately |
| Rule created during compromise window | Timed with suspicious login | Remove immediately |

- document every rule removed with rule name, conditions, actions, and creation timestamp

#### 7.5 External Forwarding Removal

Actions:
- disable external SMTP forwarding at the mailbox level
- disable external forwarding at the tenant level if organization-wide policy allows
- check and disable mail flow rules or transport rules that forward externally

| Check | Command or Location | Action |
|-------|---------------------|--------|
| Mailbox-level forwarding | Get-Mailbox -Identity [user] or ForwardingSMTPAddress | Set to empty if unauthorized |
| Tenant-level transport rules | Exchange Admin Center: Mail Flow > Rules | Disable or remove unauthorized rules |
| Organization forwarding policy | Anti-spam outbound policy in Security and Compliance Center | Enforce block on external auto-forwarding |

#### 7.6 OAuth and Application Consent Revocation

Actions:
- identify all OAuth application consents granted during the compromise window
- review permissions scope for each application
- revoke consent for any application that is unrecognized or has excessive permissions

| Application Permission to Flag | Risk | Action |
|-------------------------------|------|--------|
| Mail.ReadWrite | Full mailbox read and write access | Revoke immediately if not approved |
| Mail.Send | Can send email as the user | Revoke immediately |
| offline_access | Maintains persistent access without user present | Revoke immediately |
| Calendars.ReadWrite | Access to scheduling and meeting details | Revoke if not approved |
| Files.ReadWrite | Access to OneDrive or SharePoint files | Revoke if not approved |

#### 7.7 Delegate and Permission Removal

Actions:
- run Get-MailboxPermission and Get-RecipientPermission for affected accounts
- remove any Full Access or Send As permissions granted to unauthorized accounts
- review shared mailbox access and remove unauthorized delegates
- document all permission changes with timestamps and approver

---

### Phase 4: Email and Infrastructure Containment

This phase removes the malicious content from the environment and blocks
attacker infrastructure across all control layers.

#### 7.8 Email Purge (Campaign Removal)

Actions:
- identify all recipients of the phishing email across the organization or client tenant
- submit search and purge request to email administrator

| Purge Scope | Method | Notes |
|-------------|--------|-------|
| Single mailbox | Remove from mailbox directly | For targeted incidents |
| Organization-wide | Content Search and Purge in Compliance Center | For campaigns; requires appropriate admin role |
| Quarantine release prevention | Ensure email remains quarantined | Do not release quarantined phishing emails |

- document purge confirmation including number of mailboxes purged and timestamp

#### 7.9 IOC Blocking Across Control Layers

Block all confirmed IOCs simultaneously across all available control layers:

| IOC Type | Blocking Layer | Method |
|---------|---------------|--------|
| Sender email domain | Email gateway | Add to blocked sender list or domain block list |
| Phishing URL | Web proxy and DNS | Add to URL block category and DNS sinkhole |
| Hosting IP address | Perimeter firewall | Add outbound block rule |
| Attachment file hash | EDR platform | Add to block list or custom IOC feed |
| Reply-To domain | Email gateway | Add to blocked domain list |
| C2 domain (if malware) | DNS and firewall | Add to DNS sinkhole and outbound firewall block |
| Phishing kit redirect domain | Web proxy | Add to URL block list |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md`
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md`

---

### Phase 5: Endpoint Containment (If Payload Was Executed)

If the phishing email contained a malicious attachment and execution was confirmed
on an endpoint, the following additional containment steps are required.

Actions:
- isolate the affected endpoint immediately via EDR network containment
- confirm isolation is effective (no network connections from endpoint)
- preserve EDR telemetry and memory artifacts before any remediation
- notify L3 and IR Team for full endpoint forensic investigation

| Endpoint Containment Action | Method | Approval Required |
|----------------------------|--------|-------------------|
| EDR network containment (single endpoint) | EDR console isolation command | SOC Lead |
| EDR network containment (multiple endpoints) | Bulk isolation via EDR console | SOC Lead and IR Team Lead |
| Physical network disconnection | IT Ops physical action | SOC Lead and IT Ops |
| Evidence preservation before remediation | Memory and disk triage | L3 performs prior to any cleanup |

Reference:
`02_PLAYBOOKS/02.3_Malware-Trojan/PB-Malware-Containment.md`
`04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Containment-Commands.md`

---

## 8. Containment Action Approval Matrix

| Containment Action | L1 Authority | L2 Authority | SOC Lead Authority | Management Authority |
|-------------------|--------------|--------------|-------------------|----------------------|
| Block sender or domain in email gateway | Submit request | Execute | Approve | Not required |
| Block URL in proxy or DNS | Submit request | Execute | Approve | Not required |
| Purge email from single mailbox | Submit request | Execute with email admin | Approve | Not required |
| Purge email organization-wide | Not authorized | Recommend | Approve and coordinate | Inform |
| Reset standard user password | Not authorized | Execute if authorized | Approve | Not required |
| Reset privileged account password | Not authorized | Recommend | Approve | Inform for P1 |
| Revoke user sessions and tokens | Not authorized | Execute if authorized | Approve | Not required |
| Remove inbox rules | Not authorized | Execute | Approve | Not required |
| Remove OAuth consent | Not authorized | Recommend | Approve | Not required |
| Disable external forwarding | Not authorized | Recommend | Approve and coordinate | Not required |
| EDR endpoint isolation | Not authorized | Recommend | Approve | Inform for P1 |
| Place hold on financial payment | Not authorized | Not authorized | Escalate to Finance | Finance Controller |
| Disable compromised account | Not authorized | Recommend | Approve | Inform for P1 |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 9. Containment Verification (Definition of Effective Containment)

Every containment action must be verified as effective.
Do not mark containment as complete without confirming each item below.

| Containment Area | Verification Check | Verified By |
|-----------------|-------------------|-------------|
| Financial | Finance confirms payment hold is active or wire recall initiated | Finance Controller |
| Sessions | No active sessions visible for compromised accounts in identity platform | L2 or IAM Team |
| Passwords | All compromised accounts show password last changed after incident timestamp | L2 or IAM Team |
| MFA | No unauthorized MFA devices remain on compromised accounts | L2 or IAM Team |
| Inbox rules | No malicious rules remain; verified via PowerShell including hidden rules | L2 |
| External forwarding | ForwardingSMTPAddress is empty for all affected accounts | L2 or Email Admin |
| OAuth consents | No unauthorized application consents remain active | L2 or IAM Team |
| Email purge | Purge confirmation received from email admin with affected mailbox count | Email Admin |
| IOC blocks | All confirmed IOCs are blocked in email gateway, proxy, DNS, and firewall | L2 or Network Team |
| Endpoint isolation | EDR console confirms affected endpoints are isolated | L2 or EDR Team |

---

## 10. Communication During Containment

### 10.1 Internal Communication

| Audience | Trigger | Message Type | Frequency |
|---------|---------|--------------|-----------|
| SOC Lead | Any P2 or above | Direct notification immediately | As status changes |
| Management | P1 or confirmed financial fraud | Management notification template | Initial plus updates per SLA |
| Finance Team | Any BEC with payment indicator | Direct phone call immediately | Immediate then as needed |
| IT Ops and IAM Team | Any account or endpoint action required | Direct coordination | Per action required |
| Legal | Confirmed financial loss or data exfiltration | Via SOC Lead and CISO | As soon as P1 confirmed |

### 10.2 MSSP Client Communication

| Trigger | Communication Method | Owner | Timeline |
|--------|---------------------|-------|---------|
| Containment actions initiated affecting client systems | Client notification template | SOC Lead via SDM | Per client SLA |
| Financial fraud confirmed in client environment | Direct escalation to client SDM | SOC Lead | Immediately |
| High-impact containment action requiring client approval | Verbal confirmation then written approval | SDM | Before action is taken |
| Containment complete | Status update to client | SOC Lead via SDM | Per client SLA |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md`
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/P1-Initial-Alert-Template.md`

---

## 11. Transition to Eradication

Containment is complete and eradication may begin when all of the following are confirmed:

| Condition | Confirmed |
|-----------|-----------|
| No active attacker sessions detected in identity platform | Yes / No |
| All compromised account passwords reset and sessions revoked | Yes / No |
| All inbox rules, forwarding, and delegate persistence removed | Yes / No |
| All unauthorized OAuth consents revoked | Yes / No |
| All known IOCs blocked across email, proxy, DNS, and firewall | Yes / No |
| Phishing emails purged from all mailboxes | Yes / No |
| Financial payment held or wire recall initiated (BEC) | Yes / No |
| Endpoint isolated (if malware executed) | Yes / No |
| Evidence fully preserved before any destructive action | Yes / No |

Do not proceed to eradication until all applicable conditions are confirmed.

Reference:
`02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Eradication.md`

---

## 12. Common Containment Mistakes to Avoid

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Revoking sessions before preserving audit logs | Critical forensic evidence lost permanently | Always preserve mailbox audit logs and sign-in logs before revoking sessions |
| Purging emails before confirming all recipients | Incomplete campaign removal; some users still exposed | Always scope full recipient list before purging |
| Removing inbox rules without documenting them first | Evidence destroyed; audit trail broken | Document rule name, conditions, and actions before removal |
| Not checking for hidden inbox rules using GUI only | Hidden rules remain active giving attacker persistent forwarding | Always use PowerShell with -IncludeHidden flag |
| Blocking only the phishing URL but not the domain | Attacker rotates to new URL on same domain | Block at domain level not just URL level |
| Not placing financial payment hold immediately | Funds transferred and irreversible | Financial containment is always Priority 0 for BEC |
| Resetting passwords without revoking sessions | Attacker remains active using existing token | Always revoke sessions immediately after or before password reset |
| Assuming containment is complete without verification | Attacker retains access via missed persistence mechanism | Use verification checklist in Section 9 for every incident |

---

## 13. MSSP Client Handling Notes

For containment actions in MSSP client environments:
- all high-impact containment actions require documented client approval before execution
- do not perform account disables, mass password resets, or email purges without explicit client authorization
- financial containment actions must be escalated to client SDM immediately; SOC does not contact client Finance directly
- document every containment action taken in the client-specific incident ticket
- provide client with a containment status summary at the cadence defined in the client SLA
- ensure all evidence collected during containment remains in client-scoped storage

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`
`00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`

---

## 14. Related Documents

| Document | Path |
|---------|------|
| Phishing Master | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Master.md` |
| L1 Triage | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L1-Triage.md` |
| L2 Investigation | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L2-Investigation.md` |
| L3 Forensics | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L3-Forensics.md` |
| BEC Detection Analysis | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-BEC-Detection-Analysis.md` |
| Eradication | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Eradication.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-MITRE-Mapping.md` |
| Containment Authority Matrix | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md` |
| Firewall Block Request SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md` |
| IOC Handling SOP | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md` |
| EDR Containment Commands | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Containment-Commands.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| MSSP Client Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md` |
| MSSP Multi-Client Handling | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md` |

---

## 15. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Lead / IR Team Lead | Initial version |

---

## 16. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**