# Status Update Template – 30 Minutes (P1)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Template – Status Update (30 Minutes) |
| Document ID | COM-TPL-006 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Lead / SOC Operations Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This template standardizes the **30-minute status update** cadence required for **P1 (Critical)** incidents.

A structured 30-minute status update is critical because:

- P1 incidents require continuous coordination and leadership visibility
- Frequent updates reduce confusion and support timely decisions
- It supports SLA compliance and measurable incident handling performance
- It provides an audit-ready timeline of actions, decisions, and outcomes
- It ensures MSSP clients receive consistent and accurate updates where required

This template ensures:

- Every status update includes the minimum operational and executive information
- Confirmed facts are separated from hypotheses
- Decisions required are clearly highlighted
- Actions and evidence references are documented consistently

---

# 3. Scope

Use this template:

- For **P1** incidents: mandatory every 30 minutes (minimum)
- For P2 incidents: when SOC Lead requires 30-minute cadence due to risk/impact

Recipients may include:

- SOC/IR teams and IT operations
- Management/CISO
- MSSP client stakeholders (if applicable and contractually required)

---

# 4. Instructions (Mandatory)

- Use UTC timestamps.
- Provide “since last update” changes first.
- Avoid raw sensitive evidence in the update body; provide secure references.
- Record each status update in:
  - incident ticket, and/or
  - bridge call notes document linked to the ticket

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

# 5. Template (Copy/Paste)

## Subject Line (Recommended)

**`P1 Status Update – [Incident ID] – [Incident Category] – Update #[N] – [UTC Time]`**

Example:
`P1 Status Update – INC-2026-0102 – Ransomware – Update #3 – 2026-05-25 05:00 UTC`

---

## Message Body (Mandatory)

**Incident Ticket ID:** `INC-YYYY-####`  
**Severity:** P1 (Critical)  
**Incident Category:** `...`  
**Client/Tenant (if applicable):** `Client ID/Name`  
**Update Number:** `#N`  
**Update Time (UTC):** `YYYY-MM-DD HH:MM`  
**Incident Commander:** `Name/Role`  
**Bridge Call:** `Active/Not Active`  

---

### 1) Since Last Update (What Changed)
- `Change 1…`
- `Change 2…`
- `Change 3…`

---

### 2) Current Status (One Line)
- `Triage / Investigation / Containment / Eradication / Recovery / Monitoring`

---

### 3) Scope (Best Known)
- **Affected Hosts:** `...`
- **Affected Users/Accounts:** `...`
- **Affected Services:** `...`
- **Spread Indicators:** `Yes/No/Unknown` + notes
- **Exfiltration Indicators:** `Yes/No/Unknown` + notes

---

### 4) Actions Completed (Last 30 Minutes)
> Include execution + authorization + time (UTC) for major actions.

| Action | Owner (Executor) | Authorized By | Time (UTC) | Outcome |
|---|---|---|---:|---|
|  |  |  |  |  |
|  |  |  |  |  |

---

### 5) Current Investigation Findings (Key Points)
- **Confirmed facts:**  
  - `...`
- **Suspected/under validation:**  
  - `...`

**Evidence references (safe links/IDs):**  
- SIEM: `...`  
- EDR: `...`  
- Network/Cloud: `...`  

---

### 6) Containment / Recovery Progress
- **Containment status:** `Not started / In progress / Completed` + notes
- **Recovery status:** `Not started / In progress / Completed` + notes
- **Risks:** `reinfection risk / persistence unknown / spread risk` + notes

---

### 7) Decisions Required (If Any)
> Highlight approvals needed and time sensitivity.

| Decision Needed | Why | Needed By (UTC) | Owner | Status |
|---|---|---:|---|---|
|  |  |  |  |  |

---

### 8) Communications / Notifications
- **Management notified:** `Yes/No` + time (UTC)
- **Compliance/Legal engaged:** `Yes/No` + time (UTC)
- **Client notified (MSSP):** `Yes/No` + time (UTC)
- **Regulatory readiness check:** `Required/Not required/Under assessment`

---

### 9) Next 30-Minute Plan (Next Actions)
| Next Action | Owner | Due (UTC) | Notes |
|---|---|---:|---|
|  |  |  |  |
|  |  |  |  |

---

### 10) Next Update Commitment
- **Next update by (UTC):** `YYYY-MM-DD HH:MM` (30 minutes cadence)
- **Next bridge checkpoint:** `YYYY-MM-DD HH:MM`

---

# 6. Mandatory Ticket Entry (After Sending)

Update the incident ticket with:

- Update number and timestamp (UTC)
- Summary of changes since last update
- Actions completed and outcomes
- Decisions made and approvals
- Evidence references added/updated
- Next update time commitment

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 7. Related Documents

| Document | Path |
|---|---|
| P1 Initial Alert Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/P1-Initial-Alert-Template.md` |
| Bridge Call Agenda Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Bridge-Call-Agenda-Template.md` |
| Management Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md` |
| Status Update Template (1 hr) | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-1hr.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Emergency Escalation – P1 | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md` |

---

# 8. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | SOC Lead / SOC Operations Lead | Initial version |

---

# 9. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**