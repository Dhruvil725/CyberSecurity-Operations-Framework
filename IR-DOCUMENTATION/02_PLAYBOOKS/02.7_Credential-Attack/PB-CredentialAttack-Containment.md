# Playbook: Credential Attack – Containment

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Credential Attack (Containment) |
| Document ID | IR-PB-CRA-004 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | IR Team Lead / SOC Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 credential attack incident |

---

## 2. Purpose

This document defines the containment procedures for credential-based attacks.

Credential attack containment focuses on:
- stopping the active attack at the perimeter and identity layers
- revoking attacker sessions and invalidating stolen tokens
- resetting compromised credentials in the correct priority order
- restoring MFA integrity
- applying identity controls to prevent re-entry
- protecting critical infrastructure during the containment window
- minimizing business disruption while maximizing attacker lockout

Containment for credential attacks differs from malware or ransomware
containment because:
- the attacker uses **legitimate authentication systems**
- network isolation alone does NOT remove attacker access
- session tokens and OAuth grants may survive password resets
- the attacker may have established persistence before containment begins
- cloud and hybrid identity require coordinated multi-platform actions

Improper containment sequence may:
- allow attacker to maintain access via active tokens
- trigger account lockouts affecting legitimate users
- cause operational disruption to critical services
- alert attacker to investigation and trigger destructive behavior

---

## 3. Scope

Applies to:
- active brute force attacks
- confirmed or suspected password spray compromise
- credential stuffing with success indicators
- MFA fatigue with user approval
- token/session replay (AiTM outcomes)
- Kerberoasting and NTLM hash abuse indicators
- cloud and hybrid identity compromise
- VPN credential compromise
- web application account compromise
- privileged and service account credential exposure
- MSSP-managed client environments

---

## 4. Containment Principles

| Principle | Description |
|-----------|-------------|
| Stop Active Attack First | Block attack sources before remediating accounts |
| Revoke Before Reset | Revoke sessions and tokens before password reset |
| Contain by Priority | Privileged accounts before standard users |
| Coordinate Before Acting | High-impact actions require approval |
| Preserve Evidence | Never destroy authentication artifacts before export |
| Validate Effectiveness | Confirm each action worked before moving forward |
| Document Everything | Timestamped records required for audit and legal |

---

## 5. Containment Priority Order

The sequence matters. Executing in the wrong order will leave the attacker active.

| Priority | Objective | Example Actions |
|----------|-----------|----------------|
| P0 | Stop active attack traffic | Block source IPs at perimeter/WAF |
| P1 | Invalidate active attacker sessions | Revoke all sessions and refresh tokens |
| P2 | Reset compromised credentials | Start with privileged accounts |
| P3 | Restore MFA integrity | Remove unauthorized MFA devices |
| P4 | Close authentication gaps | Disable legacy auth, apply conditional access |
| P5 | Protect supporting infrastructure | Secure AD, SSO, VPN, admin portals |
| P6 | Scope clean-up | Verify all impacted accounts addressed |

---

## 6. Preconditions Before Containment

Containment actions must only begin when the following are confirmed:

| Requirement | Verification |
|-------------|-------------|
| Evidence preserved (auth logs, MFA logs, cloud logs) | L2 confirmed evidence export |
| Attack type and scope identified | L2 investigation complete |
| Compromised accounts identified (at least initial set) | L2 output |
| Business impact reviewed | SOC Lead awareness |
| Approval obtained for high-impact actions | Per authority matrix |
| Client notified (MSSP environments) | SDM communication |

Reference:
`02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-L2-Investigation.md`

---

# 7. Containment Workflow Overview

| Phase | Focus Area |
|------|-------------|
| Phase 1 | Block attack source infrastructure |
| Phase 2 | Revoke sessions and tokens |
| Phase 3 | Reset compromised credentials |
| Phase 4 | MFA remediation |
| Phase 5 | Identity hardening and policy controls |
| Phase 6 | Infrastructure protection |
| Phase 7 | Validation and monitoring |

---

# 8. Phase 1 – Block Attack Source Infrastructure

The first objective is stopping the active attack before identity actions begin.

---

## 8.1 IP and ASN Blocking

Actions:
- identify top attacking IPs and ASNs from L2 scope tables
- submit block requests through approved channels
- prioritize firewall, VPN, and WAF layers simultaneously

---

### IP Blocking Decision Matrix

| Attack Pattern | Blocking Approach |
|----------------|-------------------|
| Single or small IP set | Direct IP block at firewall |
| Large distributed spray | ASN block or upstream filtering |
| VPS provider heavy | Block provider ASN or ranges |
| Web application attack | WAF rule + CAPTCHA enforcement |
| Geo-concentrated attack | Consider temporary geo-blocking with approval |

---

### Blocking Considerations

| Consideration | Risk | Mitigation |
|---------------|------|------------|
| Large IP block | Legitimate user impact | Validate with L2 scope before blocking |
| Geo-blocking | Customer impact | Executive and management approval required |
| ASN block | Shared infrastructure | Validate business usage first |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md`

---

## 8.2 VPN and Remote Access Controls

Actions:
- restrict VPN access for compromised accounts
- enforce VPN device compliance where possible
- apply VPN conditional access rules for suspicious regions
- temporarily restrict VPN from high-risk geographies if approved

---

## 8.3 Web Application Rate Limiting

Actions:
- enable aggressive rate limiting on login endpoints
- enforce CAPTCHA challenges
- enable WAF under-attack mode if applicable
- monitor WAF block effectiveness

---

# 9. Phase 2 – Session and Token Revocation

Session and token revocation is critical and must be executed immediately after or before password reset.

Resetting a password alone does NOT invalidate:
- existing refresh tokens
- active SSO sessions
- OAuth application tokens
- browser session cookies
- VPN sessions

---

## 9.1 Session Revocation by Platform

| Platform | Revocation Action | Notes |
|---------|-------------------|------|
| Entra ID / Azure AD | Revoke all refresh tokens | Invalidates all sessions immediately |
| Active Directory | Force logoff / KRBTGT reset (if Kerberoasting) | Coordinate with AD team |
| VPN Platform | Kill active VPN sessions | Coordinate with network team |
| Google Workspace | Sign out all devices | Admin Console action |
| Okta / SSO | Terminate all sessions | Admin Console action |
| SaaS Apps | Force logout from app admin console | Per-app action |

---

## 9.2 AiTM (Token Replay) Specific Actions

If token/session theft is suspected:
- revoke refresh tokens immediately
- revoke OAuth consents
- enforce sign-in frequency policy to require re-authentication
- enable continuous access evaluation where supported
- monitor for further sign-in attempts from same ASN/device

---

## 9.3 Kerberos-Specific Revocation

If Kerberoasting or Pass-the-Ticket is suspected:
- coordinate with AD team for KRBTGT password reset (requires two resets with interval)
- disable targeted service accounts temporarily if confirmed compromised
- change service account passwords
- monitor for new ticket requests post-reset

---

## 9.4 Revocation Verification

| Verification Check | Expected Result |
|-------------------|----------------|
| Active sessions post-revocation | Zero active attacker sessions |
| Token refresh attempts post-revocation | Blocked or requiring re-auth |
| New login from same attacker IP | Blocked by IP controls |

---

# 10. Phase 3 – Credential Reset

Passwords must be reset in priority order to maximize impact.

---

## 10.1 Reset Priority Order

| Priority | Account Category | Reason |
|----------|------------------|--------|
| 1 | Domain Admin and Global Admin | Enterprise-wide access risk |
| 2 | Security and IAM administrators | Can bypass other controls |
| 3 | Privileged cloud admins | Tenant-level access risk |
| 4 | Finance and executive accounts | High BEC risk |
| 5 | Service accounts (confirmed or likely exposed) | Persistence risk |
| 6 | Standard users (confirmed compromised) | Individual risk |
| 7 | Standard users (spray targets, no confirmed success) | Precautionary |

---

## 10.2 Service Account Reset Guidance

Service account resets require special care:
- identify all dependent applications before reset
- plan reset during low-impact window
- coordinate with IT Ops and application owners
- validate application functionality post-reset

---

## 10.3 Password Reset Standards

| Requirement | Purpose |
|-------------|---------|
| New passwords must meet complexity policy | Reduce brute force risk |
| Temporary passwords must require change at next login | Prevent reuse |
| Reuse of previous passwords prohibited | Prevent easy reversal |
| Breached password list check | Prevent known weak passwords |

---

## 10.4 Reset Documentation Requirements

For each reset, document:
- account name
- account type
- reset timestamp
- performed by
- reason (confirmed / suspected / precautionary)

---

# 11. Phase 4 – MFA Remediation

MFA compromise is a key attacker persistence mechanism.

---

## 11.1 MFA Device Audit

Review all MFA devices for compromised accounts.

| Check | Action |
|-------|--------|
| MFA devices registered during compromise window | Remove immediately |
| Unknown device registered | Remove immediately |
| Recovery methods changed | Review and remediate |
| Phone number changed | Verify with user and revert if unauthorized |

---

## 11.2 MFA Re-enrollment

After unauthorized device removal:
- force MFA re-enrollment through secure verified channel
- require manager verification for high-risk accounts
- do not allow self-service MFA registration immediately after an attack

---

## 11.3 MFA Policy Hardening

| Hardening Action | Purpose |
|------------------|---------|
| Enforce number matching | Prevent MFA fatigue approval |
| Enable additional context | Show request details in push |
| Reduce session validity | Force re-authentication |
| Require phishing-resistant MFA for privileged | FIDO2/hardware key |
| Block MFA registration from suspicious locations | Prevent attacker persistence |

---

# 12. Phase 5 – Identity Hardening and Policy Controls

After immediate account containment, apply preventive controls.

---

## 12.1 Conditional Access Improvements

| Policy | Purpose |
|--------|---------|
| Block legacy authentication | Remove MFA bypass vector |
| Require compliant device | Reduce unmanaged device risk |
| Apply risk-based conditional access | Automatic risky sign-in response |
| Apply geo-restrictions temporarily | Reduce attack surface |
| Require re-auth for sensitive applications | Additional protection layer |

---

## 12.2 Legacy Authentication Blocking

Legacy authentication protocols bypass MFA.

| Protocol | Risk |
|----------|------|
| SMTP AUTH | Email-based compromise |
| POP3/IMAP | Mail client abuse |
| Basic Auth | No MFA support |
| NTLM over internet | Pass-the-Hash risk |

Actions:
- disable legacy auth via conditional access
- monitor for legacy auth usage during blocking
- coordinate with application teams for protocol migration

---

## 12.3 Account Lockout Policy Review

| Configuration | Purpose |
|---------------|---------|
| Lockout threshold | Calibrate between spray resistance and lockout risk |
| Lockout observation window | Control spray window |
| Smart lockout (cloud) | Enable for cloud identity |

---

# 13. Phase 6 – Infrastructure Protection

Credential attacks may target authentication infrastructure directly.

---

## 13.1 Active Directory Protection

| Action | Purpose |
|--------|---------|
| Restrict AD admin access to jump hosts | Reduce exposure |
| Increase DC logging | Improve visibility |
| Enable Enhanced Security Admin Environment | Privileged access |
| Review service account permissions | Least privilege |
| Validate replication integrity | Detect domain compromise |

---

## 13.2 Cloud Identity Protection

| Action | Purpose |
|--------|---------|
| Review OAuth app consents | Remove unauthorized apps |
| Audit admin role assignments | Detect escalation |
| Enable Privileged Identity Management | Just-in-time access |
| Review break-glass accounts | Ensure integrity |

---

## 13.3 VPN and Remote Access Hardening

| Action | Purpose |
|--------|---------|
| Restrict VPN to managed devices | Reduce attack surface |
| Apply MFA to all VPN connections | Remove password-only access |
| Review split tunnel configurations | Reduce exposure |
| Restrict VPN from non-business geos | Block known attack regions |

---

# 14. Phase 7 – Containment Validation and Monitoring

Containment is NOT complete until verified.

---

## 14.1 Containment Validation Checklist

| Validation Check | Expected Result | Status |
|-----------------|----------------|--------|
| No active attacker sessions | Zero sessions in IAM | ☐ |
| Password resets complete | All affected accounts reset | ☐ |
| Sessions and tokens revoked | No active attacker tokens | ☐ |
| MFA devices reviewed and cleaned | Only authorized devices | ☐ |
| Source IPs blocked | No successful auth from blocked IPs | ☐ |
| Legacy auth blocked | No legacy auth events | ☐ |
| Conditional access applied | Risk-based policies active | ☐ |
| No post-login activity | No suspicious actions in audit logs | ☐ |

---

## 14.2 Enhanced Monitoring Requirements

After containment, enable enhanced monitoring:

| Monitoring Area | Detection Goal |
|-----------------|---------------|
| Authentication logs | Detect repeated attempts or re-entry |
| MFA events | Detect new device registration |
| Session activity | Detect token replay |
| Privilege changes | Detect escalation |
| New user or app creation | Detect persistence |
| Lateral movement indicators | Detect post-compromise activity |

---

## 14.3 Monitoring Window Recommendations

| Severity | Minimum Monitoring Window |
|----------|--------------------------|
| P1 | 72 hours enhanced |
| P2 | 48 hours enhanced |
| P3 | 24 hours enhanced |

---

# 15. Containment Approval Matrix

| Action | L1 | L2 | SOC Lead | Management |
|--------|----|----|----------|------------|
| Block single IP at firewall | Recommend | Execute | Approve | No |
| Block ASN/range | No | Recommend | Approve | Inform |
| Geo-block | No | Recommend | Approve | Yes |
| Standard user password reset | No | Recommend | Approve | No |
| Privileged account reset | No | Recommend | Approve | Inform |
| Revoke all sessions | No | Recommend | Approve | Inform P1 |
| MFA device removal | No | Recommend | Approve | No |
| Disable legacy auth | No | Recommend | Approve | Inform |
| KRBTGT reset | No | Recommend | Yes | Yes |
| Conditional access changes | No | Recommend | Approve | Inform |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 16. Communication During Containment

---

## 16.1 Internal Communication

| Audience | Trigger | Timing |
|---------|---------|--------|
| SOC Lead | Any P2+ | Immediate |
| Management | P1 incidents | Per SLA |
| IAM Team | Any account action | Per action |
| IT Ops | Service account reset | Per action |
| Legal/Compliance | If regulatory trigger | As required |

---

## 16.2 MSSP Client Communication

| Trigger | Communication | Owner |
|---------|--------------|-------|
| Containment initiated | Status update | SDM |
| High-impact action required | Client approval | SDM |
| Containment complete | Summary | SOC Lead |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

---

# 17. Common Containment Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Resetting passwords without revoking sessions | Attacker stays logged in |
| Blocking IP before evidence preserved | Evidence loss |
| Not removing MFA devices | Attacker re-authenticates |
| Ignoring service accounts | Persistence survives |
| Mass lockout causing business disruption | Operational impact |
| Not validating containment effectiveness | Attacker remains active |

---

# 18. Transition to Post-Incident Activities

Containment is complete when:
- all compromised accounts reset and sessions revoked
- attacker access paths blocked
- MFA integrity restored
- monitoring active and stable
- SOC Lead approval obtained

Post-incident actions:
- lessons learned
- detection engineering improvements
- policy and control improvements

Reference:
`08_POST-INCIDENT/`

---

# 19. MSSP Client Handling Notes

For MSSP-managed environments:
- all high-impact containment requires written client approval
- maintain evidence segregation
- coordinate identity actions with client IAM teams
- follow client contractual SLAs for communication
- provide containment summary at client-agreed cadence

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 20. Related Documents

| Document | Path |
|---------|------|
| Credential Attack Master | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-Master.md` |
| Credential Attack L1 Triage | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-L1-Triage.md` |
| Credential Attack L2 Investigation | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-L2-Investigation.md` |
| Credential Attack MITRE Mapping | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-MITRE-Mapping.md` |
| Firewall Block SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md` |
| EDR Containment | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Containment-Commands.md` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 21. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | IR Team Lead / SOC Lead | Initial version |

---

## 22. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**