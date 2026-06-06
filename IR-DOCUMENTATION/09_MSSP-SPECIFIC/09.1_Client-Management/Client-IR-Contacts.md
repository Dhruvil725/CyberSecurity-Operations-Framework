# Client IR Contacts Directory (MSSP)

---

# 1. Document Control

| Field          | Value                                             |
| -------------- | ------------------------------------------------- |
| Document Name  | Directory – Client IR Contacts                    |
| Document ID    | MSSP-CM-002                                       |
| Version        | 1.0                                               |
| Effective Date | 30-May-2026                                       |
| Owner          | MSSP Service Delivery Manager (SDM) / SOC Manager |
| Approved By    | CISO                                              |
| Classification | Confidential – Client Restricted                  |
| Review Cycle   | Quarterly (or upon contact change notification)   |

---

# 2. Purpose

This document provides the standardized **Client IR Contacts Directory** template used by the MSSP to maintain authoritative, up-to-date contact information for each client's incident response, escalation, and operational coordination needs.

A formal client IR contacts directory is critical because:

- timely escalation depends on accurate, current contact information
- P1/P2 incidents require immediate reach to the right people within minutes
- incorrect contact data delays response and breaches SLAs
- regulatory reporting (RBI, CERT-In) requires verified client representative contacts
- NIST CSF Respond (RS.CO) function requires structured communication coordination
- ISO 27001 Annex A.5.5 requires defined contact with authorities and special interest groups
- RBI Cyber Security Framework expects defined escalation paths
- audit and compliance reviews require evidence of contact maintenance
- multi-tenant operations require strict client-specific contact segregation
- contact directories support 24x7 coverage and on-call rotations
- legal/regulatory engagements require verified executive sponsors
- bridge call coordination depends on accurate participant lists

This directory ensures:

- consistent contact structure across the MSSP client portfolio
- complete coverage of operational, escalation, executive, and regulatory contacts
- defined ownership for contact maintenance
- audit-ready evidence of contact directory currency
- linkage to escalation matrix, environment profile, and onboarding
- support for 24x7 coverage with primary/backup designations
- handling of out-of-office and emergency overrides

Reference alignment:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Onboarding-Checklist.md`
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`

---

# 3. Scope

This directory covers:

| Contact Category             | Coverage                                     |
| ---------------------------- | -------------------------------------------- |
| Primary operational contacts | Day-to-day SOC liaison                       |
| Escalation contacts          | L2/L3 escalation per severity                |
| Executive sponsors           | CISO, CIO, business sponsor                  |
| 24x7 on-call contacts        | After-hours escalation                       |
| Technical specialists        | Cloud, network, identity, application owners |
| Regulatory representatives   | Compliance, legal, reporting officers        |
| HR/Legal contacts            | Insider threat, legal hold, employee actions |
| Third-party coordinators     | Vendor, IR retainer, forensics partner       |
| Crisis management contacts   | Crisis communications, executive war room    |
| Geographic-specific contacts | Multi-region client coverage                 |

Out of scope:

- General employee contact directories (maintained by client)
- Detailed RACI assignments (maintained in `Client-Environment-Profile-Template.md`)
- Internal MSSP contacts (maintained in `Internal-Contacts-Master.md`)
- Generic vendor contacts (maintained in `Vendor-Contacts.md`)

---

# 4. Definitions

| Term                | Definition                                                                   |
| ------------------- | ---------------------------------------------------------------------------- |
| Primary Contact     | First person to be contacted for a given category                            |
| Backup Contact      | Second person to be contacted if primary unavailable                         |
| Escalation Contact  | Person reached when issue cannot be resolved at lower level                  |
| On-Call Contact     | Person designated for after-hours coverage in rotation                       |
| Executive Sponsor   | Senior executive accountable for the engagement                              |
| Authorized Approver | Person with authority to approve specific actions (containment, comms, etc.) |
| RACI Role           | Responsibility/Accountability/Consulted/Informed designation                 |
| OOO                 | Out of Office                                                                |
| Coverage Window     | Hours during which a contact is available                                    |
| Reach Time SLA      | Maximum time to successfully reach a contact                                 |

---

# 5. Roles and Responsibilities

| Role                      | Responsibilities                                            |
| ------------------------- | ----------------------------------------------------------- |
| MSSP SDM                  | Owns client contacts directory; quarterly validation        |
| MSSP Onboarding Lead      | Captures initial contacts during onboarding                 |
| SOC Manager               | Approves directory; validates completeness                  |
| L1/L2/L3 Analysts         | Reference directory during incidents; report changes        |
| SOC Lead                  | Validates contacts during incident escalation               |
| Client Primary Contact    | Maintains accuracy on client side; notifies MSSP of changes |
| Client HR / IT Operations | Provides timely notification of contact changes             |
| Compliance Lead           | Validates regulatory contact accuracy                       |

---

# 6. Contact Maintenance Principles (Mandatory)

| Principle              | Requirement                                            |
| ---------------------- | ------------------------------------------------------ |
| Single source of truth | This directory is authoritative for client IR contacts |
| Tenant segregation     | Strict separation from other client directories        |
| Confidentiality        | Treat as Client Restricted; never share across clients |
| Currency               | Updated within 48 hours of change notification         |
| Verified               | Annually validated via test communication              |
| Primary + Backup       | Every category must have primary AND backup            |
| 24x7 coverage          | After-hours coverage explicitly documented             |
| Multi-channel          | Email + Phone + Mobile minimum                         |
| Versioned              | All changes tracked with date and reason               |
| Audit-ready            | Change history maintained                              |

---

# 7. Contact Directory Template (Copy/Paste)

## 7.1 Directory Metadata (Mandatory)

| Field                      | Value                             |
| -------------------------- | --------------------------------- |
| Client ID                  | `CL-####`                         |
| Client Name                |                                   |
| Directory Version          | v1.0 / v1.1 / etc.                |
| Date Created (UTC)         |                                   |
| Last Updated (UTC)         |                                   |
| Last Validated (UTC)       | (test communication verification) |
| Next Review Date (UTC)     |                                   |
| Directory Owner (MSSP SDM) |                                   |
| Client Approver            |                                   |
| Total Contacts             | Count                             |
| Classification             | Confidential – Client Restricted  |

---

## 7.2 Primary Operational Contacts (Mandatory)

> Day-to-day SOC liaison; first point of contact for routine matters.

### 7.2.1 Primary Operational Contact

| Field             | Value                                            |
| ----------------- | ------------------------------------------------ |
| Role              | Primary Operational Contact (Client SOC Liaison) |
| Name              |                                                  |
| Designation       |                                                  |
| Department        |                                                  |
| Email             |                                                  |
| Office Phone      |                                                  |
| Mobile            |                                                  |
| Secondary Mobile  |                                                  |
| Alternate Email   |                                                  |
| Preferred Channel | Email / Phone / Both                             |
| Coverage Hours    | e.g., 9 AM – 6 PM IST, Mon–Fri                   |
| Time Zone         | IST                                              |
| Languages         | English / Hindi / Other                          |
| Notes             |                                                  |

### 7.2.2 Backup Operational Contact

| Field             | Value                      |
| ----------------- | -------------------------- |
| Role              | Backup Operational Contact |
| Name              |                            |
| Designation       |                            |
| Email             |                            |
| Office Phone      |                            |
| Mobile            |                            |
| Preferred Channel |                            |
| Coverage Hours    |                            |
| Notes             |                            |

---

## 7.3 24x7 On-Call Contacts (Mandatory)

> After-hours coverage for P1/P2 incidents.

### 7.3.1 Primary 24x7 On-Call

| Field                     | Value                               |
| ------------------------- | ----------------------------------- |
| Coverage                  | 24x7 / Specific hours               |
| Primary On-Call Name      | (or rotation name)                  |
| On-Call Phone (24x7)      | Dedicated number                    |
| On-Call Email             |                                     |
| On-Call Schedule          | Rotation reference / Calendar link  |
| Reach Time SLA            | Max 15 minutes                      |
| Escalation if Unreachable | Section 7.3.2 contact within 15 min |

### 7.3.2 Backup 24x7 On-Call

| Field                     | Value                         |
| ------------------------- | ----------------------------- |
| Backup On-Call Name       |                               |
| Backup Phone (24x7)       |                               |
| Backup Email              |                               |
| Reach Time SLA            | Max 15 minutes                |
| Escalation if Unreachable | Section 7.5 Executive Sponsor |

### 7.3.3 On-Call Rotation Calendar (Reference)

| Week | Primary On-Call | Backup On-Call |
| ---- | --------------- | -------------- |
|      |                 |                |

**Note:** Rotation calendar maintained at: `[Client portal link / Document path]`

---

## 7.4 Escalation Contacts (Mandatory)

### 7.4.1 L2 Escalation (Technical)

| Field          | Value                           |
| -------------- | ------------------------------- |
| Role           | Client Security Operations Lead |
| Name           |                                 |
| Designation    |                                 |
| Email          |                                 |
| Mobile         |                                 |
| Reach Time SLA | Max 30 minutes                  |
| Authority      |                                 |

### 7.4.2 L3 Escalation (Management)

| Field          | Value                              |
| -------------- | ---------------------------------- |
| Role           | Client Security Manager / Head SOC |
| Name           |                                    |
| Designation    |                                    |
| Email          |                                    |
| Mobile         |                                    |
| Reach Time SLA | Max 1 hour                         |
| Authority      |                                    |

### 7.4.3 IR Team Lead (Client Side, if applicable)

| Field          | Value |
| -------------- | ----- |
| Name           |       |
| Designation    |       |
| Email          |       |
| Mobile         |       |
| Reach Time SLA |       |

---

## 7.5 Executive Sponsors (Mandatory)

### 7.5.1 CISO

| Field                    | Value                                             |
| ------------------------ | ------------------------------------------------- |
| Name                     |                                                   |
| Designation              |                                                   |
| Email                    |                                                   |
| Office Phone             |                                                   |
| Mobile                   |                                                   |
| Executive Assistant Name |                                                   |
| EA Email                 |                                                   |
| EA Phone                 |                                                   |
| Reach Time SLA           | Max 1 hour (P1)                                   |
| Approvals Authority      | Major incident decisions / external communication |

### 7.5.2 CIO / IT Head

| Field               | Value |
| ------------------- | ----- |
| Name                |       |
| Designation         |       |
| Email               |       |
| Mobile              |       |
| Reach Time SLA      |       |
| Approvals Authority |       |

### 7.5.3 Business Sponsor / COO

| Field              | Value                                       |
| ------------------ | ------------------------------------------- |
| Name               |                                             |
| Designation        |                                             |
| Email              |                                             |
| Mobile             |                                             |
| Reach Time SLA     |                                             |
| Engagement Trigger | P1 with business impact / Material incident |

### 7.5.4 CEO / MD (P1 / Material Incidents Only)

| Field              | Value                                    |
| ------------------ | ---------------------------------------- |
| Name               |                                          |
| Designation        |                                          |
| Engagement Method  | Through CISO / Direct                    |
| Engagement Trigger | Material incident / Regulatory reporting |
| Reach Method       |                                          |

---

## 7.6 Technical Specialists (Mandatory)

### 7.6.1 Network Operations

| Field           | Value                               |
| --------------- | ----------------------------------- |
| Primary Contact |                                     |
| Backup Contact  |                                     |
| Email           |                                     |
| Phone           |                                     |
| Coverage Hours  |                                     |
| Authority       | Firewall changes, network isolation |

### 7.6.2 Active Directory / Identity

| Field           | Value                                               |
| --------------- | --------------------------------------------------- |
| Primary Contact |                                                     |
| Backup Contact  |                                                     |
| Email           |                                                     |
| Phone           |                                                     |
| Coverage Hours  |                                                     |
| Authority       | Account disable, password reset, privileged actions |

### 7.6.3 Cloud Operations (AWS)

| Field           | Value                              |
| --------------- | ---------------------------------- |
| Primary Contact |                                    |
| Backup Contact  |                                    |
| Email           |                                    |
| Phone           |                                    |
| Coverage Hours  |                                    |
| Authority       | Cloud account actions, IAM changes |

### 7.6.4 Cloud Operations (Azure)

| Field           | Value |
| --------------- | ----- |
| Primary Contact |       |
| Backup Contact  |       |
| Email           |       |
| Phone           |       |
| Coverage Hours  |       |
| Authority       |       |

### 7.6.5 Cloud Operations (GCP)

| Field           | Value |
| --------------- | ----- |
| Primary Contact |       |
| Backup Contact  |       |
| Email           |       |
| Phone           |       |
| Coverage Hours  |       |
| Authority       |       |

### 7.6.6 Endpoint Operations

| Field           | Value                                 |
| --------------- | ------------------------------------- |
| Primary Contact |                                       |
| Backup Contact  |                                       |
| Email           |                                       |
| Phone           |                                       |
| Coverage Hours  |                                       |
| Authority       | Endpoint actions, software deployment |

### 7.6.7 Email / Messaging Operations

| Field           | Value                         |
| --------------- | ----------------------------- |
| Primary Contact |                               |
| Backup Contact  |                               |
| Email           |                               |
| Phone           |                               |
| Coverage Hours  |                               |
| Authority       | Email blocks, account actions |

### 7.6.8 Database Operations

| Field           | Value                             |
| --------------- | --------------------------------- |
| Primary Contact |                                   |
| Backup Contact  |                                   |
| Email           |                                   |
| Phone           |                                   |
| Coverage Hours  |                                   |
| Authority       | Database actions, query execution |

### 7.6.9 Application Owners (Critical Apps)

| Application      | Primary Owner | Backup | Email | Phone |
| ---------------- | ------------- | ------ | ----- | ----- |
| Core Banking     |               |        |       |       |
| Internet Banking |               |        |       |       |
| Mobile Banking   |               |        |       |       |
| Payment Gateway  |               |        |       |       |
| ERP              |               |        |       |       |
| CRM              |               |        |       |       |
| Email            |               |        |       |       |
| Other            |               |        |       |       |

---

## 7.7 Compliance and Legal Contacts (Mandatory)

### 7.7.1 Compliance Officer

| Field          | Value                                   |
| -------------- | --------------------------------------- |
| Name           |                                         |
| Designation    | Compliance Officer / Head of Compliance |
| Email          |                                         |
| Phone          |                                         |
| Reach Time SLA |                                         |
| Authority      | Regulatory reporting decisions          |

### 7.7.2 Regulatory Reporting Officer (RBI / SEBI / IRDAI)

| Field           | Value                                    |
| --------------- | ---------------------------------------- |
| Name            |                                          |
| Designation     |                                          |
| Email           |                                          |
| Phone           |                                          |
| Regulatory Body | RBI / SEBI / IRDAI / Other               |
| Authority       | RBI/CERT-In/regulatory report submission |

References:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`

### 7.7.3 Data Protection Officer (DPO)

| Field              | Value                                    |
| ------------------ | ---------------------------------------- |
| Name               |                                          |
| Designation        | DPO                                      |
| Email              |                                          |
| Phone              |                                          |
| Engagement Trigger | Personal data breach / DPDP Act incident |

### 7.7.4 General Counsel / Legal Head

| Field              | Value                                                  |
| ------------------ | ------------------------------------------------------ |
| Name               |                                                        |
| Designation        |                                                        |
| Email              |                                                        |
| Phone              |                                                        |
| Engagement Trigger | Legal hold / Litigation risk / External counsel needed |

### 7.7.5 External Legal Counsel (if retained)

| Field              | Value                            |
| ------------------ | -------------------------------- |
| Firm Name          |                                  |
| Primary Attorney   |                                  |
| Email              |                                  |
| Phone              |                                  |
| Engagement Trigger | Major breach / Regulatory action |

References:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

---

## 7.8 HR Contacts (Mandatory for Insider Threat)

### 7.8.1 HR Business Partner

| Field              | Value                                      |
| ------------------ | ------------------------------------------ |
| Name               |                                            |
| Designation        |                                            |
| Email              |                                            |
| Phone              |                                            |
| Engagement Trigger | Insider threat investigation               |
| Authority          | Employee actions (suspension, termination) |

### 7.8.2 HR Head / CHRO

| Field              | Value                  |
| ------------------ | ---------------------- |
| Name               |                        |
| Designation        |                        |
| Email              |                        |
| Phone              |                        |
| Engagement Trigger | Major insider incident |

References:
`02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md`

---

## 7.9 Communications Contacts (Mandatory for Major Incidents)

### 7.9.1 Internal Communications

| Field              | Value                                           |
| ------------------ | ----------------------------------------------- |
| Name               |                                                 |
| Designation        |                                                 |
| Email              |                                                 |
| Phone              |                                                 |
| Engagement Trigger | Major incident requiring employee communication |

### 7.9.2 External Communications / PR

| Field              | Value                                   |
| ------------------ | --------------------------------------- |
| Name               |                                         |
| Designation        |                                         |
| Email              |                                         |
| Phone              |                                         |
| Engagement Trigger | Media inquiry / Public statement needed |

### 7.9.3 Customer Communications

| Field              | Value                          |
| ------------------ | ------------------------------ |
| Name               |                                |
| Designation        |                                |
| Email              |                                |
| Phone              |                                |
| Engagement Trigger | Customer notification required |

---

## 7.10 Crisis Management Team (Mandatory for P1)

| Role                     | Name | Email | Phone | Engagement Trigger |
| ------------------------ | ---- | ----- | ----- | ------------------ |
| Crisis Lead              |      |       |       | P1 declared        |
| Communications Lead      |      |       |       |                    |
| Technical Lead           |      |       |       |                    |
| Business Continuity Lead |      |       |       |                    |
| Legal Lead               |      |       |       |                    |
| Executive Sponsor        |      |       |       |                    |

---

## 7.11 Third-Party Coordinators (If Applicable)

### 7.11.1 IR Retainer (External Forensics/IR Firm)

| Field                | Value                           |
| -------------------- | ------------------------------- |
| Firm Name            |                                 |
| Account Manager      |                                 |
| Email                |                                 |
| Phone                |                                 |
| 24x7 Hotline         |                                 |
| Engagement Authority | Who can engage / Approval limit |

References:
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Third-Party-IR-Retainer-Contacts.md`

### 7.11.2 Cyber Insurance Carrier

| Field              | Value                            |
| ------------------ | -------------------------------- |
| Insurance Provider |                                  |
| Policy Number      |                                  |
| Claims Contact     |                                  |
| Email              |                                  |
| Phone              |                                  |
| 24x7 Hotline       |                                  |
| Engagement Trigger | Incident likely to trigger claim |

### 7.11.3 Key Technology Vendors (Critical)

| Vendor          | Product | Account Manager | Support Hotline | Severity 1 Contact |
| --------------- | ------- | --------------- | --------------- | ------------------ |
| SIEM Vendor     |         |                 |                 |                    |
| EDR Vendor      |         |                 |                 |                    |
| Firewall Vendor |         |                 |                 |                    |
| Cloud Provider  |         |                 |                 |                    |
| Other           |         |                 |                 |                    |

### 7.11.4 Managed Service Providers (Client's Other Vendors)

| Vendor | Service         | Contact | Phone | Notes |
| ------ | --------------- | ------- | ----- | ----- |
|        | Network MSP     |         |       |       |
|        | Cloud MSP       |         |       |       |
|        | Application MSP |         |       |       |

---

## 7.12 Regulatory Body Contacts (Mandatory if Applicable)

> Authoritative regulator contacts for client.

### 7.12.1 RBI (if applicable)

| Field                                           | Value                   |
| ----------------------------------------------- | ----------------------- |
| Cyber Security Cell Email                       | csc@rbi.org.in          |
| Department of Banking Supervision (DBS) Contact |                         |
| Client's RBI Supervisory Contact                |                         |
| Submission Method                               | Email / Portal / Letter |

### 7.12.2 CERT-In

| Field                    | Value                      |
| ------------------------ | -------------------------- |
| Incident Reporting Email | incident@cert-in.org.in    |
| Helpline                 | +91-1800-11-4949           |
| Portal                   | https://www.cert-in.org.in |

### 7.12.3 NCIIPC (if CII)

| Field           | Value |
| --------------- | ----- |
| Reporting Email |       |
| Helpline        |       |

### 7.12.4 Other Regulators

| Regulator | Contact | Email | Phone |
| --------- | ------- | ----- | ----- |
| SEBI      |         |       |       |
| IRDAI     |         |       |       |
| TRAI      |         |       |       |

References:
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Regulatory-Body-Contacts.md`

---

## 7.13 Law Enforcement Contacts (If Applicable)

| Field                    | Value                         |
| ------------------------ | ----------------------------- |
| Local Police Cyber Cell  |                               |
| State Cyber Crime        |                               |
| CBI Cyber Crime          |                               |
| FIR Coordinator (Client) |                               |
| Engagement Authority     | Through Legal / CISO approval |

References:
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Law-Enforcement-Contacts.md`

---

## 7.14 Geographic / Site-Specific Contacts (If Applicable)

> For clients with multiple geographic locations.

### 7.14.1 Site: `[Site Name]`

| Field                           | Value |
| ------------------------------- | ----- |
| Site Manager                    |       |
| Site IT Lead                    |       |
| Site Security Lead              |       |
| Email                           |       |
| Phone                           |       |
| Local Languages                 |       |
| Local Time Zone                 |       |
| Local Regulatory Considerations |       |

> Repeat for each site as needed.

---

# 8. Contact Quick Reference Card (Mandatory)

> Single-page summary for quick reference during incidents.

## 8.1 P1 Incident – Immediate Contacts (Reach within 15 min)

| Priority | Role                        | Name | Phone |
| -------- | --------------------------- | ---- | ----- |
| 1        | 24x7 On-Call (Primary)      |      |       |
| 2        | 24x7 On-Call (Backup)       |      |       |
| 3        | Primary Operational Contact |      |       |
| 4        | CISO                        |      |       |

## 8.2 P2 Incident – Standard Escalation

| Priority | Role                        | Name | Phone |
| -------- | --------------------------- | ---- | ----- |
| 1        | Primary Operational Contact |      |       |
| 2        | Backup Operational Contact  |      |       |
| 3        | L2 Escalation               |      |       |

## 8.3 P3/P4 – Routine Contact

| Priority | Role                        | Name | Email |
| -------- | --------------------------- | ---- | ----- |
| 1        | Primary Operational Contact |      |       |

## 8.4 Special Scenarios

| Scenario              | Contact                              |
| --------------------- | ------------------------------------ |
| Insider Threat        | HR + Legal                           |
| Data Breach (PII)     | DPO + Legal                          |
| Ransomware            | CISO + Cyber Insurance + IR Retainer |
| Customer Impact       | Customer Comms + Business Sponsor    |
| Media Inquiry         | External Comms + CISO                |
| Regulatory Reportable | Compliance Officer + CISO            |
| Legal Hold Needed     | General Counsel                      |

---

# 9. Out-of-Office and Overrides (Mandatory)

## 9.1 OOO Notification Protocol

When a primary or backup contact is OOO:

- Client notifies MSSP SDM in advance (minimum 48 hours)
- Coverage assignment documented (temporary backup)
- Directory updated with OOO note and coverage assignment
- Restored upon return

## 9.2 Emergency Override

In extreme emergencies (P1 with critical business impact and unreachable primary contacts):

- Escalate to CISO directly
- Escalate to Executive Sponsor
- Document override and rationale
- Post-incident review of escalation path

References:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`

---

# 10. Contact Verification (Mandatory)

## 10.1 Annual Verification

Conducted annually by SDM:

| Contact Category      | Verification Method        | Frequency |
| --------------------- | -------------------------- | --------- |
| Primary Operational   | Email + phone confirmation | Annually  |
| 24x7 On-Call          | Test call (announced)      | Quarterly |
| Executive Sponsors    | Email confirmation         | Annually  |
| Regulatory Contacts   | Email confirmation         | Annually  |
| Technical Specialists | Email confirmation         | Annually  |

## 10.2 Verification Record

| Verification Date | Contact Category | Method | Result                           | Verifier |
| ----------------- | ---------------- | ------ | -------------------------------- | -------- |
|                   |                  |        | Verified / Updated / Unreachable |          |

## 10.3 Quarterly Spot-Check

SDM conducts random spot-checks (5 contacts per quarter):

- Verify email reachable
- Verify phone reachable
- Verify role still accurate

---

# 11. Contact Change Management (Mandatory)

## 11.1 Change Notification Requirements

Client must notify MSSP within 48 hours of any:

- Role changes affecting IR responsibilities
- Department transfers
- Resignations / Terminations
- Contact information changes (email, phone)
- Coverage hour changes
- Authority/approval limit changes

## 11.2 Change Process

| Step | Action                        | Owner  | SLA             |
| ---- | ----------------------------- | ------ | --------------- |
| 1    | Client notifies SDM of change | Client | Within 48 hours |
| 2    | SDM acknowledges receipt      | SDM    | Within 24 hours |
| 3    | SDM updates directory         | SDM    | Within 48 hours |
| 4    | Directory version incremented | SDM    | At update       |
| 5    | Confirmation to client        | SDM    | At update       |
| 6    | SOC team notified             | SDM    | At update       |

## 11.3 Change Log Template

| Date (UTC) | Change Type | Old Value | New Value | Notified By | Updated By |
| ---------- | --------------------------------------- | --------- | --------- | ----------- | ---------- |
|            | Add / Update / Remove                   |           |           |             |            |

---

# 12. Quality Checklist (Per Directory)

Before approving a client contacts directory:

- [ ] Directory metadata complete
- [ ] Primary operational contact with primary + backup
- [ ] 24x7 on-call coverage documented with rotation
- [ ] L2 and L3 escalation contacts defined
- [ ] CISO contact and approval authority documented
- [ ] CIO / Business Sponsor contacts captured
- [ ] All technical specialist roles populated
- [ ] Application owners for critical apps listed
- [ ] Compliance Officer with regulatory reporting authority
- [ ] Legal contact (internal + external if retained)
- [ ] HR contacts for insider threat
- [ ] Communications contacts (internal / PR / customer)
- [ ] Crisis management team for P1 defined
- [ ] IR retainer details (if applicable)
- [ ] Cyber insurance carrier details
- [ ] Key technology vendor support contacts
- [ ] Regulatory body contacts populated
- [ ] Quick reference card completed
- [ ] OOO and emergency override defined
- [ ] Annual verification completed
- [ ] Change log maintained
- [ ] Client approval obtained
- [ ] Tenant segregation verified
- [ ] Classification marked Client Restricted

---

# 13. Directory Access Control (Mandatory)

| Audience                            | Access Level                   |
| ----------------------------------- | ------------------------------ |
| Assigned SDM                        | Full read/write                |
| Assigned SOC team (per client)      | Full read                      |
| SOC Lead (on-shift)                 | Full read                      |
| MSSP SOC Manager                    | Full read/write                |
| MSSP CISO                           | Full read                      |
| Other clients                       | NO ACCESS                      |
| Other MSSP SOC teams (not assigned) | NO ACCESS                      |
| Third parties                       | NO ACCESS                      |
| Auditors                            | Read only with client approval |

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 14. Review Process (Mandatory)

## 14.1 Monthly Review

SDM reviews:

- Recent change notifications
- OOO entries and coverage
- Pending verifications

## 14.2 Quarterly Review

SDM + SOC Manager review:

- Quarterly spot-check completion
- Test call results (on-call)
- Change log completeness
- Directory currency

## 14.3 Annual Review

SDM + Client review:

- Full directory re-validation
- All contacts confirmed
- Authority/approval limits validated
- Coverage gaps identified

---

# 15. MSSP Considerations (Mandatory)

All client contact directories must:

- Be **tenant-scoped** with no cross-client information
- Be **access-controlled** to assigned SDM + SOC team only
- Be **stored** in client-specific secure repository
- Use **client-specific identifiers** consistently
- Maintain **data residency** per client requirements
- Support **client right to inspect** their own directory
- Be **destroyed** upon offboarding per retention policy

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Offboarding-Checklist.md`

---

# 16. Integration with Other Processes

| Process                    | Integration Point                           |
| -------------------------- | ------------------------------------------- |
| Onboarding                 | Initial directory created during onboarding |
| Client Environment Profile | Contacts referenced in profile              |
| Incident Response          | Directory accessed during all incidents     |
| Escalation                 | Escalation matrix references contacts       |
| Regulatory Reporting       | Regulatory officer contact used             |
| Crisis Management          | Crisis team contacts activated              |
| Tabletop Exercises         | Contacts validated through exercises        |
| Quarterly Business Review  | Contact accuracy reviewed                   |
| Offboarding                | Directory archived per retention            |

---

# 17. Related Documents

| Document                             | Path                                                                                                |
| ------------------------------------ | --------------------------------------------------------------------------------------------------- |
| Client Environment Profile Template  | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`                    |
| Client Onboarding Checklist          | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Onboarding-Checklist.md`                            |
| Client Offboarding Checklist         | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Offboarding-Checklist.md`                           |
| Client Asset Register Template       | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Asset-Register-Template.xlsx`                       |
| Client Data Segregation Policy       | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`                   |
| Internal-to-MSSP Escalation          | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`              |
| Emergency Escalation P1              | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`                  |
| MSSP Client Notification Template    | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md` |
| Bridge Call Agenda Template          | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Bridge-Call-Agenda-Template.md`       |
| Regulatory Body Contacts             | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Regulatory-Body-Contacts.md`                |
| Law Enforcement Contacts             | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Law-Enforcement-Contacts.md`                |
| Third-Party IR Retainer Contacts     | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Third-Party-IR-Retainer-Contacts.md`        |
| Vendor Contacts                      | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Vendor-Contacts.md`                         |
| RBI Incident Reporting SOP           | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`       |
| CERT-In Reporting SOP                | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`            |
| Legal Counsel Engagement SOP         | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`     |
| MSSP-Client SLA Template             | `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`                                        |
| Insider Threat HR-Legal Coordination | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md`                       |

---

# 18. Revision History

| Version | Date        | Author                 | Changes         |
| ------- | ----------- | ---------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP SDM / SOC Manager | Initial version |

---

# 19. Approval

Approved by (MSSP):

Name: ____________________
Title: ____________________
Date: ____________________

Validated by (Client):

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**
