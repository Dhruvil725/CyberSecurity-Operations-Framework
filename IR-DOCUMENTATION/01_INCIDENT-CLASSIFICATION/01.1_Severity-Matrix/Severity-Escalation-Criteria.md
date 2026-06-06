# Severity Escalation Criteria – Incident Response

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Document Name | Severity Escalation Criteria – IR |
| Document ID | IR-CLS-006 |
| Version | 1.0 |
| Effective Date | 14-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Purpose

This document defines the decision rules and trigger conditions
for **escalating** security incidents between severity levels
(P4 → P3 → P2 → P1) and for **downgrading** them when appropriate.

It ensures that:
- Escalations are **timely** and **well-justified**
- Proper **approval and documentation** are applied
- SLA and resource activation occur at the correct time
- The organization maintains **situational awareness**

---

## 3. Scope

Applies to:
- All SOC analysts and IR Team members
- All incidents managed under the IR-DOCUMENTATION framework
- Both internal and MSSP client environments

---

## 4. Escalation Principles

1. **Escalate early, downgrade later.**  
   It’s safer to over-classify than to under-classify.

2. **Escalate on potential, not just confirmation.**  
   If the pattern shows credible indicators of expansion or data exposure, escalate immediately.

3. **Document every escalation action.**  
   The ticket must contain the timestamp, reason, and approver.

4. **Confirm escalation acknowledgment.**  
   Receiving tier (L2/L3/IRT) must confirm SLA-based acknowledgment.

5. **Escalate severity and priority simultaneously.**  
   P-level controls SLA timers; ticket priority must match severity.

---

## 5. Escalation Triggers

Use this as a service-wide reference.

---

### 5.1 P4 → P3 (Informational → Suspicious)

| Trigger ID | Trigger | Action | Approver |
|-------------|----------|---------|-----------|
| ESC-401 | Execution or process creation confirmed | Escalate to P3 | L1 Analyst + SOC Lead |
| ESC-402 | User interaction confirmed (phishing click/open) | Escalate to P3 | L1 Analyst + SOC Lead |
| ESC-403 | Same alert repeated >3 times on same host | Escalate to P3 | L1 Analyst |
| ESC-404 | Alert seen on multiple hosts/users | Escalate to P3 | L1 Analyst |
| ESC-405 | False positive rejected (not FP) | Escalate to P3 | L1 Analyst |
| ESC-406 | Account login anomalies detected | Escalate to P3 | L1 Analyst |
| ESC-407 | IOC related to active campaign in TI feeds | Escalate to P3 | L1 Analyst |
| ESC-408 | Recurring monthly pattern with user interaction | Escalate to P3 | SOC Lead |

---

### 5.2 P3 → P2 (Suspicious → Confirmed)

| Trigger ID | Trigger | Action | Approver |
|-------------|----------|---------|-----------|
| ESC-321 | Confirmed malware execution on one or more hosts | Escalate to P2 | SOC Lead |
| ESC-322 | Unauthorized privilege escalation | Escalate to P2 | SOC Lead |
| ESC-323 | Lateral movement attempt confirmed | Escalate to P2 | SOC Lead |
| ESC-324 | Sensitive data at potential risk (unconfirmed exfil) | Escalate to P2 | SOC Lead |
| ESC-325 | Credential compromise of admin/non-admin user | Escalate to P2 | SOC Lead |
| ESC-326 | Web application exploit partially successful | Escalate to P2 | SOC Lead |
| ESC-327 | Multiple related incidents (2+ hosts/systems) | Escalate to P2 | SOC Lead |
| ESC-328 | Privileged account used unexpectedly | Escalate to P2 | SOC Lead |
| ESC-329 | External communication with suspicious server/IP | Escalate to P2 | SOC Lead |

---

### 5.3 P2 → P1 (Significant → Critical)

| Trigger ID | Trigger | Action | Approver |
|-------------|----------|---------|-----------|
| ESC-211 | Ransomware encryption or wiper execution confirmed | Escalate to P1 | SOC Lead + IR Team |
| ESC-212 | Sensitive data exfiltration confirmed | Escalate to P1 | SOC Lead + IR Team |
| ESC-213 | Domain Controller, AD, or IAM system compromise | Escalate to P1 | SOC Lead + IR Team |
| ESC-214 | Business-critical system outage caused by attack | Escalate to P1 | SOC Lead + IR Team |
| ESC-215 | Privileged identity compromise (Domain Admin/CISO) | Escalate to P1 | SOC Lead + CISO |
| ESC-216 | Multi-vector or APT-style coordinated attack | Escalate to P1 | SOC Lead + CISO |
| ESC-217 | Recurrence of recently contained critical threat | Escalate to P1 | IR Team Lead |
| ESC-218 | Supply chain or third-party compromise affecting production | Escalate to P1 | CISO / Manager |
| ESC-219 | Regulatory impact confirmed (RBI/CERT-In required) | Escalate to P1 | Compliance / CISO |
| ESC-220 | Encryption of shared resources or backups | Escalate to P1 | SOC Lead / IR Team |

---

## 6. Downward Reclassification (De-Escalation)

When investigation confirms downgraded severity, apply these rules:

| From → To | Condition | Approval Required | Documentation Required |
|------------|-----------|-------------------|------------------------|
| P1 → P2 | Incident impact limited to single system / no data exfiltration | CISO / SOC Manager | RCA confirms limited scope |
| P2 → P3 | Activity contained; no user compromise / valid change found | SOC Lead | Ticket note and log evidence |
| P3 → P4 | Alert confirmed false positive / irrelevant | SOC Lead | Ticket note and closure |
| P1 → P4 | False positive confirmed at elevated stage (rare) | CISO | RCA + corrective action record |

---

## 7. Escalation Workflow Summary
L1 Analyst detects alert
│
├── If FP confirmed → Remain P4 / Close
│
├── If suspicious / user interaction → P3
│
├── If confirmed malicious or privilege escalation → P2
│
└── If severe service/data impact → P1


---

## 8. Ticket Documentation Requirements

Each escalation (upward or downward) must include the following within the ticket:

**[SEVERITY CHANGE LOG]**
**Previous Severity: [P#]**
**New Severity: [P#]**
**Reason/Trigger: [Brief explanation]**
**Evidence Reference: [Log/file ID, screenshot, IOC, etc.]**
**Approval / Approver: [Name, Role]**
**Time Escalated: [YYYY-MM-DD HH:MM UTC]**


SLA timers reset automatically based on the new severity level.

---

## 9. Escalation Communication Rules

| Stakeholder | Severity Escalation To Notify | Medium | Timing |
|-------------|-------------------------------|--------|--------|
| SOC Lead | P3 → P2 or higher | Teams / Call | Immediately |
| SOC Manager | P2 → P1 | Call + Email | < 5 minutes |
| CISO | P1 declared | Bridge Call | Immediate |
| MSSP Client | P2 or higher | Email / Portal | Within 15 minutes |
| GRC / Compliance | P1 or Regulatory Trigger | Email | Within 30 minutes |

---

## 10. Escalation with Regulatory Impact

When escalation reaches **P1** and involves regulated data or BFSI sector:

| Regulatory Trigger | Action |
|---------------------|--------|
| RBI Cyber Framework | Report to RBI as per Cyber Security Directions |
| CERT-In | Notify CERT-In within required timeline |
| ISO 27001 ISMS | Log as Major Nonconformity (if applicable) |
| Client / Regulator Contract | Follow defined reporting SLA (within hours) |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 11. Escalation Matrix (Quick View)

| From Severity | To Severity | Immediate Contact | Escalation Medium | Max Response Time |
|----------------|--------------|-------------------|-------------------|-------------------|
| P4 → P3 | SOC Lead | Ticket / Message | 15 mins |
| P3 → P2 | SOC Lead / L2 Analyst | Call / Ticket | 10 mins |
| P2 → P1 | SOC Lead / IR Team | Call + Email / Bridge | 5 mins |
| P1 | Management / CISO | Phone + Bridge | Immediate |
| For Client SLA Impact | SDM + Client Contact | Email / Call | 15–30 mins |
| Regulatory | GRC / Compliance | Email | As per law |

---

## 12. Audit Evidence Required for Escalation Compliance

Maintain the following for audit trails:

- Ticket with complete escalation history
- Evidence of detection and validation
- Communication logs with timestamps
- Bridge call minutes (P1/P2)
- Approval evidence (emails or ticket notes)
- SLA metrics before and after escalation
- RCA referencing escalation accuracy

---

## 13. Escalation Effectiveness KPIs

Measure accuracy and timeliness quarterly:

| Metric | Description | Target |
|--------|--------------|---------|
| Escalation Accuracy | % of correct upgrades vs. total escalations | ≥ 95% |
| Escalation Timeliness | % within SLA escalation windows | ≥ 95% |
| False Positive Escalation | % of escalations later downgraded to FP | ≤ 5% |
| SLA Breach Rate Post Escalation | % of escalations causing SLA miss | ≤ 2% |
| P1 Notification Compliance | % P1 where management notified ≤ 15 mins | 100% |

---

## 14. Review & Improvement

Escalation efficiency shall be reviewed:

- Monthly in SOC managerial review
- Quarterly in SLA/SLO Review
- After each critical incident (P1)
- After auditor recommendations

Improvements tracked in:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Action-Items-Tracker.xlsx`

---

## 15. Roles & Responsibilities Summary

| Role | Escalation Responsibility |
|------|---------------------------|
| L1 Analyst | Identify and trigger initial escalation |
| L2 Analyst | Confirm escalation, enrich with details |
| L3 Analyst | Validate severity and coordinate root cause |
| SOC Lead | Approve and communicate escalation |
| IR Team Lead | Direct containment and recovery actions |
| CISO | Strategic oversight and regulatory decision |
| MSSP SDM | Manage client communication and SLA implications |
| Compliance | Manage regulatory notifications and documentation |

---

## 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
