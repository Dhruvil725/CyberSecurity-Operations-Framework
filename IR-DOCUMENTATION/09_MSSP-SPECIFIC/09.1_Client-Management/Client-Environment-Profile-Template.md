# Client Environment Profile Template (MSSP)

---

# 1. Document Control

| Field          | Value                                                     |
| -------------- | --------------------------------------------------------- |
| Document Name  | Template – Client Environment Profile                     |
| Document ID    | MSSP-CM-001                                               |
| Version        | 1.0                                                       |
| Effective Date | 30-May-2026                                               |
| Owner          | MSSP Service Delivery Manager (SDM) / SOC Manager         |
| Approved By    | CISO                                                      |
| Classification | Confidential – Client Restricted                          |
| Review Cycle   | Quarterly (or upon significant client environment change) |

---

# 2. Purpose

This template provides the standardized **Client Environment Profile** format used by the MSSP to document, maintain, and operationalize knowledge about each client's IT and security environment.

A comprehensive client environment profile is critical because:

- accurate environment knowledge is the foundation of effective monitoring, detection, and response
- the SOC must understand client context to correctly triage and prioritize alerts
- incident response requires immediate access to environment specifics (assets, contacts, escalation paths)
- false positive reduction depends on understanding client baseline and legitimate activity
- regulatory reporting (RBI, CERT-In) requires accurate client entity information
- NIST CSF Identify (ID.AM) function mandates asset management as foundational
- ISO 27001 Annex A.5.9 requires inventory of information and other associated assets
- onboarding new SOC analysts requires structured client environment knowledge
- audit and compliance reviews require evidence of client knowledge maintenance
- multi-tenant operations require strict client-specific documentation segregation
- contractual SLAs depend on accurate scope and asset inventory

This template ensures:

- consistent client profile structure across the MSSP portfolio
- complete coverage of technical, operational, and contractual aspects
- defined ownership for profile maintenance
- audit-ready evidence of client environment knowledge
- linkage to client onboarding, asset registers, IR contacts, and playbooks
- support for client-specific playbook customization
- foundation for client-specific detection tuning and threat intelligence

Reference alignment:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Onboarding-Checklist.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 3. Scope

This template applies to:

| Scope                   | Coverage                                                   |
| ----------------------- | ---------------------------------------------------------- |
| All MSSP clients        | Mandatory profile per client                               |
| Client environments     | On-premises, cloud, hybrid, multi-cloud                    |
| Client business context | Industry, geography, regulatory scope                      |
| Monitored assets        | Servers, endpoints, network, cloud, identity, applications |
| Security tools          | Client-owned and MSSP-deployed                             |
| Operational scope       | 24x7 / business hours / co-managed                         |
| Service scope           | Monitoring only / Full MDR / Co-managed SOC                |
| Compliance scope        | Industry regulations applicable to client                  |

Out of scope:

- Detailed asset inventory (maintained in `Client-Asset-Register-Template.xlsx`)
- Detailed playbook customization (maintained in client-specific playbook folder)
- Incident records (maintained in ticketing system)
- Detailed network diagrams (maintained as client-controlled artifacts, referenced here)

---

# 4. Definitions

| Term                | Definition                                                                |
| ------------------- | ------------------------------------------------------------------------- |
| Client Profile      | Comprehensive documentation of client environment and operational context |
| MSSP                | Managed Security Service Provider                                         |
| SDM                 | Service Delivery Manager – primary client relationship owner              |
| Co-Managed SOC      | Shared responsibility model between MSSP and client SOC                   |
| Crown Jewels        | Critical assets/data identified by client as highest priority             |
| Tenant              | Isolated client environment within MSSP multi-tenant architecture         |
| RACI                | Responsibility/Accountability/Consulted/Informed matrix                   |
| RTO                 | Recovery Time Objective                                                   |
| RPO                 | Recovery Point Objective                                                  |
| In-Scope Assets     | Assets covered by MSSP monitoring per contract                            |
| Out-of-Scope Assets | Assets explicitly excluded from MSSP monitoring                           |
| BAU                 | Business as Usual                                                         |

---

# 5. Roles and Responsibilities

| Role                   | Responsibilities                                         |
| ---------------------- | -------------------------------------------------------- |
| MSSP SDM               | Owns client profile; ensures accuracy; quarterly review  |
| MSSP Onboarding Lead   | Creates initial profile during onboarding                |
| SOC Manager            | Validates profile completeness; approves changes         |
| L1/L2/L3 Analysts      | Reference profile during operations; report inaccuracies |
| Detection Engineer     | Uses profile for client-specific detection tuning        |
| Threat Intel Analyst   | Uses profile to assess client-specific threat relevance  |
| Compliance Lead        | Validates regulatory scope accuracy                      |
| Client Primary Contact | Validates profile accuracy; approves significant changes |
| Client Security Lead   | Provides technical environment details                   |
| Client IT Operations   | Provides infrastructure details                          |

---

# 6. Profile Maintenance Principles (Mandatory)

| Principle              | Requirement                                                  |
| ---------------------- | ------------------------------------------------------------ |
| Single source of truth | This document is the authoritative client profile            |
| Tenant segregation     | Strict separation from other client profiles                 |
| Confidentiality        | Treat as Client Restricted; never share across clients       |
| Currency               | Updated within 7 days of significant change                  |
| Validated              | Client-validated annually at minimum                         |
| Versioned              | All changes version-controlled                               |
| Accessible             | Available to authorized SOC personnel only                   |
| Referenced             | Links to detailed artifacts (asset register, contacts, etc.) |
| Audit-ready            | Maintains audit trail of changes                             |

---

# 7. Client Environment Profile Template (Copy/Paste)

## 7.1 Client Identification (Mandatory)

| Field                                 | Value                                                         |
| ------------------------------------- | ------------------------------------------------------------- |
| Client ID (MSSP Internal)             | `CL-####`                                                     |
| Client Legal Name                     |                                                               |
| Client Trading Name (if different)    |                                                               |
| Industry / Sector                     | BFSI / Healthcare / Manufacturing / Government / Tech / Other |
| Sub-Industry                          | e.g., Private Bank / NBFC / PSO / Insurance                   |
| Client Size                           | Employees / Revenue (range)                                   |
| Headquarters Location                 |                                                               |
| Primary Geography of Operations       | India / APAC / Global                                         |
| Regulatory Registration Numbers       | RBI / SEBI / IRDAI / Other                                    |
| Public Company?                       | Yes / No (Stock Exchange, Ticker if Yes)                      |
| Parent Company (if applicable)        |                                                               |
| Subsidiaries in Scope (if applicable) |                                                               |
| Profile Created Date (UTC)            |                                                               |
| Profile Last Updated (UTC)            |                                                               |
| Profile Next Review Date (UTC)        |                                                               |
| Profile Owner (MSSP)                  |                                                               |
| Profile Approver (Client)             |                                                               |

---

## 7.2 Service Engagement (Mandatory)

| Field                            | Value                                                   |
| -------------------------------- | ------------------------------------------------------- |
| Contract Start Date              |                                                         |
| Contract End Date / Renewal Date |                                                         |
| Service Tier                     | Monitoring Only / MDR / Full SOC / Co-Managed           |
| Coverage Hours                   | 24x7 / Business Hours / Custom                          |
| Coverage Days                    | 7 days / 5 days / Custom                                |
| MSSP SDM (Primary)               |                                                         |
| MSSP SDM (Backup)                |                                                         |
| Client Service Tier              | Bronze / Silver / Gold / Platinum (per MSSP tier model) |
| Service Inclusions               | Reference contract clause                               |
| Service Exclusions               | Reference contract clause                               |
| Out-of-Scope Services            | Reference contract clause                               |
| Custom Service Agreements        |                                                         |

References:
`00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`

---

## 7.3 Business Context (Mandatory)

### 7.3.1 Business Overview

- **Brief business description:** `1–3 sentence summary of what client does`
- **Critical business processes:** `List top 3–5 critical business processes`
- **Peak business periods:** `e.g., Month-end, Year-end, Festival season, Tax season`
- **Off-hours sensitivity:** `Critical business activity outside standard hours`
- **Customer-facing services:** `Online services that impact end customers`

### 7.3.2 Crown Jewels (Mandatory)

> Client-identified critical assets and data.

| #   | Asset / Data | Description | Criticality              | Compromise Impact |
| --- | ------------ | ----------- | ------------------------ | ----------------- |
| 1   |              |             | Critical / High / Medium |                   |
| 2   |              |             |                          |                   |
| 3   |              |             |                          |                   |

### 7.3.3 Business Impact Tiers

| Tier              | Examples                                               | Max Tolerable Downtime |
| ----------------- | ------------------------------------------------------ | ---------------------- |
| Tier 1 (Critical) | Core banking, payment gateway, customer-facing portals | < 15 min               |
| Tier 2 (High)     | Internal applications, email                           | < 4 hours              |
| Tier 3 (Medium)   | Development environments, internal tools               | < 24 hours             |
| Tier 4 (Low)      | Non-production, test systems                           | < 7 days               |

---

## 7.4 Regulatory and Compliance Scope (Mandatory)

| Regulation / Standard              | Applicable (Y/N) | Compliance Status             | Notes |
| ---------------------------------- | ---------------- | ----------------------------- | ----- |
| RBI Cyber Security Framework       | Y/N              |                               |       |
| RBI Master Direction IT Governance | Y/N              |                               |       |
| CERT-In Directions (2022)          | Y/N              |                               |       |
| ISO/IEC 27001                      | Y/N              | Certified / In Progress / N/A |       |
| PCI-DSS                            | Y/N              | Level 1-4 / N/A               |       |
| SEBI Cybersecurity Framework       | Y/N              |                               |       |
| IRDAI Information & Cyber Security | Y/N              |                               |       |
| DPDP Act (India)                   | Y/N              |                               |       |
| GDPR (if EU exposure)              | Y/N              |                               |       |
| HIPAA (if healthcare)              | Y/N              |                               |       |
| SOC 2                              | Y/N              | Type I / Type II / N/A        |       |
| NIST CSF                           | Y/N              | Alignment level               |       |
| NCIIPC (if CII)                    | Y/N              |                               |       |
| Other                              |                  |                               |       |

### 7.4.1 Mandatory Reporting Obligations

| Authority       | Reporting Trigger             | Timeline       | Reporting Responsibility |
| --------------- | ----------------------------- | -------------- | ------------------------ |
| RBI             | Material cyber incident       | 2–6 hours      | Client (MSSP supports)   |
| CERT-In         | Cyber incident per directions | 6 hours        | Client (MSSP supports)   |
| NCIIPC (if CII) | Per guidelines                | Per guidelines | Client                   |
| Other           |                               |                |                          |

References:
`07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 7.5 Technical Environment Overview (Mandatory)

### 7.5.1 Environment Type

| Aspect                     | Details                                     |
| -------------------------- | ------------------------------------------- |
| On-Premises                | Yes / No (Locations, scale)                 |
| Cloud – AWS                | Yes / No (Accounts, regions)                |
| Cloud – Azure              | Yes / No (Tenants, subscriptions, regions)  |
| Cloud – GCP                | Yes / No (Projects, regions)                |
| Cloud – Other              | OCI / IBM Cloud / Alibaba / Other           |
| SaaS Major                 | M365 / Google Workspace / Salesforce / etc. |
| Hybrid Architecture        | Description                                 |
| Co-location / Data Centers | Locations                                   |

### 7.5.2 Scale Indicators (High-Level)

| Asset Category                          | Approximate Count | In MSSP Scope      |
| --------------------------------------- | ----------------- | ------------------ |
| Servers (physical + virtual)            |                   | Yes / No / Partial |
| Endpoints (workstations + laptops)      |                   |                    |
| Mobile devices                          |                   |                    |
| Network devices (FW, switches, routers) |                   |                    |
| Cloud workloads (VMs, containers)       |                   |                    |
| Cloud accounts/subscriptions            |                   |                    |
| Applications (production)               |                   |                    |
| Databases (production)                  |                   |                    |
| Identity stores (AD, Entra ID, Okta)    |                   |                    |
| Users (employees + contractors)         |                   |                    |
| External-facing assets                  |                   |                    |

Reference:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Asset-Register-Template.xlsx`

### 7.5.3 Network Topology Summary

- **Internet edge:** `ISPs, edge providers, CDN, WAF`
- **DMZ design:** `Description`
- **Internal segmentation:** `VLAN/zone strategy`
- **Site-to-site connectivity:** `MPLS / SD-WAN / VPN`
- **Remote access:** `VPN / ZTNA / VDI`
- **Cloud connectivity:** `Direct Connect / ExpressRoute / Interconnect`
- **Network diagram reference:** `[Path to client-controlled diagram]`

---

## 7.6 Security Tools and Telemetry (Mandatory)

### 7.6.1 Security Tools Inventory

| Tool Category                | Tool / Vendor | Ownership              | MSSP Access | Telemetry to MSSP |
| ---------------------------- | ------------- | ---------------------- | ----------- | ----------------- |
| SIEM                         |               | Client / MSSP / Shared | Yes / No    | Yes / No          |
| EDR / XDR                    |               |                        |             |                   |
| NDR / IDS / IPS              |               |                        |             |                   |
| Firewall (perimeter)         |               |                        |             |                   |
| Firewall (internal)          |               |                        |             |                   |
| Web Application Firewall     |               |                        |             |                   |
| DDoS Protection              |               |                        |             |                   |
| Email Security               |               |                        |             |                   |
| Web Proxy / SWG              |               |                        |             |                   |
| CASB                         |               |                        |             |                   |
| DLP (Endpoint)               |               |                        |             |                   |
| DLP (Network)                |               |                        |             |                   |
| IAM / SSO                    |               |                        |             |                   |
| PAM                          |               |                        |             |                   |
| MFA                          |               |                        |             |                   |
| Vulnerability Management     |               |                        |             |                   |
| Patch Management             |               |                        |             |                   |
| Threat Intelligence Platform |               |                        |             |                   |
| SOAR                         |               |                        |             |                   |
| CSPM / CNAPP                 |               |                        |             |                   |
| Container Security           |               |                        |             |                   |
| Backup / Recovery            |               |                        |             |                   |
| Encryption / KMS             |               |                        |             |                   |

### 7.6.2 Log Sources to MSSP SIEM

| Log Source               | Status                    | Coverage % | EPS (avg) | Notes |
| ------------------------ | ------------------------- | ---------- | --------- | ----- |
| Windows Servers          | Onboarded / Pending / N/A |            |           |       |
| Linux Servers            |                           |            |           |       |
| Endpoints (EDR)          |                           |            |           |       |
| Firewall (perimeter)     |                           |            |           |       |
| Firewall (internal)      |                           |            |           |       |
| Web Application Firewall |                           |            |           |       |
| Proxy / SWG              |                           |            |           |       |
| Email Gateway            |                           |            |           |       |
| Active Directory         |                           |            |           |       |
| Entra ID / Azure AD      |                           |            |           |       |
| O365 / M365              |                           |            |           |       |
| AWS CloudTrail           |                           |            |           |       |
| Azure Activity Logs      |                           |            |           |       |
| GCP Audit Logs           |                           |            |           |       |
| DNS Logs                 |                           |            |           |       |
| VPN Logs                 |                           |            |           |       |
| DLP Events               |                           |            |           |       |
| Database Audit Logs      |                           |            |           |       |
| Application Logs         |                           |            |           |       |
| Container/Kubernetes     |                           |            |           |       |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Integration-Map.md`

### 7.6.3 EDR Coverage

| Aspect                 | Details               |
| ---------------------- | --------------------- |
| EDR Vendor             |                       |
| Total endpoints        |                       |
| Endpoints with EDR     |                       |
| Coverage %             |                       |
| Gap analysis           |                       |
| Containment authority  | MSSP / Client / Joint |
| Auto-response enabled? | Yes / No              |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Deployment-Coverage-Check.md`

---

## 7.7 Identity and Access Architecture (Mandatory)

| Aspect                      | Details                       |
| --------------------------- | ----------------------------- |
| Primary IdP                 | AD / Entra ID / Okta / Other  |
| Secondary IdP               |                               |
| SSO Coverage                | % of applications             |
| MFA Coverage                | % of users                    |
| Privileged Accounts         | Count                         |
| PAM Solution                |                               |
| Service Accounts            | Count + management approach   |
| Federation Partners         |                               |
| Guest/External Access       | Approach                      |
| Conditional Access Policies | Implemented Y/N               |
| Zero Trust Maturity         | Initial / Developing / Mature |

---

## 7.8 Critical Applications and Services (Mandatory)

| Application      | Type | Hosting         | Tier   | Business Owner | Technical Owner |
| ---------------- | ---- | --------------- | ------ | -------------- | --------------- |
| Core Banking     |      | On-prem / Cloud | Tier 1 |                |                 |
| Internet Banking |      |                 |        |                |                 |
| Mobile Banking   |      |                 |        |                |                 |
| Payment Gateway  |      |                 |        |                |                 |
| ERP              |      |                 |        |                |                 |
| CRM              |      |                 |        |                |                 |
| Email            |      |                 |        |                |                 |
| Other            |      |                 |        |                |                 |

---

## 7.9 Data Sensitivity and Classification (Mandatory)

| Data Type                    | Volume (Est.) | Storage Locations | Sensitivity  |
| ---------------------------- | ------------- | ----------------- | ------------ |
| Customer PII                 |               |                   | Restricted   |
| Financial / Transaction Data |               |                   | Restricted   |
| Card Data (PCI)              |               |                   | Restricted   |
| Health Records (PHI)         |               |                   | Restricted   |
| Employee Data                |               |                   | Confidential |
| Intellectual Property        |               |                   | Confidential |
| Operational Data             |               |                   | Internal     |
| Public Data                  |               |                   | Public       |

---

## 7.10 Threat Landscape (Mandatory)

### 7.10.1 Industry-Specific Threats

| Threat Type         | Relevance        | Notes |
| ------------------- | ---------------- | ----- |
| Ransomware          | High / Med / Low |       |
| Phishing / BEC      |                  |       |
| Insider Threat      |                  |       |
| Supply Chain Attack |                  |       |
| Nation-State (APT)  |                  |       |
| Hacktivism          |                  |       |
| DDoS                |                  |       |
| Card Fraud (BFSI)   |                  |       |
| Other               |                  |       |

### 7.10.2 Relevant Threat Actors

| Actor | Aliases | Relevance        | Profile Reference |
| ----- | ------- | ---------------- | ----------------- |
|       |         | High / Med / Low | `TAP-YYYY-####`   |

Reference:
`08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md`

### 7.10.3 Past Incidents (High-Level Summary)

| Date | Incident Category | Severity | Outcome | Reference       |
| ---- | ----------------- | -------- | ------- | --------------- |
|      |                   |          |         | `INC-YYYY-####` |

---

## 7.11 Operational Context (Mandatory)

### 7.11.1 Maintenance Windows

| Window               | Day/Time | Scope | Notification Required |
| -------------------- | -------- | ----- | --------------------- |
| Standard maintenance |          |       |                       |
| Emergency change     |          |       |                       |
| Patching cycle       |          |       |                       |

### 7.11.2 Change Management

- **Change management process:** `ITIL / Custom / None`
- **Change approval body:** `CAB / Manager / Automated`
- **Change notification to MSSP:** `Yes / No (Method)`
- **MSSP awareness window:** `Notice lead time`

### 7.11.3 Known False Positive Patterns

| Pattern | Source | Reason | Tuning Approach |
| ------- | ------ | ------ | --------------- |
|         |        |        |                 |

References:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md`

### 7.11.4 Approved Software / Tools (Whitelist Context)

| Category      | Approved Tools | Notes |
| ------------- | -------------- | ----- |
| Remote Access |                |       |
| Admin Tools   |                |       |
| Scripting     |                |       |
| File Sharing  |                |       |
| Other         |                |       |

---

## 7.12 Escalation and Communication (Mandatory)

> Detailed contacts maintained in `Client-IR-Contacts.md`. Summary below.

### 7.12.1 Primary Contacts

| Role                      | Name | Available Hours |
| ------------------------- | ---- | --------------- |
| Primary Business Contact  |      |                 |
| Primary Technical Contact |      |                 |
| Primary Security Contact  |      |                 |
| 24x7 On-Call (P1)         |      |                 |
| Executive Sponsor         |      |                 |

### 7.12.2 Communication Preferences

| Topic            | Preferred Channel      | Backup Channel |
| ---------------- | ---------------------- | -------------- |
| P1 Notifications | Phone + Email + Bridge |                |
| P2 Notifications | Email + Phone          |                |
| Routine Updates  | Email                  |                |
| Reports          | Email + Portal         |                |
| Bridge calls     | Tool / Number          |                |

References:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`

---

## 7.13 SLA Summary (Mandatory)

| Metric                                | Target | Notes |
| ------------------------------------- | ------ | ----- |
| P1 Acknowledgement                    |        |       |
| P1 Response                           |        |       |
| P2 Acknowledgement                    |        |       |
| P2 Response                           |        |       |
| P3 Acknowledgement                    |        |       |
| P3 Response                           |        |       |
| Incident reporting (initial)          |        |       |
| Incident reporting (final)            |        |       |
| Monthly report delivery               |        |       |
| RBI reporting support (if applicable) |        |       |

References:
`00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`
`00_GOVERNANCE/00.4_SLA-and-SLO/SLA-Breach-Escalation-Procedure.md`

---

## 7.14 RACI – MSSP vs Client (Mandatory)

| Activity                         | MSSP           | Client   |
| -------------------------------- | -------------- | -------- |
| Monitoring (24x7)                | R              |          |
| Triage                           | R              |          |
| Investigation (L1/L2)            | R              |          |
| Investigation (L3)               | R / Joint      | Joint    |
| Containment Authority (network)  | Joint / Client | A        |
| Containment Authority (endpoint) | R              | A        |
| Containment Authority (cloud)    | Joint          | A        |
| Eradication                      | Joint          | R        |
| Recovery                         | Support        | R        |
| Forensics                        | R              | Approver |
| Communication to End Users       | Support        | R        |
| Regulatory Reporting             | Support        | R        |
| Customer Notification            | Support        | R        |
| Media Communication              | N/A            | R        |
| Law Enforcement Engagement       | Support        | R        |

References:
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`

---

## 7.15 Containment Authority Matrix (Mandatory)

| Action                       | Severity | MSSP Authority | Pre-Approved? | Approval Required From |
| ---------------------------- | -------- | -------------- | ------------- | ---------------------- |
| Endpoint isolation (EDR)     | P1       | Yes            | Yes           |                        |
| Endpoint isolation (EDR)     | P2       | Yes            | Yes           |                        |
| Disable user account         | P1       | Yes / No       | Yes / No      |                        |
| Disable user account         | P2       |                |               |                        |
| Block IP at firewall         | Any      | Yes / No       | Yes / No      |                        |
| Block domain                 | Any      | Yes / No       | Yes / No      |                        |
| Block email sender           | Any      | Yes / No       | Yes / No      |                        |
| Disable cloud account        | P1       |                |               |                        |
| Reset privileged credentials | P1       |                |               |                        |
| Take system offline          | P1       |                |               |                        |
| Network segment isolation    | P1       |                |               |                        |

References:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 7.16 Backup and Recovery Context (Mandatory)

| Aspect                   | Details                   |
| ------------------------ | ------------------------- |
| Backup Solution          |                           |
| Backup Storage Locations | On-prem / Cloud / Offsite |
| Air-Gapped Backups       | Yes / No                  |
| Immutable Backups        | Yes / No                  |
| Backup Frequency         | Critical / Standard       |
| RTO (Critical Systems)   |                           |
| RPO (Critical Systems)   |                           |
| Disaster Recovery Site   |                           |
| DR Test Frequency        |                           |
| Last DR Test Date        |                           |
| Recovery Documentation   | Available Y/N             |

---

## 7.17 Third-Party and Supply Chain (Mandatory)

| Third Party | Service Type                  | Access Level | Risk Rating      |
| ----------- | ----------------------------- | ------------ | ---------------- |
|             | SaaS / IT Outsourcer / Vendor |              | High / Med / Low |

### 7.17.1 Critical Third-Party Dependencies

| Dependency         | Provider | Impact if Compromised |
| ------------------ | -------- | --------------------- |
| Payment processing |          |                       |
| Cloud hosting      |          |                       |
| Identity provider  |          |                       |
| Email service      |          |                       |
| Other              |          |                       |

---

## 7.18 Reporting Requirements (Mandatory)

| Report Type                  | Frequency | Recipient        | Format         | Delivery Method |
| ---------------------------- | --------- | ---------------- | -------------- | --------------- |
| Daily incident summary       | Daily     | Client SOC       | Email / Portal |                 |
| Weekly summary               | Weekly    | Client Mgmt      | PDF            |                 |
| Monthly comprehensive        | Monthly   | Client Mgmt      | PDF            |                 |
| Quarterly executive briefing | Quarterly | CISO / Executive | Presentation   |                 |
| SLA compliance report        | Monthly   | Client Mgmt      | PDF            |                 |
| Threat intelligence brief    | Quarterly | Client Security  | PDF            |                 |
| Custom reports               | As agreed |                  |                |                 |

References:
`07_REPORTING/07.3_MSSP-Client-Reports/`

---

## 7.19 Client-Specific Customizations (Mandatory)

### 7.19.1 Custom Playbooks

| Playbook | Path                                                                 |
| -------- | -------------------------------------------------------------------- |
|          | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/` |

### 7.19.2 Custom Detection Rules

| Rule Name | Purpose | Reference |
| --------- | ------- | --------- |
|           |         |           |

### 7.19.3 Custom Use Cases

| Use Case | Purpose | Reference |
| -------- | ------- | --------- |
|          |         |           |

References:
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`

---

## 7.20 Known Constraints and Limitations (Mandatory)

| Constraint | Impact | Workaround |
| ---------- | ------ | ---------- |
|            |        |            |

Examples:

- Log source not yet onboarded
- Tool licensing limitation
- Network bandwidth constraint
- Regulatory restriction
- Time zone considerations
- Language requirements

---

## 7.21 Evidence and Data Handling (Mandatory)

| Aspect                        | Details                                       |
| ----------------------------- | --------------------------------------------- |
| Evidence storage location     | MSSP secure storage / Client storage / Hybrid |
| Evidence retention period     |                                               |
| Chain of Custody requirements |                                               |
| Data residency requirements   | India / Specific country / No restriction     |
| Cross-border data transfer    | Permitted Y/N                                 |
| Encryption requirements       |                                               |
| Client right to inspect       | Yes / No                                      |
| Data destruction process      |                                               |

References:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md`
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

## 7.22 Joint Initiatives and Exercises (Mandatory)

| Initiative                | Frequency | Last Conducted | Next Scheduled |
| ------------------------- | --------- | -------------- | -------------- |
| Tabletop exercise         |           |                |                |
| Red team / Purple team    |           |                |                |
| Joint incident drill      |           |                |                |
| Security review meeting   |           |                |                |
| Quarterly business review |           |                |                |
| Annual strategy session   |           |                |                |

References:
`10_TRAINING-AND-EXERCISES/`

---

# 8. Profile Lifecycle (Mandatory)

| Phase                         | Activities                           | Owner           | Frequency                  |
| ----------------------------- | ------------------------------------ | --------------- | -------------------------- |
| **Creation**                  | Initial profile during onboarding    | Onboarding Lead | At onboarding              |
| **Validation**                | Client validation of accuracy        | SDM + Client    | Within 30 days of creation |
| **Maintenance**               | Updates as environment changes       | SDM             | Continuous                 |
| **Quarterly Review**          | Comprehensive review with client     | SDM             | Quarterly                  |
| **Annual Refresh**            | Full re-validation                   | SDM + Client    | Annually                   |
| **Significant Change Update** | Update within 7 days of major change | SDM             | As needed                  |
| **Offboarding**               | Archive profile per retention        | SDM             | At contract end            |

---

# 9. Triggers for Profile Update (Mandatory)

Update the profile within 7 days when:

- New asset categories added to scope
- Significant infrastructure changes (cloud migration, data center change)
- New security tool deployment
- Change in regulatory scope
- Mergers/acquisitions affecting environment
- Change in business processes
- Change in client contacts (primary roles)
- SLA changes
- Service tier changes
- New compliance obligations
- Significant incident with environment learning
- Threat landscape changes affecting client
- Geographic expansion
- New subsidiary addition

---

# 10. Quality Checklist (Per Profile)

Before approving a client profile:

- [ ] All mandatory sections completed
- [ ] Client validation obtained
- [ ] Service tier and SLAs documented
- [ ] Regulatory scope accurately captured
- [ ] Crown jewels identified
- [ ] Asset register linked
- [ ] Security tools inventoried
- [ ] Log sources documented with coverage
- [ ] EDR coverage assessed
- [ ] Critical applications listed
- [ ] Threat landscape relevant to client
- [ ] Escalation contacts current
- [ ] Containment authority matrix completed
- [ ] RACI matrix completed
- [ ] Backup/recovery context captured
- [ ] Reporting requirements documented
- [ ] Constraints documented
- [ ] Evidence handling defined
- [ ] Custom playbooks/rules referenced
- [ ] Profile owner and approver assigned
- [ ] Next review date set
- [ ] Tenant segregation verified
- [ ] Classification marked as Client Restricted

---

# 11. Profile Access Control (Mandatory)

| Audience                                 | Access Level                                |
| ---------------------------------------- | ------------------------------------------- |
| Assigned SDM                             | Full read/write                             |
| Assigned SOC team (per client)           | Full read                                   |
| MSSP SOC Manager                         | Full read/write                             |
| MSSP CISO                                | Full read                                   |
| Onboarding team (during onboarding only) | Full read/write                             |
| Other clients                            | NO ACCESS                                   |
| Other MSSP SOC teams (not assigned)      | NO ACCESS                                   |
| Third parties                            | NO ACCESS (unless explicit client approval) |
| Auditors                                 | Read only with client approval              |

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 12. Review Process (Mandatory)

## 12.1 Quarterly Review

SDM + Client review:

- Environment changes since last review
- Asset register updates
- Contact updates
- SLA performance
- Reporting needs
- Custom playbook needs

## 12.2 Annual Review

SDM + SOC Manager + Client review:

- Full profile re-validation
- Strategic alignment
- Service tier assessment
- Coverage gap analysis
- Joint roadmap planning

## 12.3 Triggered Review

Immediate review when triggers occur (see Section 9).

---

# 13. Integration with Other Processes

| Process                | Integration Point                   |
| ---------------------- | ----------------------------------- |
| Onboarding             | Profile created during onboarding   |
| Asset Management       | Profile references asset register   |
| Contact Management     | Profile references IR contacts      |
| Playbook Customization | Profile drives custom playbooks     |
| Detection Engineering  | Profile informs detection tuning    |
| Threat Intelligence    | Profile informs threat relevance    |
| Incident Response      | Profile referenced during IR        |
| Reporting              | Profile drives report content       |
| Offboarding            | Profile archived during offboarding |

---

# 14. Related Documents

| Document                          | Path                                                                                      |
| --------------------------------- | ----------------------------------------------------------------------------------------- |
| Client Onboarding Checklist       | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Onboarding-Checklist.md`                  |
| Client IR Contacts                | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`                           |
| Client Asset Register Template    | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Asset-Register-Template.xlsx`             |
| Client Offboarding Checklist      | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Offboarding-Checklist.md`                 |
| Client-Specific Playbook Guide    | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`   |
| Client Data Segregation Policy    | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`         |
| MSSP-Client SLA Template          | `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`                              |
| MSSP-Client Responsibility Matrix | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`      |
| Internal-to-MSSP Escalation       | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`    |
| MSSP Monthly Client Report        | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Monthly-Client-Report.md`                     |
| MSSP Client Evidence Handling     | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md` |
| SIEM Integration Map              | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Integration-Map.md`                               |
| EDR Deployment Coverage Check     | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Deployment-Coverage-Check.md`                       |
| IRT Containment Authority Matrix  | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`      |
| RBI Mandatory Report Template     | `07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`                   |

---

# 15. Revision History

| Version | Date        | Author                 | Changes         |
| ------- | ----------- | ---------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP SDM / SOC Manager | Initial version |

---

# 16. Approval

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
