# Third-Party IR Retainer Contacts

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Register – Third-Party IR Retainer Contacts |
| Document ID | DIR-CON-005 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | IR Team Lead / SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This register maintains contact and engagement details for **third-party incident response retainers** and external support providers used during major incidents (P1/P2), including forensic firms, breach coaches, managed forensic labs, and specialist support.

Maintaining these contacts is critical because:

- Major incidents require rapid external assistance under tight timelines
- Contract and retainer details must be accessible during high-pressure events
- Incorrect engagement steps can delay response or reduce legal privilege protections
- Evidence handling and chain-of-custody must be coordinated with external parties
- MSSP incidents require client authorization and tenant-safe engagement
- Audit readiness requires traceability of who was engaged, when, and why

This register ensures:

- Verified 24x7 engagement contacts and procedures
- Clear retainer scope and activation steps
- Defined SLAs for external response and escalation
- Controlled sharing of evidence and sensitive data
- Documentation requirements for engagement and follow-ups

---

# 3. Scope

This register includes:

| Provider Type | Examples |
|---|---|
| IR retainer | Incident response consulting firm |
| Forensics lab | Disk/memory analysis, malware analysis |
| Breach coach / external legal | Counsel supporting breach response (where applicable) |
| Cyber insurance panel | Incident hotline and assigned responders (if applicable) |
| Specialist support | OT/ICS IR, cloud IR specialists, ransomware negotiation support |

Out of scope:

- General vendor contacts (kept in Vendor Contacts)
- Law enforcement contacts (kept separately)

References:  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Vendor-Contacts.md`  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Law-Enforcement-Contacts.md`

---

# 4. Confidentiality and Handling Requirements (Mandatory)

This document is **Restricted**.

| Control | Requirement |
|---|---|
| Storage | Access-controlled repository only |
| Access | IR Team, SOC Manager, Compliance, Legal, CISO (need-to-know) |
| Sharing | Do not share externally; do not paste full contact details in tickets/chats |
| Export | Requires SOC Manager + CISO approval |
| Printing | Avoid; if used in crisis kit, store locked and track issuance |
| Updates | Logged and verified quarterly |

Ticket documentation rule:
- Record “Provider engaged: [Provider Name], time (UTC), method, case/reference number.”

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| IR Team Lead | Primary engager for third-party IR; defines scope of support requested |
| SOC Manager | Approves engagement for cost/operational impact; coordinates internal resources |
| CISO | Approves external engagement and any sensitive data sharing; executive oversight |
| Compliance Lead | Ensures regulatory alignment and reporting support |
| Legal Counsel | Advises on privilege, contracts, NDAs, evidence disclosure |
| Evidence Custodian | Coordinates secure evidence transfer and CoC |
| MSSP SDM (if applicable) | Ensures client approvals and contract constraints for client incidents |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`

---

# 6. Engagement Governance (Mandatory)

## 6.1 When to Engage Third-Party IR

Engage retainer when:

| Trigger | Examples |
|---|---|
| P1 incident | Ransomware, confirmed breach, DC compromise, major outage |
| P2 with high uncertainty | Complex intrusion without clear scope/entry point |
| Specialist expertise needed | Cloud compromise, malware reverse engineering |
| Legal/regulatory sensitivity | Significant breach risk, regulator scrutiny expected |
| Capacity constraints | Internal resources insufficient for scale/time |

## 6.2 Approval Requirements

| Engagement Type | Minimum Approval |
|---|---|
| Initial consult (no evidence shared) | IR Team Lead + SOC Manager |
| Full activation (billable) | SOC Manager + CISO |
| Evidence transfer to third party | Legal Counsel + IR Team Lead + Evidence Custodian |
| MSSP client case engagement | Client approval (contract-dependent) + MSSP SDM + CISO |

---

# 7. Retainer Activation Workflow (Step-by-Step)

## 7.1 Step 1 — Prepare Engagement Request

Owner: IR Team Lead

Minimum information to provide:

- Incident ID and severity
- Incident category and summary
- Current status (containment/investigation/recovery)
- Scope (known affected systems/users)
- What is requested (forensics, containment strategy, malware analysis, etc.)
- Time constraints and key deadlines (regulatory, business)
- Evidence available and how it will be transferred (if required)

## 7.2 Step 2 — Confirm Contract and NDA Requirements

Owner: Legal Counsel + SOC Manager

- Confirm retainer is active and in scope
- Confirm any NDAs or data processing agreements required
- Confirm billing authorization path
- Confirm whether engagement should be routed “through counsel” to preserve privilege (if applicable)

## 7.3 Step 3 — Establish Secure Collaboration

Owner: IR Team Lead + Provider

- Define primary comms channel (secure email, portal, dedicated bridge)
- Set meeting cadence
- Confirm who can access evidence and what restrictions apply
- Confirm points of contact (primary + backup, 24x7)

## 7.4 Step 4 — Evidence Transfer (If Needed)

Owner: Evidence Custodian

Mandatory controls:

- Use secure transfer method approved by Legal
- Maintain CoC for evidence-grade artifacts
- Hash packages (SHA256) and record
- Document what was shared and when

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

## 7.5 Step 5 — Ongoing Management and Outputs

Owner: IR Team Lead

Track provider outputs:

- forensic findings and timelines
- IOC sets and recommendations
- containment and recovery advice
- draft reports or evidence summaries (as applicable)

Ensure outputs are stored in evidence repository and referenced in ticket.

---

# 8. Standard Fields (Mandatory)

Each provider entry must include:

| Field | Requirement |
|---|---|
| Provider Name | Mandatory |
| Service Type | IR/Forensics/Malware/Cloud specialist |
| Contract/Retainer ID | Mandatory |
| Scope Summary | Mandatory |
| Activation Method | Hotline/email/portal |
| 24x7 Contact | Mandatory (phone/email) |
| Primary POC | Mandatory |
| Backup POC | Mandatory |
| SLA (response times) | Mandatory if defined |
| Evidence Transfer Method | Recommended |
| Billing/Authorization Notes | Mandatory (who approves) |
| NDA/Legal Notes | Recommended |
| Last Verified Date (UTC) | Mandatory |

---

# 9. IR Retainer Contacts Register (Fill-In Table)

| Provider Name | Service Type | Retainer/Contract ID | Activation Method | 24x7 Hotline | Email | Portal URL | Primary POC | Backup POC | SLA | Billing Approval | Notes | Last Verified (UTC) |
|---|---|---|---|---|---|---|---|---|---|---|---|---:|
| `[Provider]` | IR/Forensics | `RET-...` | Phone/Email | `+__` | `__@__` | `https://...` | `Name` | `Name` | `...` | `SOC Manager/CISO` | `...` | `YYYY-MM-DD` |
|  |  |  |  |  |  |  |  |  |  |  |  |  |

---

# 10. MSSP Considerations (Mandatory)

For MSSP incidents:

- Determine whether retainer engagement is:
  - MSSP internal only, or
  - client-funded/client-approved
- Ensure evidence is tenant-scoped and client approvals are documented
- Ensure third party is authorized to access client data under contract and DPA
- Ensure no cross-client data is shared

References:  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`  
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 11. Documentation Checklist (Mandatory)

When engaging a third-party IR provider, record in ticket:

| Item | Requirement |
|---|---|
| Provider engaged | Mandatory |
| Activation time (UTC) | Mandatory |
| Method used | Mandatory |
| Case/reference number | Mandatory if provided |
| Scope requested | Mandatory |
| Approvals recorded | Mandatory (SOC Manager/CISO/Legal as required) |
| Evidence shared (IDs only) | Mandatory |
| Key recommendations | Mandatory (high-level) |
| Outputs stored (paths/IDs) | Mandatory |

---

# 12. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Retainer details not accessible during P1 | Delay | Maintain verified 24x7 contacts and quarterly review |
| Engaging provider without approvals | Cost/legal risk | Approval matrix enforced |
| Evidence shared without CoC/hashes | Integrity risk | Evidence custody controls mandatory |
| Cross-client evidence sharing (MSSP) | Compliance breach | Tenant verification and segregation |
| No record of provider guidance | Audit gaps | Ticket documentation checklist |

---

# 13. Related Documents

| Document | Path |
|---|---|
| Legal Counsel Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| CoC Transfer Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md` |
| MSSP Client Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/MSSP-Client-Contacts.md` |
| Vendor Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Vendor-Contacts.md` |
| Internal Contacts Master | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Internal-Contacts-Master.md` |

---

# 14. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | IR Team Lead / SOC Manager | Initial version |

---

# 15. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
