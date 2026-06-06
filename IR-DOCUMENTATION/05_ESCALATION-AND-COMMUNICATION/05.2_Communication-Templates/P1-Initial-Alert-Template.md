# P1 Initial Alert Template (Critical Incident)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Template – P1 Initial Alert |
| Document ID | COM-TPL-002 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Lead / SOC Operations Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This template standardizes the **initial alert notification** for **P1 (Critical)** incidents.

A standardized P1 initial alert is critical because:

- It ensures immediate awareness and rapid activation of bridge call/IR team
- It provides a consistent executive-friendly summary while preserving key technical details
- It ensures SLA-aligned notification and reduces communication delays
- It creates an audit-ready communication record (who was notified, when, and what was known)
- It supports MSSP operations by ensuring tenant-safe and client-scoped messaging

This template ensures:

- Minimum required fields are always communicated
- Facts vs assumptions are clearly separated
- Decisions required are highlighted early
- Next update time and cadence is clearly set

---

# 3. Scope

Use this template when:

- A P1 is **declared** or **strongly suspected**
- A P2 rapidly escalates into a P1 due to new evidence
- Bridge call initiation is required

Applicable recipients (as needed):

- SOC Lead, SOC Manager, IR Team Lead
- CISO / executive stakeholders
- IT Ops / Network / Cloud leads
- Compliance/Legal (if breach/regulatory triggers possible)
- MSSP client contacts (if MSSP and contract requires)

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`

---

# 4. Instructions (Mandatory)

- Send via approved channels (P1 requires **phone/on-call** + written notification).
- Use UTC timestamps.
- Do not include sensitive data (credentials/PII) in the message body.
- If the incident is MSSP, verify tenant/client ID before sending.

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 5. Template (Copy/Paste)

## Subject Line (Mandatory)

**`P1 CRITICAL – [Incident Category] – [Client/Business Unit] – [Primary System/Service] – [UTC Time]`**

Examples:
- `P1 CRITICAL – Ransomware – Internal – File Server Cluster – 2026-05-25 04:12 UTC`
- `P1 CRITICAL – Data Exfiltration – ClientABC – M365 – 2026-05-25 09:30 UTC`

---

## Message Body (Mandatory)

**Severity:** P1 (Critical)  
**Incident Ticket ID:** `INC-YYYY-####`  
**Incident Category:** `Ransomware / Data Breach / Intrusion / Cloud / DDoS / Other`  
**Client/Tenant (if applicable):** `Client ID + Name`  
**Detected At (UTC):** `YYYY-MM-DD HH:MM`  
**Reported By / Detection Source:** `SIEM / EDR / User / Client / TI`  

### 1) What We Know (Confirmed Facts)
- `Fact 1…`
- `Fact 2…`
- `Fact 3…`

### 2) What We Suspect (Unconfirmed / Under Investigation)
- `Hypothesis 1…`
- `Hypothesis 2…`

### 3) Current Impact
- **Business Services Affected:** `...`
- **Systems/Hosts Affected (best known):** `...`
- **Users/Accounts Affected (best known):** `...`
- **Customer Impact:** `Yes/No/Unknown` + `details`
- **Data Exposure Risk:** `High/Medium/Low/Unknown` + `why`

### 4) Immediate Actions Taken (So Far)
> Include **who executed**, **who authorized**, and **time (UTC)** where possible.

- `Action 1 – executed by … – authorized by … – time …`
- `Action 2 – executed by … – authorized by … – time …`

### 5) Evidence Summary (High-Level)
- **SIEM:** `Rule/Alert IDs + short description`
- **EDR:** `Detection IDs + impacted hosts`
- **Network/Cloud:** `Firewall/proxy/cloud audit indicators`
- **IOCs/TTPs (if known):** `IPs/domains/hashes/techniques`

> Do not attach raw evidence in email unless approved. Provide secure references/paths.

### 6) Containment Plan (Next 30–60 Minutes)
- `Planned containment action 1…`
- `Planned containment action 2…`
- `Planned evidence preservation step…`

### 7) Decisions Required (If Any)
> Highlight approvals needed and timelines.

- `Decision required: …  Needed by: [UTC time]  Impact if delayed: …`

### 8) Bridge Call / War Room Details
- **Bridge Call Start Time (UTC):** `YYYY-MM-DD HH:MM`
- **Bridge Link / Dial-in:** `...`
- **War Room Channel:** `...`
- **Incident Commander:** `Name/Role`
- **Technical Lead:** `Name/Role`
- **Comms Lead:** `Name/Role`

### 9) Next Update Commitment
- **Next update by (UTC):** `YYYY-MM-DD HH:MM`
- **Update cadence:** Every 30 minutes (minimum)

---

# 6. Mandatory Ticket Update (After Sending)

After sending the P1 initial alert, record in the incident ticket:

- Who was notified (names/roles)
- Notification method (phone/email/chat)
- Notification timestamp (UTC)
- Summary of message
- Bridge call start time and link
- Next update commitment

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 7. Related Documents

| Document | Path |
|---|---|
| Bridge Call Agenda Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Bridge-Call-Agenda-Template.md` |
| Status Update Template (30 min) | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-30min.md` |
| Management Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md` |
| MSSP Client Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md` |
| Emergency Escalation – P1 | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |

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