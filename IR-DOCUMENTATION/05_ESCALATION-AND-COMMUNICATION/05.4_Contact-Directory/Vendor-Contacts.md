# Vendor Contacts (Security / IT / Critical Services)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Register – Vendor Contacts |
| Document ID | DIR-CON-006 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Vendor Management Lead / SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This register maintains verified contact details for **critical vendors and service providers** required during incident response and security operations, including:

- emergency support during P1/P2 incidents,
- SaaS/platform security escalation,
- infrastructure/provider abuse reporting,
- expedited patching and outage resolution,
- coordinated response for supply chain incidents.

Vendor contact readiness is critical because:

- Vendor delays can significantly increase incident impact (e.g., cloud lockout, email compromise, DDoS mitigation)
- Supply chain incidents require rapid coordination and evidence exchange
- Incorrect contact routing wastes time and increases downtime
- Audit readiness requires traceability of third-party engagement and actions taken
- MSSP environments require client-specific vendor routing and tenant-safe communications

This register ensures:

- A central, controlled vendor escalation directory
- Standard vendor contact fields and escalation paths (primary/backup/24x7)
- Clear vendor scope mapping (what they support)
- Documentation requirements for vendor engagement
- Quarterly verification to prevent outdated contacts

---

# 3. Scope

This register covers vendor contacts for:

| Vendor Category | Examples |
|---|---|
| Cloud providers | AWS/Azure/GCP support and security contacts |
| Email/SaaS | M365/Google Workspace support, abuse/security escalation |
| EDR/SIEM vendors | Support escalation, critical incident hotlines |
| Network/ISP | DDoS mitigation, routing blocks, upstream provider coordination |
| MSSP tooling | Ticketing/SOAR/TI platform support |
| Managed service providers | Data center, hosting, backup services |
| Certificate/DNS providers | DNS hijack response, domain takedown |
| Payment/critical BFSI vendors | Channel partners impacting regulated services |
| IR retainers | (Listed separately but may be referenced here as cross-link) |

Out of scope:

- Client contacts (stored separately)
- Regulatory body contacts (stored separately)
- Law enforcement contacts (stored separately)

References:  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/MSSP-Client-Contacts.md`  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Regulatory-Body-Contacts.md`  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Law-Enforcement-Contacts.md`

---

# 4. Confidentiality and Handling Requirements (Mandatory)

This document is **Restricted**.

| Control | Requirement |
|---|---|
| Storage | Access-controlled repository only |
| Access | SOC Manager, SOC Lead, IR Team Lead, Vendor Mgmt, on-call engineers (need-to-know) |
| Sharing | Do not share externally; do not paste full vendor contacts in general tickets/chats |
| Export | Requires SOC Manager approval |
| Updates | Logged and verified quarterly |

Ticket documentation rule:
- Record: “Vendor engaged: [Vendor Name], case #[ID], time (UTC), outcome.”

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| Vendor Management Lead | Maintains vendor list, contract IDs, support tiers, and escalation routes |
| SOC Manager | Ensures vendor contacts support IR needs and on-call readiness |
| IR Team Lead | Engages vendors during P1/P2; coordinates evidence and technical requirements |
| SOC Lead | Coordinates vendor engagement during incident bridge calls |
| Legal Counsel | Reviews NDAs/data sharing for sensitive evidence exchange |
| Compliance Lead | Ensures vendor engagement aligns to regulatory obligations |
| MSSP SDM | Coordinates vendor engagement for client incidents (tenant-safe) |

---

# 6. Vendor Engagement Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Use official channels | Engage via vendor’s official support/escalation routes |
| Minimum necessary disclosure | Share only required info; avoid customer PII unless necessary and approved |
| Track case IDs | Always capture vendor support case/reference number |
| Time-bound escalation | Escalate to vendor management if no response within SLA |
| Evidence integrity | Use secure transfer; hash evidence bundles where applicable |
| Tenant segregation (MSSP) | Ensure vendor engagement references correct tenant/account |
| Document outcomes | Actions taken by vendor must be recorded in ticket |

---

# 7. When to Engage Vendors (Common Triggers)

| Trigger | Examples |
|---|---|
| Vendor platform compromise suspected | SaaS admin logs show suspicious activity |
| Account lockout / access loss | Cloud root lockout, MFA issues |
| DDoS or upstream routing issue | ISP mitigation required |
| Security control failure | EDR not isolating, SIEM ingestion outage |
| Supply chain alert | Vendor reports compromise or suspicious update |
| Takedown/abuse request | Phishing site takedown, malicious domain reporting |
| Patch/mitigation coordination | Zero-day workaround, emergency patch availability |

---

# 8. Standard Fields (Mandatory)

Each vendor entry must include:

| Field | Requirement |
|---|---|
| Vendor Name | Mandatory |
| Service/Platform | Mandatory |
| Category | Cloud/EDR/SIEM/ISP/SaaS/etc. |
| Contract / Support Plan ID | Mandatory |
| Tenant/Account ID (MSSP/client) | Mandatory where applicable |
| Primary Support Channel | Mandatory (portal/email/phone) |
| 24x7 Hotline | Mandatory for critical vendors |
| Security/Abuse Contact | Recommended |
| Escalation Manager Contact | Recommended |
| Severity Routing | Mandatory (how to raise P1/P2 with vendor) |
| Evidence Transfer Method | Recommended |
| Notes/Constraints | Mandatory if any (e.g., “client must open ticket”) |
| Last Verified Date (UTC) | Mandatory |

---

# 9. Vendor Contacts Register (Fill-In Table)

> Populate with your actual vendors. Add rows as needed.

| Vendor Name | Platform/Service | Category | Support Plan / Contract ID | Tenant/Account ID | P1 Hotline | Support Email | Support Portal | Security/Abuse Contact | Escalation Path | Notes/Constraints | Last Verified (UTC) |
|---|---|---|---|---|---|---|---|---|---|---|---:|
| `[Vendor]` | `...` | `Cloud` | `CON-...` | `...` | `+__` | `__@__` | `https://...` | `__@__` | “Call hotline + open Sev-1 ticket” | `...` | `YYYY-MM-DD` |
|  |  |  |  |  |  |  |  |  |  |  |  |

---

# 10. Vendor Engagement Documentation Checklist (Mandatory)

When a vendor is engaged, the incident ticket must record:

| Item | Requirement |
|---|---|
| Vendor name and platform | Mandatory |
| Reason for engagement | Mandatory |
| Engagement time (UTC) | Mandatory |
| Contact method (portal/email/phone) | Mandatory |
| Case/reference number | Mandatory |
| Summary of information shared | Mandatory (high-level) |
| Actions taken by vendor | Mandatory |
| ETAs provided | Mandatory |
| Escalations to vendor management | Mandatory if delays occur |
| Outcome/closure | Mandatory |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 11. Escalation for Vendor Non-Response (Mandatory)

If vendor does not respond within support SLA:

1. Re-contact via alternate channel (phone + portal)
2. Use vendor escalation manager path
3. Escalate internally to SOC Manager + Vendor Management Lead
4. For P1: notify CISO and document business impact risk
5. Record all attempts and timestamps (UTC)

---

# 12. MSSP Considerations (Mandatory)

For MSSP incidents:

- Confirm whether **client** must open vendor tickets (often required)
- If MSSP is authorized to open vendor tickets:
  - use correct client tenant/account identifiers
  - ensure communications remain tenant-scoped
  - document client approval if required
- Ensure evidence shared does not include other client data
- Store vendor correspondence in client-segregated evidence location

References:  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`  
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 13. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Wrong tenant/account used | Misrouting, data disclosure | Tenant verification before engagement |
| Missing vendor case ID | Audit gap | Case ID mandatory in ticket |
| Over-sharing sensitive data | Confidentiality breach | Minimum necessary disclosure + legal review |
| No escalation for non-response | Delay | Non-response escalation workflow |
| Cross-client evidence leakage (MSSP) | Compliance breach | Segregated evidence and communications |

---

# 14. Related Documents

| Document | Path |
|---|---|
| Third-Party IR Retainer Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Third-Party-IR-Retainer-Contacts.md` |
| Internal Contacts Master | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Internal-Contacts-Master.md` |
| MSSP Client Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/MSSP-Client-Contacts.md` |
| Legal Counsel Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |

---

# 15. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Vendor Management Lead / SOC Manager | Initial version |

---

# 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**