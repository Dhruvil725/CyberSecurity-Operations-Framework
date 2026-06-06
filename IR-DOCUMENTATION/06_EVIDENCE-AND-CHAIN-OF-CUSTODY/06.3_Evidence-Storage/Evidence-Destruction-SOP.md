# SOP: Evidence Destruction

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Evidence Destruction |
| Document ID | EVD-STR-003 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Evidence Custodian / Compliance Lead |
| Approved By | CISO |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines the controlled process for **secure destruction** of evidence (digital and physical) after:

- retention requirements are satisfied,
- legal holds are cleared, and
- approvals are obtained.

Evidence destruction is critical because:

- Evidence often contains highly sensitive information (credentials, PII, customer data)
- Retaining evidence longer than necessary increases breach risk and storage exposure
- Improper destruction can lead to data recovery, compliance violations, and audit findings
- Legal holds and regulatory inquiries may require preservation beyond standard retention
- MSSP contracts may require client-specific destruction and confirmation

This SOP ensures:

- secure and auditable destruction of evidence
- documented approvals, methods, and destruction logs
- verification that legal holds do not apply
- tenant/client segregation and contractual compliance for MSSP evidence
- alignment with retention schedule and evidence storage policy

---

# 3. Scope

This SOP applies to destruction of:

| Evidence Type | Examples |
|---|---|
| Digital evidence | logs, exports, PCAP, disk images, memory dumps, malware samples (where permitted) |
| Digital records | CoC forms, transfer forms, evidence indices (subject to retention) |
| Physical evidence | devices, drives, USBs, printed materials, access tokens |
| MSSP client evidence | client-specific evidence packages stored by MSSP |

Out of scope:

- destruction of general IT data unrelated to incidents
- decommissioning of production systems not treated as evidence

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Destruction | Secure elimination of evidence such that it cannot be recovered |
| Legal hold | Instruction to preserve evidence; destruction prohibited until released |
| Destruction candidate | Evidence item that has reached retention end and is eligible for destruction |
| Sanitization | Secure wiping of digital media to recognized standards |
| Physical destruction | Shredding, degaussing, crushing, or certified disposal methods |
| Destruction certificate | Vendor-provided confirmation of destruction (if used) |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| Evidence Custodian | Maintains destruction list, coordinates approvals, executes/oversees destruction, records logs |
| Compliance Lead | Validates retention completion and regulatory constraints |
| Legal Counsel | Confirms legal hold release and approves destruction for sensitive cases |
| IR Team Lead | Confirms evidence is no longer required for investigation/PIR |
| SOC Manager | Oversight; approves high-risk destruction actions; ensures governance |
| MSSP SDM | Ensures client approvals and contractual constraints for client evidence |
| Approved Disposal Vendor (if used) | Performs certified destruction and provides certificates |

---

# 6. Evidence Destruction Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Do not destroy under legal hold | Legal hold overrides retention schedule |
| Approval required | Destruction must be approved per authority matrix |
| Secure methods only | Must meet organizational security standards |
| Audit trail | Destruction must be logged and traceable to evidence IDs |
| Verification | Confirm deletion/wipe success and document method |
| Tenant segregation (MSSP) | Client evidence destroyed per client-specific rules and approvals |
| Minimum retention | Never destroy before retention end date |

---

# 7. Preconditions (Mandatory)

Evidence may be destroyed only when:

| Condition | Requirement |
|---|---|
| Retention end date reached | Mandatory |
| Legal hold check completed | Mandatory |
| Regulatory inquiry check completed | Mandatory (if applicable) |
| IR Team confirms no further need | Mandatory for P1/P2 evidence |
| MSSP client confirms (if required) | Mandatory for client evidence |
| Approvals obtained | Mandatory |
| Destruction method selected | Mandatory |
| Evidence IDs and storage locations verified | Mandatory |

---

# 8. Approval Authority (Minimum Standard)

| Evidence Sensitivity | Minimum Approval |
|---|---|
| Internal | Evidence Custodian + Compliance Lead |
| Confidential | Evidence Custodian + Compliance Lead + SOC Manager |
| Restricted (disk/memory/customer data) | Evidence Custodian + Legal Counsel + CISO |
| MSSP client evidence | Evidence Custodian + MSSP SDM + client approval (contract-dependent) + Legal (if hold) |

---

# 9. Destruction Workflow (End-to-End)

## 9.1 Step 1 — Generate Destruction Candidate List

Owner: Evidence Custodian (Quarterly minimum)

Include:

- Evidence ID(s)
- Incident ID
- Evidence type and sensitivity
- Retention end date
- Storage location
- Legal hold status
- Recommended method

---

## 9.2 Step 2 — Perform Legal Hold and Compliance Checks

Owner: Legal Counsel + Compliance Lead

Confirm:

- no active legal hold applies, or legal hold has been released
- no regulator inquiry or audit requires continued retention
- no contractual retention requirement remains (MSSP)

Document approvals and checks.

---

## 9.3 Step 3 — Obtain Approvals

Owner: Evidence Custodian

- Collect approvals based on sensitivity (Section 8)
- Record approvals in destruction log
- For MSSP, obtain client approval if required

---

## 9.4 Step 4 — Execute Secure Destruction

Owner: Evidence Custodian / Approved Vendor

### Digital Evidence Destruction Methods (Approved)

| Method | When Used | Requirements |
|---|---|---|
| Secure wipe (software) | Reusable media | Must meet recognized wipe standard; verify completion |
| Cryptographic erase | Encrypted storage | Destroy encryption keys; validate irrecoverability |
| Physical destruction | Non-reusable drives | Shred/crush/degauss as appropriate |
| Secure deletion in object storage | Cloud evidence | Versioning lifecycle + delete markers; confirm permanent deletion policy |

### Physical Evidence Destruction Methods (Approved)

| Method | When Used | Requirements |
|---|---|---|
| Shredding | Paper | Cross-cut shred; secure disposal |
| Crushing/shredding | Drives/devices | Use certified service; obtain certificate |
| Degaussing | Magnetic media | Verify effectiveness; follow vendor specs |
| Certified e-waste disposal | Devices | Ensure data destruction performed before disposal |

If a third-party vendor performs destruction:

- maintain certificate of destruction
- record chain-of-custody transfer to vendor
- store certificate in evidence repository

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`

---

## 9.5 Step 5 — Validate and Record Destruction

Owner: Evidence Custodian

Validation requirements:

| Requirement | Standard |
|---|---|
| Record destruction time (UTC) | Mandatory |
| Record destruction method and tool/vendor | Mandatory |
| Record who performed destruction | Mandatory |
| Record evidence IDs destroyed | Mandatory |
| Store certificates/logs | Mandatory |
| Update evidence index and CoC records | Mandatory |
| Update retention register | Mandatory |

---

# 10. Destruction Log Template (Mandatory)

> Maintain a destruction log as a controlled record.

| Destruction ID | Evidence ID(s) | Incident ID | Sensitivity | Method | Performed By | Date/Time (UTC) | Approval Ref | Certificate Ref | Notes |
|---|---|---|---|---|---|---:|---|---|---|
| DEST-YYYY-#### | EVD-... | INC-... | Restricted/Confidential/Internal | Wipe/Crypto erase/Destroy | Name/Role/Vendor |  | Ticket/Approval | Path/ID |  |

---

# 11. Special Cases

## 11.1 Evidence Under Legal Hold

- Destruction prohibited
- Evidence must be flagged “Legal Hold”
- Retention end date is suspended
- Only Legal Counsel may authorize release

## 11.2 Evidence Shared Externally

If evidence was transferred to:

- law enforcement,
- regulator,
- external IR retainer,
- client,

ensure transfer records are complete and destruction is scoped to internal copies only unless otherwise authorized.

## 11.3 Malware Samples

Malware samples may be retained only in isolated, approved repositories and destroyed only after ensuring no legal/regulatory need remains.

---

# 12. MSSP Client Evidence Destruction (Mandatory)

For client evidence:

- follow contract-defined retention and destruction requirements
- obtain client approval where required
- ensure tenant-scoped destruction (no impact to other clients)
- provide destruction confirmation to client if required

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md`

---

# 13. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Destroying evidence under legal hold | Legal exposure | Legal hold check mandatory |
| Destroying before retention end | Audit failure | Retention validation required |
| No certificate/log | Audit gap | Destruction log mandatory |
| Incomplete destruction (recoverable) | Data leak | Approved secure methods only + validation |
| Cross-tenant destruction mistakes (MSSP) | Compliance breach | Tenant verification and client approvals |

---

# 14. Related Documents

| Document | Path |
|---|---|
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| Evidence Retention Schedule | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md` |
| MSSP Client Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md` |
| CoC Transfer Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md` |
| Legal Counsel Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Policy Exception Register | `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md` |

---

# 15. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Evidence Custodian / Compliance Lead | Initial version |

---

# 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**