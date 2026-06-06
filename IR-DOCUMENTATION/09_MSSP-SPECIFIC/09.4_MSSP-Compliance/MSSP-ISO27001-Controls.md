# MSSP ISO/IEC 27001:2022 Controls Alignment

---

# 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | MSSP – ISO/IEC 27001:2022 Controls Alignment                 |
| Document ID    | MSSP-CMP-001                                                 |
| Version        | 1.0                                                          |
| Effective Date | 30-May-2026                                                  |
| Owner          | MSSP Compliance Lead / CISO                                  |
| Approved By    | MSSP CISO                                                    |
| Classification | Confidential – MSSP Internal                                 |
| Review Cycle   | Annually (or upon ISO standard update / certification audit) |

---

# 2. Purpose

This document defines how the MSSP's Incident Response (IR) program and Security Operations Center (SOC) operations align with **ISO/IEC 27001:2022** (Information Security Management System) and **ISO/IEC 27002:2022** (Information Security Controls Guidance) — providing audit-ready evidence of control implementation across the MSSP multi-tenant environment.

A formal ISO 27001 controls alignment document is critical because:

- the MSSP serves multiple regulated clients requiring ISO 27001-certified service providers
- ISO 27001:2022 certification is a contractual requirement in most MSSP MSAs and DPAs
- client procurement, vendor risk assessments, and audits demand demonstrable control mapping
- ISO 27001 Annex A controls (93 controls in 2022 version) must each be evidenced
- the MSSP's multi-tenant architecture creates unique ISO control implementation requirements
- annual surveillance audits and triennial recertification require traceable evidence
- internal ISMS audits depend on mapped control implementations
- nonconformities discovered without mapped controls cause certification risk
- SOC 2, RBI, NIST CSF, and DPDP audits frequently leverage ISO 27001 control mappings
- threat intelligence sharing, tenant segregation, and incident response require ISO-aligned governance
- client audit rights clauses require MSSP to produce control evidence on demand
- MSSP personnel must understand which controls govern their daily operations
- new controls in ISO 27001:2022 (threat intelligence, cloud, ICT readiness, etc.) require explicit mapping
- detection engineering, playbook updates, and lessons learned must feed ISO control improvement
- this alignment is the single source of truth for ISO certification evidence
- without structured alignment, audit findings cascade across regulatory frameworks

This alignment ensures:

- complete mapping of all 93 ISO 27001:2022 Annex A controls to MSSP implementations
- alignment with ISMS clauses 4–10 of the main standard
- evidence references for each control (policies, procedures, logs, reports)
- per-control ownership and review cycles
- multi-tenant specific control considerations documented
- audit-ready evidence package for internal and external audits
- continuous improvement loop tied to control performance
- linkage to NIST CSF, RBI, SOC 2, DPDP, and other framework mappings

**Reference alignment:**

- `00_GOVERNANCE/00.1_Policies/IR-Policy-ISO27001-Alignment.md`
- `00_GOVERNANCE/00.2_Frameworks-Mapping/ISO27001-Annex-A-Mapping.xlsx`
- `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-NIST-Alignment.md`
- `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-Audit-Readiness-Checklist.md`

---

# 3. Scope

This document covers ISO 27001:2022 alignment across all MSSP operations:

| Scope Element                    | Coverage                                  |
| -------------------------------- | ----------------------------------------- |
| ISMS clauses                     | Clauses 4–10 (main standard)              |
| Annex A controls                 | All 93 controls (4 themes)                |
| MSSP SOC operations              | 24x7 monitoring, IR, threat hunting       |
| MSSP multi-tenant infrastructure | All client environments                   |
| MSSP personnel                   | All SOC, IR, compliance, support staff    |
| MSSP technology stack            | SIEM, EDR, SOAR, TI, ticketing, forensics |
| MSSP third parties               | Sub-processors, vendors, contractors      |
| MSSP documentation               | All policies, procedures, playbooks       |
| Client-facing services           | All MSSP service tiers                    |
| Audit evidence                   | All control evidence artifacts            |

Out of scope:

- Client-internal ISO 27001 compliance (client's responsibility)
- ISO 27017 (cloud-specific) detailed mapping (separate document)
- ISO 27018 (PII in cloud) detailed mapping (separate document)
- ISO 27701 (privacy) detailed mapping (separate document)
- Detailed ISMS operating procedures (covered by MSSP ISMS Manual)

---

# 4. Definitions

| Term                             | Definition                                        |
| -------------------------------- | ------------------------------------------------- |
| ISMS                             | Information Security Management System            |
| Annex A                          | ISO 27001:2022 catalog of 93 reference controls   |
| Statement of Applicability (SoA) | Document declaring applicable Annex A controls    |
| Control Owner                    | Person accountable for control implementation     |
| Control Operator                 | Person performing control activities              |
| Evidence                         | Documented artifacts proving control operation    |
| Nonconformity                    | Failure to meet ISO requirement                   |
| Corrective Action                | Action to eliminate cause of nonconformity        |
| Continual Improvement            | Ongoing enhancement of ISMS                       |
| Internal Audit                   | ISMS audit by internal/independent auditor        |
| Surveillance Audit               | Annual external audit by certification body       |
| Recertification Audit            | Triennial full external audit                     |
| Management Review                | Periodic ISMS review by top management            |
| Risk Treatment                   | Process to modify risk                            |
| Multi-Tenant Control             | Control with specific multi-tenant implementation |

---

# 5. Roles and Responsibilities

| Role                            | Responsibilities                                             |
| ------------------------------- | ------------------------------------------------------------ |
| **MSSP CISO**                   | ISMS owner; SoA approval; management review chair            |
| **MSSP Compliance Lead**        | ISO program management; audit coordination; control evidence |
| **MSSP SOC Manager**            | Operational controls; SOC-specific evidence                  |
| **MSSP IT/Platform Lead**       | Technical controls; infrastructure evidence                  |
| **MSSP HR Lead**                | Personnel controls; training; background checks              |
| **MSSP Legal Counsel**          | Legal controls; contracts; regulatory alignment              |
| **MSSP Internal Auditor**       | ISMS internal audits                                         |
| **Control Owners**              | Per-control accountability                                   |
| **Control Operators**           | Daily control execution                                      |
| **All Personnel**               | Adherence to ISMS policies and procedures                    |
| **External Certification Body** | Surveillance and recertification audits                      |

---

# 6. ISO 27001:2022 Structure Overview (Mandatory)

ISO 27001:2022 consists of:

| Section         | Content                                |
| --------------- | -------------------------------------- |
| **Clauses 0–3** | Introduction, scope, references, terms |
| **Clause 4**    | Context of the organization            |
| **Clause 5**    | Leadership                             |
| **Clause 6**    | Planning                               |
| **Clause 7**    | Support                                |
| **Clause 8**    | Operation                              |
| **Clause 9**    | Performance evaluation                 |
| **Clause 10**   | Improvement                            |
| **Annex A**     | 93 reference controls in 4 themes      |

### Annex A Themes (ISO 27001:2022)

| Theme                    | Control Count | Range          |
| ------------------------ | ------------- | -------------- |
| **A.5 – Organizational** | 37            | A.5.1 – A.5.37 |
| **A.6 – People**         | 8             | A.6.1 – A.6.8  |
| **A.7 – Physical**       | 14            | A.7.1 – A.7.14 |
| **A.8 – Technological**  | 34            | A.8.1 – A.8.34 |
| **Total**                | **93**        |                |

---

# 7. ISMS Clauses Alignment (Mandatory)

## 7.1 Clause 4 – Context of the Organization

| Sub-Clause | Requirement                            | MSSP Implementation                                    | Evidence                |
| ---------- | -------------------------------------- | ------------------------------------------------------ | ----------------------- |
| 4.1        | Understanding internal/external issues | Annual context analysis; threat landscape review       | Context Analysis Report |
| 4.2        | Interested parties needs               | Client/regulator/employee requirements register        | Stakeholder Register    |
| 4.3        | ISMS scope                             | Documented scope including MSSP SOC + multi-tenant ops | ISMS Scope Document     |
| 4.4        | ISMS establishment                     | Documented ISMS processes                              | ISMS Manual             |

## 7.2 Clause 5 – Leadership

| Sub-Clause | Requirement                          | MSSP Implementation                                    | Evidence                        |
| ---------- | ------------------------------------ | ------------------------------------------------------ | ------------------------------- |
| 5.1        | Leadership commitment                | CISO-led ISMS; executive sponsorship                   | Management Commitment Statement |
| 5.2        | Policy                               | Information Security Policy approved by top management | InfoSec Policy                  |
| 5.3        | Roles, responsibilities, authorities | RACI Matrix; role definitions                          | RACI Matrix; Role Documents     |

## 7.3 Clause 6 – Planning

| Sub-Clause | Requirement                          | MSSP Implementation         | Evidence                        |
| ---------- | ------------------------------------ | --------------------------- | ------------------------------- |
| 6.1.1      | Risks and opportunities              | Annual ISMS risk assessment | Risk Register                   |
| 6.1.2      | Information security risk assessment | Documented risk methodology | Risk Methodology Doc            |
| 6.1.3      | Information security risk treatment  | Risk treatment plan + SoA   | Risk Treatment Plan; SoA        |
| 6.2        | Information security objectives      | Measurable ISMS objectives  | ISMS Objectives + KPI Dashboard |
| 6.3        | Planning of changes                  | Change management process   | Change Mgmt Procedure           |

## 7.4 Clause 7 – Support

| Sub-Clause | Requirement            | MSSP Implementation                  | Evidence                   |
| ---------- | ---------------------- | ------------------------------------ | -------------------------- |
| 7.1        | Resources              | Budgeted ISMS resources              | Budget; Resource Plan      |
| 7.2        | Competence             | Training & certification program     | Training Records           |
| 7.3        | Awareness              | Security awareness program           | Awareness Records          |
| 7.4        | Communication          | Internal/external communication plan | Communication Plan         |
| 7.5        | Documented information | Document control system              | Document Control Procedure |

## 7.5 Clause 8 – Operation

| Sub-Clause | Requirement                    | MSSP Implementation         | Evidence                  |
| ---------- | ------------------------------ | --------------------------- | ------------------------- |
| 8.1        | Operational planning & control | SOC operating procedures    | SOC SOPs                  |
| 8.2        | Risk assessment (operational)  | Periodic risk reassessments | Risk Reassessment Records |
| 8.3        | Risk treatment (operational)   | Risk treatment execution    | Treatment Action Records  |

## 7.6 Clause 9 – Performance Evaluation

| Sub-Clause | Requirement                                   | MSSP Implementation             | Evidence               |
| ---------- | --------------------------------------------- | ------------------------------- | ---------------------- |
| 9.1        | Monitoring, measurement, analysis, evaluation | KPI tracking; metrics dashboard | Metrics Reports        |
| 9.2        | Internal audit                                | Annual ISMS internal audit      | Audit Reports          |
| 9.3        | Management review                             | Quarterly management review     | Review Meeting Minutes |

## 7.7 Clause 10 – Improvement

| Sub-Clause | Requirement                       | MSSP Implementation           | Evidence             |
| ---------- | --------------------------------- | ----------------------------- | -------------------- |
| 10.1       | Continual improvement             | CAPA program; lessons learned | Improvement Register |
| 10.2       | Nonconformity & corrective action | NCR process                   | NCR Register         |

---

# 8. Annex A.5 – Organizational Controls (37 Controls)

| Control | Title                                                                  | MSSP Implementation                     | Owner              | Evidence                         |
| ------- | ---------------------------------------------------------------------- | --------------------------------------- | ------------------ | -------------------------------- |
| A.5.1   | Policies for information security                                      | InfoSec Policy + sub-policies           | CISO               | IR-Policy-Master.md              |
| A.5.2   | Information security roles and responsibilities                        | RACI Matrix; role definitions           | CISO               | RACI-Matrix-IR.xlsx              |
| A.5.3   | Segregation of duties                                                  | SOC tier separation; PAM controls       | SOC Manager        | Role separation docs             |
| A.5.4   | Management responsibilities                                            | Management review process               | CISO               | Management Review Minutes        |
| A.5.5   | Contact with authorities                                               | Law enforcement / CERT contact register | CISO               | Law-Enforcement-Contacts.md      |
| A.5.6   | Contact with special interest groups                                   | Industry groups; ISAC membership        | Threat Intel Lead  | Membership records               |
| A.5.7   | Threat intelligence                                                    | TI program + platform                   | Threat Intel Lead  | TI-Feed-Management.md            |
| A.5.8   | Information security in project management                             | Project security gate process           | CISO               | Project security checklist       |
| A.5.9   | Inventory of information and other associated assets                   | Asset register                          | IT Lead            | Asset Register                   |
| A.5.10  | Acceptable use of information and other associated assets              | AUP policy                              | HR + IT            | AUP Document                     |
| A.5.11  | Return of assets                                                       | Offboarding checklist                   | HR                 | Offboarding records              |
| A.5.12  | Classification of information                                          | Data classification policy              | CISO               | Data Classification Policy       |
| A.5.13  | Labelling of information                                               | Labelling standards                     | CISO               | Labelling Standards              |
| A.5.14  | Information transfer                                                   | Transfer policy; encryption standards   | CISO               | Transfer Policy                  |
| A.5.15  | Access control                                                         | Access control policy                   | IT Lead            | Access Control Policy            |
| A.5.16  | Identity management                                                    | IAM program                             | IT Lead            | IAM Procedures                   |
| A.5.17  | Authentication information                                             | Credential policy; MFA mandate          | IT Lead            | Credential Policy                |
| A.5.18  | Access rights                                                          | Provisioning/deprovisioning             | IT Lead            | Access Review Records            |
| A.5.19  | Information security in supplier relationships                         | Supplier security policy                | Procurement + CISO | Supplier Security Policy         |
| A.5.20  | Addressing information security within supplier agreements             | Contract clauses                        | Legal              | Contract Templates               |
| A.5.21  | Managing information security in the ICT supply chain                  | Supply chain risk mgmt                  | CISO               | Supply Chain Risk Register       |
| A.5.22  | Monitoring, review and change management of supplier services          | Supplier review cycle                   | Procurement        | Supplier Review Records          |
| A.5.23  | Information security for use of cloud services                         | Cloud security policy                   | CISO               | Cloud Security Policy            |
| A.5.24  | Information security incident management planning and preparation      | IR Policy + Playbooks                   | SOC Manager        | IR-Policy-Master.md; Playbooks   |
| A.5.25  | Assessment and decision on information security events                 | Severity matrix; triage SOPs            | SOC Manager        | Severity-Classification-Guide.md |
| A.5.26  | Response to information security incidents                             | IR Team + Playbooks                     | IR Team Lead       | All Playbooks                    |
| A.5.27  | Learning from information security incidents                           | Lessons Learned program                 | IR Team Lead       | Lessons-Learned-Register.xlsx    |
| A.5.28  | Collection of evidence                                                 | Chain-of-Custody procedures             | IR Team Lead       | CoC-Master-Form.md               |
| A.5.29  | Information security during disruption                                 | BC/DR alignment                         | CISO               | BCP Document                     |
| A.5.30  | ICT readiness for business continuity                                  | ICT continuity plan                     | IT Lead            | ICT Continuity Plan              |
| A.5.31  | Legal, statutory, regulatory and contractual requirements              | Compliance register                     | Compliance Lead    | Compliance Register              |
| A.5.32  | Intellectual property rights                                           | IPR policy                              | Legal              | IPR Policy                       |
| A.5.33  | Protection of records                                                  | Records management policy               | CISO               | Records Management Policy        |
| A.5.34  | Privacy and protection of PII                                          | Privacy policy; DPDP alignment          | DPO/CISO           | Privacy Policy                   |
| A.5.35  | Independent review of information security                             | Annual independent review               | CISO               | Independent Review Reports       |
| A.5.36  | Compliance with policies, rules and standards for information security | Compliance monitoring                   | Compliance Lead    | Compliance Reports               |
| A.5.37  | Documented operating procedures                                        | SOP library                             | All Owners         | All SOPs                         |

## 8.1 Multi-Tenant Considerations for A.5 Controls

| Control | Multi-Tenant Consideration                         |
| ------- | -------------------------------------------------- |
| A.5.7   | Threat intel sanitized for cross-tenant sharing    |
| A.5.12  | Per-tenant data classification respected           |
| A.5.15  | Tenant-scoped RBAC enforced                        |
| A.5.19  | Per-client supplier requirements assessed          |
| A.5.24  | Per-tenant IR plans + master playbooks             |
| A.5.26  | Tenant-scoped response with portfolio coordination |
| A.5.28  | Per-tenant evidence vaults                         |
| A.5.34  | Per-client PII handling per DPA                    |

---

# 9. Annex A.6 – People Controls (8 Controls)

| Control | Title                                                      | MSSP Implementation                        | Owner      | Evidence                  |
| ------- | ---------------------------------------------------------- | ------------------------------------------ | ---------- | ------------------------- |
| A.6.1   | Screening                                                  | Background verification for all personnel  | HR         | BV Records                |
| A.6.2   | Terms and conditions of employment                         | Employment contracts with security clauses | HR + Legal | Employment Contracts      |
| A.6.3   | Information security awareness, education and training     | Annual + role-based training               | HR + CISO  | Training Records          |
| A.6.4   | Disciplinary process                                       | Disciplinary policy for violations         | HR         | Disciplinary Policy       |
| A.6.5   | Responsibilities after termination or change of employment | Offboarding + continuing obligations       | HR         | Offboarding Checklist     |
| A.6.6   | Confidentiality or non-disclosure agreements               | NDA program (general + client-specific)    | Legal + HR | NDA Records               |
| A.6.7   | Remote working                                             | Remote work policy + security controls     | IT + HR    | Remote Work Policy        |
| A.6.8   | Information security event reporting                       | Internal reporting channel                 | CISO       | Event Reporting Procedure |

## 9.1 Multi-Tenant Considerations for A.6 Controls

| Control | Multi-Tenant Consideration                               |
| ------- | -------------------------------------------------------- |
| A.6.1   | Enhanced screening for analysts with multi-client access |
| A.6.3   | Multi-tenant policy training mandatory                   |
| A.6.5   | Per-client NDA continuing obligations                    |
| A.6.6   | Per-client NDAs where contractually required             |
| A.6.8   | Cross-tenant segregation breaches reportable             |

---

# 10. Annex A.7 – Physical Controls (14 Controls)

| Control | Title                                                 | MSSP Implementation              | Owner                | Evidence                    |
| ------- | ----------------------------------------------------- | -------------------------------- | -------------------- | --------------------------- |
| A.7.1   | Physical security perimeters                          | Office + datacenter perimeters   | Facilities           | Physical Security Standards |
| A.7.2   | Physical entry                                        | Access card + biometric controls | Facilities           | Access Logs                 |
| A.7.3   | Securing offices, rooms and facilities                | SOC secure area                  | Facilities + SOC Mgr | SOC Physical Standards      |
| A.7.4   | Physical security monitoring                          | CCTV + alarm systems             | Facilities           | Monitoring Logs             |
| A.7.5   | Protecting against physical and environmental threats | Fire, flood, power protections   | Facilities           | Environmental Standards     |
| A.7.6   | Working in secure areas                               | Secure area procedures           | SOC Manager          | Secure Area SOP             |
| A.7.7   | Clear desk and clear screen                           | Clear desk/screen policy         | CISO + HR            | CDS Policy                  |
| A.7.8   | Equipment siting and protection                       | Equipment standards              | IT                   | Equipment Standards         |
| A.7.9   | Security of assets off-premises                       | Off-site asset policy            | IT                   | Off-Site Asset Procedure    |
| A.7.10  | Storage media                                         | Media management policy          | IT                   | Media Policy                |
| A.7.11  | Supporting utilities                                  | UPS, generator, HVAC             | Facilities           | Utility Maintenance Logs    |
| A.7.12  | Cabling security                                      | Cable management standards       | IT                   | Cabling Standards           |
| A.7.13  | Equipment maintenance                                 | Maintenance schedule             | IT                   | Maintenance Records         |
| A.7.14  | Secure disposal or re-use of equipment                | Disposal procedure               | IT                   | Disposal Records            |

## 10.1 Multi-Tenant Considerations for A.7 Controls

| Control | Multi-Tenant Consideration                               |
| ------- | -------------------------------------------------------- |
| A.7.3   | SOC physical access logged per shift/tenant assignment   |
| A.7.7   | Multi-tenant analyst stations cleared between sessions   |
| A.7.10  | Per-tenant evidence media segregated                     |
| A.7.14  | Tenant-tagged equipment securely wiped per client policy |

---

# 11. Annex A.8 – Technological Controls (34 Controls)

| Control | Title                                                       | MSSP Implementation                             | Owner             | Evidence               |
| ------- | ----------------------------------------------------------- | ----------------------------------------------- | ----------------- | ---------------------- |
| A.8.1   | User endpoint devices                                       | Endpoint hardening + EDR                        | IT Lead           | Endpoint Standards     |
| A.8.2   | Privileged access rights                                    | PAM solution                                    | IT Lead           | PAM Records            |
| A.8.3   | Information access restriction                              | RBAC + ABAC                                     | IT Lead           | Access Control Matrix  |
| A.8.4   | Access to source code                                       | Source code repository controls                 | IT/Dev            | Repo Access Policy     |
| A.8.5   | Secure authentication                                       | MFA + strong auth                               | IT Lead           | Auth Policy            |
| A.8.6   | Capacity management                                         | Capacity planning process                       | IT Lead           | Capacity Plans         |
| A.8.7   | Protection against malware                                  | EDR + AV across MSSP                            | IT Lead           | EDR Coverage Report    |
| A.8.8   | Management of technical vulnerabilities                     | Vuln mgmt program                               | IT Lead           | Vuln Reports           |
| A.8.9   | Configuration management                                    | Configuration baselines                         | IT Lead           | Baseline Docs          |
| A.8.10  | Information deletion                                        | Data deletion procedures                        | IT Lead           | Deletion Records       |
| A.8.11  | Data masking                                                | Data masking in test/dev                        | IT/Dev            | Masking Standards      |
| A.8.12  | Data leakage prevention                                     | DLP solution                                    | IT Lead           | DLP Reports            |
| A.8.13  | Information backup                                          | Backup program                                  | IT Lead           | Backup Logs            |
| A.8.14  | Redundancy of information processing facilities             | HA/DR architecture                              | IT Lead           | HA/DR Design           |
| A.8.15  | Logging                                                     | Centralized logging                             | SOC Manager       | SIEM Logs              |
| A.8.16  | Monitoring activities                                       | 24x7 SOC monitoring                             | SOC Manager       | SOC Reports            |
| A.8.17  | Clock synchronization                                       | NTP across all systems                          | IT Lead           | NTP Config             |
| A.8.18  | Use of privileged utility programs                          | Privileged utility restriction                  | IT Lead           | Utility Inventory      |
| A.8.19  | Installation of software on operational systems             | Software install controls                       | IT Lead           | Install Policy         |
| A.8.20  | Networks security                                           | Network security architecture                   | IT Lead           | Network Diagrams       |
| A.8.21  | Security of network services                                | Network service hardening                       | IT Lead           | Service Standards      |
| A.8.22  | Segregation of networks                                     | Network segmentation (multi-tenant)             | IT Lead           | Segmentation Design    |
| A.8.23  | Web filtering                                               | Web filtering solution                          | IT Lead           | Filtering Reports      |
| A.8.24  | Use of cryptography                                         | Cryptography policy                             | CISO + IT         | Crypto Policy          |
| A.8.25  | Secure development life cycle                               | SDLC policy (if applicable to detection eng)    | Dev Lead          | SDLC Policy            |
| A.8.26  | Application security requirements                           | App security standards                          | Dev Lead          | App Security Standards |
| A.8.27  | Secure system architecture and engineering principles       | Secure architecture standards                   | IT Architect      | Architecture Standards |
| A.8.28  | Secure coding                                               | Secure coding standards (detection rules, SOAR) | Dev Lead          | Coding Standards       |
| A.8.29  | Security testing in development and acceptance              | Testing in dev pipeline                         | Dev Lead          | Test Records           |
| A.8.30  | Outsourced development                                      | Outsourced dev controls                         | Procurement + Dev | Outsourcing Standards  |
| A.8.31  | Separation of development, test and production environments | Environment separation                          | IT Lead           | Environment Design     |
| A.8.32  | Change management                                           | Change management process                       | IT Lead           | Change Records         |
| A.8.33  | Test information                                            | Test data protection                            | IT/Dev            | Test Data Policy       |
| A.8.34  | Protection of information systems during audit testing      | Audit testing controls                          | CISO              | Audit Testing SOP      |

## 11.1 Multi-Tenant Considerations for A.8 Controls

| Control | Multi-Tenant Consideration                            |
| ------- | ----------------------------------------------------- |
| A.8.2   | Privileged access vaulted; cross-tenant access logged |
| A.8.3   | Tenant-scoped RBAC enforced across all platforms      |
| A.8.7   | Per-client EDR coverage tracked                       |
| A.8.8   | Per-tenant vulnerability scanning                     |
| A.8.12  | DLP rules per-tenant (where applicable)               |
| A.8.13  | Per-tenant backup segregation                         |
| A.8.15  | Per-tenant log indexes; tenant-tagged events          |
| A.8.16  | 24x7 monitoring per tenant SLAs                       |
| A.8.22  | Tenant network segregation (VLAN/VPN)                 |
| A.8.24  | Per-tenant encryption keys (where supported)          |
| A.8.31  | Tenant test environments isolated from production     |

---

# 12. Statement of Applicability (SoA) Summary

The MSSP's Statement of Applicability declares:

| Total Annex A Controls | Applicable     | Excluded       | Justification for Exclusions |
| ---------------------- | -------------- | -------------- | ---------------------------- |
| 93                     | TBD (per MSSP) | TBD (per MSSP) | Documented in SoA            |

Common exclusion considerations:

- A.8.25–A.8.30 may be partially applicable if MSSP does not develop custom software
- A.8.4 partially applicable if no source code maintained
- Document each exclusion with risk-based justification

**SoA Owner:** MSSP CISO
**SoA Review:** Annually + on scope change

---

# 13. Multi-Tenant ISO Implementation Architecture (Mandatory)

┌──────────────────────────────────────────────────────────────┐
│ Theme A.5: ORGANIZATIONAL (Multi-Tenant Adaptations) │
│ • Per-tenant policies referenced in master │
│ • Tenant segregation policy as overlay │
│ • Threat intel sanitization │
├──────────────────────────────────────────────────────────────┤
│ Theme A.6: PEOPLE (Multi-Tenant Adaptations) │
│ • Enhanced screening for cross-tenant analysts │
│ • Multi-tenant policy training │
│ • Per-client NDA tracking │
├──────────────────────────────────────────────────────────────┤
│ Theme A.7: PHYSICAL (Multi-Tenant Adaptations) │
│ • SOC physical access tied to tenant assignment │
│ • Per-tenant evidence storage zones │
├──────────────────────────────────────────────────────────────┤
│ Theme A.8: TECHNOLOGICAL (Multi-Tenant Adaptations) │
│ • Tenant-scoped RBAC/ABAC │
│ • Per-tenant logging indexes │
│ • Network segregation per tenant │
│ • Per-tenant encryption keys │
│ • Tenant-tagged backups │
└──────────────────────────────────────────────────────────────┘

---

# 14. Evidence Management (Mandatory)

## 14.1 Evidence Repository Structure

Evidence-Repository/
├── ISMS-Clauses/
│ ├── Clause-4-Context/
│ ├── Clause-5-Leadership/
│ ├── Clause-6-Planning/
│ ├── Clause-7-Support/
│ ├── Clause-8-Operation/
│ ├── Clause-9-Performance/
│ └── Clause-10-Improvement/
├── Annex-A-Controls/
│ ├── A.5-Organizational/
│ ├── A.6-People/
│ ├── A.7-Physical/
│ └── A.8-Technological/
├── Audit-Records/
│ ├── Internal-Audits/
│ ├── Surveillance-Audits/
│ └── Recertification-Audits/
└── Management-Reviews/

## 14.2 Evidence Standards

| Standard        | Requirement                     |
| --------------- | ------------------------------- |
| Format          | Documented, dated, attributable |
| Retention       | Per evidence retention schedule |
| Access          | Compliance Lead + auditors      |
| Versioning      | Controlled versions             |
| Cross-reference | Linked to control ID            |
| Multi-tenant    | Tenant-tagged where applicable  |

**References:**

- `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`

---

# 15. Internal Audit Program (Mandatory)

## 15.1 Audit Schedule

| Audit Type              | Frequency             | Scope                         |
| ----------------------- | --------------------- | ----------------------------- |
| Full ISMS audit         | Annually              | All clauses + all controls    |
| Focused control audit   | Quarterly             | Subset of controls (rotating) |
| Pre-certification audit | Before external audit | All clauses + all controls    |
| Spot-check audit        | Ad-hoc                | Specific control concerns     |

## 15.2 Audit Process

| Step | Action                    | Owner            |
| ---- | ------------------------- | ---------------- |
| 1    | Audit plan approval       | CISO             |
| 2    | Audit notification        | Internal Auditor |
| 3    | Document review           | Internal Auditor |
| 4    | On-site/virtual audit     | Internal Auditor |
| 5    | Findings communication    | Internal Auditor |
| 6    | Audit report              | Internal Auditor |
| 7    | CAPA initiation           | Control Owners   |
| 8    | CAPA closure verification | Internal Auditor |
| 9    | Management review input   | Compliance Lead  |

---

# 16. External Audit Readiness (Mandatory)

## 16.1 Surveillance Audit (Annual)

| Activity                     | Timeline        |
| ---------------------------- | --------------- |
| Pre-audit document review    | T-30 days       |
| Internal audit completion    | T-60 days       |
| Management review completion | T-30 days       |
| Open NCR closure             | T-15 days       |
| Audit logistics confirmation | T-7 days        |
| External audit execution     | T-day           |
| Audit findings response      | T+15 days       |
| CAPA closure                 | Per CB timeline |

## 16.2 Recertification Audit (Triennial)

| Activity                     | Timeline  |
| ---------------------------- | --------- |
| Full Stage 1 readiness       | T-90 days |
| Full Stage 2 readiness       | T-30 days |
| All evidence current         | T-30 days |
| All policies reviewed        | T-60 days |
| All risk assessments current | T-30 days |
| Recertification execution    | T-day     |

**References:**

- `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-Audit-Readiness-Checklist.md`

---

# 17. Client Audit Support (Mandatory)

## 17.1 Client Audit Rights

Per MSA/DPA, clients may request:

| Audit Type            | Frequency      | Scope         |
| --------------------- | -------------- | ------------- |
| Documentation review  | On request     | Per MSA scope |
| Remote evidence audit | Annually       | Per MSA scope |
| On-site audit         | Per MSA        | Per MSA scope |
| Regulator-led audit   | Per regulation | Per regulator |

## 17.2 Client Audit Process

| Step | Action                               | Owner                         |
| ---- | ------------------------------------ | ----------------------------- |
| 1    | Audit request received               | SDM + Compliance Lead         |
| 2    | Scope confirmation                   | Compliance Lead + Client      |
| 3    | NDA / confidentiality                | Legal                         |
| 4    | Evidence preparation (tenant-scoped) | Compliance Lead               |
| 5    | Audit execution                      | Compliance Lead + SOC Manager |
| 6    | Audit response                       | Compliance Lead               |
| 7    | Action items closure                 | Per item                      |

## 17.3 Multi-Tenant Audit Constraints

| Constraint                             | Requirement       |
| -------------------------------------- | ----------------- |
| Client cannot view other clients' data | Strictly enforced |
| Evidence tenant-scoped                 | Mandatory         |
| Sanitized policies shareable           | Mandatory         |
| Other clients' identifiers redacted    | Mandatory         |

---

# 18. Continual Improvement (Mandatory)

## 18.1 Improvement Inputs

| Source               | Examples                       |
| -------------------- | ------------------------------ |
| Internal audits      | NCRs and observations          |
| External audits      | NCRs and recommendations       |
| Management reviews   | Action items                   |
| Risk assessments     | New/changed risks              |
| Incidents            | Lessons learned                |
| Client feedback      | Audit findings                 |
| Threat landscape     | New threats requiring controls |
| ISO standard updates | New control requirements       |

## 18.2 CAPA Process

| Step | Action                     | Owner             |
| ---- | -------------------------- | ----------------- |
| 1    | NCR / observation logged   | Auditor / Manager |
| 2    | Root cause analysis        | Control Owner     |
| 3    | Corrective action plan     | Control Owner     |
| 4    | Implementation             | Control Owner     |
| 5    | Effectiveness verification | Compliance Lead   |
| 6    | NCR closure                | Compliance Lead   |

**References:**

- `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`
- `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`

---

# 19. Management Review (Mandatory)

## 19.1 Frequency

Quarterly minimum + annual comprehensive review.

## 19.2 Standard Agenda (Per ISO 9.3)

| Agenda Item                                  | Source               |
| -------------------------------------------- | -------------------- |
| Status of previous review actions            | Action tracker       |
| Changes affecting ISMS                       | Internal/external    |
| Feedback on information security performance | KPIs                 |
| Audit results                                | Internal + external  |
| Achievement of objectives                    | KPI dashboard        |
| Risk treatment status                        | Risk register        |
| Opportunities for continual improvement      | Improvement register |
| Stakeholder feedback                         | Client/regulator     |
| Resource adequacy                            | Resource plan        |

## 19.3 Review Outputs

| Output                    | Required |
| ------------------------- | -------- |
| Decisions on improvements | Yes      |
| Resource needs            | Yes      |
| Changes to ISMS           | Yes      |
| Updated objectives        | Yes      |
| Action items with owners  | Yes      |

---

# 20. Quality Checklist (Annual ISO Validation)

Before annual ISO surveillance audit:

- [ ] All 93 Annex A controls evidenced
- [ ] SoA current and approved
- [ ] All ISMS clauses (4–10) evidenced
- [ ] Risk register current
- [ ] Risk treatment plan current
- [ ] Internal audit completed
- [ ] All internal NCRs closed
- [ ] Management review completed
- [ ] ISMS objectives reviewed and updated
- [ ] Training records ≥95% completion
- [ ] Awareness program executed
- [ ] All policies reviewed and current
- [ ] All SOPs reviewed and current
- [ ] Incident records and lessons learned current
- [ ] Supplier reviews completed
- [ ] Multi-tenant controls validated
- [ ] Tenant segregation tested
- [ ] Penetration testing completed
- [ ] Vulnerability scans current
- [ ] Disaster recovery test completed
- [ ] Business continuity test completed
- [ ] All previous audit CAPAs closed
- [ ] Evidence repository organized and accessible
- [ ] CISO sign-off obtained

---

# 21. Integration with Other Frameworks

| Framework                    | Mapping                        |
| ---------------------------- | ------------------------------ |
| NIST CSF 2.0                 | `MSSP-NIST-Alignment.md`       |
| SOC 2                        | Trust Service Criteria mapping |
| RBI Cyber Security Framework | `IR-Policy-RBI-Alignment.md`   |
| DPDP Act                     | Privacy controls overlay       |
| CIS Controls v8              | Technical controls mapping     |
| PCI DSS (if applicable)      | Per client                     |
| HIPAA (if applicable)        | Per client                     |

**Reference:**

- `00_GOVERNANCE/00.2_Frameworks-Mapping/Multi-Framework-Gap-Analysis.xlsx`

---

# 22. Related Documents

| Document                        | Path                                                                                    |
| ------------------------------- | --------------------------------------------------------------------------------------- |
| IR Policy Master                | `00_GOVERNANCE/00.1_Policies/IR-Policy-Master.md`                                       |
| IR Policy ISO27001 Alignment    | `00_GOVERNANCE/00.1_Policies/IR-Policy-ISO27001-Alignment.md`                           |
| IR Policy NIST Alignment        | `00_GOVERNANCE/00.1_Policies/IR-Policy-NIST-Alignment.md`                               |
| IR Policy RBI Alignment         | `00_GOVERNANCE/00.1_Policies/IR-Policy-RBI-Alignment.md`                                |
| Policy Exception Register       | `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`                              |
| ISO27001 Annex A Mapping        | `00_GOVERNANCE/00.2_Frameworks-Mapping/ISO27001-Annex-A-Mapping.xlsx`                   |
| NIST CSF Control Mapping        | `00_GOVERNANCE/00.2_Frameworks-Mapping/NIST-CSF-Control-Mapping.xlsx`                   |
| Multi-Framework Gap Analysis    | `00_GOVERNANCE/00.2_Frameworks-Mapping/Multi-Framework-Gap-Analysis.xlsx`               |
| RACI Matrix IR                  | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx`                     |
| MSSP NIST Alignment             | `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-NIST-Alignment.md`                          |
| MSSP Audit Readiness Checklist  | `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-Audit-Readiness-Checklist.md`               |
| Client Data Segregation Policy  | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`       |
| Cross-Client Incident Procedure | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`      |
| Multi-Client Alert Handling     | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`          |
| Evidence Retention Schedule     | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md` |
| Security Improvement Register   | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`         |
| Control Gap Tracker             | `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`                   |
| Lessons Learned Register        | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Register.xlsx`                   |
| All Playbooks                   | `02_PLAYBOOKS/`                                                                         |
| All SOC Tier SOPs               | `03_SOC-TIER-PROCEDURES/`                                                               |

---

# 23. Revision History

| Version | Date        | Author                      | Changes                                   |
| ------- | ----------- | --------------------------- | ----------------------------------------- |
| 1.0     | 30-May-2026 | MSSP Compliance Lead / CISO | Initial version aligned to ISO 27001:2022 |

---

# 24. Approval

Approved by:

| Role                 | Name | Signature | Date |
| -------------------- | ---- | --------- | ---- |
| MSSP Compliance Lead |      |           |      |
| MSSP SOC Manager     |      |           |      |
| MSSP Legal Counsel   |      |           |      |
| MSSP CISO            |      |           |      |

---

**End of Document**
