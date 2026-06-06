# Chain of Custody (CoC) – Master Form

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Form – Chain of Custody (Master) |
| Document ID | EVD-COC-002 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Evidence Custodian |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This master form is the standardized **Chain of Custody (CoC)** record used to document:

- evidence identification and description,
- collection details,
- integrity verification (hashes),
- custody ownership and storage location,
- transfers and access events (where applicable),
- final disposition (archive/return/destruction).

This form is audit-ready and supports regulatory, contractual, and legal defensibility of evidence handling.

Use this form for:

- Digital evidence (disk images, memory dumps, logs, PCAP, exports)
- Physical evidence (when combined with physical CoC addendum where needed)

Reference SOPs:
- `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`
- `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Physical-Evidence.md`

---

# 3. Instructions (Mandatory)

1. Assign a unique **Evidence ID** and record the **Incident/Ticket ID**.
2. Complete Sections A–D at collection time (or immediately after for emergencies).
3. Compute and record **SHA256 hashes** for evidence-grade digital artifacts.
4. Store the evidence in the approved evidence repository and record location + custodian.
5. Use **CoC Transfer Form** for each custody transfer and reference it in Section E.
6. Use UTC timestamps for all time entries.
7. Do not write sensitive content into the form if it is not required (use references/paths).

---

# 4. Form (Copy/Paste and Fill)

## Section A — Case / Incident Details

| Field | Value |
|---|---|
| Incident / Ticket ID | `INC-YYYY-####` |
| Case Name / Short Title |  |
| Severity | P1 / P2 / P3 / P4 |
| Incident Category |  |
| Client/Tenant (MSSP, if applicable) | Client ID / Name |
| Requesting Team | SOC / IR / Legal / Compliance |
| Legal Hold Issued? | Yes / No / Unknown |
| CoC Required Trigger | P1/P2 / Regulatory / Legal / Contract / Other |
| Form Created By | Name / Role |
| Form Created Time (UTC) | `YYYY-MM-DD HH:MM` |

---

## Section B — Evidence Identification

| Field | Value |
|---|---|
| Evidence ID | `EVD-INC-YYYY-####-####` |
| Evidence Type | Digital / Physical |
| Evidence Sub-Type | Disk image / Memory dump / Logs / PCAP / Email / Device / Other |
| Evidence Description | Short description of what the evidence is |
| Source System / Location | Hostname/IP/Device/Cloud tenant/site |
| Evidence Sensitivity | Restricted / Confidential / Internal |
| Collection Priority | Immediate (P1/P2) / Standard |
| Related Evidence IDs | (If part of a set) |

---

## Section C — Collection Details

| Field | Value |
|---|---|
| Collector Name |  |
| Collector Role/Team | L2 / L3 / IR / Network / Other |
| Collection Date/Time Start (UTC) | `YYYY-MM-DD HH:MM` |
| Collection Date/Time End (UTC) | `YYYY-MM-DD HH:MM` |
| Collection Method | Export / Live capture / Offline imaging / Snapshot / Other |
| Tool(s) Used | Tool name + version |
| Collection Parameters | Query/filter/time window/interface (as applicable) |
| System State (if relevant) | Powered on/off, isolated, user logged in |
| Issues/Errors Observed | None / Details |
| Notes | Optional |

---

## Section D — Integrity Verification (Digital Evidence)

> Complete for all digital evidence where hashing is applicable.

| Field | Value |
|---|---|
| Hash Algorithm | SHA256 (required) |
| Source Hash (if applicable) |  |
| Evidence File Hash (SHA256) |  |
| Hash Verified? | Yes / No |
| Verification Time (UTC) | `YYYY-MM-DD HH:MM` |
| Verified By | Name / Role |
| Integrity Notes | e.g., “Live acquisition; source hash not feasible” |

**If multiple files:** attach a hash manifest or list file names and hashes below:

| File Name | Size | SHA256 |
|---|---:|---|
|  |  |  |
|  |  |  |

---

## Section E — Custody and Storage

| Field | Value |
|---|---|
| Evidence Custodian | Name / Role |
| Custody Accepted Time (UTC) | `YYYY-MM-DD HH:MM` |
| Storage Location (Reference) | Evidence vault path / ID (tenant-scoped if MSSP) |
| Access Restrictions | Who can access + approval requirements |
| Encryption at Rest | Yes / No / N/A |
| Access Logging Enabled | Yes / No / N/A |
| Working Copy Created? | Yes / No |
| Working Copy Location (Reference) |  |
| Working Copy Hash (SHA256) |  |

---

## Section F — Transfer and Handling History (Summary)

> Use CoC Transfer Form for each transfer and list references here.

| Transfer # | Date/Time (UTC) | From | To | Purpose | Method | Transfer Form Ref |
|---:|---:|---|---|---|---|---|
| 1 |  |  |  |  |  | `COC-TRF-...` |
| 2 |  |  |  |  |  | `COC-TRF-...` |

---

## Section G — Disposition (Retention / Return / Destruction)

| Field | Value |
|---|---|
| Retention Requirement | Standard / Legal hold / Contract / Regulatory |
| Retention End Date (UTC) | `YYYY-MM-DD` |
| Final Disposition | Archived / Returned / Destroyed |
| Disposition Date/Time (UTC) | `YYYY-MM-DD HH:MM` |
| Approved By | Name / Role |
| Disposition Method | Secure archive / Secure wipe / Physical destruction / Return to owner |
| Disposition Evidence Ref | Ticket/record reference |

References:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Destruction-SOP.md`

---

## Section H — Sign-Off

| Role | Name | Signature | Date/Time (UTC) |
|---|---|---|---:|
| Collector |  |  |  |
| Evidence Custodian |  |  |  |
| Forensics Lead (if applicable) |  |  |  |
| Legal Counsel (if applicable) |  |  |  |

---

# 5. Related Documents

| Document | Path |
|---|---|
| CoC Digital Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| CoC Transfer Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md` |
| CoC Physical Evidence | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Physical-Evidence.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| Evidence Retention Schedule | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md` |

---

# 6. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Evidence Custodian | Initial version |

---

# 7. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Form**