# Internal Contacts Master (SOC / IR / IT / Management)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Register – Internal Contacts Master |
| Document ID | DIR-CON-001 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | SOC Manager / SOC Operations Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This document provides a single, controlled **Internal Contacts Master** used for incident response operations, SOC escalations, bridge calls, regulatory readiness coordination, and crisis communications.

A controlled contact directory is critical because:

- Incident response requires **time-bound escalation** and rapid stakeholder engagement
- Outdated contacts lead to delays, missed SLA targets, and ineffective containment
- Audit readiness requires evidence of a defined escalation chain and response governance
- Access to sensitive contact data must be restricted and monitored
- MSSP operations require clear delineation between internal contacts and client contacts

This register ensures:

- Standard fields and formats for all internal contacts
- Clear primary/backup contacts for critical roles (24x7 where required)
- Defined ownership and update process
- Controlled distribution and confidentiality handling
- Operational readiness for P1/P2 bridge calls

---

# 3. Scope

This contacts master includes internal contacts for:

| Function | Examples |
|---|---|
| SOC Operations | L1/L2/L3 on-call, SOC Lead, SOC Manager |
| IR Team | IR Team Lead, Forensics Lead, Incident Commander backups |
| IT Operations | Server, Endpoint, Network, Cloud, IAM/Identity, Backup/DR |
| Security Engineering | SIEM, EDR, Network Security, Vulnerability/Patch |
| Governance / Risk | Compliance, ISMS, GRC |
| Legal / Privacy | Legal Counsel, Privacy/DPO (if applicable) |
| HR | Insider threat coordination, employee actions |
| Facilities / Physical | Access control, CCTV, visitor logs (if needed) |
| Executive Leadership | CISO, CIO/CTO, COO/CEO (as defined) |
| Communications | PR/Corporate comms lead (if applicable) |

Out of scope:

- Client contacts (stored in `MSSP-Client-Contacts.md`)
- Vendor contacts (stored in `Vendor-Contacts.md`)
- Regulatory body contacts (stored in `Regulatory-Body-Contacts.md`)
- Third-party IR retainer contacts (stored in `Third-Party-IR-Retainer-Contacts.md`)

---

# 4. Confidentiality and Handling Requirements (Mandatory)

This document contains sensitive operational contact data.

## 4.1 Handling Rules

| Control | Requirement |
|---|---|
| Storage | Store only in approved, access-controlled repository |
| Access | Minimum necessary access (SOC/IR leadership + on-call staff) |
| Sharing | Do not share externally; do not paste into public tickets/chats |
| Printing | Avoid printing; if printed for crisis kit, store in locked cabinet |
| Updates | Changes must be logged and reviewed quarterly |
| Export | Exports require SOC Manager approval (and must be sanitized) |

## 4.2 Ticket Documentation Rule

Do **not** paste personal phone numbers/emails into general incident tickets.  
Instead, document: “Internal contact notified: [Role/Name], time (UTC), method (phone/email).”

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| SOC Operations Lead | Maintains accuracy of SOC/IR contact entries; manages on-call mapping |
| SOC Manager | Approves directory changes affecting escalation chain; ensures quarterly review |
| CISO | Approves document and major changes impacting executive escalation |
| Team Leads (Network/Cloud/IAM/etc.) | Provide updates for their teams; confirm backups and coverage |
| HR/Legal/Compliance Leads | Ensure their contact paths are correct for incident use |
| All listed contacts | Notify SOC Ops of changes to phone/email/role within 24 hours |

---

# 6. Minimum Data Fields (Standard)

Each contact entry must include:

| Field | Requirement |
|---|---|
| Full Name | Mandatory |
| Role / Title | Mandatory |
| Team / Function | Mandatory |
| Primary Email | Mandatory |
| Primary Phone | Mandatory |
| Backup Phone (optional) | Recommended |
| On-Call Coverage | Mandatory (Yes/No; schedule reference) |
| Time Zone | Mandatory |
| Escalation Tier | Mandatory (Operational / Management / Executive) |
| Authorized Actions | Recommended (e.g., “approve isolation,” “approve firewall change”) |
| Backup Contact | Mandatory for critical roles |
| Preferred Contact Method | Recommended (phone first for P1) |
| Notes | Optional (e.g., “do not call after 22:00 local unless P1”) |
| Last Verified Date (UTC) | Mandatory |

---

# 7. Escalation Coverage Requirements (Mandatory)

The following roles must have **primary + backup** coverage:

| Role | Coverage Requirement |
|---|---|
| SOC Lead | 24x7 (primary + backup) |
| IR Team Lead | 24x7 (primary + backup) |
| Network Security Lead / Firewall Admin | On-call for P1/P2 |
| IAM / Directory Services Lead | On-call for privileged compromise |
| EDR Admin | On-call for containment actions |
| SIEM Engineer | On-call for P1/P2 correlation and evidence exports |
| IT Ops Incident Manager | On-call for P1 |
| SOC Manager | On-call for P1 escalation |
| CISO | On-call for P1 and regulatory/breach risk |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md`

---

# 8. Update and Verification Process

## 8.1 Change Types

| Change Type | Examples | Approval |
|---|---|---|
| Minor update | Phone/email change | SOC Ops Lead |
| Role change | New SOC Lead, new IR Lead | SOC Manager |
| Executive change | CISO/CIO changes | CISO (or delegated) |
| On-call mapping update | Rotation changes | SOC Ops Lead (document schedule reference) |

## 8.2 Quarterly Verification (Mandatory)

Quarterly, SOC Ops Lead must:

1. Confirm each critical role has primary + backup
2. Validate on-call numbers and escalation paths
3. Confirm team leads certify their team contacts
4. Update “Last Verified Date (UTC)” for all entries reviewed
5. Record review completion in revision history

## 8.3 Emergency Updates (Mandatory)

For urgent corrections (e.g., wrong on-call number):

- Update within 4 hours
- Notify SOC Lead + SOC Manager
- Document update in revision history

---

# 9. Contact Directory Templates (Fill-In Tables)

> Populate the tables below. Add/remove rows as needed.

## 9.1 SOC Operations Contacts

| Name | Role | Coverage | Primary Phone | Primary Email | Backup Contact | Preferred Method | Time Zone | Last Verified (UTC) |
|---|---|---|---|---|---|---|---|---:|
| `[Full Name]` | SOC Lead | 24x7 On-call | `+__` | `__@__` | `[Name/Role]` | Phone | `UTC+__` | `YYYY-MM-DD` |
|  | L1 Lead / Shift Lead | 24x7 |  |  |  |  |  |  |
|  | L2 Lead | Business/On-call |  |  |  |  |  |  |
|  | L3 Lead | Business/On-call |  |  |  |  |  |  |
|  | SOC Operations Lead | Business/On-call |  |  |  |  |  |  |

---

## 9.2 IR Team and Forensics Contacts

| Name | Role | Coverage | Primary Phone | Primary Email | Backup Contact | Authorized Actions | Last Verified (UTC) |
|---|---|---|---|---|---|---|---:|
| `[Full Name]` | IR Team Lead (Incident Commander) | 24x7 On-call |  |  |  | Approve containment (P1) |  |
|  | Deputy IR Lead | 24x7 Backup |  |  |  | Approve containment |  |
|  | Forensics Lead | On-call |  |  |  | Approve forensic acquisition scope |  |
|  | Evidence Custodian | Business/On-call |  |  |  | Evidence storage access approvals |  |

References:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 9.3 IT Operations (Servers / Endpoints / Backup / DR)

| Name | Team | Role | Coverage | Primary Phone | Primary Email | Backup Contact | Notes | Last Verified (UTC) |
|---|---|---|---|---|---|---|---|---:|
|  | Server Ops | Lead | On-call |  |  |  |  |  |
|  | Endpoint Ops | Lead | On-call |  |  |  |  |  |
|  | Backup/DR | Lead | On-call |  |  |  | Critical for ransomware |  |
|  | IT Service Desk | Manager | 24x7 |  |  |  | User comms routing |  |

---

## 9.4 Network / Firewall / Cloud / IAM Contacts

| Name | Function | Role | Coverage | Primary Phone | Primary Email | Backup Contact | Authorized Actions | Last Verified (UTC) |
|---|---|---|---|---|---|---|---|---:|
|  | Network Security | Firewall Admin | On-call |  |  |  | Implement emergency block |  |
|  | Network Ops | Lead | On-call |  |  |  | VLAN isolation changes |  |
|  | Cloud Ops | Lead | On-call |  |  |  | Quarantine SG/VNET changes |  |
|  | IAM/AD | Lead | On-call |  |  |  | Disable accounts / reset creds |  |
|  | SIEM Engineering | Lead | On-call |  |  |  | Evidence exports / rule adjustments |  |
|  | EDR Admin | Lead | On-call |  |  |  | Isolate host / policy changes |  |

References:
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Containment-Commands.md`

---

## 9.5 GRC / Compliance / ISMS Contacts

| Name | Function | Role | Coverage | Primary Phone | Primary Email | Backup Contact | Last Verified (UTC) |
|---|---|---|---|---|---|---|---:|
|  | Compliance | Compliance Lead | On-call |  |  |  |  |
|  | ISMS | ISMS Manager | Business/On-call |  |  |  |  |
|  | GRC | GRC Manager | Business |  |  |  |  |

References:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 9.6 Legal / Privacy / HR Contacts

| Name | Function | Role | Coverage | Primary Phone | Primary Email | Backup Contact | Notes | Last Verified (UTC) |
|---|---|---|---|---|---|---|---|---:|
|  | Legal | Legal Counsel (Primary) | On-call |  |  |  | Privileged comms |  |
|  | Privacy | DPO/Privacy Lead | On-call |  |  |  | If personal data involved |  |
|  | HR | HR Lead | Business/On-call |  |  |  | Insider cases |  |

References:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`  
`02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md`

---

## 9.7 Executive and Crisis Communications Contacts

| Name | Function | Role | Coverage | Primary Phone | Primary Email | Backup Contact | Notes | Last Verified (UTC) |
|---|---|---|---|---|---|---|---|---:|
|  | Security | CISO | On-call |  |  |  | P1 + regulatory |  |
|  | IT | CIO/CTO | On-call |  |  |  | Major outage |  |
|  | Operations | COO (if applicable) | On-call |  |  |  | Business impact |  |
|  | Communications | PR/Corp Comms Lead | On-call |  |  |  | Media risk |  |

---

# 10. Break-Glass Contacts (Restricted Use)

Break-glass contacts are used only when:

- primary + backup are unreachable within SLA, and
- P1 containment or regulatory deadline risk exists.

Rules:

- SOC Lead must document break-glass use in ticket
- SOC Manager must be notified
- Post-incident review must confirm whether directory needed correction

| Role | Break-Glass Contact | Method | Conditions | Last Verified (UTC) |
|---|---|---|---|---:|
| SOC Lead Backup | `[Name]` | Phone | P1 no-response |  |
| IR Lead Backup | `[Name]` | Phone | P1 no-response |  |
| Network Emergency | `[Name]` | Phone | Active exfil/C2 |  |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`

---

# 11. Related Documents

| Document | Path |
|---|---|
| Escalation Matrix – Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| Emergency Escalation – P1 | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md` |
| Internal-to-MSSP Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md` |
| Legal Counsel Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Regulatory Body Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Regulatory-Body-Contacts.md` |
| Vendor Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Vendor-Contacts.md` |
| Third-Party IR Retainer Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Third-Party-IR-Retainer-Contacts.md` |

---

# 12. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | SOC Manager / SOC Operations Lead | Initial version |

---

# 13. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**