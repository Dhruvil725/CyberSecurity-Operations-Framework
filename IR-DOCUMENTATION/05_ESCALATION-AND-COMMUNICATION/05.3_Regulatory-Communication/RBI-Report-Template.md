# RBI Incident Report Template

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Template – RBI Incident Report |
| Document ID | REG-COM-005 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Compliance Lead / SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This document provides a standardized **RBI incident report template** to support:

- Initial reporting to RBI (as required)
- Follow-up updates as incident facts mature
- Consistent, audit-ready documentation of incident details and response actions
- MSSP support for RBI-regulated clients (tenant-scoped)

This template ensures:

- Required fields are consistently captured
- Clear separation of confirmed facts vs assumptions
- Traceable timelines in UTC
- Clear description of impact, containment, and corrective actions
- Evidence references maintained without sharing sensitive raw data unnecessarily

> IMPORTANT: RBI reporting requirements and format expectations may change. This template must be reviewed against the latest RBI circulars/directions during each quarterly review and updated accordingly.

---

# 3. Instructions (Mandatory)

- Use **UTC** for all timestamps.
- Keep content **fact-based**; label assumptions clearly.
- Avoid including raw sensitive evidence (PII/credentials/PCAP) in the report body.
- Reference evidence using IDs/paths from approved evidence repository.
- For MSSP: verify client/tenant scope and ensure zero cross-client disclosure.
- Record report submission details in the incident ticket (time, channel, reference number).

Reference SOP:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`

---

# 4. Template (Copy/Paste)

## Section A — Report Metadata (Mandatory)

| Field | Value |
|---|---|
| Report Type | Initial / Follow-up / Final |
| RBI Reference / Ack No. (if available) |  |
| Incident Ticket ID | `INC-YYYY-####` |
| Reporting Entity Name |  |
| Reporting Entity Regulator Category | Bank / NBFC / Payment System / Other |
| Client Name (if MSSP) |  |
| Client ID (if MSSP) |  |
| Prepared By | Name / Role |
| Reviewed By | Name / Role |
| Approved By | Name / Role (CISO/Compliance) |
| Date Prepared (UTC) | `YYYY-MM-DD HH:MM` |
| Date Submitted (UTC) | `YYYY-MM-DD HH:MM` |
| Submission Channel | Email / Portal / Other (specify) |
| Confidentiality Classification | Internal – Confidential |

---

## Section B — Incident Summary (Mandatory)

**Incident Category:**  
`Ransomware / Malware / Data Breach / Phishing-BEC / Credential Attack / DDoS / Web Attack / Cloud / Insider / Supply Chain / Other`

**Executive Summary (3–8 lines):**  
- `What happened (confirmed)`  
- `Which systems/services impacted`  
- `Current status (active/contained/recovered)`  
- `High-level impact`  
- `Actions taken`  

**Current Status:**  
- `Active / Contained / Under Recovery / Recovered / Monitoring`

---

## Section C — Timeline (UTC) (Mandatory)

> Use UTC. If original logs are in local time, include conversion notes.

| Event | Time (UTC) | Notes |
|---|---:|---|
| Noticing time (first awareness) |  |  |
| Detection time (tool/alert time) |  |  |
| Incident declared (P1/P2) |  |  |
| IR team activated |  |  |
| Containment started |  |  |
| Containment completed |  |  |
| Eradication started |  |  |
| Recovery started |  |  |
| Services restored |  |  |
| Monitoring period started |  |  |

**Timeline Notes:**  
- `Any gaps, uncertainties, or ongoing validation items`

---

## Section D — Affected Scope (Mandatory)

### D1. Systems / Infrastructure Impacted

| Item | Details |
|---|---|
| Number of hosts/systems impacted |  |
| Critical systems impacted | `Yes/No` + list |
| Servers impacted | list/count |
| Endpoints impacted | list/count |
| Network devices impacted | list/count |
| Cloud resources impacted | list/tenant/subscription |

### D2. Users / Accounts Impacted

| Item | Details |
|---|---|
| Number of accounts impacted |  |
| Privileged accounts impacted | `Yes/No` + details |
| Customer accounts impacted (if applicable) | `Yes/No/Unknown` + details |

### D3. Services / Channels Impacted (BFSI Context)

| Channel/Service | Impact | Duration (UTC) | Notes |
|---|---|---:|---|
| Internet banking | `None/Degraded/Down` |  |  |
| Mobile banking |  |  |  |
| ATM/POS |  |  |  |
| Payment rails (UPI/IMPS/NEFT/RTGS) |  |  |  |
| Branch operations |  |  |  |

---

## Section E — Incident Details (Technical Summary, High Level)

### E1. Suspected/Confirmed Attack Vector

- **Suspected entry point:** `Phishing / Exploit / Credential abuse / Vendor / Other`
- **Confirmed entry point:** `If confirmed; otherwise state “under investigation”`
- **Initial compromised asset/account:** `...`

### E2. Observed Techniques / Behaviors (TTPs)

- `Lateral movement observed: Yes/No/Unknown`
- `Privilege escalation observed: Yes/No/Unknown`
- `Persistence observed: Yes/No/Unknown`
- `C2 communication observed: Yes/No/Unknown`
- `Exfiltration observed: Yes/No/Unknown`

(Optional) MITRE mapping summary:
- `Txxxx – Technique – confidence`

### E3. Indicators (As Appropriate)

> Include only necessary indicators. Avoid broad/untested IOCs.

- **IPs:** `...`
- **Domains/URLs:** `...`
- **File hashes (SHA256 preferred):** `...`
- **Email indicators (if phishing/BEC):** `sender domain, subject patterns`

---

## Section F — Impact Assessment (Mandatory)

### F1. Availability Impact

- **Service outage:** `Yes/No`
- **Duration:** `...`
- **Business impact summary:** `...`

### F2. Data Impact (Confidentiality)

- **Data access/exposure:** `Suspected/Confirmed/No evidence/Unknown`
- **Data types involved:** `PII / Financial / Credentials / Proprietary / Other`
- **Approx. volume/records affected:** `...` (if known)
- **Customer impact:** `Yes/No/Unknown` + notes

### F3. Integrity Impact

- **Data/system integrity compromised:** `Yes/No/Unknown`
- **Evidence:** `...`

### F4. Financial / Fraud Impact (If Applicable)

- **Fraud observed:** `Yes/No/Unknown`
- **Estimated loss:** `...` (if available)

---

## Section G — Actions Taken (Mandatory)

### G1. Containment Actions

| Action | Scope | Executed By | Authorized By | Time (UTC) | Outcome |
|---|---|---|---|---:|---|
|  |  |  |  |  |  |
|  |  |  |  |  |  |

### G2. Eradication Actions

- `Malware removal, patching, credential resets, persistence removal, etc.`

### G3. Recovery Actions

- `Restoration from backup, system rebuild, validation checks, re-enablement steps`

### G4. Monitoring and Assurance

- `SIEM/EDR monitoring enhancements, IOC watchlists, additional logging enabled`

---

## Section H — Root Cause and Corrective Actions (As Available)

> If RCA is not complete, state “RCA in progress” and provide interim findings.

- **Root cause (interim/final):** `...`
- **Control gaps identified:** `...`
- **Corrective actions planned:** `...`
- **Target completion dates:** `...`
- **Owner(s):** `...`

Reference:
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`

---

## Section I — Notifications and Coordination (Mandatory)

| Party | Notified? (Y/N) | Time (UTC) | Notes / Reference |
|---|---|---:|---|
| CISO / Management |  |  |  |
| Compliance / Legal |  |  |  |
| CERT-In (if applicable) |  |  |  |
| Customers (if applicable) |  |  |  |
| Law enforcement (if applicable) |  |  |  |
| Vendors / IR retainer |  |  |  |

---

## Section J — Evidence References (Internal Only)

> Do not attach raw evidence to RBI report unless requested and approved.

| Evidence Item | Reference ID / Path | Hash (SHA256 if applicable) | Notes |
|---|---|---|---|
| SIEM export |  |  |  |
| EDR timeline |  |  |  |
| Firewall/proxy logs |  |  |  |
| Disk image |  |  |  |
| Memory dump |  |  |  |
| PCAP |  |  |  |

---

## Section K — Declaration

I confirm that the information provided above is accurate to the best of our knowledge as of **[Date/Time UTC]** and that any unknown items are under investigation and will be updated as information becomes available.

**Name:** ____________________  
**Title:** ____________________  
**Organization:** ____________________  
**Signature:** ____________________  
**Date (UTC):** ____________________

---

# 5. Related Documents

| Document | Path |
|---|---|
| RBI Incident Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md` |
| CERT-In Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md` |
| Legal Counsel Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Ticket Closure Criteria | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Final Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md` |
| RBI Mandatory Report Template | `07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md` |

---

# 6. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Compliance Lead / SOC Manager | Initial version |

---

# 7. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**