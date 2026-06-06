# Playbook: Credential Attack Response (Master)

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Credential Attack Response (Master) |
| Document ID | IR-PB-CRA-001 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | SOC Manager / IR Team Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 credential attack incident |

---

## 2. Purpose

This master playbook defines the end-to-end response procedures for
credential-based attacks across enterprise and MSSP-managed environments.

Credential attacks include:
- brute force attacks
- password spraying
- credential stuffing
- Kerberoasting
- Pass-the-Hash
- Pass-the-Ticket
- LDAP enumeration
- MFA bypass attempts
- token theft
- credential phishing outcomes

Credential attacks are critical because:
- they exploit the identity layer
- they frequently lead to broader compromise
- they may not trigger traditional malware detections
- they use legitimate authentication mechanisms
- successful attacks can lead to ransomware or data theft

This playbook standardizes:
- alert triage and classification
- investigation and scoping
- containment and account remediation
- detection improvements
- escalation criteria

---

## 3. Scope

Applies to:
- Active Directory environments
- Azure AD / Entra ID environments
- cloud identity platforms
- VPN authentication attacks
- web application login attacks
- API authentication abuse
- MSSP-managed client environments

Includes:
- on-premises identity
- cloud identity
- hybrid identity
- privileged accounts
- service accounts

---

## 4. Definitions

| Term | Definition |
|:-----|------------|
| Brute Force | Systematic password guessing |
| Password Spray | Low-and-slow attempts across many accounts |
| Credential Stuffing | Using leaked credentials to test accounts |
| Kerberoasting | Requesting service tickets to crack offline |
| Pass-the-Hash | Reusing captured NTLM hashes |
| Pass-the-Ticket | Reusing Kerberos tickets |
| MFA Fatigue | Overwhelming user with MFA prompts |
| Token Theft | Stealing authentication tokens |
| Credential Stuffing | Using breached credential lists |

---

## 5. Credential Attack Categories

| Category | Description | Risk |
|----------|-------------|------|
| Brute Force | Repeated password attempts | High |
| Password Spray | Distributed slow attacks | High |
| Credential Stuffing | Known credential reuse | High |
| Kerberoasting | Service account targeting | Critical |
| Pass-the-Hash | NTLM hash reuse | Critical |
| MFA Fatigue | Push bombing | High |
| Token Theft | Session/OAuth abuse | Critical |

---

# 6. Severity Classification Guidance

Severity depends on:
- account type targeted
- success of attack
- privilege level
- lateral movement indicators
- business impact

---

## 6.1 Credential Attack Severity Matrix

| Scenario | Recommended Severity |
|----------|----------------------|
| Privileged account compromise | P1 |
| Domain Admin compromise suspected | P1 |
| Widespread password spray with successes | P1 |
| Service account compromise | P2 |
| Standard user compromise confirmed | P2 |
| Failed brute force only | P3 |
| Low-volume failed attempts | P4 |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

# 7. Activation Criteria

Activate this playbook when any of the following occur:

| Trigger | Example |
|---------|---------|
| High failed login volume | Brute force indicator |
| Low-and-slow failed logins | Password spray |
| Known credential list usage | Stuffing indicator |
| Service ticket anomalies | Kerberoasting |
| NTLM hash usage anomalies | Pass-the-Hash |
| MFA push fatigue | Repeated push |
| Token reuse anomalies | Token theft |
| Account lockout spike | Active spray |

---

# 8. Roles and Responsibilities

| Role | Responsibilities |
|------|------------------|
| L1 SOC Analyst | Alert validation and escalation |
| L2 SOC Analyst | Investigation and scope analysis |
| L3 Analyst | Advanced identity forensics |
| SOC Lead | Coordination and escalation |
| IR Team | Major incident response |
| IAM Team | Account remediation |
| AD/Identity Team | Directory investigation |
| MSSP SDM | Client communication |

Reference:
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx`

---

# 9. Credential Attack Incident Lifecycle

| Phase | Description |
|------|-------------|
| Detection and Triage | Validate attack indicators |
| Investigation | Scope and classify attack |
| Containment | Stop attack and remediate accounts |
| Eradication | Remove attacker access |
| Recovery | Restore secure authentication |
| Post-Incident | Improve detections and controls |

---

# 10. High-Level Response Workflow

---

## Phase A – Detection and Qualification

Activities:
- validate authentication anomalies
- identify attack type
- determine success indicators
- classify severity

Reference:
`02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-L1-Triage.md`

---

## Phase B – Investigation and Scoping

Activities:
- identify targeted accounts
- determine attack method
- review authentication logs
- identify successful compromises
- assess lateral movement

Reference:
`02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-L2-Investigation.md`

---

## Phase C – Containment

Activities:
- block attack sources
- reset compromised credentials
- revoke sessions and tokens
- enforce MFA
- apply conditional access

Reference:
`02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-Containment.md`

---

## Phase D – Post-Incident

Activities:
- improve detection coverage
- improve authentication controls
- conduct lessons learned
- track action items

Reference:
`08_POST-INCIDENT/`

---

# 11. Key Investigation Areas

| Investigation Area | Purpose |
|--------------------|---------|
| Authentication logs | Attack validation |
| Account lockouts | Spray detection |
| Service ticket requests | Kerberoasting review |
| NTLM authentication | Pass-the-Hash |
| MFA logs | Fatigue detection |
| Token usage | Session abuse |
| Lateral movement | Post-compromise review |

---

# 12. Escalation Criteria

---

## 12.1 Escalate to IR Team if:

| Condition | Reason |
|-----------|--------|
| Privileged account compromised | Enterprise risk |
| Domain Admin compromise | Critical escalation |
| Widespread successful attacks | Major incident |
| Lateral movement confirmed | Ransomware precursor risk |

---

## 12.2 Escalate to L3 if:

| Condition | Reason |
|-----------|--------|
| Kerberoasting suspected | Advanced analysis |
| Pass-the-Hash indicators | Memory forensics |
| Token theft suspected | Identity forensics |
| Unknown attack vector | Advanced investigation |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/`

---

# 13. Evidence Handling Requirements

Preserve:
- authentication logs
- AD event logs
- MFA logs
- cloud sign-in logs
- network logs
- endpoint telemetry

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 14. Common Credential Attack Response Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Resetting only attacked accounts | Missing compromised accounts |
| Ignoring service accounts | Persistence risk |
| Failing to revoke sessions | Attacker remains active |
| Not checking lateral movement | Wider compromise missed |
| Blocking only known IPs | Attacker rotates IPs |
| Ignoring cloud identity | Hybrid compromise missed |

---

# 15. MSSP Considerations

For MSSP-managed environments:
- follow client-specific identity architectures
- coordinate account remediation with client IAM teams
- maintain evidence segregation
- follow client SLA timelines
- document all containment actions

Reference:
`09_MSSP-SPECIFIC/`

---

# 16. Related Documents

| Document | Path |
|---------|------|
| Credential Attack L1 Triage | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-L1-Triage.md` |
| Credential Attack L2 Investigation | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-L2-Investigation.md` |
| Credential Attack Containment | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-Containment.md` |
| Credential Attack MITRE Mapping | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-MITRE-Mapping.md` |
| Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 17. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | SOC Manager / IR Team Lead | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**