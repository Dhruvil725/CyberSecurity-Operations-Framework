# Playbook: Phishing and BEC – Eradication

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Phishing and BEC (Eradication) |
| Document ID | IR-PB-PHB-007 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | IR Team Lead / L3 Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 phishing or BEC incident |

---

## 2. Purpose

This document defines the eradication procedures for phishing and Business
Email Compromise (BEC) incidents after containment has been verified.

Eradication is the phase where:
- attacker access is permanently removed
- persistence mechanisms are eliminated
- compromised credentials and sessions are invalidated
- malicious cloud applications and mailbox configurations are removed
- systems are hardened to prevent re-entry
- the environment is validated as clean before recovery begins

Unlike containment, which focuses on stopping the active threat,
eradication focuses on ensuring the attacker cannot return using:
- stolen refresh tokens
- OAuth application access
- hidden mailbox rules
- delegated mailbox permissions
- compromised endpoints
- residual malware or scripts
- weak identity controls

This phase must be executed carefully because incomplete eradication
is one of the most common causes of phishing and BEC reinfection.

---

## 3. Scope

Applies to:
- credential phishing incidents
- mailbox takeover and internal account compromise
- BEC incidents involving internal account abuse
- OAuth consent abuse and token theft
- AiTM (Adversary-in-the-Middle) phishing incidents
- phishing-delivered malware execution
- Microsoft 365 / Google Workspace / cloud identity compromise
- enterprise and MSSP-managed environments

---

## 4. Preconditions Before Eradication

Eradication must not begin until containment is verified.

The following conditions are mandatory:

| Precondition | Required Verification | Owner |
|--------------|----------------------|-------|
| Active attacker sessions revoked | No active sessions visible in IAM platform | IAM Team / L2 |
| IOC blocks active | Firewall, DNS, email gateway, and EDR blocks confirmed | SOC Lead |
| Evidence preserved | Headers, audit logs, sign-in logs, mailbox exports completed | L2 / L3 |
| Scope confirmed | All impacted users, accounts, endpoints, and mailboxes identified | L2 / L3 |
| Financial containment complete (BEC) | Payment hold, wire recall, or fraud escalation complete | Finance + SOC Lead |
| Client approval obtained (MSSP) | Written approval documented | SDM |

Critical note:
- If eradication begins before evidence collection is complete, critical forensic artifacts may be lost permanently.
- Never delete mailbox rules, OAuth apps, or logs before they are exported and documented.

Reference:
`02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Containment.md`

---

## 5. Eradication Objectives and Outputs

### 5.1 Primary Objectives

1. Remove all attacker persistence mechanisms
2. Eliminate all unauthorized access paths
3. Rotate and secure compromised credentials
4. Remove malicious or unauthorized OAuth applications
5. Clean or rebuild impacted endpoints
6. Harden controls to prevent recurrence
7. Validate the environment is safe for recovery

---

### 5.2 Required Outputs

| Output | Description |
|--------|-------------|
| Eradication Action Log | Timestamped record of all actions taken |
| Persistence Removal Record | List of rules, apps, permissions, and artifacts removed |
| Credential Rotation Record | Accounts reset and MFA re-registered |
| IOC Update Package | Newly discovered indicators added to TI feeds |
| Validation Checklist | Confirmation no persistence remains |
| Hardening Actions Log | Security improvements implemented |
| Final Eradication Status | Clean / Monitoring / Escalated |

---

## 6. Eradication Workstreams Overview

Eradication must occur in parallel workstreams coordinated by the SOC Lead or IR Team Lead.

| Workstream | Focus Area | Primary Owner |
|------------|------------|----------------|
| Identity Eradication | Passwords, sessions, MFA, tokens | IAM Team |
| Mailbox Eradication | Rules, forwarding, delegates | Email Admin |
| OAuth and Cloud App Cleanup | App consents and API access | IAM Team |
| Endpoint Eradication | Malware cleanup or rebuild | EDR / IT Ops |
| Infrastructure Hardening | Security configuration improvements | Security Engineering |
| Monitoring Validation | Confirm no attacker activity remains | SOC / L3 |

---

# 7. Identity Eradication Procedures

Identity compromise is the most common long-term persistence mechanism
in phishing and BEC incidents.

This phase is considered the highest priority eradication workstream.

---

## 7.1 Password Reset and Credential Rotation

Password resets must be coordinated and prioritized carefully.
Improper sequencing may allow the attacker to maintain active sessions.

Actions:
- force password reset for all confirmed compromised accounts
- reset passwords for all suspected compromised accounts
- rotate passwords for any privileged or administrative account accessed during the compromise window
- rotate service account credentials if there is any indication of exposure

---

### Recommended Reset Priority

| Account Type | Priority | Reason |
|--------------|----------|--------|
| Global Admin / Cloud Admin | Immediate | Full tenant compromise risk |
| Domain Admin | Immediate | Enterprise-wide compromise risk |
| Finance / Payroll Accounts | Immediate | Active fraud risk |
| Executive Accounts | Immediate | High-value BEC targeting |
| Security Team Accounts | Immediate | Monitoring bypass risk |
| Service Accounts | Coordinated | Operational impact possible |
| Standard User Accounts | Within 1 hour | User-level exposure |

---

### Additional Mandatory Actions

| Action | Purpose |
|--------|---------|
| Require password change at next login | Prevent password reuse |
| Invalidate all old password hashes if supported | Prevent replay |
| Enforce password policy compliance | Reduce weak password risk |
| Block previously used passwords | Prevent reuse |

---

### Verification Requirements

| Verification Check | Expected Result |
|--------------------|----------------|
| Last password change timestamp | After incident detection |
| Active session count | Zero active attacker sessions |
| New successful login source | Expected user location/device only |

---

## 7.2 Session and Token Invalidation

Modern phishing attacks frequently rely on stolen refresh tokens and session cookies.

Password resets alone are NOT sufficient.

Actions:
- revoke all active sessions
- revoke all refresh tokens
- invalidate browser sessions where supported
- terminate active VPN sessions
- revoke SaaS application tokens

---

### Platform-Specific Actions

| Platform | Action |
|----------|--------|
| Microsoft 365 / Entra ID | Revoke all refresh tokens |
| VPN Platforms | Kill active VPN sessions |
| Google Workspace | Sign out user from all devices |
| SaaS Applications | Force logout and token invalidation |
| SSO Platforms | Revoke federation sessions |

---

### AiTM (Adversary-in-the-Middle) Considerations

If AiTM phishing is suspected:
- assume the attacker captured active session cookies
- revoke sessions BEFORE or immediately AFTER password reset
- monitor for repeated token replay attempts
- review all active device registrations

Indicators requiring enhanced review:
- MFA was reportedly used but attacker still gained access
- sign-ins show “MFA already satisfied”
- suspicious OAuth consent immediately after login
- attacker activity from VPS or proxy infrastructure

---

## 7.3 MFA Remediation

Attackers may register additional MFA methods during compromise.

Actions:
- review all MFA methods registered during the compromise window
- remove unauthorized MFA devices
- force MFA re-registration where appropriate
- review MFA fatigue attack indicators

---

### MFA Review Checklist

| Check | Action Required |
|-------|----------------|
| Unknown device registered | Remove immediately |
| SMS MFA in use | Recommend migration to stronger method |
| MFA disabled during incident | Re-enable immediately |
| Push fatigue suspected | Temporarily disable push notifications |
| New recovery methods added | Remove and investigate |

---

### MFA Hardening Recommendations

| Hardening Action | Security Benefit |
|------------------|------------------|
| Enforce Authenticator App | Stronger than SMS |
| Use Number Matching | Prevent MFA fatigue attacks |
| Deploy FIDO2 Tokens for admins | Phishing-resistant MFA |
| Restrict MFA registration by location | Reduce attacker registration attempts |

---

# 8. Mailbox and Email Eradication

Mailbox persistence is one of the most common persistence methods
used in phishing and BEC incidents.

Attackers frequently:
- create forwarding rules
- hide emails
- auto-delete alerts
- add delegate permissions
- abuse shared mailboxes

---

## 8.1 Inbox Rule Investigation and Removal

GUI-only review is NOT sufficient.

Always use PowerShell with:
- `Get-InboxRule -IncludeHidden`

Actions:
- export all inbox rules before deletion
- identify suspicious or attacker-created rules
- remove all malicious rules

---

### Rule Types and Risk

| Rule Type | Risk | Action |
|-----------|------|--------|
| ForwardTo external email | Data exfiltration | Remove immediately |
| Delete matching messages | Hides security alerts | Remove immediately |
| MoveToFolder hidden path | Hides user responses | Remove immediately |
| Hidden rule | Advanced persistence | Remove immediately |
| Rule created during compromise window | Strong compromise indicator | Remove immediately |

---

### Required Documentation Before Removal

| Data Required | Reason |
|--------------|--------|
| Rule name | Audit evidence |
| Creation timestamp | Timeline reconstruction |
| Rule conditions | Understand attacker objective |
| Rule actions | Identify persistence behavior |
| Mailbox owner | Scope validation |

---

## 8.2 External Forwarding Removal

Actions:
- disable mailbox forwarding
- disable transport-rule forwarding
- review tenant-wide forwarding policy

---

### Verification Requirements

| Verification Item | Expected State |
|-------------------|---------------|
| Mailbox forwarding | Disabled |
| Transport rule forwarding | Disabled |
| Shared mailbox forwarding | Disabled unless approved |
| Tenant external forwarding | Restricted or blocked |

---

## 8.3 Delegate Permission Cleanup

Actions:
- review Full Access permissions
- review Send As permissions
- remove unauthorized delegates
- review shared mailbox access

---

### High-Risk Permission Types

| Permission | Risk |
|------------|------|
| Full Access | Full mailbox visibility |
| Send As | User impersonation |
| Send on Behalf | Social engineering risk |
| Shared mailbox access | Lateral information exposure |

---

# 9. OAuth and Cloud Application Eradication

OAuth abuse provides stealthy persistence without passwords.

Attackers may:
- register malicious apps
- grant delegated permissions
- maintain persistent mailbox access through API tokens

---

## 9.1 OAuth Consent Review

Actions:
- identify all apps consented during compromise window
- review permission scopes
- revoke unauthorized apps immediately

---

### High-Risk OAuth Permissions

| Permission Scope | Risk |
|------------------|------|
| Mail.ReadWrite | Full mailbox access |
| Mail.Send | Send as compromised user |
| Files.ReadWrite | OneDrive / SharePoint exfiltration |
| offline_access | Persistent access without user login |
| Calendars.ReadWrite | Meeting intelligence gathering |

---

### Verification Requirements

| Verification | Expected Result |
|-------------|----------------|
| Unauthorized app consents | Removed |
| API calls after revocation | None |
| Unknown enterprise apps | Removed or disabled |

---

## 9.2 Enterprise Application Cleanup

Actions:
- remove rogue enterprise applications
- remove malicious service principals
- disable suspicious app registrations

---

### Indicators of Suspicious Enterprise Applications

| Indicator | Risk |
|-----------|------|
| Unknown publisher | Malicious or fake app |
| High privilege permissions | Full tenant compromise |
| Registered during compromise window | Strong persistence indicator |
| No business owner | Unauthorized deployment |

---

# 10. Endpoint Eradication (If Malware Executed)

If phishing resulted in malware execution, endpoint eradication becomes mandatory.

---

## 10.1 Malware Cleanup Actions

Actions:
- run full EDR scan
- remove malicious binaries
- remove persistence mechanisms
- verify no outbound connections remain

---

### Common Persistence Locations

| Persistence Type | Example |
|------------------|---------|
| Scheduled Tasks | schtasks |
| Registry Run Keys | HKCU Run |
| Startup Folder | Startup persistence |
| WMI Event Subscription | Fileless persistence |
| Browser Extensions | Credential theft persistence |

---

## 10.2 Rebuild Decision Guidance

| Scenario | Recommended Action |
|----------|-------------------|
| Critical system compromised | Full rebuild mandatory |
| Malware execution confirmed | Rebuild preferred |
| Unknown persistence detected | Rebuild mandatory |
| Single low-risk endpoint | Cleanup acceptable after validation |

Preferred approach:
- rebuild from golden image whenever feasible

Reference:
`02_PLAYBOOKS/02.3_Malware-Trojan/PB-Malware-Eradication.md`

---

# 11. Security Hardening After Eradication

Eradication is incomplete without implementing security improvements.

---

## 11.1 Identity Hardening

| Hardening Action | Purpose |
|------------------|---------|
| Enforce MFA for all users | Prevent credential-only compromise |
| Disable legacy authentication | Prevent MFA bypass |
| Apply conditional access | Restrict risky sign-ins |
| Restrict admin login locations | Reduce privileged attack surface |

---

## 11.2 Email Security Hardening

| Hardening Action | Purpose |
|------------------|---------|
| DMARC reject policy | Prevent spoofing |
| Block external forwarding | Prevent exfiltration |
| Anti-phishing policy tuning | Improve detection |
| Impersonation protection | Protect executives |

---

## 11.3 Monitoring Improvements

| Improvement | Purpose |
|-------------|---------|
| Inbox rule alerts | Detect persistence |
| OAuth consent alerts | Detect rogue apps |
| Impossible travel alerts | Detect account compromise |
| Mass outbound email alerts | Detect internal phishing |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 12. Eradication Validation (Definition of Done)

Eradication is ONLY complete when ALL validation checks pass.

---

## 12.1 Validation Checklist

| Validation Check | Verification Method | Status |
|------------------|--------------------|--------|
| No active attacker sessions | IAM logs | Complete / Incomplete |
| Passwords reset for all affected accounts | Identity platform review | Complete / Incomplete |
| MFA remediated | MFA audit | Complete / Incomplete |
| Hidden inbox rules removed | PowerShell verification | Complete / Incomplete |
| External forwarding removed | Mailbox audit | Complete / Incomplete |
| OAuth apps removed | Azure AD review | Complete / Incomplete |
| Endpoint rebuilt or validated clean | EDR review | Complete / Incomplete |
| IOC blocks active | Firewall / Proxy / DNS | Complete / Incomplete |
| No suspicious activity during monitoring window | SIEM monitoring | Complete / Incomplete |

---

## 12.2 Enhanced Monitoring Requirements

| Severity | Monitoring Window |
|----------|------------------|
| P1 | Minimum 72 hours |
| P2 | Minimum 48 hours |
| P3 | Minimum 24 hours |

Monitor for:
- repeated login attempts
- token replay attempts
- new inbox rules
- OAuth consent events
- unusual outbound mail activity

---

# 13. Common Eradication Mistakes to Avoid

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Resetting passwords without revoking sessions | Attacker remains logged in | Revoke sessions first |
| Checking inbox rules only via GUI | Hidden rules remain active | Use PowerShell IncludeHidden |
| Ignoring OAuth applications | Persistent API access remains | Audit all app consents |
| Not rebuilding compromised endpoints | Residual malware remains | Rebuild critical systems |
| Removing rules before export | Evidence lost | Export before deletion |
| Forgetting service account rotation | Persistence remains | Review all exposed service accounts |

---

# 14. Transition to Recovery

Eradication is complete only after:
- persistence removed
- credentials rotated
- monitoring stable
- SOC Lead approval obtained

Recovery may begin once all validation checks are complete.

Reference:
`02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Recovery.md`

---

# 15. MSSP Client Handling Notes

For MSSP environments:
- document all eradication actions in client-specific ticket
- obtain client approval for high-impact actions
- ensure evidence remains client-scoped
- provide eradication summary to client management
- coordinate password resets with client IT teams

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 16. Related Documents

| Document | Path |
|---------|------|
| Phishing Master | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Master.md` |
| L2 Investigation | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L2-Investigation.md` |
| L3 Forensics | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L3-Forensics.md` |
| Containment | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Containment.md` |
| BEC Detection Analysis | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-BEC-Detection-Analysis.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-MITRE-Mapping.md` |
| Malware Eradication | `02_PLAYBOOKS/02.3_Malware-Trojan/PB-Malware-Eradication.md` |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |

---

## 17. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | IR Team Lead / L3 Lead | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document