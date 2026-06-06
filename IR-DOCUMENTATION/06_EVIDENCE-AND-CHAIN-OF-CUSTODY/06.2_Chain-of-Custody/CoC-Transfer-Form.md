# Chain of Custody (CoC) – Transfer Form

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Form – Chain of Custody Transfer |
| Document ID | EVD-COC-004 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Evidence Custodian |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential / Restricted |
| Review Cycle | Quarterly |

---

# 2. Purpose

This form is used to document **every transfer** (custody change) of evidence, including:

- collector → evidence custodian,
- custodian → analyst (working copy issuance),
- analyst → custodian (return),
- organization → external parties (vendors, IR retainer, client, regulator, law enforcement) where approved.

Evidence transfers are critical because:

- custody changes must be traceable for legal/regulatory defensibility
- transfers are common points of evidence loss or integrity failure
- properly recorded transfers protect both the organization and individuals involved

This form ensures:

- consistent documentation of transfer details (who/when/why/how)
- integrity verification checkpoints (hash confirmation)
- confirmation of authorization and access restrictions
- linkage to master CoC record and incident ticket

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`

---

# 3. Instructions (Mandatory)

1. Complete this form **for every evidence transfer**.
2. Use UTC timestamps.
3. Confirm recipient authorization before transfer.
4. For digital evidence:
   - record SHA256 hashes (or reference the hash manifest)
   - confirm integrity after transfer (recommended)
5. For physical evidence:
   - record seal status and seal ID
6. Store the completed transfer form in the evidence repository and reference it in:
   - the incident ticket (high level), and
   - the CoC Master Form (Section F).

---

# 4. Form (Copy/Paste and Fill)

## Section A — Transfer Identification

| Field | Value |
|---|---|
| Transfer Form ID | `COC-TRF-YYYY-####` |
| Incident / Ticket ID | `INC-YYYY-####` |
| Evidence ID(s) | `EVD-...` / `PHY-...` |
| Evidence Type | Digital / Physical / Hybrid |
| Transfer Date/Time (UTC) | `YYYY-MM-DD HH:MM` |
| Transfer Reason / Purpose | e.g., “Forensic analysis”, “Regulatory submission prep”, “Client review” |
| Authorization Required? | Yes / No |
| Authorized By | Name / Role |
| Authorization Time (UTC) | `YYYY-MM-DD HH:MM` |

---

## Section B — From / To Parties

### B1. Transfer From (Current Custodian)

| Field | Value |
|---|---|
| Name |  |
| Role / Team |  |
| Organization | Internal / Client / Vendor / Regulator |
| Contact Method | Phone / Email |
| Signature |  |
| Date/Time Signed (UTC) | `YYYY-MM-DD HH:MM` |

### B2. Transfer To (New Custodian/Recipient)

| Field | Value |
|---|---|
| Name |  |
| Role / Team |  |
| Organization | Internal / Client / Vendor / Regulator |
| Contact Method | Phone / Email |
| Signature |  |
| Date/Time Signed (UTC) | `YYYY-MM-DD HH:MM` |

---

## Section C — Evidence Details

> Complete one row per item if multiple evidence items are transferred.

| Evidence ID | Description | Sensitivity | Format | Size | Seal ID (Physical) | Notes |
|---|---|---|---|---:|---|---|
|  |  | Restricted/Confidential/Internal | E01/RAW/PCAP/CSV/Device |  |  |  |
|  |  |  |  |  |  |  |

---

## Section D — Integrity Verification (Digital Evidence)

> For physical evidence, complete Section E instead. For hybrid evidence, complete both.

| Field | Value |
|---|---|
| Hash Algorithm | SHA256 (required for evidence-grade) |
| Hash Manifest Reference | File name/path (if multiple items) |
| Hash Verified Before Transfer? | Yes / No |
| Verified By (Before) | Name / Role |
| Verification Time (UTC) | `YYYY-MM-DD HH:MM` |
| Hash Verified After Transfer? | Yes / No / N/A |
| Verified By (After) | Name / Role |
| Verification Time (UTC) | `YYYY-MM-DD HH:MM` |
| Integrity Notes | e.g., “Encrypted archive; verified archive hash” |

If listing hashes inline:

| Evidence ID / File | SHA256 |
|---|---|
|  |  |
|  |  |

---

## Section E — Physical Evidence Seal and Condition Check

| Field | Value |
|---|---|
| Tamper Seal Applied? | Yes / No |
| Seal ID / Number |  |
| Seal Status at Transfer | Intact / Broken / Not applicable |
| Item Condition | Good / Damaged / Other |
| Packaging Type | Evidence bag/box type |
| Notes |  |

---

## Section F — Transfer Method and Security Controls

| Field | Value |
|---|---|
| Transfer Method | Secure portal / Encrypted drive / Courier / Hand delivery / Other |
| Encryption Used | Yes / No / N/A (specify method) |
| Tracking Number (if courier) |  |
| Transfer Location | Site/room or digital portal name |
| Access Restrictions Communicated | Yes / No |
| Recipient Authorized Access Confirmed | Yes / No |
| Evidence Repository Reference | Where transfer form is stored |

---

## Section G — Acknowledgment and Receipt

I acknowledge receipt of the evidence listed above and accept responsibility for maintaining evidence integrity and access controls as required.

**Recipient Signature:** ____________________  
**Date/Time (UTC):** ____________________

---

# 5. Related Documents

| Document | Path |
|---|---|
| CoC Master Form | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md` |
| CoC Digital Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| CoC Physical Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Physical-Evidence.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| Legal Counsel Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |

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