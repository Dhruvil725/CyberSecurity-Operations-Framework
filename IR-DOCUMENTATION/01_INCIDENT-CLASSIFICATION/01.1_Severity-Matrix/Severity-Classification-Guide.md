# Severity Classification Guide – Incident Response

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Document Name | Severity Classification Guide |
| Document ID | IR-CLS-001 |
| Version | 1.0 |
| Effective Date | 14-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Purpose

This document provides the master guide for classifying
cybersecurity incidents and alerts into severity levels
(P1–P4) across all SOC tiers, IR Team, and MSSP client
environments.

It ensures:
- Consistent classification across all shifts and analysts
- Correct SLA timers are applied from first triage
- Appropriate escalation paths are triggered
- Right resources are assigned at the right time
- Audit-ready documentation from first ticket creation

This is the **primary reference** for all analysts during
triage. All P1–P4 detailed definitions reference this guide.

---

## 3. Scope

Applies to:
- All security alerts triaged by SOC (L1/L2/L3)
- All declared incidents (internal and MSSP client)
- All attack categories (see 01.2_Incident-Categories)
- Cloud, on-premises, and hybrid environments
- All shifts (24x7 operations)

Excludes:
- IT operational incidents with no security component
- Planned maintenance windows
- Authorized penetration testing (note in ticket as authorized)

---

## 4. Severity Levels – Quick Reference

| Level | Name | Color Code | Response Mode | Team Required |
|-------|------|------------|---------------|---------------|
| P1 | Critical | 🔴 RED | Immediate – Crisis Response | L1 + L2 + L3 + IRT + Management |
| P2 | High | 🟠 ORANGE | Urgent – Active Investigation | L1 + L2 + SOC Lead |
| P3 | Medium | 🟡 YELLOW | Investigate within shift | L1 + L2 |
| P4 | Low | 🔵 BLUE | Standard triage and close | L1 |

---

## 5. Four Dimensions of Classification

Every alert/incident must be assessed across these
four dimensions before assigning severity:

---

### Dimension 1 – Business Impact

| Score | Level | Description |
|-------|-------|-------------|
| 4 | P1 | Core business service disrupted or imminent disruption |
| 3 | P2 | Non-critical service degraded; operational risk |
| 2 | P3 | Isolated activity; no service impact |
| 1 | P4 | No operational impact; informational only |

---

### Dimension 2 – Scope of Compromise

| Score | Level | Description |
|-------|-------|-------------|
| 4 | P1 | Multiple systems, servers, or domain-level compromise |
| 3 | P2 | Single server or limited user set confirmed |
| 2 | P3 | Single endpoint or single user (contained) |
| 1 | P4 | Single alert, single asset, blocked/prevented |

---

### Dimension 3 – Data Sensitivity

| Score | Level | Description |
|-------|-------|-------------|
| 4 | P1 | Customer PII / financial / credentials confirmed exposed |
| 3 | P2 | Internal confidential data at risk or accessed |
| 2 | P3 | No sensitive data confirmed; low-risk data only |
| 1 | P4 | No data involved; configuration or log-level only |

---

### Dimension 4 – Threat Activity

| Score | Level | Description |
|-------|-------|-------------|
| 4 | P1 | Active exploitation, ransomware, C2, confirmed APT |
| 3 | P2 | Malware execution, privilege escalation, credential compromise |
| 2 | P3 | Suspicious behavior, anomalous activity, low confidence |
| 1 | P4 | Blocked/prevented, informational, policy violation |

---

### Scoring Guide

> Use the highest single dimension score as the primary
> severity indicator. If two or more dimensions score 3+,
> consider upgrading one level.

| Highest Dimension Score | Assigned Severity |
|-------------------------|-------------------|
| 4 in any dimension | P1 |
| 3 in any dimension | P2 |
| 2 in any dimension | P3 |
| All dimensions = 1 | P4 |
| 3 in two+ dimensions | Consider P1 |
| 2 in two+ dimensions | Consider P2 |

---

## 6. Severity Definition Summary Table

| Field | P1 – Critical | P2 – High | P3 – Medium | P4 – Low |
|-------|--------------|-----------|-------------|---------|
| Triage SLA | ≤ 5 mins | ≤ 10 mins | ≤ 15 mins | ≤ 30 mins |
| Escalation | L2 ≤ 10 mins | L2 ≤ 15 mins | L2 if needed | L1 handles |
| Bridge Call | Yes – mandatory | Yes – if needed | No | No |
| Management Notify | ≤ 15 mins | ≤ 30 mins | Not required | Not required |
| Client Notify (MSSP) | ≤ 15 mins | ≤ 30 mins | Per contract | Monthly summary |
| IR Team Activate | Yes – mandatory | If needed | No | No |
| Containment Target | ≤ 1 hour | ≤ 2 hours | Within shift | Not required |
| Resolution Target | ≤ 4 hours | ≤ 8 hours | ≤ 24 hours | ≤ 72 hours |
| PIR Required | Yes | Yes | No (unless P2+) | No |
| RCA Required | Yes | Yes | No | No |
| Regulatory Review | Yes | Assess | No | No |
| Report Required | Yes – within 24hrs | Yes – within 48hrs | Weekly summary | Monthly summary |

---

## 7. Classification Decision Tree

Use this step-by-step flow during every triage:
🟩 **START**

│
▼
❓ **Is there ACTIVE harm to business operations occurring RIGHT NOW?**
│
├── ✅ **YES** → 🔍 _Check data exposure_
│   │
│   ├── 🔒 **Sensitive data (PII / financial / credentials) confirmed at risk?**
│   │       ├── ✅ YES → 🔴 **P1 – CRITICAL**
│   │       └── ❌ NO  → 🖥️ **Is it multi‑system impact?**
│   │               ├── ✅ YES → 🔴 **P1 – CRITICAL**
│   │               └── ❌ NO  → 🟠 **P2 – HIGH**
│   │
│
└── ❌ **NO** → ⚠️ **Is unauthorized / suspicious activity CONFIRMED on a system?**
    │
    ├── ✅ YES → 🧑‍💻 **Is it a privileged account or critical server?**
    │       ├── ✅ YES → 🟠 **P2 – HIGH**
    │       └── ❌ NO  → 💻 **Is it single endpoint or single user?**
    │               ├── ✅ YES → 🟡 **P3 – MEDIUM**
    │               └── ❌ NO  → 🟠 **P2 – HIGH**
    │
    └── ❌ NO → 🧱 **Was the activity BLOCKED or PREVENTED?**
            ├── ✅ YES → 🔵 **P4 – LOW**
            └── ❌ NO  → 📋 **Is it informational / policy‑level alert?**
                    ├── ✅ YES → 🔵 **P4 – LOW**
                    └── ❌ NO  → 📞 **Escalate to SOC Lead for manual review**

🏁 **END**


---

## 8. Attack Category to Default Severity Mapping

Use as a starting point during triage.
**Always validate against actual impact before finalizing.**

| Attack Category | Default Severity | May Escalate To |
|----------------|-----------------|----------------|
| Ransomware – Active Encryption | P1 | Stay P1 |
| Ransomware – Precursor Activity | P2 | P1 |
| Phishing – User Credentials Entered | P2 | P1 |
| Phishing – Email Blocked (No Click) | P4 | P3 |
| Phishing – Click Confirmed, No Creds | P3 | P2 |
| Malware Execution – Confirmed | P2 | P1 |
| Malware Blocked – No Execution | P4 | P3 |
| Data Exfiltration – Confirmed | P1 | Stay P1 |
| Data Exfiltration – Suspected | P2 | P1 |
| Insider Threat – Confirmed Access | P2 | P1 |
| Insider Threat – Anomalous Behavior | P3 | P2 |
| DDoS – Service Down | P1 | Stay P1 |
| DDoS – Degraded Performance | P2 | P1 |
| Credential Attack – Success | P2 | P1 |
| Credential Attack – Failed | P4 | P3 |
| Web Application – Exploit Success | P2 | P1 |
| Web Application – Probing/Scanning | P4 | P3 |
| Supply Chain – Confirmed | P1 | Stay P1 |
| Supply Chain – Suspected | P2 | P1 |
| APT – Confirmed | P1 | Stay P1 |
| APT – Suspected TTPs | P2 | P1 |
| Cloud – Admin Takeover | P1 | Stay P1 |
| Cloud – Anomalous Login | P3 | P2 |
| Network Intrusion – Active | P2 | P1 |
| Network Port Scan – External Blocked | P4 | P3 |
| Zero Day – Confirmed Exploitation | P1 | Stay P1 |
| Zero Day – Patching Required | P3 | P2 |

---

## 9. Reclassification Rules

Severity may be changed during the incident lifecycle.

### Upgrade Rules
| Trigger | From | To | Approver |
|---------|------|----|---------|
| Lateral movement detected | P3 | P2 | SOC Lead |
| Sensitive data confirmed at risk | P2 | P1 | SOC Lead |
| Domain controller impacted | P2 | P1 | SOC Lead |
| Ransomware confirmed | P2/P3 | P1 | SOC Lead |
| Scope expands beyond initial host | P3 | P2 | SOC Lead |

### Downgrade Rules
| Trigger | From | To | Approver |
|---------|------|----|---------|
| Investigation confirms FP | P2 | P4 close | SOC Lead |
| Scope confirmed single endpoint (low risk) | P2 | P3 | SOC Lead |
| Data confirmed not at risk | P1 | P2 | SOC Lead + Manager |
| Threat fully contained (limited scope) | P1 | P2 | SOC Lead + Manager |

### Reclassification Documentation Required
Every reclassification must include in ticket:

**RECLASSIFICATION NOTE:**
**Previous Severity: [P?]**
**New Severity: [P?]**
**Reason: [Why reclassified]**
**Approved By: [Name + Role]**
**Timestamp: [Date Time]**


---

## 10. MSSP Client Classification Notes

For MSSP-managed clients:

- Client may define custom severity thresholds
  in their Client-IR-Policy.md
- Business impact must be assessed from CLIENT
  perspective not MSSP internal
- Client approval required before downgrading P1 → P2
- Client must be notified of reclassification for P1/P2

Reference:
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/
[CLIENT-NAME]/Client-IR-Policy.md`

---

## 11. Compliance Alignment

| Framework | Alignment |
|-----------|-----------|
| ISO 27001 | A.5.25 – Assessment of information security events |
| NIST CSF | RS.AN-1 – Notifications investigated |
| NIST SP 800-61 | Section 3.2 – Detection and Analysis |
| RBI CSF | V.1 – Incident Response Plan |
| CERT-In | Standard triage and classification requirements |

---

## 12. Common Classification Mistakes to Avoid

| Mistake | Impact | Correct Approach |
|---------|--------|-----------------|
| Classifying blocked events as P2+ | SLA waste; resource drain | Blocked = P4 unless execution confirmed |
| Under-classifying ransomware precursors | P1 declared too late | Any ransomware TTP = P2 minimum |
| Not considering business context | Wrong priority assigned | Always ask: what is the client's business impact? |
| Classifying authorized pentest as incident | False SLA metrics | Check authorized activity register first |
| Not reclassifying when scope expands | P1 response delayed | Continuously reassess during investigation |

---

## 13. Quick Reference Card (Print-Friendly)

> **When in doubt → go higher → downgrade later with SOC Lead.**

---

## ⏱️ SLA Targets (Triage / Escalation / Notification)

| **Metric** | 🔴 P1 Critical | 🟠 P2 High | 🟡 P3 Medium | 🔵 P4 Low |
|:------------|:---------------:|:------------:|:--------------:|:-------------:|
| **Triage Start** | ≤ **5 min** | ≤ **10 min** | ≤ **15 min** | ≤ **30 min** |
| **Bridge Call Activation** | 🛠️ Immediate | ⚙️ If required | 🚫 None | 🚫 None |
| **Mgmt / Client Notification** | 🕴️ ≤ 15 min | 🕴️ ≤ 30 min | ❌ Not required | ❌ Not required |
| **IRT Activation** | 🚨 Yes – mandatory | ⚙️ If needed | ❌ No | ❌ No |
| **Containment Target** | ≤ 1 hour | ≤ 2 hours | Within shift | ≤ 72 hours |
| **Resolution Target** | ≤ 4 hours | ≤ 8 hours | ≤ 24 hours | ≤ 72 hours |
| **Status Updates** | Every 30 min | Every 1 hr | Shift summary | Daily / batch |
| **PIR / RCA Required** | ✅ Yes | ✅ Yes | ⚪ Optional | ⚪ Not needed |

---

## 🔥 One‑Glance Table (Display Version)

| **Tier** | 🔴 P1 | 🟠 P2 | 🟡 P3 | 🔵 P4 |
|:----------|:----:|:----:|:----:|:----:|
| **Title** | 🧨 Critical | ⚡ High | 🔍 Medium | 💬 Low |
| **Triage SLA** | ⏱️ ≤ 5 min | ⏱️ ≤ 10 min | ⏱️ ≤ 15 min | ⏱️ ≤ 30 min |
| **Bridge Call** | 🔔 NOW | 🔔 If needed | 🚫 No | 🚫 No |
| **Mgmt Notify** | 🕴️ ≤ 15 min | 🕴️ ≤ 30 min | – | – |
| **IRT Activate** | 🚨 Yes | ⚙️ If needed | – | – |
| **Scope Examples** | Ransomware, Data Breach | Privilege Escalation, Malware | Suspicious Activity | Blocked Threat, Info |

---


## 14. Related Documents

| Document | Path |
|---------|------|
| P1 Critical Definition | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md |
| P2 High Definition | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P2-High-Definition.md |
| P3 Medium Definition | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P3-Medium-Definition.md |
| P4 Low Definition | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P4-Low-Definition.md |
| Severity Escalation Criteria | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Escalation-Criteria.md |
| Triage Decision Tree | 01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Master-Triage-Decision-Tree.md |
| Internal SLA Definitions | 00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md |
| RACI Matrix | 00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx |

---

## 15. Review & Update

This document shall be reviewed:
- Quarterly
- After every major classification error/lesson learned
- Upon addition of new attack categories
- Upon SOC tooling or detection changes

---

## 16. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**