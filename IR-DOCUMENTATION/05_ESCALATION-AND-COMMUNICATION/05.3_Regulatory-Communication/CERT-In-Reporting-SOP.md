# SOP: CERT-In Incident Reporting

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – CERT-In Incident Reporting |
| Document ID | REG-COM-001 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Compliance Lead / SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines the process to **identify, assess, report, and track reportable cyber security incidents** to **CERT-In** (Indian Computer Emergency Response Team), including required internal approvals, evidence handling, submission steps, and audit-ready documentation.

CERT-In reporting is critical because:

- CERT-In directions require **time-bound reporting** for specified incident types.
- Delayed or incomplete reporting can create regulatory exposure and audit findings.
- Accurate reporting requires structured collection of incident facts and timelines.
- Incident reporting must not compromise evidence integrity or client confidentiality.
- MSSP environments require strict **tenant/client segregation** and defined roles for who submits reports.

This SOP ensures:

- Clear triggers for CERT-In reporting consideration.
- Consistent and SLA-aligned internal decision-making for reportability.
- Standard reporting data fields and submission workflow.
- Secure evidence preservation and record retention alignment.
- Audit-ready traceability from ticket → decision → submission → follow-up.

> NOTE: CERT-In requirements may change over time. This SOP must be validated against the **latest CERT-In directions/advisories** at each review cycle.

---

# 3. Regulatory Basis (Reference)

This SOP is designed to align with:

- CERT-In Directions (including time-bound incident reporting requirements)
- Applicable Indian cyber security legal and regulatory obligations (as applicable to the organization and/or clients)

Where conflict exists between this SOP and updated regulatory directions, **the latest regulator direction prevails**, and this SOP must be updated.

---

# 4. Scope

This SOP applies to:

| Scope Area | Included |
|---|---|
| Organization | All business units, subsidiaries, and IT environments in scope |
| MSSP Operations | All client environments where reporting obligations apply under contract and law |
| Incident Types | All suspected/confirmed incidents that may be reportable to CERT-In |
| Reporting Stages | Initial reporting + subsequent updates + closure/final details (as requested) |
| Evidence | Logs, artifacts, indicators, and communication records required for report support |

Out of scope:

- RBI reporting workflow (covered under separate RBI SOP)
- ISO 27001 internal notification workflow (covered separately)

References:  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/ISO27001-Incident-Notification.md`

---

# 5. Definitions

| Term | Definition |
|---|---|
| CERT-In | Indian Computer Emergency Response Team |
| Reportable incident | Incident type(s) and thresholds that must be reported under CERT-In directions |
| “Noticing” time | The time the organization first becomes aware of an incident that may be reportable (used for reporting timeline calculations) |
| Initial report | First submission containing minimum required details within required timeline |
| Follow-up report | Additional information submitted after initial report as details mature |
| Regulatory package | The structured set of fields, evidence references, and approvals supporting reporting |
| Tenant | MSSP client environment (segregated) |

---

# 6. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L1 Analyst | Flag potential reportability, create/maintain incident ticket, preserve basic details and timestamps |
| L2 Analyst | Validate incident type and scope, collect evidence references, support drafting technical details |
| L3 Analyst / Forensics | Provide advanced findings, timelines, evidence integrity validation, IOC and TTP summaries |
| SOC Lead | Confirms severity (P1/P2), ensures rapid escalation to Compliance/CISO, maintains update cadence |
| IR Team Lead | Incident commander for major incidents; validates containment actions and impact statements |
| Compliance Lead | Owns reportability assessment and submission coordination; maintains reporting evidence |
| Legal Counsel | Advises on sensitive disclosures, legal hold, law enforcement engagement (as required) |
| CISO | Final approval for reporting submissions (unless delegated in writing); executive escalation |
| MSSP SDM | Ensures client communications, approvals, and tenant-safe reporting package preparation |
| Client POC (MSSP) | Provides client-side approvals, required details, and may submit report (contract-dependent) |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Regulatory-Body-Contacts.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

---

# 7. Reporting Governance Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Reportability is assessed early | Do not wait for full RCA before assessing CERT-In reporting need |
| Use “Noticing Time” | Report timeline starts from first awareness of potential reportable incident |
| Facts vs assumptions | Clearly separate confirmed facts from hypotheses in reports |
| Minimum necessary disclosure | Provide required info without exposing unrelated sensitive data |
| Evidence integrity | Preserve logs/artifacts and maintain traceability to ticket/evidence store |
| Tenant segregation (MSSP) | Never mix client data; reports must be tenant-scoped |
| Approval required | Submission must be approved by Compliance + CISO (or delegated authority) |
| Audit-ready records | Store copies of submission, timestamps, and follow-ups in evidence package |

---

# 8. CERT-In Reportability Triggers (Decision Support)

## 8.1 Common Incident Types Typically Considered Reportable (Guidance)

The following incident categories are commonly treated as reportable under CERT-In directions (confirm latest list during each review):

| Category | Examples | Internal Category Reference |
|---|---|---|
| Unauthorized access / compromise | Account takeover, privileged access abuse | Credential Attack / Network Intrusion |
| Malware / ransomware | Encryption, extortion, widespread malware | Ransomware / Malware-Trojan |
| Data breach / exfiltration | Confirmed/suspected data theft | Data Breach – Exfiltration |
| DDoS / service disruption | Material outage caused by attack | DDoS |
| Web application attacks | Exploitation of internet-facing apps | Web Application Attack |
| Insider compromise | Malicious data theft, sabotage | Insider Threat |
| Supply chain compromise | Compromised trusted vendor/software | Supply Chain Attack |
| Cloud compromise | IAM abuse, key compromise, resource tampering | Cloud Security Incident |

References:  
`01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/Category-Master-List.md`  
`02_PLAYBOOKS/`

## 8.2 “When in Doubt” Rule

If there is uncertainty about reportability:

- Treat as **“CERT-In Candidate”**
- Escalate to Compliance Lead + Legal Counsel immediately (P1/P2: within 60 minutes)
- Document decision trail in the ticket

---

# 9. Reporting Timelines (Internal Standards)

> CERT-In directions define mandatory timelines. The internal targets below ensure we meet or exceed those timelines.

| Severity | Internal Reportability Decision Target | Initial Report Submission Target (if reportable) |
|---|---:|---:|
| P1 | ≤ 60 minutes from noticing | Within regulatory requirement (target: ≤ 6 hours) |
| P2 | ≤ 4 hours from noticing | Within regulatory requirement (target: ≤ 6 hours) |
| P3/P4 | Same business day (or sooner if required) | As required by regulation/contract |

Status update cadence remains governed by:
- P1: every 30 minutes (minimum)
- P2: every 60 minutes (minimum)

References:  
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`

---

# 10. Reporting Workflow (End-to-End)

## 10.1 Step 1 — Identify “CERT-In Candidate” Incident

Owner: L1/L2/SOC Lead

Actions:

1. Create/confirm incident ticket
2. Tag ticket: **Regulatory = CERT-In Candidate**
3. Capture:
   - noticing time (UTC)
   - detection time (UTC)
   - source (SIEM/EDR/user/client)
4. Preserve initial evidence references

Reference:  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

## 10.2 Step 2 — Escalate to Compliance + CISO

Owner: SOC Lead / IR Team Lead

Actions:

- Notify Compliance Lead (phone/chat for P1/P2)
- Notify SOC Manager and CISO (per escalation matrix)
- Engage Legal Counsel if:
  - breach is suspected/confirmed
  - extortion demand received
  - law enforcement engagement is likely
  - sensitive disclosure risk exists

References:  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

---

## 10.3 Step 3 — Reportability Assessment (Decision)

Owner: Compliance Lead (with IR Team Lead + Legal Counsel as needed)

Decision must be recorded in ticket:

- **CERT-In report required:** Yes/No/Unknown
- Decision owner + time (UTC)
- Rationale
- Next steps

If “Unknown”:
- Proceed to prepare report draft in parallel until clarified (P1/P2).

---

## 10.4 Step 4 — Build CERT-In Reporting Package (Minimum Data Set)

Owner: L2/L3 + Compliance Lead

Minimum required fields (capture what is known; mark unknowns explicitly):

### A) Organization / Contact Details
- Reporting entity name
- Contact person name/designation
- Contact phone/email (approved official contact only)
- Location (city/state) as required

### B) Incident Summary
- Incident type/category
- Brief description (what happened)
- Noticing time (UTC) and detection time (UTC)
- Start time (UTC) and end time (UTC) (if known)
- Current status (active/contained/recovered)

### C) Affected Environment
- Affected systems/hosts (counts + criticality)
- Affected applications/services
- Affected users/accounts (counts; do not share unnecessary PII)
- Cloud tenant/subscription (if applicable)

### D) Impact
- Service disruption (yes/no + duration)
- Data exposure/exfiltration suspected/confirmed (yes/no/unknown)
- Business impact summary (high level)

### E) Technical Indicators (As Available)
- IPs/domains/URLs (relevant IOCs)
- File hashes (SHA256 preferred)
- Malware family/tooling (if confirmed)
- Observed TTPs / MITRE references (if available)

### F) Actions Taken
- Containment steps executed (with time UTC)
- Eradication/recovery steps (if started)
- Monitoring and validation steps

### G) Evidence References (Do Not Attach Sensitive Raw Data Unless Requested/Approved)
- SIEM export reference IDs
- EDR detection IDs
- Log bundle IDs + hashes (SHA256 where evidence-grade)
- PCAP reference IDs (if applicable)

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`  
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Log-Collection-SOP.md`

---

## 10.5 Step 5 — Review and Approval

Owner: Compliance Lead + CISO (Legal Counsel as required)

Approval checklist:

| Check | Requirement |
|---|---|
| Reportability confirmed | Mandatory |
| Minimum data fields completed | Mandatory |
| Facts vs assumptions clearly labeled | Mandatory |
| Tenant/client segregation validated (MSSP) | Mandatory |
| Sensitive data minimized | Mandatory |
| Submission channel confirmed current | Mandatory |
| Ticket updated with approval record | Mandatory |

Approval record must include:
- Approved by (name/title)
- Time (UTC)
- Any constraints (what must not be shared)

---

## 10.6 Step 6 — Submission to CERT-In

Owner: Compliance Lead (primary) / Delegate (approved in writing)

Submission rules:

- Use **current CERT-In official reporting channels** (email/portal/phone as defined by latest guidance).
- Submit within required timeline based on “noticing time.”
- If CERT-In requests additional details, provide via the same controlled workflow and record the request and response.

Ticket must record:

- Submission time (UTC)
- Channel used
- Reference/acknowledgment number (if provided)
- Copy of submitted content (stored in evidence repository)

---

## 10.7 Step 7 — Follow-Up Updates

Owner: Compliance Lead + IR Team Lead

Follow-up triggers:

- Scope changes materially
- Exfiltration confirmed or ruled out
- Major containment actions executed
- Root cause confirmed
- Service restoration completed
- Additional regulator questions received

Follow-up updates must:

- Reference original submission
- Provide delta updates (“what changed since last report”)
- Maintain evidence references

---

## 10.8 Step 8 — Closure and Record Finalization

Owner: Compliance Lead

On incident closure:

- Store final submission copies and correspondence
- Ensure evidence retention requirements are met
- Link incident final report (if produced)
- Ensure post-incident actions (RCA, lessons learned) are tracked

References:  
`07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`  
`08_POST-INCIDENT/`

---

# 11. Evidence Preservation and Retention (CERT-In Considerations)

## 11.1 Evidence Preservation (Immediate)

For CERT-In candidate incidents:

- Preserve relevant SIEM/EDR evidence exports early
- Ensure UTC timestamps and time sync context are recorded
- Avoid actions that erase telemetry without capturing evidence first (best effort)

## 11.2 Log Retention (Regulatory Alignment)

CERT-In directions require retention of specified logs for defined durations (commonly referenced as **180 days** for certain logs in applicable directions). The organization must:

- Ensure logs required by CERT-In are retained per latest direction
- Ensure retention policy is implemented and auditable
- Document limitations if retention gaps exist (and raise corrective action)

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`  
`00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`

---

# 12. MSSP-Specific Requirements (Mandatory)

For MSSP-managed incidents:

## 12.1 Who Submits the CERT-In Report?

This must be defined per client contract and local obligations:

- Some clients must submit directly (MSSP provides supporting evidence and draft).
- Some MSSP contracts allow MSSP submission on behalf of client with written authorization.

Mandatory controls:

| Control | Requirement |
|---|---|
| Client tenant verification | Mandatory before any reporting |
| Client approval to submit (if MSSP submits) | Mandatory and recorded |
| Tenant-safe evidence references | Mandatory (client-segregated storage) |
| No cross-client disclosure | Mandatory |
| Client notification of submission | Mandatory (time, reference ID, copy of report if allowed) |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`  
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 13. Documentation Requirements (Ticket-Level) (Mandatory)

For every CERT-In candidate/reportable incident, the ticket must include:

| Item | Requirement |
|---|---|
| Noticing time (UTC) | Mandatory |
| Reportability decision (Yes/No) | Mandatory |
| Decision owner + time (UTC) | Mandatory |
| Submission time (UTC) | Mandatory if submitted |
| Submission channel used | Mandatory |
| Reference/ack number (if provided) | Mandatory |
| Copy of submitted report | Mandatory (secure evidence repository reference) |
| Follow-up requests and responses | Mandatory |
| Final closure record | Mandatory |

Reference:  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 14. Common Reporting Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Incorrect noticing time | Timeline non-compliance | Record noticing time immediately in ticket |
| Waiting for full RCA before reporting | Late reporting | Parallel track: reportability + investigation |
| Including sensitive PII/credentials | Data exposure | Minimum necessary disclosure + legal review |
| Cross-tenant confusion (MSSP) | Compliance breach | Tenant verification checklist mandatory |
| No approval record | Audit failure | CISO/Compliance approval recorded in ticket |
| No copy of submission stored | Audit gap | Evidence repository reference mandatory |

---

# 15. Related Documents

| Document | Path |
|---|---|
| RBI Incident Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md` |
| Legal Counsel Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Escalation Matrix – Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| Emergency Escalation – P1 | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Evidence Retention Schedule | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md` |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |

---

# 16. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Compliance Lead / SOC Manager | Initial version |

---

# 17. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**