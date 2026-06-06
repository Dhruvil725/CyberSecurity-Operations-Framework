# Evidence Retention Schedule

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Standard – Evidence Retention Schedule |
| Document ID | EVD-STR-002 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Evidence Custodian / Compliance Lead |
| Approved By | CISO |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This document defines the minimum **retention periods** for evidence collected during security investigations and incident response, including:

- digital and physical evidence,
- chain-of-custody records,
- regulatory submissions and correspondence,
- incident reporting artifacts.

Evidence retention is critical because:

- Evidence may be needed for audits, regulatory inquiries (RBI/CERT-In), legal matters, and post-incident analysis
- Retention must balance compliance needs with data minimization and storage/security risk
- Inconsistent retention creates audit findings and operational gaps
- Legal holds override standard retention schedules
- MSSP engagements may impose client-specific retention and data residency requirements

This schedule ensures:

- standardized minimum retention periods by evidence type
- documented owner and review responsibilities
- clear linkage to legal hold and exception handling
- defensible destruction timing when retention expires

> NOTE: This schedule defines minimums. Where law/regulation/contract requires longer retention, the longer period applies.

---

# 3. Scope

This retention schedule applies to:

| Artifact Group | Examples |
|---|---|
| Incident tickets and notes | ticket history, escalation records, approvals |
| Evidence artifacts | logs, exports, PCAP, disk images, memory dumps |
| Forensic working files | parsed outputs, analysis notes (where retained) |
| CoC records | master forms, transfer forms, evidence logs |
| Regulatory artifacts | CERT-In/RBI submissions, acknowledgments, correspondence |
| MSSP artifacts | client evidence, client communications, client approvals |

Out of scope:

- General enterprise data retention unrelated to incidents
- SIEM raw retention policy (unless logs are exported as evidence)

---

# 4. Retention Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Minimum necessary | Retain only what is required; prefer summaries where feasible |
| Longer requirement wins | If multiple requirements exist, retain for the longest required period |
| Legal hold overrides | Legal hold suspends destruction until release is documented |
| Protect retained evidence | Retained evidence must remain encrypted and access-controlled |
| Maintain integrity | Hashes/CoC must remain linked and intact for retained evidence |
| Tenant segregation (MSSP) | Retention must be client-scoped with contract constraints |
| Document destruction | Evidence destruction must be logged and approved |

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Destruction-SOP.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| Evidence Custodian | Applies retention tags, manages evidence vault lifecycle, coordinates destruction approvals |
| Compliance Lead | Validates regulatory retention requirements; ensures audit readiness |
| Legal Counsel | Issues/releases legal holds; approves destruction for legally sensitive cases |
| IR Team Lead | Confirms evidence needed for RCA/post-incident; requests retention extensions where required |
| SOC Manager | Oversight; approves exceptions and escalations |
| MSSP SDM | Ensures client contract retention requirements are applied and documented |

---

# 6. Legal Holds (Retention Override)

## 6.1 Legal Hold Rule (Mandatory)

If a legal hold is issued:

- all relevant evidence and records must be retained until legal hold is lifted in writing
- evidence must be marked **“Legal Hold”** in evidence index/metadata
- destruction must not proceed regardless of standard retention end date

## 6.2 Legal Hold Documentation (Minimum)

Record:

- hold issued date/time (UTC)
- scope (incident IDs, evidence IDs, systems/time range)
- issuing authority (Legal Counsel)
- hold release date/time (UTC) when applicable

---

# 7. Retention Schedule Table (Minimum Standard)

> Customize based on local regulations and contracts. If uncertain, retain longer and log exception rationale.

## 7.1 Core Incident Records

| Record Type | Examples | Minimum Retention | Owner | Notes |
|---|---|---:|---|---|
| Incident tickets | Full ticket history, comments, status changes | 3 years | SOC Manager | Audit-ready incident record |
| Incident reports (final) | Final report + executive summary | 5 years | IR Team Lead | Longer for major incidents recommended |
| PIR / Lessons learned | PIR notes, actions | 3 years | SOC Manager | Supports continual improvement |
| RCA documents | RCA timeline, 5-Whys | 3 years | IR Team Lead | Keep linked to incident ID |

References:  
`07_REPORTING/07.1_Incident-Reports/`  
`08_POST-INCIDENT/`

---

## 7.2 Digital Evidence Artifacts

| Evidence Type | Examples | Minimum Retention | Owner | Notes |
|---|---|---:|---|---|
| Log evidence bundles | SIEM exports, firewall/proxy logs | 2 years | Evidence Custodian | Evidence-grade for regulatory cases |
| Network captures (PCAP) | Targeted PCAP files | 1 year | Evidence Custodian | High sensitivity; minimize where possible |
| Endpoint artifacts | suspicious files, triage bundles | 2 years | Evidence Custodian | Keep hashes and metadata |
| Disk images | E01/RAW images | 2 years (P1/P2: 3 years) | Evidence Custodian | High storage; retain per case risk |
| Memory dumps | RAM dumps | 1 year (P1/P2: 2 years) | Evidence Custodian | Extremely sensitive; strict access |

> If regulatory/legal case: retain as directed by Legal/Compliance, overriding above.

References:  
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`

---

## 7.3 Chain-of-Custody Records

| Record Type | Examples | Minimum Retention | Owner | Notes |
|---|---|---:|---|---|
| CoC Master Forms | Evidence CoC master records | 5 years | Evidence Custodian | Keep with incident evidence package |
| CoC Transfer Forms | Transfers to/from custodian/vendors | 5 years | Evidence Custodian | Required for defensibility |
| Evidence logs/index | Evidence inventories per incident | 5 years | Evidence Custodian | Link to hashes and storage paths |

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`

---

## 7.4 Regulatory Reporting Records

| Record Type | Examples | Minimum Retention | Owner | Notes |
|---|---|---:|---|---|
| CERT-In submissions | initial/follow-up reports, acknowledgments | 5 years | Compliance Lead | Store securely; link to incident ID |
| RBI submissions | reports, acknowledgments, correspondence | 5 years | Compliance Lead | Store securely; link to incident ID |
| Regulator correspondence | emails/letters/case references | 5 years | Compliance Lead | Legal review if sensitive |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 7.5 MSSP Client Records (Contract-Driven)

| Record Type | Examples | Minimum Retention | Owner | Notes |
|---|---|---:|---|---|
| Client incident tickets | MSSP tickets and client comms | As per contract (min 3 years) | MSSP SDM | Tenant segregated |
| Client evidence packages | logs, artifacts | As per contract (min 2 years) | Evidence Custodian | Data residency may apply |
| Client approvals | containment approvals, authorizations | As per contract (min 3 years) | MSSP SDM | Keep with ticket |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md`

---

# 8. Retention Review and Enforcement

## 8.1 Quarterly Retention Review (Mandatory)

Evidence Custodian + Compliance Lead must:

- identify evidence approaching retention end
- confirm legal holds and exceptions
- generate destruction candidate list
- obtain approvals per destruction SOP
- document retention review completion

## 8.2 Exception Handling

If evidence must be retained longer than schedule:

- record exception in evidence index
- record reason (legal hold, regulatory inquiry, client request)
- record new retention end date
- obtain approvals (Legal/Compliance)

Reference:
`00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`

---

# 9. Storage Cost and Minimization Controls (Guidance)

To reduce risk and cost:

- prefer log exports and summaries over full disk images unless necessary
- time-box and filter PCAP captures
- compress archives and store hash manifests
- avoid retaining duplicate copies; maintain single “original” + controlled working copy (if needed)

---

# 10. Related Documents

| Document | Path |
|---|---|
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| Evidence Destruction SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Destruction-SOP.md` |
| MSSP Client Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md` |
| Legal Counsel Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| CoC Digital Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| CoC Master Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md` |
| Policy Exception Register | `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md` |

---

# 11. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Evidence Custodian / Compliance Lead | Initial version |

---

# 12. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**