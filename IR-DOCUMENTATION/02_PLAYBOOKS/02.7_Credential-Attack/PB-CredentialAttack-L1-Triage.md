# Playbook: Credential Attack – L1 Triage

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Credential Attack (L1 Triage) |
| Document ID | IR-PB-CRA-002 |
| Version | 1.1 |
| Effective Date | 16-May-2026 |
| Owner | SOC Lead / SOC Manager |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 credential attack incident |

---

## 2. Purpose

This document defines the Level 1 (L1) SOC Analyst procedures for triaging **credential-based attacks** across enterprise and MSSP-managed environments.

Credential attacks target the identity layer and can be the earliest stage of:
- account takeover
- privilege escalation
- lateral movement
- data breach / exfiltration
- ransomware execution

L1’s objectives are to:
1. Validate the alert (real vs false positive / misconfiguration)
2. Identify attack type (brute force / spray / stuffing / MFA fatigue / token theft / Kerberos abuse)
3. Determine if compromise succeeded (any successful login / session)
4. Identify impacted accounts and services
5. Preserve critical evidence (authentication + MFA + cloud sign-in logs)
6. Assign a **severity recommendation** (P1–P4) with clear justification
7. Escalate rapidly to L2 / SOC Lead / IR Team when required

---

## 3. Scope

Applies to credential attack detections from:
- Active Directory (Kerberos / NTLM)
- Azure AD / Entra ID (cloud sign-in)
- SSO (Okta / Ping / etc.)
- VPN authentication
- Web applications (login endpoints)
- SaaS authentication logs
- MFA provider logs (push / OTP / token)
- MSSP client identity platforms

Attack types include:
- brute force
- password spray
- credential stuffing
- MFA fatigue (push bombing)
- token/session replay (AiTM outcomes)
- Kerberoasting (service ticket abuse)
- Pass-the-Hash / Pass-the-Ticket indicators (where visible at L1)

---

## 4. L1 Safety and Operational Rules

Credential alerts can trigger business disruption if handled incorrectly.

### 4.1 Mandatory Rules

| Rule | Reason |
|------|--------|
| Do **NOT** reset privileged or service accounts without approval | High outage risk |
| Do **NOT** disable accounts unless emergency authority exists | Could lock out legitimate users |
| Do **NOT** mass-block IP ranges without SOC Lead approval | Risk of customer/business disruption |
| Do **NOT** ignore “failed-only” patterns | Spray attacks are slow and persistent |
| Preserve logs **before** remediation actions | Evidence integrity / scoping depends on it |
| Use **UTC timestamps** for all notes and exports | Timeline consistency |

### 4.2 “High-Risk Immediately” Scenarios (Escalate Fast)

| Scenario | Why High Risk |
|----------|---------------|
| Any **successful login** to privileged account from unusual IP/location | Potential enterprise compromise |
| Successful login with **MFA not challenged** or “MFA already satisfied” | Token/session replay likely |
| Multiple successful logins across users from same IP/ASN | Active compromise campaign |
| Sudden spike of account lockouts across org | Spray/stuffing in progress |
| Kerberos ticket request anomalies targeting service accounts | Service account compromise risk |

---

## 5. L1 SLA Targets

| Severity | L1 Start Target | Escalation Target |
|----------|------------------|-------------------|
| P1 | Immediate | SOC Lead immediately; L2 immediately |
| P2 | 10 minutes | SOC Lead immediately; L2 within 15 minutes |
| P3 | 20 minutes | L2 within 30 minutes if scope expands |
| P4 | Same shift | Close/monitor per SOP |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 6. Inputs Required (Minimum Data to Collect)

### 6.1 Mandatory Alert Fields (Record in Ticket)

| Field | Required Detail |
|------|------------------|
| Alert Source | SIEM / AD / Entra ID / VPN / App |
| Detection Time | UTC timestamp |
| Targeted Account(s) | UPN/SAM + account type (user/admin/service) |
| Destination Service | VPN / O365 / AD / App name |
| Authentication Result | Success / Failure / Conditional Access blocked |
| Source IP | IP + Geo + ASN/provider |
| Client/App Type | Browser / legacy auth / mobile / API |
| MFA Result | Challenged / Approved / Denied / Not required / Unknown |
| Count Metrics | #failures, #successes, #accounts, time window |

### 6.2 Minimum Log Sources to Check (Based on Environment)

| Environment | Primary Logs |
|------------|--------------|
| AD (on-prem) | DC security logs, account lockout logs |
| Entra ID / M365 | Sign-in logs, audit logs, risky sign-in logs |
| VPN | Auth logs (failed/success), device posture logs |
| Web apps | WAF/app logs (401/403 spikes), load balancer logs |
| MFA provider | Push/OTP logs, device registration changes |

---

## 7. Quick Triage Decision Flow (L1)

Use this sequence to avoid missing compromises:

| Step | Question | If YES | If NO |
|------|----------|--------|-------|
| 1 | Any **successful** login? | Treat as likely compromise → escalate to L2 + SOC Lead | go to Step 2 |
| 2 | Are many accounts targeted (spray/stuffing)? | Escalate to L2; consider P2/P1 based on success | go to Step 3 |
| 3 | Is a privileged/service account targeted? | Escalate to SOC Lead; severity at least P2 | go to Step 4 |
| 4 | MFA fatigue / token replay indicators present? | Escalate to L2; possible P1/P2 | go to Step 5 |
| 5 | Failed-only low volume (likely scanning/noise)? | P3/P4 with monitoring | Investigate further |

---

## 8. Step-by-Step L1 Triage Procedure (Detailed)

---

### Step 1: Validate Alert Authenticity (False Positive vs Real)

Perform quick validation:

| Check | What to Look For | Notes |
|------|-------------------|------|
| Baseline comparison | Is this normal for this user/app/time? | Compare last 7–14 days if possible |
| Known system retries | MDM, mail client, password managers | Common source of repeated failures |
| Service account behavior | Expected auth patterns for service accounts | Misconfigured apps can generate spikes |
| Change window | Planned maintenance, password rotations | Cross-check change schedule |

**If likely false positive:** document reasoning and keep monitoring if pattern persists.

---

### Step 2: Classify the Attack Type

Use the patterns below.

#### 8.2 Attack Type Pattern Table

| Attack Type | Pattern | L1 Fast Indicators |
|-------------|---------|-------------------|
| Brute force | Many failures against **1 account** | Same account, same/similar IPs |
| Password spray | Few passwords across **many accounts** | Many users, few attempts each |
| Credential stuffing | Many accounts attempted with **some successes** | Successes mixed with failures |
| MFA fatigue | Repeated MFA prompts | Many push attempts to one user |
| Token/session replay | Login success without fresh MFA | “MFA already satisfied”, new device/IP |
| Kerberoasting (visible signals) | Many service ticket requests | Spikes around service accounts |

---

### Step 3: Determine Authentication Success and Risk

#### 8.3 Success & Risk Matrix

| Finding | Meaning | L1 Action |
|--------|---------|----------|
| Failures only | Attack attempt may be ongoing | Scope pattern and monitor |
| Success after failures | Strong compromise indicator | Escalate immediately |
| Success from unusual geo/ASN | Strong compromise indicator | Escalate immediately |
| Success with “no MFA” for MFA-protected user | Token/session abuse or policy gap | Escalate to L2 + SOC Lead |
| Conditional Access blocked | Attack attempted but blocked | Still scope & monitor |

---

### Step 4: Check Account Criticality (Privilege Impact)

Classify the targeted account:

| Account Category | Examples | Minimum Severity Floor |
|------------------|----------|------------------------|
| Privileged | Domain Admin, Global Admin, Security Admin | P1 if success / P2 if targeted |
| Business-critical | Finance, Payroll, HR, Executive | P1 if success / P2 if targeted |
| Service accounts | App service, automation accounts | P1/P2 depending on exposure |
| Standard users | General workforce | P2 if success / P3 if failed-only |

---

### Step 5: Perform Scope Snapshots (Fast Scoping)

L1 scoping is “quick and correct” (deep scoping is L2).

#### 8.5 Scope Snapshot Checklist

| Scope Question | How to Check |
|----------------|--------------|
| How many accounts targeted? | Count distinct usernames in time window |
| How many source IPs involved? | Count distinct IPs; identify top talkers |
| Are attacks focused on one service (VPN/O365)? | Group by destination |
| Any successful logins anywhere? | Search for success events near failures |
| Any account lockouts spike? | Check lockout logs and counts |

---

### Step 6: Platform-Specific L1 Checks (What to Look For)

#### 8.6A Active Directory / Domain Controller Indicators (If Available)

| Signal | What It Means | Notes |
|--------|---------------|------|
| Many 4625 failures for same account | Brute force | Track source IP |
| 4740 account lockouts spikes | Spray/stuffing | Often multiple accounts |
| 4624 success from unusual workstation | Possible compromise | Escalate |
| 4768/4769 anomalies (Kerberos) | Kerberos abuse patterns | L2/L3 review needed |

#### 8.6B Entra ID / M365 Indicators (If Available)

| Signal | What It Means | Notes |
|--------|---------------|------|
| Risky sign-in flagged | Account compromise likelihood | Escalate to L2 |
| New device / unfamiliar sign-in | Possible compromise | Correlate with phishing |
| “MFA requirement satisfied by claim” | Token replay / session theft | AiTM possible |
| Consent to app after suspicious sign-in | OAuth persistence | Escalate |

#### 8.6C VPN Indicators

| Signal | Meaning |
|--------|---------|
| Failures from many IPs | Distributed spray |
| Success followed by internal scans | Compromise + pivot |
| Repeated auth from same IP | Brute force |
| Sudden new country | Compromise |

---

## 9. Evidence Preservation (L1 Minimum Standard)

### 9.1 Evidence to Attach/Reference in Ticket

| Evidence Item | Minimum Detail |
|--------------|----------------|
| Sign-in log export | Include success/failure + UTC timestamps |
| MFA logs | Prompt count, approve/deny, device |
| Source IP enrichment | Geo + ASN/provider + TI reputation |
| Account list targeted | Distinct accounts targeted |
| “Success events” list | Any successful logins and details |
| Screenshots | Dashboards or charts showing spikes |

### 9.2 Evidence Handling Notes
- Use restricted access where possible (identity logs can contain PII).
- Preserve logs early (some cloud logs have limited retention).

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 10. Severity Recommendation (L1 Standard)

### 10.1 Severity Matrix (Credential Attacks)

| Scenario | Recommended Severity |
|----------|----------------------|
| Privileged account successful login (suspicious) | P1 |
| Multiple account successes (spray/stuffing) | P1 |
| Service account success or suspected compromise | P1/P2 (SOC Lead decides) |
| Standard user success from suspicious IP/geo | P2 |
| MFA fatigue with user approval | P2 |
| Failed-only spray targeting many users | P2/P3 (based on volume) |
| Failed-only brute force on one user | P3 |
| Low-volume noise, blocked, no success | P4 |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

## 11. L1 Allowed Actions (Without Additional Approval)

L1 can do **safe administrative steps** without impacting users:

| Allowed Action | Notes |
|---------------|------|
| Collect and export logs | Required |
| IOC enrichment of source IPs | Use TI sources |
| Create/Update ticket with standard fields | Required |
| Submit block request (IP/ASN) | Follow SOP; do not implement directly unless authorized |
| Notify SOC Lead per escalation rules | Required |

L1 must **NOT**:
- reset passwords
- revoke sessions/tokens
- disable accounts
- change Conditional Access policies
- modify lockout policies
without SOC Lead/IAM approval.

---

## 12. Ticket Template (Copy-Paste Standard)

Title:
- Credential Attack – [Service] – [Target Account/Group] – [Source IP/Geo] – [Severity Recommendation]

Required fields:
- Alert Source:
- Detection Time (UTC):
- Service Targeted (VPN/O365/AD/App):
- Attack Type (Brute Force/Spray/Stuffing/MFA Fatigue/Token Replay/Other):
- Target Account(s) (count + key accounts):
- Account Criticality (Privileged/Finance/Service/Standard):
- Results (Success/Failures/Blocked):
- MFA Details (Challenged/Approved/Denied/Not Required):
- Source IPs (top 5) + Geo/ASN:
- Volume Metrics (#failures, #successes, time window):
- Evidence Captured (exports/screenshots):
- Recommended Severity + Justification:
- Escalations Made (SOC Lead/L2/IAM/IR Team) + timestamps:
- Containment Recommendations (block IP, lockout review, etc.):

---

## 13. Escalation Criteria (L1)

### 13.1 Escalate to L2 if any of the following:

| Condition | Why |
|----------|-----|
| Any successful login suspected malicious | Compromise confirmation needed |
| MFA fatigue suspected | Identity response needed |
| Spray/stuffing targeting many accounts | Scope and mitigation needed |
| Token replay indicators | Advanced identity review needed |
| Service accounts targeted/success | Persistence risk |

### 13.2 Escalate to SOC Lead immediately if:

| Condition | Why |
|----------|-----|
| Privileged accounts targeted or success | Critical risk |
| Multiple successful logins | Active compromise |
| Hybrid (cloud + VPN) targeting | Coordinated campaign |
| Source is known malicious / TOR/VPS | High confidence attacker |

### 13.3 Escalate to IR Team if:

| Condition | Why |
|----------|-----|
| Domain Admin/global admin compromise suspected | Major incident |
| Post-auth activity suggests intrusion | Potential ransomware/data breach |
| Widespread compromise across business units | Coordinated IR needed |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/`

---

## 14. Common L1 Mistakes to Avoid

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Closing as noise without checking success logins | Missed compromise | Always check for success near failures |
| Ignoring cloud logs | Hybrid compromise missed | Review Entra ID sign-ins |
| Assuming MFA blocks everything | Token replay possible | Look for “MFA already satisfied” |
| Not identifying privileged account targeting | High impact missed | Tag and escalate |
| Not capturing evidence before remediation | Evidence lost | Export logs first |
| Over-blocking IP ranges | Business disruption | Use approvals + targeted blocks |

---

## 15. MSSP Client Handling Notes

For MSSP-managed environments:
- confirm tenant/client attribution before evidence capture
- follow client SLA for P1/P2 notifications via SDM
- do not implement identity changes without client approval (unless emergency authority exists)
- keep evidence strictly client-scoped

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

## 16. Related Documents

| Document | Path |
|---------|------|
| Credential Attack Master | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-Master.md` |
| Credential Attack L2 Investigation | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-L2-Investigation.md` |
| Credential Attack Containment | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-Containment.md` |
| Credential Attack MITRE Mapping | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-MITRE-Mapping.md` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |
| Escalation Paths | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/` |

---

## 17. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | SOC Lead / SOC Manager | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**