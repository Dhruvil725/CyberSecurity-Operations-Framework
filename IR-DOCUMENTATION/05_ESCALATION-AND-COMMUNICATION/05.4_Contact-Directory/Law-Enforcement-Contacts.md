# Law Enforcement Contacts (Cyber Incident)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Register – Law Enforcement Contacts |
| Document ID | DIR-CON-002 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Legal Counsel (Primary) / Compliance Lead |
| Approved By | CISO |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This register maintains approved **law enforcement contact points** to support cyber incident response, including ransomware/extortion, fraud, data breach investigations, and critical infrastructure incidents.

Maintaining law enforcement contacts is critical because:

- Engagement may be time-sensitive (ransomware, active fraud, ongoing exfiltration)
- Correct routing avoids sharing sensitive data with the wrong agency
- Legal oversight is required to protect privilege, confidentiality, and regulatory posture
- Evidence sharing must follow chain-of-custody and approved disclosure controls
- MSSP cases require clear boundaries (client vs MSSP responsibility)

This register ensures:

- A verified list of law enforcement channels and points of contact
- Clear rules for when and how to engage law enforcement
- Standard contact fields and engagement documentation requirements
- Audit-ready traceability of engagement and evidence shared

---

# 3. Scope

This register covers contacts for:

| Category | Examples |
|---|---|
| Cyber crime reporting | National/state cyber crime units |
| Financial fraud | Fraud cells and financial crime units |
| Critical infrastructure | Specialized units where applicable |
| Local police | FIR/complaint routing (as applicable) |
| National coordination | National cyber coordination centers (as applicable) |

Out of scope:

- Regulatory body contacts (kept separately)
- Vendor / third-party contacts (kept separately)

References:  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Regulatory-Body-Contacts.md`  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Vendor-Contacts.md`

---

# 4. Confidentiality and Handling Requirements (Mandatory)

This document is **Restricted** because it contains sensitive contacts and operational guidance.

## 4.1 Handling Rules

| Control | Requirement |
|---|---|
| Storage | Approved access-controlled repository only |
| Access | Legal, Compliance, CISO, SOC Manager, IR Team Lead (need-to-know) |
| Sharing | Do not share externally; do not paste full contact details in general tickets/chats |
| Printing | Avoid; if printed for crisis kit, store locked and track issuance |
| Exports | Require Legal Counsel approval |
| Updates | Logged and reviewed quarterly |

## 4.2 Ticket Documentation Rule

Do **not** place personal phone numbers/email addresses in incident tickets.  
Record: “Law enforcement contacted: [Agency/Unit], time (UTC), method, case/reference number.”

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| Legal Counsel (Primary) | Owns law enforcement engagement, disclosure approvals, legal hold guidance |
| Compliance Lead | Supports regulatory alignment and documentation; coordinates with Legal |
| CISO | Approves engagement for major incidents; approves external disclosure scope |
| IR Team Lead | Provides technical facts and evidence package; ensures CoC compliance |
| SOC Manager | Coordinates operations and timelines; ensures documentation quality |
| Evidence Custodian | Maintains custody records, hashes, secure storage, controlled transfers |
| MSSP SDM (if applicable) | Coordinates client approvals/ownership; ensures tenant-safe handling |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`

---

# 6. Engagement Governance (Mandatory)

## 6.1 When Law Enforcement Engagement Is Considered

Engagement is typically considered when:

| Scenario | Examples |
|---|---|
| Ransomware / extortion | Threat actor demands, leak threats, encryption at scale |
| Financial fraud | BEC, unauthorized transfer attempts, account takeover with fraud |
| Confirmed data breach | Large-scale customer data exposure |
| Critical infrastructure impact | Payment systems or critical channels affected |
| Insider criminal behavior | Theft or sabotage requiring criminal investigation |
| Persistent threat activity | Coordinated intrusion requiring external support |

## 6.2 Approval Requirements (Mandatory)

| Engagement Type | Minimum Approval |
|---|---|
| Informal consultation (no evidence shared) | Legal Counsel + CISO (P1) / Legal Counsel (P2+) |
| Formal complaint / case filing | Legal Counsel + CISO |
| Evidence sharing | Legal Counsel + Evidence Custodian + IR Team Lead |
| Public statements referencing law enforcement | Legal Counsel + CISO + Communications (if applicable) |
| MSSP client case | Client Legal/CISO approval + MSSP SDM coordination |

> No law enforcement contact should be initiated by analysts without Legal Counsel direction, except in immediate safety emergencies (rare). Any break-glass contact must be documented and reviewed.

---

# 7. Evidence Sharing Rules (Mandatory)

When law enforcement engagement involves evidence:

## 7.1 Minimum Evidence Handling Controls

| Control | Requirement |
|---|---|
| Evidence integrity | SHA256 hashes recorded for shared files |
| Chain of custody | CoC form completed for transfers |
| Minimum necessary disclosure | Only share what is required for the specific request |
| Secure transfer | Approved secure transfer method only |
| Redaction | Remove unrelated PII/customer data where feasible and approved |
| Logging | Document what was shared, when, and to whom |

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

## 7.2 Common Evidence Types (Examples)

- Incident summary and timeline (UTC)
- Relevant SIEM/EDR exports (sanitized)
- IOC lists (IPs/domains/hashes)
- Ransom notes and extortion communications
- PCAP excerpts (only when approved)
- Disk/memory images (rare; high sensitivity; strict CoC required)

---

# 8. Minimum Data Fields (Standard)

Each contact entry must include:

| Field | Requirement |
|---|---|
| Agency / Unit Name | Mandatory |
| Jurisdiction / Region | Mandatory |
| Contact Type | Hotline / Email / Portal / Local Station |
| Primary Contact Name (if applicable) | Optional (role-based preferred) |
| Phone | Mandatory (placeholder allowed in this template) |
| Email | Mandatory (placeholder allowed in this template) |
| Reporting Portal URL (if applicable) | Optional |
| Hours of Operation | Mandatory |
| Supported Case Types | Mandatory |
| Required Information for Filing | Recommended |
| Evidence Submission Method | Recommended |
| Notes / Constraints | Recommended |
| Last Verified Date (UTC) | Mandatory |

---

# 9. Verification and Update Process

## 9.1 Quarterly Verification (Mandatory)

Owner: Legal Counsel / Compliance Lead

- Validate hotline numbers, emails, and portal URLs
- Confirm jurisdiction mapping remains accurate
- Confirm evidence submission methods and documentation requirements
- Update “Last Verified Date (UTC)”
- Log changes in revision history

## 9.2 Emergency Updates

If a contact method is invalid during a P1:

- Update within 4 hours
- Notify SOC Manager + IR Team Lead
- Record in revision history

---

# 10. Contact Directory (Fill-In Tables)

> Populate with the appropriate agencies relevant to your organization’s operating regions. Use role-based contacts where possible.

## 10.1 National / Central Contacts

| Agency / Unit | Jurisdiction | Contact Type | Phone | Email | Portal URL | Hours | Supported Case Types | Last Verified (UTC) |
|---|---|---|---|---|---|---|---|---:|
| `[Agency Name]` | National | Hotline | `+__` | `__@__` | `https://...` | 24x7 | Ransomware/Fraud/Breach | `YYYY-MM-DD` |
| `[Agency Name]` | National | Email | `+__` | `__@__` |  | Business | Advisory/Coordination | `YYYY-MM-DD` |

---

## 10.2 State / Regional Cyber Crime Units

| State/Region | Agency / Unit | Phone | Email | Filing Method | Notes | Last Verified (UTC) |
|---|---|---|---|---|---|---:|
| `[State/Region]` | `[Cyber Crime Unit]` | `+__` | `__@__` | Portal/Email/In-person | `...` | `YYYY-MM-DD` |
|  |  |  |  |  |  |  |

---

## 10.3 Local Police Stations (Operational Routing)

| City | Station | Phone | Email | Address / Location | Notes | Last Verified (UTC) |
|---|---|---|---|---|---|---:|
| `[City]` | `[Station Name]` | `+__` | `__@__` | `...` | Use for formal filing as advised by Legal | `YYYY-MM-DD` |

---

## 10.4 Financial Fraud / Banking Fraud Units (If Applicable)

| Agency / Unit | Jurisdiction | Phone | Email | Supported Fraud Types | Notes | Last Verified (UTC) |
|---|---|---|---|---|---|---:|
| `[Fraud Unit]` | National/Regional | `+__` | `__@__` | BEC, unauthorized transfer | Coordinate with bank and Legal | `YYYY-MM-DD` |

---

# 11. Engagement Documentation Checklist (Mandatory)

When law enforcement is contacted, record the following in the incident ticket (high-level):

| Item | Requirement |
|---|---|
| Agency/unit contacted | Mandatory |
| Reason for contact | Mandatory |
| Contact time (UTC) | Mandatory |
| Method (phone/email/portal) | Mandatory |
| Case/reference number | Mandatory if provided |
| Summary of information shared | Mandatory (high-level) |
| Evidence shared (IDs only) | Mandatory (do not paste raw evidence) |
| Approval record (Legal + CISO) | Mandatory |
| Next steps / follow-up time | Mandatory |

---

# 12. MSSP Client Considerations (Mandatory)

For MSSP incidents:

- Confirm whether the **client** is responsible for law enforcement engagement (default)
- MSSP must not contact law enforcement on behalf of client without:
  - contractual authority, and
  - written client authorization, and
  - Legal Counsel approval
- Ensure tenant-safe evidence storage and sharing
- Document client approvals and instructions

References:  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`  
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

---

# 13. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Contacting law enforcement without legal approval | Privilege/confidentiality risk | Legal engagement SOP + approval gate |
| Sharing excessive evidence/PII | Data leakage | Minimum necessary disclosure + redaction |
| No CoC for transferred evidence | Legal defensibility risk | CoC mandatory for transfers |
| Cross-client details shared (MSSP) | Contract/compliance breach | Tenant verification checklist |
| No case/reference number recorded | Audit gap | Ticket checklist mandatory |
| Unverified contacts | Delays in P1 | Quarterly verification |

---

# 14. Related Documents

| Document | Path |
|---|---|
| Legal Counsel Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| CERT-In Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md` |
| RBI Incident Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| CoC Digital Evidence | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| CoC Transfer Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md` |
| Internal Contacts Master | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Internal-Contacts-Master.md` |
| MSSP Client Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/MSSP-Client-Contacts.md` |

---

# 15. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Legal Counsel / Compliance Lead | Initial version |

---

# 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**