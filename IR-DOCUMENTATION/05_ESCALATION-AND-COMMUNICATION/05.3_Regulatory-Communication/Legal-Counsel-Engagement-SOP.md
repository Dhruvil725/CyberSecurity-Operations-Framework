# SOP: Legal Counsel Engagement (Cyber Incident)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Legal Counsel Engagement |
| Document ID | REG-COM-003 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Legal Counsel (Primary) / Compliance Lead |
| Approved By | CISO |
| Classification | Internal – Confidential / Privileged (where applicable) |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines how and when to engage **Legal Counsel** (internal and/or external) during cyber security incidents to ensure:

- legally defensible incident handling and communications,
- preservation of legal privilege where appropriate,
- correct handling of potential data breaches, regulatory notifications, and law enforcement engagement,
- proper legal hold and evidence preservation guidance,
- alignment between IR actions and legal/compliance obligations.

Legal engagement is critical because:

- Incidents may create regulatory reporting and customer notification obligations
- Certain communications may need to be protected under attorney-client privilege
- Evidence handling may be scrutinized in audits, disputes, and legal proceedings
- Law enforcement interaction requires careful coordination
- MSSP incidents may include contractual, liability, and cross-border considerations

This SOP ensures:

- clear triggers and timelines for legal engagement
- consistent documentation of legal decisions and instructions
- controlled communications and information sharing
- coordinated evidence preservation and legal hold implementation
- audit-ready records without compromising privilege

---

# 3. Scope

This SOP applies to:

| Area | Included |
|---|---|
| Incidents | P1/P2 incidents; suspected/confirmed breaches; insider threat; extortion |
| Engagement types | Internal legal, external counsel, cyber insurance counsel (if applicable) |
| Communications | Regulator submissions, customer notifications, press statements, contractual communications |
| Evidence | Legal hold, chain-of-custody, evidence retention, discovery readiness |
| MSSP | Client incidents with contractual/regulatory implications; client legal coordination |

Out of scope:

- Routine policy/legal review unrelated to incidents
- Employment disciplinary process (covered with HR SOPs), except where incident-related

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Legal Counsel | Internal legal team and/or retained external counsel |
| Privileged communication | Communication protected under attorney-client privilege (jurisdiction dependent) |
| Work product | Materials prepared in anticipation of litigation (jurisdiction dependent) |
| Legal hold | Instruction to preserve relevant data and evidence |
| Breach | Unauthorized access to or disclosure of protected data (as defined by applicable laws/contracts) |
| Extortion | Threat actor demands (ransomware note, data leak threat, etc.) |
| Disclosure | Any external communication about an incident (regulator, client, customer, media) |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| IR Team Lead | Initiates legal engagement request; provides incident facts and evidence needs |
| SOC Manager | Ensures legal engagement occurs per triggers; coordinates executive updates |
| CISO | Approves external counsel engagement and high-impact disclosures |
| Compliance Lead | Coordinates regulatory assessment and ensures legal review of regulator submissions |
| Legal Counsel | Advises on privilege, breach obligations, legal hold, communications wording, law enforcement engagement |
| Evidence Custodian | Implements preservation and access controls as instructed |
| IT Ops / Records Management | Supports legal hold implementation across systems |
| MSSP SDM | Coordinates client legal contacts and contractual obligations (MSSP) |
| HR Lead (if insider) | Coordinates HR/legal actions with IR under appropriate confidentiality |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Legal-Counsel-Engagement-SOP.md` (if separate contact file)  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Internal-Contacts-Master.md`

---

# 6. Legal Engagement Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Engage early for breach risk | If breach is suspected, involve legal immediately (do not wait for full confirmation) |
| Preserve privilege | Route sensitive drafts and analysis through legal where appropriate |
| Facts first | Communications should be based on confirmed facts; label assumptions |
| Controlled disclosure | No regulator/customer/media statement without legal review (where required) |
| Evidence integrity | Follow legal hold and chain-of-custody guidance |
| Document instructions | Legal guidance must be recorded in ticket (without disclosing privileged content where not appropriate) |
| MSSP clarity | Client-specific legal obligations must be contract-aligned and tenant-safe |

---

# 7. Triggers for Legal Counsel Engagement (Mandatory)

Engage Legal Counsel when any of the following apply:

## 7.1 Mandatory Triggers

| Trigger | Examples |
|---|---|
| Suspected or confirmed data breach | PII/financial data exposure, unauthorized database access |
| Regulatory reporting required/likely | CERT-In / RBI or other regulator thresholds |
| Extortion / ransomware demands | Ransom note, leak threats, negotiation considerations |
| Law enforcement engagement | Police/cyber crime unit contact required or initiated |
| Insider threat with HR implications | Suspected malicious employee activity |
| Significant contractual exposure | Client notification obligations, SLA disputes |
| Potential litigation risk | Customer harm claims, vendor disputes |
| Cross-border data issues | Data residency or cross-border transfer concerns |

## 7.2 Conditional Triggers

- Major service outage with customer impact
- Public rumors/media inquiries
- Incident involves third-party processor/vendor failure

---

# 8. Engagement Timelines (Internal Targets)

| Severity / Condition | Engage Legal Target |
|---|---:|
| P1 with breach/extortion risk | ≤ 60 minutes from noticing |
| P2 with breach/regulatory risk | ≤ 4 hours from noticing |
| Insider threat (credible) | Same business day (or sooner if active harm) |
| Media inquiry / public disclosure risk | Immediate |

---

# 9. Engagement Workflow (Step-by-Step)

## 9.1 Step 1 — Initiate Legal Engagement Request

Owner: IR Team Lead / SOC Manager

Actions:

1. Create/confirm incident ticket
2. Mark ticket tag: **Legal = Engaged (Pending)** or **Legal = Required**
3. Notify Legal Counsel using approved channels (phone/email per on-call)

Minimum information to provide (non-privileged summary):

- Incident ID and severity
- Summary of what is confirmed
- Potential breach/data categories involved (high level)
- Regulatory considerations (CERT-In/RBI likely?)
- Whether extortion demand exists
- Key timelines (UTC): noticing time, detection time
- Decisions needed from Legal (e.g., legal hold, disclosure review)

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

## 9.2 Step 2 — Establish Privileged Workstream (If Applicable)

Owner: Legal Counsel

Legal may instruct that:

- Certain analysis and documents should be produced “at the direction of counsel”
- Drafts of external communications must be reviewed and stored in privileged workspace
- External forensic firm engagement be coordinated via counsel (common to preserve privilege)

Mandatory:
- Follow legal’s instructions on where to store privileged drafts.
- Do not forward privileged emails outside authorized recipients.

---

## 9.3 Step 3 — Legal Hold Decision and Implementation

Owner: Legal Counsel (decision) + Evidence Custodian / IT Ops (implementation)

Legal hold triggers typically include:

- breach suspected/confirmed
- extortion
- insider threat
- expected litigation/regulatory inquiry

Implementation tasks:

| Task | Owner | Requirement |
|---|---|---|
| Issue legal hold notice | Legal | Mandatory if directed |
| Identify systems/data to preserve | IR + IT Ops | Mandatory |
| Preserve logs and evidence exports | IR/Evidence Custodian | Mandatory |
| Restrict deletion/rotation (where feasible) | IT Ops | As directed |
| Track preserved evidence inventory | Evidence Custodian | Mandatory |
| Document hold scope and time | Ticket (high-level) | Mandatory |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`

---

## 9.4 Step 4 — Review of External Communications

Owner: Legal Counsel + Compliance + CISO

External communications include:

- Regulator reports (CERT-In, RBI)
- Client notifications (MSSP)
- Customer notifications
- Press/PR statements
- Vendor notifications (supply chain)

Controls:

- Use approved templates
- Ensure facts are verified
- Avoid attribution claims without evidence
- Avoid including raw sensitive evidence
- Ensure alignment with contractual obligations and applicable law

References:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`

---

## 9.5 Step 5 — Law Enforcement Engagement (If Applicable)

Owner: Legal Counsel (primary) + CISO

Law enforcement engagement may be appropriate when:

- extortion/ransomware occurred
- significant fraud occurred
- national security/critical infrastructure risk exists
- regulator requires notification

Rules:

- Legal must approve what evidence is shared externally
- Chain-of-custody must be maintained
- Document date/time/contact and summary in ticket (without privileged details)

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Law-Enforcement-Contacts.md`

---

## 9.6 Step 6 — Post-Incident Legal Review Inputs

Owner: IR Team Lead + Legal Counsel

Legal may request:

- final incident report
- timeline and evidence package
- decisions and approvals record
- corrective actions and remediation plan

Provide sanitized, role-appropriate versions as directed.

References:
`07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`  
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`

---

# 10. Documentation Requirements (Ticket-Level) (Mandatory)

The incident ticket must record (high-level) the legal engagement trail without exposing privileged content:

| Item | Requirement |
|---|---|
| Legal engagement requested time (UTC) | Mandatory |
| Legal acknowledged time (UTC) | Mandatory |
| Legal hold issued? (Yes/No) | Mandatory |
| External communications reviewed by legal? | Mandatory |
| Key decisions requiring legal input | Mandatory (high-level summary) |
| Law enforcement engaged? (Yes/No) | Mandatory |
| Evidence preservation actions taken | Mandatory references |

Do NOT paste privileged legal advice verbatim into general-access tickets.  
Instead, record: “Legal advised [high-level action], reference [privileged doc ID/location].”

---

# 11. MSSP Client Considerations (Mandatory)

For MSSP incidents:

- Determine whether the **client’s legal counsel** must be engaged (contract/incident type)
- Ensure tenant-safe communication and evidence sharing
- Clarify whether MSSP is authorized to communicate with regulators on client’s behalf
- Ensure all client communications are reviewed under the correct authority chain

References:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`  
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

---

# 12. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Engaging legal too late | Missteps in disclosure/legal hold | Mandatory triggers and timelines |
| Sharing raw sensitive evidence externally | Data leakage | Minimum necessary disclosure + legal approval |
| Losing privilege by broad forwarding | Legal exposure | Privileged workstream controls |
| Not documenting legal engagement | Audit gaps | Ticket-level logging (high-level) |
| Cross-client disclosures (MSSP) | Contract/regulatory breach | Tenant segregation verification |

---

# 13. Related Documents

| Document | Path |
|---|---|
| CERT-In Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md` |
| RBI Incident Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md` |
| ISO 27001 Incident Notification | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/ISO27001-Incident-Notification.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| CoC Digital Evidence | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| Ticket Closure Criteria | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md` |
| Law Enforcement Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Law-Enforcement-Contacts.md` |

---

# 14. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Legal Counsel / Compliance Lead | Initial version |

---

# 15. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**