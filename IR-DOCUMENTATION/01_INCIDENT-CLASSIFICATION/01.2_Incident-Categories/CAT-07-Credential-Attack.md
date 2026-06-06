# CAT-07 – Credential Attack Incident Category

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Incident Category – Credential Attack |
| Document ID | IR-CAT-007 |
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
| Category ID | CAT-07 |
| Default Severity | P2 – High (successful compromise) / P3 – Medium (suspicious attempts) / P4 – Low (blocked/benign) |
| Escalation Priority | High when privileged accounts, MFA bypass, or widespread attempts are observed |
| Attack Goal | Obtain valid credentials for unauthorized access and persistence |
| Threat Actors | Cybercriminals, APT groups, ransomware affiliates, insider threats |
| Playbook Reference | `02_PLAYBOOKS/02.7_Credential-Attack/` |

---

## 3. What is a Credential Attack?

A credential attack is any attempt to obtain, guess, steal, reuse, or
abuse authentication credentials to gain unauthorized access to systems,
applications, or cloud services.

Credential attacks are often the first step in larger intrusions and may
lead to:

- Account takeover
- Privilege escalation
- Lateral movement
- Data theft or ransomware deployment
- Fraud (especially in email and financial systems)

Credential attacks can target:
- End-user accounts
- Service accounts
- Privileged administrator accounts
- Cloud identities and federated SSO accounts

---

## 4. Credential Attack Types

| Type | Description |
|------|-------------|
| Brute Force | High-volume password guessing for a single account |
| Password Spraying | Attempting common passwords across many accounts |
| Credential Stuffing | Using stolen username/password pairs from other breaches |
| MFA Fatigue / Push Bombing | Repeated MFA prompts to trick user into approving |
| MFA Bypass (AiTM) | Phishing proxy capturing tokens/session cookies |
| Token Theft | Stealing access tokens, refresh tokens, or session cookies |
| Keylogging | Capturing credentials via malware |
| Credential Dumping | Extracting credentials from memory or local stores |
| Pass-the-Hash / Pass-the-Ticket | Using hashes or tickets instead of plaintext passwords |
| Kerberoasting | Extracting Kerberos service tickets to crack offline |
| OAuth Abuse | Malicious OAuth grants enabling access without passwords |
| Password Reset Abuse | Abuse of password reset flows or helpdesk processes |

---

## 5. Common Credential Attack Scenarios

| Scenario | Description |
|---------|-------------|
| VPN Attack | Password spraying or credential stuffing against VPN portal |
| Email Account Takeover | Compromise of mailbox used for BEC or internal phishing |
| Privileged Account Compromise | Unauthorized admin access leading to broad impact |
| Cloud Sign-in Anomalies | Impossible travel, risky sign-in, new device sign-ins |
| Service Account Misuse | Service account used interactively or outside expected context |
| Directory Attack | LDAP/Kerberos-based attacks against Active Directory |
| External Exposure | Compromised credentials from third-party breach reused internally |

---

## 6. Indicators of Credential Attack (IoCs and Observables)

### 6.1 Authentication Pattern Indicators

| Indicator | Details |
|----------|---------|
| High Failure Rate | Many failed logins from a single IP or multiple IPs |
| Spray Pattern | Few attempts per account across many accounts |
| Stuffing Pattern | Many accounts attempted from same IP with varied usernames |
| Success After Failures | Successful login following repeated failures |
| Impossible Travel | Same user logging in from distant locations quickly |
| New Device / New Location | First-time device, new browser fingerprint, new ASN |
| Unusual Hours | Admin logins late night or outside working hours |
| Concurrent Sessions | Multiple sessions for same user from different locations |

### 6.2 MFA and Token Indicators

| Indicator | Details |
|----------|---------|
| Repeated MFA Prompts | Numerous push notifications to user device |
| MFA Method Change | MFA settings changed unexpectedly |
| MFA Enrollment | New MFA device added without user request |
| Token Replay | Reuse of refresh token from unusual source |
| Session Cookie Abuse | Suspicious session hijacking indicators |

### 6.3 AD / Privileged Indicators

| Indicator | Details |
|----------|---------|
| Group Changes | Admin group membership changes (Domain Admins, Enterprise Admins) |
| Kerberos Anomalies | Service ticket requests spike, unusual SPNs targeted |
| LSASS Access | Processes reading LSASS memory (potential credential dumping) |
| NTLM Usage Increase | Unusual NTLM authentication spikes (possible PtH) |
| Password Reset Events | Bulk resets or resets outside normal workflow |

### 6.4 Key Log Sources

| Source | What to Look For |
|--------|------------------|
| AD / Domain Controller Logs | Failed logins, successful logins, group changes |
| VPN Logs | Failed/successful logins, source IP patterns |
| Cloud Identity Logs | Risky sign-ins, impossible travel, token activity |
| Email Platform Logs | Mailbox login anomalies, rule creation, session revocation |
| EDR Telemetry | Credential dumping tools, LSASS access, suspicious scripts |
| SIEM Correlation | Multi-source signals (VPN + AD + cloud) |

---

## 7. Severity Classification

| Scenario | Severity |
|----------|----------|
| Privileged account compromise confirmed (Domain Admin, Cloud Admin) | P1 – Critical |
| Multiple privileged accounts compromised or widespread account takeover | P1 – Critical |
| MFA bypass confirmed for privileged or high-impact account | P1 – Critical |
| Successful compromise of non-privileged account with suspicious behavior | P2 – High |
| Credential stuffing/spraying with confirmed account takeover | P2 – High |
| Suspicious successful login from unusual geo/device (unconfirmed compromise) | P3 – Medium |
| Password spraying attempts blocked (no success) but high volume | P3 – Medium |
| Low-volume failed login attempts blocked and not persistent | P4 – Low |

Note: Escalate quickly when there is confirmation of success or privileged involvement.

---

## 8. Immediate Response Actions

### 8.1 First 15 Minutes

- Create incident ticket and classify initial severity
- Notify SOC Lead immediately for P2 and above
- Identify impacted user(s), system(s), and authentication source (VPN, AD, cloud, email)
- Determine whether the attempt was successful (confirmed login) or blocked
- Block attacking IPs where appropriate (avoid blocking legitimate customer IP ranges without approval)
- If MFA fatigue reported, engage user and security team immediately
- Collect relevant authentication logs for the time window

### 8.2 First 1 Hour

- If compromise suspected or confirmed:
  - Reset password for impacted account(s)
  - Revoke active sessions and tokens (cloud and email)
  - Enforce MFA and verify MFA device enrollment integrity
- Review sign-in logs for:
  - location anomalies
  - device anomalies
  - impossible travel
  - concurrent sessions
- Check for changes to:
  - mailbox rules
  - MFA settings
  - group memberships
  - privileged role assignments
- Determine if the same source IPs are targeting other accounts
- Escalate to P1 if privileged accounts are affected or lateral movement begins

### 8.3 First 4 Hours

- Perform scoping:
  - identify all affected accounts
  - check authentication across AD, VPN, cloud, and email
  - identify lateral movement indicators
- Review endpoints for credential dumping indicators if applicable
- Validate no persistence mechanisms were established (new accounts, new tokens, new rules)
- Implement broader mitigations if campaign-level attack detected (geo-block, adaptive MFA, rate limits)
- Prepare management update for P2/P1 incidents

---

## 9. Containment and Mitigation Guidance

| Control | Purpose | Notes |
|--------|---------|------|
| Password Reset | Removes attacker access | Use strong password policy; reset related service accounts |
| Session Revocation | Kills active attacker sessions | Cloud and email platforms support token revocation |
| MFA Enforcement | Reduces success of password-only attacks | Validate enrollment and remove unknown devices |
| Conditional Access | Limits access based on risk | Apply geo, device, and risk rules |
| Rate Limiting | Slows brute force/spray attempts | Apply on VPN, SSO, and web portals |
| IP Blocking | Stops known attacker sources | Must avoid blocking legitimate users |
| Privileged Access Lockdown | Protects admin accounts | Use break-glass accounts and approval workflows |

Reference: `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md`

---

## 10. MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|--------|-----------|----|
| Credential Access | Brute Force | T1110 |
| Credential Access | Password Spraying | T1110.003 |
| Credential Access | Credential Stuffing | T1110.004 |
| Credential Access | Valid Accounts | T1078 |
| Credential Access | OS Credential Dumping | T1003 |
| Credential Access | Steal Web Session Cookie | T1539 |
| Credential Access | Adversary-in-the-Middle | T1557 |
| Credential Access | Kerberoasting | T1558.003 |
| Lateral Movement | Pass the Hash | T1550.002 |
| Lateral Movement | Remote Services | T1021 |
| Persistence | Account Manipulation | T1098 |
| Defense Evasion | Modify Authentication Process | T1556 |

---

## 11. Key Investigation Questions

1. Was authentication successful or blocked?
2. Which system was targeted (VPN, AD, cloud identity, email, application)?
3. Which accounts were targeted and which accounts were successful?
4. Is the account privileged or associated with sensitive systems?
5. What were the source IPs, geolocation, and ASN of attempts?
6. Do logs indicate spray/stuffing patterns across multiple accounts?
7. Is MFA enabled and was it challenged, bypassed, or fatigue abused?
8. Were MFA settings, devices, or recovery options changed?
9. Were mailbox rules, forwarding rules, or delegates changed?
10. Is there evidence of credential dumping on endpoints?
11. Are there signs of lateral movement or persistence after login?
12. What immediate remediation is required to stop continued attempts?

---

## 12. Critical Do's and Do Not's

### Do

- Confirm success vs failure quickly using authoritative identity logs
- Reset credentials and revoke sessions immediately on confirmed compromise
- Validate MFA enrollment integrity and remove unknown devices
- Review privileged access changes and group memberships
- Check for persistence indicators (new accounts, tokens, rules)
- Apply rate limits and conditional access controls during campaign attacks
- Document all actions, approvals, and timeline events

### Do Not

- Assume failed logins are harmless when spray patterns exist
- Reset passwords without revoking sessions (attacker may remain active)
- Block wide IP ranges without understanding business impact
- Ignore mailbox rule changes (common persistence after compromise)
- Close the incident without verifying no further access exists

---

## 13. Escalation Path

| Stage | Action |
|-------|--------|
| L1 Triage | Detect pattern, create ticket, classify severity |
| L2 Investigation | Confirm success, scope impacted accounts, recommend actions |
| SOC Lead | Approve containment actions and communications |
| L3 / IR Team | Engage for privileged compromise, credential dumping, or widespread takeover |
| IAM / AD Team | Execute account actions (reset, disable, group rollback) |
| Management / CISO | Engage for P1 and major business impact |
| MSSP SDM / Client Owner | Notify client and coordinate actions in client environments |

---

## 14. Regulatory and Client Reporting Considerations

| Trigger | Action |
|--------|--------|
| Privileged identity compromise | Treat as major incident; assess reporting requirements |
| Customer data access using compromised accounts | Assess breach notification requirements |
| Regulated client or BFSI context | Assess RBI and CERT-In reporting obligations |
| MSSP client impact | Notify client per SLA and document actions |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 15. Evidence Collection Requirements

| Evidence Type | Priority | Notes |
|--------------|----------|-------|
| AD / DC authentication logs | Critical | Failed/success logins, group changes |
| VPN authentication logs | Critical | Attempts and session details |
| Cloud identity sign-in logs | Critical | Risky sign-ins, device, conditional access |
| MFA logs | High | Enrollment changes, prompt fatigue events |
| Mailbox audit logs | High | Rules, forwarding, delegate changes |
| SIEM correlation output | High | Multi-source correlation evidence |
| Firewall/proxy logs | Medium | Source IP reputation and network indicators |
| EDR telemetry (if dumping suspected) | High | LSASS access, dumping tools, scripts |
| Change records | Critical | Password reset, disablement, policy changes |

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 16. Related Documents

| Document | Path |
|---------|------|
| Credential Attack Master Playbook | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-Master.md` |
| L1 Triage Playbook | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-L1-Triage.md` |
| L2 Investigation Playbook | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-L2-Investigation.md` |
| Containment Playbook | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-Containment.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-MITRE-Mapping.md` |
| P1 Critical Definition | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md` |
| P2 High Definition | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P2-High-Definition.md` |
| Firewall Block Request SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md` |
| Ticketing Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |

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