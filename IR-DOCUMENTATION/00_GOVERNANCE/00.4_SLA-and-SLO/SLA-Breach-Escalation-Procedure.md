# SLA Breach Escalation Procedure – Incident Response

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Document Name | SLA Breach Escalation Procedure |
| Document ID | IR-SLA-003 |
| Version | 1.0 |
| Effective Date | 14-May-2026 |
| Owner | SOC Manager / Service Delivery Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Purpose

This document defines the procedure to be followed when an SLA
breach occurs or is at risk of occurring during incident response
operations — for both internal SOC SLAs and MSSP client SLAs.

It ensures:
- Breaches are identified early and escalated appropriately
- Corrective actions are taken without delay
- Breaches are documented for audit and improvement purposes
- Client trust and regulatory obligations are maintained

---

## 3. Scope

Applies to:
- All SOC tiers (L1/L2/L3)
- SOC Lead / Shift Lead
- IR Team
- MSSP Service Delivery Manager (SDM)
- SOC Manager / Head of SOC

Covers:
- Internal SLA breaches (SOC operations)
- MSSP client SLA breaches

---

## 4. SLA Breach Categories

### 4.1 At-Risk (Warning State)
SLA timer has reached **75% of allowed time** with no completion.

Action:
- SOC Lead alerted immediately
- Analyst provides status update in ticket
- SOC Lead assesses if acceleration is required

---

### 4.2 Breached (SLA Missed)
SLA timer has **exceeded the defined target time**.

Action:
- Immediate escalation per procedure below
- Breach documented in ticket
- Root cause identified

---

### 4.3 Repeated Breach
Same SLA metric breached **2 or more times** in a rolling 30-day
period.

Action:
- Formal service improvement plan initiated
- SOC Manager/CISO briefed
- Client notification (if MSSP breach)

---

## 5. SLA Breach Escalation Matrix

| Breach Type | Severity | Immediate Escalation To | Timeframe |
|-------------|----------|------------------------|-----------|
| Triage SLA breach (P1) | Critical | SOC Lead → SOC Manager | Immediately |
| Triage SLA breach (P2) | High | SOC Lead | Within 5 mins |
| Triage SLA breach (P3/P4) | Medium/Low | SOC Lead (next check-in) | Within 15 mins |
| Escalation SLA breach (P1) | Critical | SOC Lead → IR Team → CISO | Immediately |
| Escalation SLA breach (P2) | High | SOC Lead → SOC Manager | Within 10 mins |
| Notification SLA breach (P1/P2) | Critical/High | SOC Lead → SDM → Manager | Immediately |
| Containment SLA breach (P1) | Critical | IR Team Lead → CISO | Immediately |
| Containment SLA breach (P2) | High | SOC Lead → IR Team | Within 15 mins |
| Resolution SLA breach (P1/P2) | Critical/High | IR Team → CISO → Management | Immediately |
| Client SLA breach (any severity) | Varies | SDM → SOC Manager → Account Lead | Per client SLA |
| Repeated SLA breach (any) | Any | SOC Manager → CISO → Management | Within 24 hrs |

---

## 6. Step-by-Step Breach Procedure

---

### Step 1 – Identify Breach / At-Risk State

**Who:** L1/L2 Analyst or automated ticket system alert

Actions:
- [ ] Check SLA timer in ticketing system
- [ ] Identify which SLA metric is at risk or breached
- [ ] Note timestamp of breach
- [ ] Document in ticket: `SLA BREACH - [Metric] - [Time] - [Reason]`

---

### Step 2 – Immediate Notification to SOC Lead

**Who:** Analyst identifies → SOC Lead notified

Actions:
- [ ] Notify SOC Lead via:
  - Direct message (Teams/Slack/Radio) for P1/P2
  - Ticket update for P3/P4
- [ ] SOC Lead acknowledges within:
  - P1: 2 minutes
  - P2: 5 minutes
  - P3/P4: 15 minutes

---

### Step 3 – SOC Lead Assessment & Acceleration

**Who:** SOC Lead

Actions:
- [ ] Review current incident status and blocker
- [ ] Identify reason for breach:
  - Resource constraint
  - Technical complexity
  - Awaiting client/third party
  - Tool/access issue
- [ ] Accelerate response:
  - Re-assign analyst
  - Pull in L3/IR Team
  - Request additional resources from management
- [ ] Update incident ticket with breach note and action taken

---

### Step 4 – Management Notification (P1/P2 Breaches)

**Who:** SOC Lead → SOC Manager / CISO

Actions:
- [ ] Notify SOC Manager immediately for P1 breach
- [ ] Notify SOC Manager within 15 minutes for P2 breach
- [ ] Provide:
  - Incident ID and severity
  - SLA metric breached
  - Current status
  - Reason for breach
  - Action being taken

---

### Step 5 – Client Notification (MSSP Only)

**Who:** SOC Lead / SDM

Actions:
- [ ] Notify client primary contact when client SLA is breached
- [ ] Use approved communication template:

Subject: [URGENT] SLA Notification – Incident [ID] – [Client Name]

Dear [Client Contact],

We are writing to inform you that the [SLA metric] for Incident
[ID] has exceeded the agreed service level target of [X minutes].

Current Status: [Status]
Reason for Delay: [Reason]
Actions Being Taken: [Actions]
Expected Resolution: [ETA]

We apologize for this delay and are actively working to resolve
this incident as quickly as possible.

MSSP SOC Team

- [ ] Document client notification in incident ticket

---

### Step 6 – Breach Documentation

**Who:** SOC Lead / Analyst

Mandatory fields to complete in the ticket:

| Field | Entry Required |
|-------|---------------|
| SLA Metric Breached | e.g., Triage Time P1 |
| SLA Target | e.g., ≤ 5 minutes |
| Actual Time Taken | e.g., 12 minutes |
| Breach Duration | e.g., 7 minutes over SLA |
| Root Cause | e.g., Analyst queue overload |
| Action Taken | e.g., Escalated to L2 at [time] |
| Management Notified | Yes/No + Name + Time |
| Client Notified (MSSP) | Yes/No + Time |
| Preventive Action | e.g., Alert queue balancing |

---

### Step 7 – Post-Breach Review

**Who:** SOC Manager / IR Team Lead

Actions:
- [ ] Conduct breach review within 24 hours for P1/P2 breaches
- [ ] Identify:
  - Root cause
  - Contributing factors
  - Process/tool/resource gaps
- [ ] Define corrective actions with owners and deadlines
- [ ] Update SLA Breach Register

---

## 7. SLA Breach Register

All breaches must be recorded in the following register:

| Breach ID | Date | Incident ID | Severity | SLA Metric | Target | Actual | Duration Over | Root Cause | Action Taken | Owner | Status |
|-----------|------|------------|---------|------------|--------|--------|---------------|-----------|--------------|-------|--------|
| BR-001 | | | | | | | | | | | |

> Maintained by: SOC Manager / SDM
> Reviewed: Monthly in Operational Review Meeting

---

## 8. Repeated Breach – Formal Improvement Plan

If the same SLA metric is breached 2+ times in 30 days:

- [ ] SOC Manager initiates formal Service Improvement Plan (SIP)
- [ ] SIP includes:
  - Gap analysis
  - Root cause summary
  - Corrective actions with deadlines
  - Resource requirements
  - Review checkpoints
- [ ] SIP presented to CISO within 5 business days
- [ ] For MSSP clients: SIP shared with client in QBR or
      dedicated review call

---

## 9. SLA Breach Metrics Reporting

Breach metrics are included in:

| Report | Frequency | Audience |
|--------|-----------|---------|
| Daily SOC Report | Daily | SOC Lead / Manager |
| Weekly Incident Summary | Weekly | Management |
| Monthly Metrics Report | Monthly | Management / Client |
| Quarterly SLA Review | Quarterly | Management / Client |
| Annual IR Review | Annual | CISO / Board |

Reference:
`07_REPORTING/07.2_Operational-Reports/`

---

## 10. SLA Breach Prevention Measures

The SOC implements the following to prevent breaches:

- Automated SLA timer alerts in ticketing system
- Alert queue monitoring dashboards
- Shift handover with open SLA status review
- Balanced analyst alert queue management
- Escalation path reminders in playbooks
- Regular SLA awareness in SOC briefings

---

## 11. Review & Update

This document shall be reviewed:
- Quarterly
- After any P1/P2 SLA breach
- After formal client SLA breach notification
- Upon SOC process or tooling changes

---

## 12. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**