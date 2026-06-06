# Playbook: Credential Attack – L2 Investigation

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Credential Attack (L2 Investigation) |
| Document ID | IR-PB-CRA-003 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | L2 SOC Lead / SOC Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 credential attack incident |

---

## 2. Purpose

This document defines the Level 2 (L2) investigation procedures for credential-based attacks escalated from L1 triage.

L2 investigation objectives are to:
- confirm the credential attack type (brute force / spray / stuffing / Kerberos abuse / token replay / MFA fatigue)
- identify **successful compromises** (who, when, from where)
- determine full scope (accounts, services, applications, locations, IPs, ASNs)
- assess privileged impact (admins, service accounts, finance/executive)
- determine whether the activity is **only authentication attempts** or **post-compromise behavior**
- recommend containment actions with the correct approval level
- determine escalation to L3/IR Team and regulatory/legal triggers (where applicable)

L2 investigation must remain fast and structured:
- **confirm compromise first**
- **then scope**
- **then contain**
- while preserving evidence required for audits and legal defensibility

---

## 3. Scope

Applies to:
- Active Directory credential attacks (Kerberos / NTLM / LDAP)
- Entra ID / Azure AD / cloud identity attacks (OAuth, sessions, risky sign-ins)
- VPN login attacks
- web application login attacks
- API authentication abuse
- password spray/brute force/stuffing campaigns
- MFA fatigue/push bombing
- suspicious token/session reuse (AiTM outcomes)
- MSSP-managed client identity platforms

---

## 4. Preconditions (Inputs from L1)

L2 investigation begins only when the ticket contains, at minimum:

| Required Input | Source | Required |
|---------------|--------|----------|
| Attack summary + L1 classification | L1 ticket notes | Yes |
| Target accounts list (distinct usernames) | SIEM/IAM exports | Yes |
| Source IP list (top IPs + geo/ASN) | SIEM/IAM | Yes |
| Success/failure counts and time window | SIEM/IAM | Yes |
| Any known successful logins flagged | SIEM/IAM | Yes |
| Evidence exports/screenshots | L1 attachments | Yes |
| Severity recommendation | L1 | Yes |

Reference:
`02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-L1-Triage.md`

---

## 5. L2 Investigation Required Outputs

L2 must produce the following outputs before handoff/closure:

| Output | Description |
|--------|-------------|
| Confirmed Attack Type | Brute force / spray / stuffing / token replay / MFA fatigue / Kerberos abuse / other |
| Compromise Determination | Confirmed / Likely / Not detected (with justification) |
| Scope Summary | #accounts, #sources, #services, #successes, time window |
| Privileged Impact Assessment | Admin/service/finance/executive affected or targeted |
| IOC Package | Source IPs, ASNs, user-agents, targeted services, suspicious apps |
| Containment Recommendations | Prioritized actions with approvers |
| Timeline Summary | Key timestamps: first seen, first success, containment start |
| Escalation Decision | L3/IR Team escalation with reasons (or not) |

---

## 6. Investigation Workflow Overview

| Phase | Goal | Key Deliverable |
|------|------|-----------------|
| Phase 1 | Confirm attack type | Attack classification |
| Phase 2 | Confirm success/compromise | Compromised account list |
| Phase 3 | Scope expansion | Full impacted set |
| Phase 4 | Platform-specific deep checks | MFA/token/Kerberos findings |
| Phase 5 | Post-compromise activity check | Lateral movement indicators |
| Phase 6 | Containment recommendation | Action plan + approvals |
| Phase 7 | Escalation and reporting support | IR/Legal/Compliance triggers |

---

# 7. Phase 1 – Confirm Credential Attack Type

Use patterns (volume, distribution, success rate, targets) to classify.

## 7.1 Classification Table (L2 Standard)

| Attack Type | Pattern | L2 Confirmation Checks |
|-------------|---------|------------------------|
| Brute Force | High failures on 1 account | Same username + many failures + few IPs |
| Password Spray | Low failures across many accounts | Many users + few attempts each + same IP/ASN |
| Credential Stuffing | Many accounts + mix of successes | Successes dispersed + common UA patterns + leaked password reuse behavior |
| MFA Fatigue | Repeated MFA prompts | Many push prompts + user denial/approval sequence |
| Token Replay (AiTM) | Success without fresh MFA | “MFA already satisfied” + new device/IP + fast mailbox/app access |
| Kerberoasting | Unusual service ticket requests | High TGS requests + targeted service accounts + time clustering |
| Pass-the-Hash/Ticket (signals) | NTLM/Kerberos anomalies | NTLM usage anomalies + Kerberos ticket anomalies + lateral auth patterns |

---

# 8. Phase 2 – Confirm Success and Compromise

Compromise determination is the highest priority.

## 8.1 Success Identification Checklist

| Check | What to Look For | Outcome |
|------|-------------------|---------|
| Success after failures | A success event close to failure burst | Likely compromised |
| Success from unusual geo/ASN | New country/VPS/Tor | Likely compromised |
| Success without MFA | MFA not prompted when expected | Token/session risk |
| Success on multiple services | VPN + O365 + SSO | Broader compromise |
| Success for service account | Non-interactive account authenticating interactively | High risk |

## 8.2 Compromise Confidence Levels

| Level | Meaning | Minimum Evidence |
|------|---------|------------------|
| Confirmed | Direct evidence of attacker login/session | Success logs + source IP/device evidence |
| Likely | Strong signals but missing a direct artifact | Risky sign-in + impossible travel + correlated failures |
| Not Detected | No success and no token misuse indicators | Failures only + expected system retry patterns |

---

# 9. Phase 3 – Scope Expansion (Accounts, Sources, Services)

L2 must expand scope beyond the initially flagged events.

## 9.1 Scope Expansion Queries (Conceptual)

| Scope Question | Data Needed | What to Produce |
|----------------|------------|-----------------|
| How many distinct accounts targeted? | auth logs | list + counts |
| How many accounts succeeded? | success logs | compromised list |
| How many distinct source IPs? | auth logs | top IPs table |
| Which services are targeted? | destination/service field | service map |
| Which auth methods used? | protocol/client field | legacy auth detection |
| Is attack still active? | last seen timestamp | active/inactive status |

## 9.2 Required Scope Tables (Attach to Ticket)

### 9.2A Targeted Accounts Summary

| Account | Type (User/Admin/Service) | Dept/Role | Attempts | Success (Y/N) | Notes |
|--------|----------------------------|-----------|----------|---------------|------|
| | | | | | |

### 9.2B Source IP Summary

| Source IP | Geo | ASN/Provider | Attempts | Successes | First Seen (UTC) | Last Seen (UTC) |
|----------|-----|--------------|----------|-----------|------------------|-----------------|
| | | | | | | |

### 9.2C Target Services Summary

| Service | Attempts | Successes | Notes |
|---------|----------|-----------|------|
| VPN | | | |
| O365/SSO | | | |
| AD | | | |
| Web App | | | |

---

# 10. Phase 4 – Platform-Specific Deep Checks

This is where L2 confirms advanced identity outcomes (MFA, tokens, Kerberos).

---

## 10.1 Active Directory (On-Prem) Checks (If Applicable)

### 10.1A Key Event Categories to Review

| Area | What to Review | Why |
|------|----------------|-----|
| Failures | failed logins + lockouts | spray/brute confirmation |
| Successes | successful logins + workstation | compromise confirmation |
| Kerberos | ticket request anomalies | kerberoasting indicators |
| Privileged changes | group membership changes | escalation indicator |

### 10.1B AD Indicators Table

| Indicator | What it Means | L2 Action |
|----------|---------------|----------|
| Lockout spikes | spray/stuffing in progress | recommend containment |
| Success from unusual workstation | possible compromise | escalate |
| Service account interactive login | account misuse | urgent remediation |
| Abnormal Kerberos ticket volume | kerberoasting | escalate to L3 if needed |

---

## 10.2 Entra ID / Cloud Identity Checks (If Applicable)

### 10.2A Cloud Compromise Indicators

| Signal | Meaning | Priority |
|--------|---------|----------|
| Risky sign-in high | likely compromised | High |
| Impossible travel | likely compromised | High |
| MFA “already satisfied” | token replay possible | High |
| New device registered | persistence | High |
| OAuth consent post-login | app persistence | Critical |
| Legacy auth used | MFA bypass vector | High |

### 10.2B MFA Review

| MFA Pattern | Interpretation | L2 Action |
|------------|----------------|----------|
| Many prompts denied | fatigue attempt | containment recommendation |
| Prompt approved unexpectedly | probable compromise | immediate escalation |
| No MFA prompted | token or policy gap | investigate CA/policies |

---

## 10.3 VPN / Remote Access Checks

| Indicator | Meaning | L2 Action |
|----------|---------|----------|
| Success from new geo | compromised credentials | recommend reset + session kill |
| Burst failures from many IPs | distributed spray | recommend upstream blocks + throttling |
| Multiple accounts attacked via VPN | spray campaign | escalate to SOC Lead |
| Post-VPN internal scan alerts | attacker foothold | escalate to IR Team |

---

## 10.4 Web Application Login Attack Checks

| Indicator | Meaning | L2 Action |
|----------|---------|----------|
| High 401/403 spikes | brute/spray | recommend rate limiting/WAF |
| Same UA string across many IPs | automation | WAF rule tuning |
| Successes followed by unusual actions | account takeover | IR escalation |
| Credential stuffing patterns | breached credential list | recommend password reset campaign |

---

# 11. Phase 5 – Post-Compromise Activity Check (Critical)

L2 must determine whether the incident is **only login attempts** or if the attacker did something after access.

## 11.1 Post-Compromise Indicators

| Indicator | Meaning |
|----------|---------|
| Privileged role changes | escalation |
| New MFA device added | persistence |
| OAuth consent / app registration | persistence |
| New mailbox rules/forwarding | BEC/data theft risk |
| Mass file downloads | exfiltration |
| New VPN sessions + internal scans | foothold + pivot |
| Access to admin portals | escalation attempt |

## 11.2 Decision: “Credential Attack Only” vs “Intrusion in Progress”

| Condition | Classification | Next Step |
|----------|----------------|----------|
| No successes, no token signals | Attempted credential attack | containment + monitoring |
| Success on standard account only | Potential compromise | contain + verify no post activity |
| Success on privileged/service account | Active compromise | IR Team + emergency containment |
| Evidence of post-login actions | Intrusion in progress | switch to IR mode; consider other playbooks (Data Breach/Network Intrusion) |

---

# 12. Phase 6 – Containment Recommendations (L2 Output)

L2 recommends or executes (if authorized) containment steps.

## 12.1 Containment Actions Menu (Prioritized)

| Priority | Action | When to Use | Approval |
|----------|--------|-------------|----------|
| P0 | Block source IPs/ASNs (targeted) | confirmed spray/stuffing | SOC Lead / Network |
| P0 | Revoke sessions/tokens | confirmed/likely compromise | SOC Lead / IAM |
| P0 | Reset passwords (compromised accounts) | any confirmed success | IAM |
| P1 | Enforce MFA / reset MFA | MFA fatigue or device change | IAM |
| P1 | Disable legacy authentication | legacy auth detected | IAM/Change Mgmt |
| P1 | Conditional access tightening | risky geo/ASN patterns | IAM |
| P2 | Increase lockout thresholds carefully | high brute force | IAM (risk review) |
| P2 | WAF rate limiting/CAPTCHA | web login attacks | App/WAF owner |
| P2 | Temporary geo restrictions | clear non-business geos | SOC Lead + Mgmt if high impact |

Reference:
`02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-Containment.md`

---

# 13. Phase 7 – Escalation Criteria (L2)

## 13.1 Escalate to L3 if:

| Condition | Reason |
|----------|--------|
| Kerberoasting suspected | advanced Kerberos analysis |
| Pass-the-Hash/Ticket suspected | deeper auth + endpoint correlation |
| Token replay suspected | session/token forensic analysis |
| OAuth persistence suspected | cloud forensic review |
| Unclear compromise path | advanced investigation needed |

## 13.2 Escalate to IR Team if:

| Condition | Reason |
|----------|--------|
| Privileged/service account compromise | enterprise-wide risk |
| Post-compromise actions detected | intrusion in progress |
| Lateral movement indicators | ransomware/data breach precursor |
| Multiple successful compromises | coordinated incident management |
| Evidence of data access/exfiltration | potential data breach |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/`

---

# 14. Documentation Requirements (Ticket Checklist)

Before closing or handing off, L2 must complete:

| Requirement | Status |
|------------|--------|
| Attack type confirmed | ☐ |
| Success/compromise determination | ☐ |
| Targeted accounts table completed | ☐ |
| Source IP/ASN table completed | ☐ |
| Services targeted summarized | ☐ |
| MFA/token indicators reviewed | ☐ |
| Post-compromise indicators reviewed | ☐ |
| IOC package documented | ☐ |
| Containment recommendations submitted | ☐ |
| Escalation decision documented | ☐ |

---

# 15. Common L2 Mistakes to Avoid

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Stopping after confirming “spray” without checking successes | missed compromise | always search for successes |
| Not reviewing cloud sign-ins in hybrid org | cloud compromise missed | review Entra/SSO logs |
| Resetting passwords without session revocation | attacker stays active | revoke sessions/tokens |
| Ignoring service accounts | persistent access risk | prioritize service accounts |
| Not checking post-login actions | intrusion missed | review audit events quickly |
| Over-blocking causing business disruption | operational impact | targeted blocks with approval |

---

# 16. MSSP Client Handling Notes

For MSSP-managed environments:
- ensure correct tenant/client attribution before exporting logs
- follow client-specific IAM workflows and approvals
- do not execute mass resets/CA policy changes without client authorization (unless emergency authority exists)
- maintain evidence segregation (client-scoped storage only)
- coordinate client communications through SDM per SLA

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 17. Related Documents

| Document | Path |
|---------|------|
| Credential Attack Master | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-Master.md` |
| Credential Attack L1 Triage | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-L1-Triage.md` |
| Credential Attack Containment | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-Containment.md` |
| Credential Attack MITRE Mapping | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-MITRE-Mapping.md` |
| Phishing/BEC (if credential entry suspected) | `02_PLAYBOOKS/02.2_Phishing-BEC/` |
| Data Breach (if exfil suspected) | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/` |
| Network Intrusion (if lateral movement suspected) | `02_PLAYBOOKS/02.11_Network-Intrusion/` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 18. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | L2 SOC Lead / SOC Lead | Initial version |

---

## 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**