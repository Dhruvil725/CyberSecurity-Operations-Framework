# RBI Mandatory Incident Report Template

---

# 1. Document Control

| Field          | Value                                    |
| -------------- | ---------------------------------------- |
| Document Name  | Template – RBI Mandatory Incident Report |
| Document ID    | RPT-REG-004                              |
| Version        | 1.0                                      |
| Effective Date | 30-May-2026                              |
| Owner          | CISO / Compliance Lead                   |
| Approved By    | CISO                                     |
| Classification | Confidential – Restricted                |
| Review Cycle   | Quarterly (or upon RBI circular update)  |

---

# 2. Purpose

This template provides the standardized **RBI Mandatory Incident Report** format used to report cyber security incidents to the **Reserve Bank of India (RBI)** in alignment with:

- **RBI Cyber Security Framework (June 2016)** and subsequent circulars
- **RBI Master Direction on Information Technology Governance, Risk, Controls and Assurance Practices (2023)**
- **RBI Guidelines on Information Security, Electronic Banking, Technology Risk Management and Cyber Frauds**
- **CERT-In Directions dated 28-April-2022** (6-hour mandatory reporting)
- **RBI Incident Reporting Requirements** for Scheduled Commercial Banks, NBFCs, UCBs, Payment System Operators, and other regulated entities

This template is critical because:

- RBI mandates timely reporting of **unusual cyber incidents** within strict timelines
- non-reporting or delayed reporting attracts regulatory penalties and supervisory action
- consistent reporting structure ensures completeness, traceability, and audit defensibility
- BFSI incidents often involve customer data, financial impact, and service disruption requiring structured disclosure
- MSSP-managed BFSI clients require tenant-scoped RBI-compliant reports
- CERT-In parallel reporting must be tracked alongside RBI submissions

This template ensures:

- consistent minimum content for every RBI submission
- proper classification of incidents as **Material / Unusual / Reportable**
- linkage to internal incident tickets, evidence, and RCA outcomes
- evidence of regulatory communication for audit trail
- timely submission tracking with acknowledgment references

Reference alignment:
`00_GOVERNANCE/00.1_Policies/IR-Policy-RBI-Alignment.md`
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`

---

# 3. Scope

This template applies to:

| Scenario                           | Reporting Requirement                                         |
| ---------------------------------- | ------------------------------------------------------------- |
| Material/Unusual cyber incident    | Mandatory RBI reporting (within 2–6 hours of detection)       |
| Customer data breach               | Mandatory RBI + CERT-In reporting                             |
| Payment system disruption          | Mandatory RBI reporting                                       |
| Ransomware/Destructive malware     | Mandatory RBI + CERT-In reporting                             |
| ATM/Card/UPI fraud at scale        | Mandatory RBI reporting                                       |
| Critical infrastructure compromise | Mandatory RBI + CERT-In + NCIIPC reporting                    |
| MSSP client (RBI-regulated)        | Report prepared and shared with client; client submits to RBI |

Out of scope:

- non-cyber operational incidents (covered under separate RBI operational risk reporting)
- minor security events without business or customer impact
- false positive alerts

References:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`
`01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/Category-Master-List.md`

---

# 4. Definitions

| Term                     | Definition                                                                                     |
| ------------------------ | ---------------------------------------------------------------------------------------------- |
| Material Cyber Incident  | Cyber incident causing significant impact on operations, customers, data, or financial systems |
| Unusual Cyber Incident   | Any cyber incident outside normal threat activity requiring RBI notification                   |
| Reportable Incident      | Incident meeting RBI/CERT-In criteria for mandatory reporting                                  |
| RE                       | Regulated Entity (bank, NBFC, PSO, etc.) under RBI supervision                                 |
| CERT-In                  | Indian Computer Emergency Response Team                                                        |
| NCIIPC                   | National Critical Information Infrastructure Protection Centre                                 |
| Acknowledgment Reference | Unique reference issued by RBI/CERT-In upon report submission                                  |
| Initial Report           | First mandatory notification (within 2–6 hours)                                                |
| Interim Report           | Updates during incident handling (as required)                                                 |
| Final Report             | Complete post-incident report with RCA and corrective actions                                  |

---

# 5. Roles and Responsibilities

| Role                     | Responsibilities                                                                  |
| ------------------------ | --------------------------------------------------------------------------------- |
| CISO                     | Owns RBI reporting decision; approves report content; primary signatory           |
| Compliance Lead          | Validates regulatory requirements; tracks submission timelines; maintains records |
| SOC Manager              | Provides incident details, technical evidence, and timeline                       |
| IR Team Lead             | Provides technical analysis, scope, RCA, and corrective actions                   |
| Legal Counsel            | Reviews report for legal implications and privilege                               |
| CEO/MD (where required)  | Co-signs material incident reports as per RBI requirement                         |
| MSSP SDM (if applicable) | Coordinates with client for client-managed RBI submission                         |
| Evidence Custodian       | Provides evidence references and CoC details                                      |

---

# 6. RBI Reporting Timelines (Mandatory)

| Report Type                    | Timeline                                             | Submitted To                                     |
| ------------------------------ | ---------------------------------------------------- | ------------------------------------------------ |
| **CERT-In Initial Report**     | Within **6 hours** of noticing incident              | CERT-In (incident@cert-in.org.in)                |
| **RBI Initial Notification**   | Within **2–6 hours** of detection (per circular)     | RBI Cyber Security Cell / Supervisory Department |
| **RBI Interim Report**         | As requested by RBI / significant updates            | RBI                                              |
| **RBI Final Report**           | Within **timeline specified by RBI** post-resolution | RBI                                              |
| **Root Cause Analysis Report** | As mandated by RBI (typically 14–30 days)            | RBI                                              |
| **NCIIPC Report (if CII)**     | Per NCIIPC guidelines                                | NCIIPC                                           |

**Critical:** Timelines start from **incident detection time**, not declaration time.

References:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`

---

# 7. Instructions (Mandatory)

- All timestamps must be in **IST** (RBI standard) with UTC equivalent in brackets.
- Provide **factual information only**; mark unverified items as "Under Investigation".
- Do not include **raw customer data, credentials, or sensitive PII** in the report body; use evidence references.
- Mark sections as **Confirmed / Suspected / Unknown** clearly.
- Engage **Legal Counsel** before submission for material incidents.
- For **MSSP**: prepare tenant-scoped report; share with client for their RBI submission.
- Maintain **acknowledgment references** from RBI/CERT-In as audit evidence.
- All material incident reports require **CISO sign-off** before submission.
- Maintain **submission log** with timestamp, mode, recipient, and acknowledgment.

References:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

# 8. Report Template (Copy/Paste)

## 8.1 Report Metadata (Mandatory)

| Field                             | Value                                     |
| --------------------------------- | ----------------------------------------- |
| Report ID                         | `RBI-RPT-YYYY-####`                       |
| Internal Incident ID / Ticket ID  | `INC-YYYY-####`                           |
| Report Type                       | Initial / Interim / Final / RCA           |
| Regulated Entity Name             | `Bank / NBFC / PSO Name`                  |
| RBI License/Registration Number   | `...`                                     |
| Entity Category                   | SCB / NBFC / UCB / PSO / PA-PG / Other    |
| Reporting Officer                 | `Name / Designation`                      |
| CISO Name                         | `...`                                     |
| CEO/MD (if required)              | `...`                                     |
| Date of Report (IST)              | `YYYY-MM-DD HH:MM IST (UTC: HH:MM)`       |
| Submission Mode                   | Email / RBI Portal / Letter / Online Form |
| RBI Recipient Department          | Cyber Security Cell / DBS / DPSS / Other  |
| CERT-In Reference (if applicable) | `CERT-In Ack #`                           |
| Acknowledgment Reference          | `To be filled post-submission`            |
| Client/Tenant (MSSP only)         | `Client ID / Name`                        |

---

## 8.2 Executive Summary (Mandatory)

- **Nature of Incident:** `Brief description (1–2 lines)`
- **Date & Time of Detection (IST):** `...`
- **Date & Time of Occurrence (IST):** `...` (or "Under Investigation")
- **Current Status:** Detected / Contained / Eradicated / Recovered / Closed
- **Severity Classification:** Material / Non-Material / Unusual
- **Customer Impact:** Yes / No / Under Assessment
- **Financial Impact:** Yes / No / Under Assessment (Estimated: `₹...`)
- **Service Disruption:** Yes / No (Duration: `...`)
- **Data Compromise:** Yes / No / Under Assessment
- **Regulatory Reportability:** RBI / CERT-In / NCIIPC / Other

---

## 8.3 Incident Classification (Mandatory)

| Field                   | Value                                                                |
| ----------------------- | -------------------------------------------------------------------- |
| Incident Category       | Ransomware / Phishing / Data Breach / DDoS / Insider / Fraud / Other |
| Attack Vector           | Email / Web / Network / Insider / Supply Chain / Unknown             |
| Threat Actor (if known) | External / Insider / Unknown / APT (named if attributed)             |
| MITRE ATT&CK Mapping    | `Tactics/Techniques (if available)`                                  |
| Initial Severity        | P1 / P2 / P3 / P4                                                    |
| Final Severity          | P1 / P2 / P3 / P4                                                    |
| Material Incident (Y/N) | Yes / No                                                             |

---

## 8.4 Incident Timeline (Mandatory)

| Event                           | Date & Time (IST) | UTC Equivalent | Source |
| ------------------------------- | ----------------- | -------------- | ------ |
| Incident Occurrence (estimated) |                   |                |        |
| Initial Noticing                |                   |                |        |
| Detection by SOC                |                   |                |        |
| Incident Declared               |                   |                |        |
| CISO Notified                   |                   |                |        |
| Containment Initiated           |                   |                |        |
| Containment Achieved            |                   |                |        |
| CERT-In Reported                |                   |                |        |
| RBI Initial Report Submitted    |                   |                |        |
| Eradication Completed           |                   |                |        |
| Recovery Completed              |                   |                |        |
| Incident Closed                 |                   |                |        |

---

## 8.5 Affected Systems and Scope (Mandatory)

### 8.5.1 Systems Affected

| System/Application | Type | Criticality | Status | Customer-Facing (Y/N) |
| ------------------ | ---- | ----------- | ------ | --------------------- |
|                    |      |             |        |                       |

### 8.5.2 Scope Assessment

| Scope Element                 | Count / Details |
| ----------------------------- | --------------- |
| Hosts/Servers Affected        |                 |
| Endpoints Affected            |                 |
| User Accounts Affected        |                 |
| Privileged Accounts Affected  |                 |
| Customer Accounts Affected    |                 |
| Databases Affected            |                 |
| Network Segments Affected     |                 |
| Cloud Resources Affected      |                 |
| Third-Party Systems Affected  |                 |
| Geographic Locations Affected |                 |

---

## 8.6 Customer Impact Assessment (Mandatory for BFSI)

| Field                                    | Value                                                                                     |
| ---------------------------------------- | ----------------------------------------------------------------------------------------- |
| Customers Affected (Count)               | `Approximate number`                                                                      |
| Customer Categories                      | Retail / Corporate / HNI / All                                                            |
| Nature of Impact                         | Service Unavailable / Data Exposed / Funds Affected / Account Locked / Other              |
| Customer Data Compromised?               | Yes / No / Under Investigation                                                            |
| Type of Data                             | Account Number / KYC / PAN / Aadhaar / Card Data / Credentials / Transaction Data / Other |
| Customer Notification Required?          | Yes / No                                                                                  |
| Customer Notification Status             | Pending / In Progress / Completed                                                         |
| Customer Grievance Mechanism Activated   | Yes / No                                                                                  |
| Helpline/Communication Channel Activated | Yes / No                                                                                  |

---

## 8.7 Financial Impact Assessment (Mandatory)

| Field                             | Value                        |
| --------------------------------- | ---------------------------- |
| Direct Financial Loss             | `₹... (or Under Assessment)` |
| Unauthorized Transactions         | `Count: ... / Value: ₹...`   |
| Funds Recovered                   | `₹...`                       |
| Customer Compensation (Estimated) | `₹...`                       |
| Operational Cost of Response      | `₹...`                       |
| Regulatory Penalty Exposure       | `Under Assessment`           |
| Insurance Claim Filed             | Yes / No                     |
| Insurance Coverage Applicable     | Yes / No                     |

---

## 8.8 Service Availability Impact (Mandatory)

| Service          | Downtime Start (IST) | Downtime End (IST) | Total Duration | Customers Affected |
| ---------------- | -------------------- | ------------------ | -------------- | ------------------ |
| Internet Banking |                      |                    |                |                    |
| Mobile Banking   |                      |                    |                |                    |
| ATM Network      |                      |                    |                |                    |
| UPI              |                      |                    |                |                    |
| Card Services    |                      |                    |                |                    |
| Core Banking     |                      |                    |                |                    |
| Payment Gateway  |                      |                    |                |                    |
| Other            |                      |                    |                |                    |

---

## 8.9 Technical Analysis (Mandatory)

### 8.9.1 Attack Description

- **How attack occurred (confirmed):** `...`
- **Entry point/initial access:** `...`
- **Lateral movement (if any):** `...`
- **Persistence mechanisms:** `...`
- **Data exfiltration (if any):** `...`
- **Payload/malware details:** `...`

### 8.9.2 Indicators of Compromise (IOCs)

| IOC Type           | Value (Sanitized/Defanged) | Source | Notes |
| ------------------ | -------------------------- | ------ | ----- |
| IP Address         |                            |        |       |
| Domain             |                            |        |       |
| File Hash (SHA256) |                            |        |       |
| Email Sender       |                            |        |       |
| URL                |                            |        |       |

### 8.9.3 Vulnerabilities Exploited

| CVE / Vulnerability | System Affected | Patch Available (Y/N) | Patch Status |
| ------------------- | --------------- | --------------------- | ------------ |
|                     |                 |                       |              |

---

## 8.10 Containment, Eradication & Recovery (Mandatory)

### 8.10.1 Containment Actions

| Action | Target | Authorized By | Time (IST) | Outcome |
| ------ | ------ | ------------- | ---------- | ------- |
|        |        |               |            |         |

### 8.10.2 Eradication Actions

| Action | Scope | Owner | Time (IST) | Outcome |
| ------ | ----- | ----- | ---------- | ------- |
|        |       |       |            |         |

### 8.10.3 Recovery Actions

| Action | System | Owner | Time (IST) | Validation |
| ------ | ------ | ----- | ---------- | ---------- |
|        |        |       |            |            |

### 8.10.4 Post-Recovery Validation

- Monitoring period: `...`
- Validation criteria met: Yes / No
- Residual risk: `...`

---

## 8.11 Root Cause Analysis (Mandatory for Final Report)

| Field                       | Value                   |
| --------------------------- | ----------------------- |
| Root Cause (Primary)        | `...`                   |
| Contributing Factors        | `...`                   |
| Control Failures Identified | `...`                   |
| Detection Gap (if any)      | `...`                   |
| Response Gap (if any)       | `...`                   |
| RCA Status                  | Completed / In Progress |
| Detailed RCA Reference      | `RCA document ID/path`  |

Reference:
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`

---

## 8.12 Corrective and Preventive Actions (Mandatory)

| Action | Category                            | Owner | Target Date | Status | Tracking Ref |
| ------ | ----------------------------------- | ----- | ----------- | ------ | ------------ |
|        | Preventive / Detective / Corrective |       |             |        |              |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`

---

## 8.13 Regulatory Notifications and Communications (Mandatory)

| Authority/Stakeholder                      | Notified (Y/N) | Date & Time (IST) | Mode | Acknowledgment Ref |
| ------------------------------------------ | -------------- | ----------------- | ---- | ------------------ |
| RBI Cyber Security Cell                    |                |                   |      |                    |
| RBI Supervisory Department (DBS/DNBS/DPSS) |                |                   |      |                    |
| CERT-In                                    |                |                   |      |                    |
| NCIIPC (if CII)                            |                |                   |      |                    |
| IDRBT (if applicable)                      |                |                   |      |                    |
| NPCI (if UPI/payment)                      |                |                   |      |                    |
| Other Regulators                           |                |                   |      |                    |
| Law Enforcement                            |                |                   |      |                    |
| Customers                                  |                |                   |      |                    |
| Media (if disclosed)                       |                |                   |      |                    |
| Board / Audit Committee                    |                |                   |      |                    |

---

## 8.14 Evidence Inventory (Mandatory)

| Evidence Type       | Reference ID / Path | Hash (SHA256 if applicable) | CoC Maintained (Y/N) |
| ------------------- | ------------------- | --------------------------- | -------------------- |
| SIEM Logs           |                     |                             |                      |
| EDR Telemetry       |                     |                             |                      |
| Network Logs / PCAP |                     |                             |                      |
| Firewall Logs       |                     |                             |                      |
| Application Logs    |                     |                             |                      |
| Database Logs       |                     |                             |                      |
| Disk/Memory Images  |                     |                             |                      |
| Malware Samples     |                     |                             |                      |
| Email Evidence      |                     |                             |                      |
| CoC Records         |                     |                             |                      |

References:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/`

---

## 8.15 Lessons Learned (Mandatory for Final Report)

- **What went well:** `...`
- **What did not go well:** `...`
- **Key learnings:** `...`
- **Process improvements identified:** `...`
- **Technology improvements identified:** `...`
- **Training/awareness gaps:** `...`

Reference:
`08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`

---

## 8.16 Declaration and Sign-Off (Mandatory)

We hereby declare that the information provided in this report is true and accurate to the best of our knowledge as of the date of submission. Updates will be provided as additional information becomes available.

| Role                              | Name | Designation | Signature | Date (IST) |
| --------------------------------- | ---- | ----------- | --------- | ---------- |
| Reporting Officer                 |      |             |           |            |
| CISO                              |      |             |           |            |
| Compliance Head                   |      |             |           |            |
| CEO / MD (for Material Incidents) |      |             |           |            |

---

# 9. Submission Tracking (Mandatory)

| Submission # | Report Type | Submitted Date (IST) | Submitted By | Mode | Recipient | Acknowledgment Ref | Remarks |
| ------------ | ----------- | -------------------- | ------------ | ---- | --------- | ------------------ | ------- |
| 1            | Initial     |                      |              |      |           |                    |         |
| 2            | Interim     |                      |              |      |           |                    |         |
| 3            | Final       |                      |              |      |           |                    |         |
| 4            | RCA         |                      |              |      |           |                    |         |

---

# 10. MSSP Considerations (If Applicable)

For RBI-regulated MSSP clients:

- MSSP **does not directly report to RBI**; client (Regulated Entity) is the reporting authority.
- MSSP prepares **tenant-scoped report** in this format and shares securely with client.
- Client validates, customizes, and submits to RBI under their entity name.
- MSSP maintains evidence in **tenant-segregated** storage.
- MSSP provides supporting evidence for **client's RBI audit/inspection**.
- No cross-client information shall be included in any report.
- MSSP SLA must define **report turnaround time** (e.g., draft within 2 hours of detection).
- Client-specific RBI reporting requirements must be documented in client onboarding.

References:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Onboarding-Checklist.md`
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 11. Quality Checklist (Pre-Submission)

Before submitting to RBI, verify:

- [ ] All mandatory sections completed
- [ ] All timestamps in IST with UTC equivalent
- [ ] Customer impact assessment completed
- [ ] Financial impact assessment completed
- [ ] Evidence references provided (no raw sensitive data)
- [ ] Legal Counsel review completed
- [ ] CISO sign-off obtained
- [ ] CEO/MD sign-off obtained (for material incidents)
- [ ] CERT-In parallel report submitted (if applicable)
- [ ] Acknowledgment references captured
- [ ] Submission logged in tracking register
- [ ] Internal stakeholders notified of submission
- [ ] Copy filed in audit evidence repository
- [ ] MSSP: tenant scoping verified (no cross-client data)

---

# 12. Related Documents

| Document                       | Path                                                                                            |
| ------------------------------ | ----------------------------------------------------------------------------------------------- |
| IR Policy – RBI Alignment      | `00_GOVERNANCE/00.1_Policies/IR-Policy-RBI-Alignment.md`                                        |
| RBI Incident Reporting SOP     | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`   |
| CERT-In Reporting SOP          | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`        |
| Legal Counsel Engagement SOP   | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Regulatory Body Contacts       | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Regulatory-Body-Contacts.md`            |
| Final Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`                          |
| ISO 27001 Incident Log         | `07_REPORTING/07.4_Regulatory-Reports/ISO27001-Incident-Log.md`                                 |
| NIST Incident Report Template  | `07_REPORTING/07.4_Regulatory-Reports/NIST-Incident-Report-Template.md`                         |
| Audit Evidence Package         | `07_REPORTING/07.4_Regulatory-Reports/Audit-Evidence-Package.md`                                |
| RCA Template                   | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`                                     |
| Lessons Learned Template       | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`                             |
| Evidence Storage Policy        | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`             |
| CoC Digital Evidence           | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`                |

---

# 13. Revision History

| Version | Date        | Author                 | Changes         |
| ------- | ----------- | ---------------------- | --------------- |
| 1.0     | 30-May-2026 | CISO / Compliance Lead | Initial version |

---

# 14. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**
