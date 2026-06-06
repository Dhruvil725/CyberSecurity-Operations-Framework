# Audit Evidence Package (Incident / SOC / IR)

---

# 1. Document Control

| Field          | Value                                |
| -------------- | ------------------------------------ |
| Document Name  | Template – Audit Evidence Package    |
| Document ID    | RPT-REG-001                          |
| Version        | 1.0                                  |
| Effective Date | 30-May-2026                          |
| Owner          | Compliance Lead / ISMS Manager       |
| Approved By    | CISO                                 |
| Classification | Internal – Confidential / Restricted |
| Review Cycle   | Quarterly                            |

---

# 2. Purpose

This template defines the structure and minimum contents of an **Audit Evidence Package** used to support:

- ISO 27001 certification and surveillance audits,
- NIST maturity assessments,
- RBI compliance inspections and reviews,
- client audits (MSSP),
- internal audits and management reviews.

An audit evidence package is critical because:

- audits require consistent, verifiable proof of control operation and incident handling
- incomplete evidence leads to audit findings and weakens regulatory posture
- evidence must be traceable to tickets, logs, and approvals with integrity controls
- sensitive evidence must be handled securely, with segregation for MSSP clients
- standardized packaging reduces time and risk during audit requests

This template ensures:

- consistent evidence structure across audits and time periods
- clear mapping between audit requests and evidence artifacts
- proper handling of sensitive evidence (hashes, access control, CoC where required)
- repeatable approach for creating evidence packages quickly and defensibly

---

# 3. Scope

This template applies to audit evidence packages for:

| Audit Type         | Examples                                                        |
| ------------------ | --------------------------------------------------------------- |
| ISO 27001          | Clause 8 incident handling; Annex A A.5.24–A.5.28               |
| NIST assessments   | CSF Respond/Recover; SP 800-61 alignment                        |
| RBI inspections    | SOC operations, incident reporting, evidence retention          |
| CERT-In related    | proof of reporting workflows (where applicable)                 |
| MSSP client audits | SLA compliance, tenant segregation, incident response practices |

Evidence may include:

- policies, SOPs, and playbooks
- incident tickets and reports
- evidence logs and CoC records
- training and exercise records
- KPI/SLA reports and dashboards
- change records and tuning logs

Out of scope:

- raw evidence dumps unless explicitly requested and approved by Legal/Compliance
- unrelated enterprise IT evidence not required for security audit scope

---

# 4. Instructions (Mandatory)

- Treat all audit evidence as **confidential** by default.
- Use secure evidence repository for all artifacts; do not email raw evidence unless approved.
- Provide **references and sanitized exports** where possible.
- For MSSP, build **tenant-scoped** packages per client. Never mix multiple clients in one package.
- Maintain an evidence package index and ensure integrity (hashing) for evidence-grade bundles.
- Record approvals for sharing evidence externally (client auditors, regulators).

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

---

# 5. Evidence Package Metadata (Mandatory)

| Field                              | Value                                                 |
| ---------------------------------- | ----------------------------------------------------- |
| Evidence Package ID                | `AUD-EVD-YYYY-####`                                   |
| Audit Type                         | ISO27001 / NIST / RBI / Client Audit / Internal Audit |
| Auditor / Requesting Party         | `Name/Organization`                                   |
| Scope                              | SOC / IR / MSSP / Specific control families           |
| Reporting Period (UTC)             | `Start → End`                                         |
| Prepared By                        | `Name / Role`                                         |
| Reviewed By                        | `Name / Role`                                         |
| Approved By                        | `Name / Role`                                         |
| Date Prepared (UTC)                | `YYYY-MM-DD HH:MM`                                    |
| Delivery Method                    | Portal / Secure transfer / Onsite review              |
| Client/Tenant (if applicable)      | `Client ID / Name`                                    |
| Confidentiality Classification     | Internal Confidential / Restricted                    |
| Legal Hold / Privilege Applicable? | Yes / No / Unknown                                    |

---

# 6. Evidence Package Structure (Standard)

Recommended folder structure:
AUD-EVD-[YYYY]-[####]/
00_Index/
01_Scope-and-Request/
02_Policies-and-Governance/
03_Procedures-and-Playbooks/
04_Operational-Records/
05_Incident-Samples/
06_Evidence-and-CoC/
07_Training-and-Exercises/
08_Metrics-and-Management-Review/
09_Change-and-Improvement/
10_Regulatory-and-External/
99_Attestations-and-Approvals/

---

# 7. Evidence Index (Mandatory)

## 7.1 Index Table (Copy/Paste)

| #   | Evidence Item | Description | Period | Location / Reference | Owner | Sensitivity                      | Notes |
| ---:| ------------- | ----------- | ------ | -------------------- | ----- | -------------------------------- | ----- |
| 1   |               |             |        |                      |       | Internal/Confidential/Restricted |       |
| 2   |               |             |        |                      |       |                                  |       |

---

# 8. Scope and Audit Request Mapping (Mandatory)

## 8.1 Audit Request Summary

| Audit Request / Control | Evidence Needed | Provided? | Evidence Reference |
| ----------------------- | --------------- | --------- | ------------------ |
|                         |                 | Yes/No    |                    |

## 8.2 Framework Mapping (Optional but Recommended)

| Framework | Control/Clause             | Evidence Reference |
| --------- | -------------------------- | ------------------ |
| ISO 27001 | A.5.24                     |                    |
| ISO 27001 | A.5.28                     |                    |
| NIST      | SP 800-61 Preparation      |                    |
| RBI       | SOC monitoring requirement |                    |

References:  
`00_GOVERNANCE/00.2_Frameworks-Mapping/`  
`00_GOVERNANCE/00.1_Policies/`

---

# 9. Policies and Governance Evidence (Typical Items)

Include applicable documents:

- IR Policy Master
- NIST/ISO/RBI alignment documents
- RACI matrix
- SLAs/SLOs and breach procedure
- policy exception register

Evidence table:

| Document                  | Version | Reference | Notes |
| ------------------------- | -------:| --------- | ----- |
| IR Policy Master          |         |           |       |
| SLA definitions           |         |           |       |
| Policy exception register |         |           |       |

---

# 10. Procedures and Playbooks Evidence (Typical Items)

Include:

- SOC tier procedures (L1/L2/L3/Lead/IR)
- evidence handling SOPs
- playbooks relevant to audit scope
- ticketing SOPs

Evidence table:

| Document                | Version | Reference | Notes |
| ----------------------- | -------:| --------- | ----- |
| L1 Alert Handling SOP   |         |           |       |
| Evidence Collection SOP |         |           |       |
| Ransomware playbook     |         |           |       |

---

# 11. Operational Records Evidence (Typical Items)

Include evidence of operations:

- daily/weekly/monthly SOC reports (as requested)
- tuning/change records
- ticket audit samples
- tool health dashboards snapshots

Evidence table:

| Record                       | Period | Reference | Notes |
| ---------------------------- | ------ | --------- | ----- |
| Daily SOC report samples     |        |           |       |
| Ticket QA sampling output    |        |           |       |
| SIEM ingestion health export |        |           |       |

---

# 12. Incident Samples (Typical Audit Sampling)

Provide a sampling set as requested by auditor.

## 12.1 Sampling Rules (Guidance)

- Provide at least:
  - 1–2 P1 incidents (if any occurred),
  - 2–5 P2 incidents,
  - 3–10 P3/P4 incidents (as requested),
  - include at least one false positive case and one true positive case.
- Ensure all samples have:
  - complete timestamps,
  - evidence references,
  - escalation and closure documentation,
  - PIR/RCA links for P1/P2.

## 12.2 Incident Sample Table

| Sample # | Incident ID | Severity | Category | Outcome | Evidence Ref | PIR/RCA Ref |
| --------:| ----------- | -------- | -------- | ------- | ------------ | ----------- |
| 1        | INC-        | P1       |          | TP      |              |             |
| 2        | INC-        | P2       |          | TP      |              |             |

---

# 13. Evidence and CoC Records (If Required)

Include:

- evidence index
- CoC master forms and transfer forms (for evidence-grade incidents)
- evidence retention and storage policy references
- evidence destruction logs (if requested)

Evidence table:

| Evidence                       | Reference | Notes |
| ------------------------------ | --------- | ----- |
| CoC forms for incident samples |           |       |
| Evidence storage policy        |           |       |
| Evidence retention schedule    |           |       |

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/`

---

# 14. Training and Exercises Evidence

Include:

- onboarding program evidence
- tabletop exercise records and scorecards
- drill after-action reports
- training attendance evidence

Evidence table:

| Evidence        | Period | Reference | Notes |
| --------------- | ------ | --------- | ----- |
| TTX scorecards  |        |           |       |
| Drill AAR       |        |           |       |
| Training roster |        |           |       |

References:
`10_TRAINING-AND-EXERCISES/`

---

# 15. Metrics and Management Review Evidence

Include:

- monthly metrics reports
- quarterly trend analysis
- annual IR review
- management review notes (if maintained)

Evidence table:

| Evidence                 | Period | Reference | Notes |
| ------------------------ | ------ | --------- | ----- |
| Monthly metrics report   |        |           |       |
| Quarterly trend analysis |        |           |       |

---

# 16. Change and Improvement Evidence

Include:

- detection improvement log extracts
- control gap tracker extracts
- playbook update logs
- corrective actions and closure evidence

Evidence table:

| Evidence                  | Reference | Notes |
| ------------------------- | --------- | ----- |
| Detection improvement log |           |       |
| Control gap tracker       |           |       |

References:
`08_POST-INCIDENT/08.3_Improvement-Tracking/`

---

# 17. Regulatory and External Communications Evidence (If Applicable)

Include:

- CERT-In/RBI reporting copies and acknowledgments (sanitized)
- legal counsel engagement records (high-level references)
- vendor case references and outcomes

Evidence table:

| Item                    | Reference | Notes |
| ----------------------- | --------- | ----- |
| CERT-In submission copy |           |       |
| RBI submission copy     |           |       |

---

# 18. Approval and Attestations (Mandatory)

## 18.1 Evidence Package Approval

Approved for release to auditor/requesting party:

| Role              | Name | Signature | Date (UTC) |
| ----------------- | ---- | --------- | ----------:|
| Prepared By       |      |           |            |
| Compliance / ISMS |      |           |            |
| Legal (if needed) |      |           |            |
| CISO              |      |           |            |

## 18.2 Disclosure Constraints

- `Any restrictions on redistribution`
- `Any items excluded due to legal hold or privilege`
- `Any items requiring onsite review only`

---

# 19. Related Documents

| Document                      | Path                                                                                |
| ----------------------------- | ----------------------------------------------------------------------------------- |
| ISO 27001 Incident Log        | `07_REPORTING/07.4_Regulatory-Reports/ISO27001-Incident-Log.md`                     |
| NIST Incident Report Template | `07_REPORTING/07.4_Regulatory-Reports/NIST-Incident-Report-Template.md`             |
| RBI Mandatory Report Template | `07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`             |
| Evidence Storage Policy       | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| CoC Digital Evidence SOP      | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`    |
| Policy Exception Register     | `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`                          |

---

# 20. Revision History

| Version | Date        | Author                         | Changes         |
| ------- | ----------- | ------------------------------ | --------------- |
| 1.0     | 30-May-2026 | Compliance Lead / ISMS Manager | Initial version |

---

# 21. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
