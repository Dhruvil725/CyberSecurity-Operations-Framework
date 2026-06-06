# Internal SLA Definitions – Incident Response

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Document Name | Internal SLA Definitions – IR |
| Document ID | IR-SLA-001 |
| Version | 1.0 |
| Effective Date | 14-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Purpose

This document defines the internal Service Level Agreements (SLAs) for the Security Operations Center (SOC) and Incident Response Team (IRT) across all incident severity levels.

These SLAs govern:
- Alert triage timelines
- Incident response timelines
- Escalation timelines
- Communication timelines
- Resolution and closure timelines

All SOC staff and IR Team members are bound by these SLAs.

---

## 3. Scope

Applies to:
- All internal SOC operations (L1/L2/L3)
- SOC Lead / Shift Lead
- IR Team
- IT Operations (containment/recovery activities)
- MSSP-monitored client environments (separate client SLAs defined in MSSP-Client-SLA-Template.md)

---

## 4. SLA Definition – Terminology

| Term | Definition |
|------|------------|
| Detection Time | Time from event occurrence to alert generation |
| Triage Time | Time from alert receipt to initial classification |
| Escalation Time | Time from triage to escalation to next tier |
| Acknowledgement Time | Time for receiving tier to acknowledge escalation |
| Response Time | Time from incident declaration to active response |
| Containment Time | Time from response to containment action completion |
| Resolution Time | Time from containment to full eradication/recovery |
| Closure Time | Time from resolution to formal ticket closure |
| Notification Time | Time from incident declaration to stakeholder notification |

---

## 5. Severity Level SLA Table

---

### P1 – Critical

| SLA Metric | Target |
|------------|--------|
| Triage Time (L1) | ≤ 5 minutes |
| Escalation to L2 | ≤ 10 minutes |
| L2 Acknowledgement | ≤ 5 minutes |
| Escalation to L3 / IRT | ≤ 15 minutes |
| IR Team Activation | ≤ 30 minutes |
| Initial Containment | ≤ 1 hour |
| Management Notification | ≤ 15 minutes from declaration |
| Status Update Cadence | Every 30 minutes |
| Resolution Target | ≤ 4 hours (containment) |
| Formal Closure | ≤ 5 business days post recovery |

---

### P2 – High

| SLA Metric | Target |
|------------|--------|
| Triage Time (L1) | ≤ 10 minutes |
| Escalation to L2 | ≤ 15 minutes |
| L2 Acknowledgement | ≤ 10 minutes |
| Escalation to L3 (if needed) | ≤ 30 minutes |
| Initial Containment | ≤ 2 hours |
| Management Notification | ≤ 30 minutes from declaration |
| Status Update Cadence | Every 1 hour |
| Resolution Target | ≤ 8 hours (containment) |
| Formal Closure | ≤ 5 business days post recovery |

---

### P3 – Medium

| SLA Metric | Target |
|------------|--------|
| Triage Time (L1) | ≤ 15 minutes |
| Escalation to L2 | ≤ 30 minutes |
| L2 Acknowledgement | ≤ 15 minutes |
| Initial Response | ≤ 4 hours |
| Status Update Cadence | Every 4 hours |
| Resolution Target | ≤ 24 hours |
| Formal Closure | ≤ 3 business days post resolution |

---

### P4 – Low

| SLA Metric | Target |
|------------|--------|
| Triage Time (L1) | ≤ 30 minutes |
| Escalation (if needed) | ≤ 1 hour |
| Initial Response | ≤ 8 hours |
| Status Update Cadence | As needed / next shift |
| Resolution Target | ≤ 72 hours |
| Formal Closure | ≤ 5 business days post resolution |

---

## 6. SLA Clock Rules

- SLA clock **starts** when alert is received in SIEM/EDR/Ticketing system
- SLA clock **pauses** only when:
  - Awaiting client/business owner approval for containment action
  - Awaiting third-party vendor response
  - Documented and approved hold (SOC Lead approval required)
- SLA clock **resumes** immediately upon approval/response received
- All pauses must be documented in the incident ticket

---

## 7. Escalation SLA Breach Actions

| Breach Scenario | Action Required |
|-----------------|----------------|
| L1 triage SLA breached | SOC Lead notified immediately |
| L2 escalation SLA breached | SOC Lead escalates to L3/IRT directly |
| Management notification SLA breached | SOC Lead directly contacts Manager/CISO |
| Containment SLA breached | IR Team Lead notified; bridge call convened |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLA-Breach-Escalation-Procedure.md`

---

## 8. SLA Measurement & Reporting

SLAs are measured:
- Per incident ticket (timestamps captured at each stage)
- Reported in:
  - Daily SOC Report
  - Weekly Incident Summary
  - Monthly Metrics Report
  - Quarterly SLA Review

Reference:
`07_REPORTING/07.2_Operational-Reports/`

---

## 9. SLA Exceptions

Exceptions may occur due to:
- Complexity of multi-vector attacks
- Dependency on external vendors/authorities
- Resource constraints (declared and approved)

All exceptions must be documented in:
`00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`

---

## 10. Roles Responsible for SLA Adherence

| Role | SLA Responsibility |
|------|-------------------|
| L1 Analyst | Triage SLA |
| L2 Analyst | Investigation and escalation SLA |
| L3 Analyst | Advanced analysis SLA |
| SOC Lead | Overall SLA governance per shift |
| IR Team | Containment and resolution SLA |
| SOC Manager | SLA reporting and improvement |

---

## 11. Review & Update

This document shall be reviewed:
- Quarterly
- After major SLA breaches
- After significant incidents
- Upon team structure changes

---

## 12. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**