# P2 Initial Alert Template (High Incident)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Template – P2 Initial Alert |
| Document ID | COM-TPL-003 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Lead / SOC Operations Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This template standardizes the **initial alert notification** for **P2 (High)** incidents.

A standardized P2 initial alert is critical because:

- It ensures timely escalation and coordinated response for high-risk events
- It reduces inconsistent messaging across SOC, IT, and management teams
- It improves decision-making by presenting clear facts, scope, and next steps
- It supports SLA compliance and predictable update cadence
- It provides an audit-ready record of notification and incident posture
- It supports MSSP client communications with tenant-safe messaging

This template ensures:

- Minimum required fields are consistently communicated
- Facts vs assumptions are clearly separated
- Planned investigation/containment steps are documented early
- Next update time and escalation path are defined

---

# 3. Scope

Use this template when:

- A P2 incident is declared (likely compromise / significant risk)
- A P3 is escalated to P2 due to new evidence
- A P2 requires multi-team coordination (IT ops, IAM, network)
- Client action/approval may be required (MSSP)

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P2-High-Definition.md`

---

# 4. Instructions (Mandatory)

- Use UTC timestamps.
- Do not include credentials or sensitive customer data in the message body.
- If incident scope is unclear, state “unknown” explicitly and list what is being validated.
- For MSSP, verify tenant/client ID before sending.

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 5. Template (Copy/Paste)

## Subject Line (Mandatory)

**`P2 HIGH – [Incident Category] – [Client/Business Unit] – [Primary System/Service] – [UTC Time]`**

Examples:
- `P2 HIGH – Malware – Internal – FIN-WS-12 – 2026-05-25 03:20 UTC`
- `P2 HIGH – Privileged Login Anomaly – ClientABC – VPN – 2026-05-25 08:05 UTC`

---

## Message Body (Mandatory)

**Severity:** P2 (High)  
**Incident Ticket ID:** `INC-YYYY-####`  
**Incident Category:** `Malware / Phishing / Credential Attack / Intrusion / Cloud / Other`  
**Client/Tenant (if applicable):** `Client ID + Name`  
**Detected At (UTC):** `YYYY-MM-DD HH:MM`  
**Detection Source:** `SIEM / EDR / User / Client / TI`  
**Assigned Owner:** `Name/Role (L2 preferred)`  

### 1) Summary (1–3 lines)
- `Short summary of what was detected and why it is P2`

### 2) What We Know (Confirmed Facts)
- `Fact 1…`
- `Fact 2…`

### 3) What We Suspect / Are Validating
- `Hypothesis 1…`
- `Hypothesis 2…`

### 4) Scope (Best Known at This Time)
- **Affected Hosts/Systems:** `...`
- **Affected Users/Accounts:** `...`
- **Criticality:** `Critical/High/Medium/Low`
- **Environment:** `Prod/Dev/Cloud`
- **Spread Indicators:** `Yes/No/Unknown`

### 5) Impact Assessment (Current)
- **Service impact:** `None / Limited / Unknown`
- **Data exposure risk:** `High/Medium/Low/Unknown` + rationale
- **Privilege risk:** `Standard / Privileged / Admin` + rationale

### 6) Actions Taken So Far
- `Action 1 – time (UTC) – owner`
- `Action 2 – time (UTC) – owner`

### 7) Planned Next Steps (Next 60–120 Minutes)
- `Investigation step 1 (e.g., EDR process tree review + hash validation)`
- `Investigation step 2 (e.g., SIEM correlation for related hosts/users)`
- `Containment candidate action (if needed) + approvals required`

### 8) Evidence Summary (High-Level)
- **SIEM:** `Rule/Alert IDs, query references`
- **EDR:** `Detection IDs, process indicators`
- **Network/Cloud:** `Relevant logs, destinations, actions`
- **IOCs/TTPs (if known):** `IPs/domains/hashes/techniques`

### 9) Escalation and Coordination
- **SOC Lead notified:** `Yes/No – time UTC`
- **IR Team engaged:** `Yes/No/Not yet – criteria`
- **Bridge call:** `Required/Not required (SOC Lead decision)`
- **Client notification (MSSP):** `Required/Not required – per SLA`

### 10) Next Update Commitment
- **Next update by (UTC):** `YYYY-MM-DD HH:MM`
- **Update cadence:** Every 60 minutes (minimum) or at milestones (as agreed)

---

# 6. Mandatory Ticket Update (After Sending)

Record in the incident ticket:

- Notification recipients (names/roles)
- Method (email/phone/chat)
- Notification time (UTC)
- Summary communicated
- Next update commitment

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 7. Related Documents

| Document | Path |
|---|---|
| Status Update Template (1 hr) | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-1hr.md` |
| Management Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md` |
| MSSP Client Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md` |
| Escalation Matrix – Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Severity Classification Guide | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md` |

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