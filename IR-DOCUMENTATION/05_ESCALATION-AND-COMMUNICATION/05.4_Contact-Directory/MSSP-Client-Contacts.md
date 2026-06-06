# MSSP Client Contacts (Incident Response)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Register – MSSP Client Contacts |
| Document ID | DIR-CON-003 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | MSSP Service Delivery Manager (SDM) / SOC Operations Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This register maintains the **authoritative client contact directory** required for MSSP incident response operations, including:

- time-bound client notifications (SLA-driven),
- bridge call participation,
- containment approvals,
- evidence handling coordination,
- executive escalation, and
- post-incident communications.

Client contact accuracy is critical because:

- Incorrect or outdated contacts cause notification delays and SLA breaches
- Certain containment actions require explicit client authorization (contract-dependent)
- MSSP operations must prevent cross-client disclosure and maintain strict tenant segregation
- Audit readiness depends on evidence of who was notified, when, and how
- Regulatory reporting coordination may require client compliance/legal contacts

This register ensures:

- Standard fields and role-based contact mapping per client
- Primary + backup contacts for P1/P2 events
- Clear notification preferences and approvals authority
- Controlled access to sensitive contact data
- Reliable escalation routing during high-pressure incidents

---

# 3. Scope

This register applies to **all MSSP-managed clients** and contains contacts for:

| Contact Category | Examples |
|---|---|
| Incident contacts | Client SOC, IT incident manager |
| Decision/approval contacts | CISO, Head of IT, IAM owner |
| Technical contacts | Network admin, EDR admin, cloud admin |
| Compliance/legal | Compliance officer, legal counsel, DPO/privacy |
| Business impact contacts | Application owner, business owner |
| Executive escalation | CIO/CTO/COO (as defined) |
| After-hours/on-call | On-call hotline, rotation reference |

Out of scope:

- Internal contacts (kept in Internal Contacts Master)
- Vendor contacts (kept separately)
- Regulatory body contacts (kept separately)

References:  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Internal-Contacts-Master.md`  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Vendor-Contacts.md`

---

# 4. Confidentiality and Handling Requirements (Mandatory)

This document is **Restricted**.

## 4.1 Handling Rules

| Control | Requirement |
|---|---|
| Storage | Access-controlled repository only |
| Access | SOC Lead, SOC Manager, MSSP SDM, IR Team Lead, on-call analysts (need-to-know) |
| Sharing | Do not share externally; do not paste full contact details into general tickets/chats |
| Export | Requires SOC Manager + MSSP SDM approval |
| Printing | Avoid; if used for crisis kit, store locked and track issuance |
| Updates | Logged; verified quarterly |

## 4.2 Ticket Documentation Rule

Do **not** paste client phone numbers/emails into incident tickets.  
Record only: “Client notified: [Client Name], [Role/Name], time (UTC), method, outcome.”

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| MSSP SDM | Owns client contact accuracy; coordinates client notifications and approvals |
| SOC Operations Lead | Ensures operational availability during P1/P2; validates use during escalations |
| SOC Lead | Uses register for escalation and bridge calls; ensures SLA compliance |
| SOC Manager | Oversight; resolves client contact failures; approves access and exports |
| Client Account Owner / AM (if applicable) | Supports relationship routing and executive escalation |
| Clients | Provide updates for role changes and on-call schedules within agreed timeline |

---

# 6. Client Contact Governance (Mandatory)

## 6.1 Minimum Coverage Requirements (Per Client)

Each client must have:

| Role | Requirement |
|---|---|
| Primary Incident Contact | Mandatory |
| Backup Incident Contact | Mandatory |
| Decision Maker (Containment Approval) | Mandatory |
| Backup Decision Maker | Mandatory |
| Compliance/Legal Contact | Mandatory for regulated clients |
| After-hours/on-call contact | Mandatory if 24x7 SLA |
| Bridge call participant list | Recommended |

## 6.2 Contact Verification Requirement

Quarterly verification must confirm:

- names and roles current
- numbers/emails valid
- escalation tiers correct
- time zone and hours accurate
- client approval authority correct

---

# 7. Standard Fields (Mandatory)

Each client contact entry must include:

| Field | Requirement |
|---|---|
| Client Name | Mandatory |
| Client ID | Mandatory |
| Client Type | BFSI / Enterprise / SMB / Other |
| Client SLA Tier | Gold/Silver/Bronze (or contract label) |
| Data Sensitivity Notes | Optional (e.g., “regulated data”) |
| Primary Incident Contact | Mandatory |
| Backup Incident Contact | Mandatory |
| Approval Authority Contact | Mandatory |
| Backup Approval Authority | Mandatory |
| Compliance Contact | Mandatory for regulated |
| Legal Contact | Recommended |
| On-call method | Mandatory (hotline/phone/email) |
| Time zone | Mandatory |
| Preferred notification method | Recommended |
| Client escalation instructions | Mandatory (if special constraints exist) |
| Last Verified Date (UTC) | Mandatory |

---

# 8. Client Notification and Approval Notes (Operational)

## 8.1 Typical Client Approvals That May Be Required

| Action | Often Requires Client Approval? |
|---|---|
| EDR host isolation | Yes (contract-dependent) |
| Disable privileged accounts | Yes (some clients allow P1 break-glass) |
| Firewall blocks impacting business | Yes |
| Quarantine VLAN / segmentation | Yes |
| Disk/memory acquisition | Yes |
| Cloud key rotation / session revocation | Yes |
| Regulatory submission on client’s behalf | Yes (written authorization required) |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`

## 8.2 Special Constraints Field (Mandatory to Capture if Any)

Examples of constraints to record per client:

- “Do not isolate production servers without CIO approval”
- “Client handles firewall changes; MSSP provides recommendation only”
- “All P2 must be notified; P3 optional”
- “No WhatsApp/SMS communications permitted”
- “Data residency: evidence must stay in client country”

---

# 9. Register Template (Client Contact Tables)

> Add one section per client. Keep this document role-based and structured.

## 9.1 Client Profile Header (Per Client)

| Field | Value |
|---|---|
| Client Name |  |
| Client ID |  |
| SLA Tier |  |
| Industry / Regulatory |  |
| Primary Time Zone |  |
| Notification Window | 24x7 / Business hours / Custom |
| Preferred Notification Method | Phone/Email/Portal |
| Client Ticketing Integration | Yes/No + details |
| Special Escalation Constraints |  |
| Last Verified Date (UTC) |  |

---

## 9.2 Incident Contacts (Per Client)

| Contact Role | Name | Title | Phone | Email | Backup? | Hours | Preferred Method | Notes |
|---|---|---|---|---|---|---|---|---|
| Primary Incident Contact |  |  |  |  | No |  |  |  |
| Backup Incident Contact |  |  |  |  | Yes |  |  |  |
| SOC/IT Incident Manager |  |  |  |  |  |  |  |  |
| Bridge Call Participant |  |  |  |  |  |  |  |  |

---

## 9.3 Containment Approval Contacts (Per Client)

| Approval Type | Approver Name | Title | Phone | Email | Backup Approver | Notes |
|---|---|---|---|---|---|---|
| EDR isolation approval |  |  |  |  |  |  |
| Account disable/reset approval |  |  |  |  |  |  |
| Firewall block approval |  |  |  |  |  |  |
| Forensic acquisition approval |  |  |  |  |  |  |
| Major outage decision |  |  |  |  |  |  |

---

## 9.4 Compliance / Legal / Privacy Contacts (Per Client)

| Role | Name | Title | Phone | Email | Notes |
|---|---|---|---|---|---|
| Compliance |  |  |  |  |  |
| Legal |  |  |  |  |  |
| Privacy/DPO |  |  |  |  |  |

---

## 9.5 Executive Escalation Contacts (Per Client)

| Role | Name | Title | Phone | Email | Notes |
|---|---|---|---|---|---|
| Client CISO |  |  |  |  |  |
| Client CIO/CTO |  |  |  |  |  |
| Client COO/Exec |  |  |  |  |  |

---

# 10. Failure Handling (Client Unreachable)

If client does not acknowledge within SLA:

1. Call primary incident contact
2. Call backup incident contact
3. Escalate to approval authority contact
4. Escalate to executive escalation contact (if P1)
5. Notify SOC Manager + MSSP SDM
6. Document all attempts in ticket (time UTC, method, result)

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`

---

# 11. MSSP Segregation Controls (Mandatory)

| Control | Requirement |
|---|---|
| Tenant separation | Do not mix contacts across clients |
| Client-safe comms | Use client-specific email threads/portals |
| Access control | Restrict access to assigned analysts |
| Audit log | Track directory access where possible |
| Sanitization | No client contacts shared outside authorized MSSP roles |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 12. Related Documents

| Document | Path |
|---|---|
| Internal-to-MSSP Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md` |
| MSSP Client Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md` |
| Escalation Matrix – Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| Client IR Contacts (Client Folder) | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md` |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |
| Vendor Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Vendor-Contacts.md` |
| Regulatory Body Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Regulatory-Body-Contacts.md` |

---

# 13. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | MSSP SDM / SOC Operations Lead | Initial version |

---

# 14. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**