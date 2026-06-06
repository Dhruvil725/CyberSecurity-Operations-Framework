# Regulatory Body Contacts

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Register – Regulatory Body Contacts |
| Document ID | DIR-CON-004 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Compliance Lead / SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This register maintains verified contact points for **regulatory bodies** and official reporting channels required during cyber incidents (e.g., RBI and CERT-In as applicable).

Maintaining accurate regulatory contacts is critical because:

- Regulatory reporting is time-bound and must use correct official channels
- Incorrect contact routing can cause delayed reporting and compliance exposure
- Evidence of reporting submission requires traceable details (who/what/when/how)
- Regulatory interactions may require legal/compliance oversight
- MSSP operations may support clients under varying regulatory obligations and contracts

This register ensures:

- Central, controlled list of regulator contact channels and reporting mechanisms
- Clear mapping of which regulator applies to which scenario/client type
- Standard fields for documentation and audit traceability
- Quarterly verification to prevent stale contact details

---

# 3. Scope

This register includes contacts for:

| Regulator / Authority | Examples |
|---|---|
| CERT-In | Incident reporting channels and escalation |
| RBI | Incident reporting and cyber framework compliance contacts |
| Sectoral regulators (if applicable) | Additional regulators based on business/clients |
| Government advisories | Official points for urgent coordination (as applicable) |

Out of scope:

- Law enforcement contacts (separate register)
- Vendor contacts (separate register)
- Client contacts (separate register)

References:  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Law-Enforcement-Contacts.md`  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/MSSP-Client-Contacts.md`

---

# 4. Confidentiality and Handling Requirements (Mandatory)

This document is **Restricted**.

| Control | Requirement |
|---|---|
| Storage | Access-controlled repository only |
| Access | Compliance, Legal, CISO, SOC Manager, IR Team Lead (need-to-know) |
| Sharing | Do not share externally; do not paste contact details in tickets/chats |
| Updates | Logged and verified quarterly |
| Export | Requires Compliance Lead + CISO approval |

Ticket documentation rule:
- Record regulator contact at high level: “CERT-In notified via official channel, time (UTC), reference ID.”

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| Compliance Lead | Owns regulator contact accuracy and reporting channel validation |
| Legal Counsel | Advises on disclosure wording and evidence sharing constraints |
| CISO | Approves major regulator interactions and submissions |
| SOC Manager | Ensures operational readiness and escalation alignment |
| IR Team Lead | Provides incident facts, timelines, and evidence references |
| MSSP SDM | Coordinates client regulatory responsibilities and approvals |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md`

---

# 6. Verification and Update Process

## 6.1 Quarterly Verification (Mandatory)

Compliance Lead must:

- Validate official reporting email addresses/portal URLs/phone hotlines
- Confirm any updated regulatory forms/templates
- Confirm any changes to reporting timelines or submission requirements
- Update “Last Verified Date (UTC)” for each entry
- Record changes in revision history

## 6.2 Emergency Update

If a contact channel fails during a P1:

- Update within 4 hours
- Notify SOC Manager + CISO
- Record in revision history

---

# 7. Standard Fields (Mandatory)

Each entry must include:

| Field | Requirement |
|---|---|
| Regulator Name | Mandatory |
| Jurisdiction | Mandatory |
| Purpose | Mandatory (incident reporting / advisory / coordination) |
| Official Reporting Channels | Mandatory (email/portal/phone) |
| Working Hours | Mandatory |
| Information Required | Recommended (minimum fields for submission) |
| Submission Acknowledgment | Recommended (how reference IDs are issued) |
| Follow-up Method | Recommended |
| Notes / Constraints | Recommended |
| Last Verified Date (UTC) | Mandatory |

---

# 8. Regulatory Contacts Register (Fill-In Tables)

> Populate with the official channels used by your organization and/or clients. Use role-based contacts and official public reporting channels where possible.

## 8.1 CERT-In (India)

| Field | Value |
|---|---|
| Regulator Name | CERT-In |
| Jurisdiction | India |
| Purpose | Incident reporting and coordination |
| Official Channels | `Email/Portal/Phone (per latest CERT-In guidance)` |
| Working Hours | `24x7 (as applicable)` |
| Information Required | Incident summary, timelines, impacted systems, IOCs, actions taken |
| Acknowledgment Method | Reference/ack number (if provided) |
| Follow-up | Email/portal case thread |
| Notes | Validate against latest CERT-In directions each review |
| Last Verified Date (UTC) | `YYYY-MM-DD` |

Reference SOP:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`

---

## 8.2 RBI (India)

| Field | Value |
|---|---|
| Regulator Name | RBI |
| Jurisdiction | India (BFSI) |
| Purpose | Cyber incident and material outage reporting for regulated entities |
| Official Channels | `As defined by regulated entity’s RBI reporting arrangement` |
| Working Hours | `Business/On-call (as applicable)` |
| Information Required | Incident type, impact, timeline, actions taken, corrective actions |
| Acknowledgment Method | Reference/ack number (if provided) |
| Follow-up | As per RBI correspondence process |
| Notes | Reporting method may be entity-specific; confirm per client |
| Last Verified Date (UTC) | `YYYY-MM-DD` |

Reference SOP:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`

---

## 8.3 Additional Regulators (If Applicable)

> Add entries based on organizational/client footprint.

| Regulator Name | Jurisdiction | Purpose | Channels (Email/Portal/Phone) | Working Hours | Notes | Last Verified (UTC) |
|---|---|---|---|---|---|---:|
|  |  |  |  |  |  |  |

---

# 9. Regulator Engagement Documentation Checklist (Mandatory)

When any regulator is engaged/submission is made, record in incident ticket:

| Item | Requirement |
|---|---|
| Regulator engaged | Mandatory |
| Reason/reportability decision | Mandatory |
| Submission time (UTC) | Mandatory |
| Channel used | Mandatory |
| Reference/ack number | Mandatory if provided |
| Copy of submission | Mandatory (secure evidence repository reference) |
| Follow-up requests and responses | Mandatory |
| Legal/Compliance approval record | Mandatory |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 10. MSSP Considerations (Mandatory)

For MSSP clients:

- Determine whether the client or MSSP submits regulator reports (contract-driven)
- Ensure client approvals for submissions (if MSSP submits)
- Ensure tenant-scoped reporting and evidence segregation
- Store regulator correspondence in client-specific evidence location

References:  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`  
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 11. Related Documents

| Document | Path |
|---|---|
| CERT-In Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md` |
| RBI Incident Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md` |
| Legal Counsel Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Law Enforcement Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Law-Enforcement-Contacts.md` |
| Internal Contacts Master | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Internal-Contacts-Master.md` |
| MSSP Client Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/MSSP-Client-Contacts.md` |

---

# 12. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Compliance Lead / SOC Manager | Initial version |

---

# 13. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**