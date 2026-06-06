# Client Incident Response Policy (Client-Specific)

---

# 1. Document Control

| Field                | Value                                 |
| -------------------- | ------------------------------------- |
| Document Name        | Client IR Policy – [CLIENT-NAME]      |
| Document ID          | MSSP-CL-POL-[CLIENT-ID]               |
| Version              | 1.0                                   |
| Effective Date       | `[YYYY-MM-DD]`                        |
| Client Name          | `[CLIENT-NAME]`                       |
| Client ID            | `CL-####`                             |
| Owner (MSSP)         | MSSP SDM / SOC Manager                |
| Owner (Client)       | Client CISO / Security Lead           |
| Approved By (MSSP)   | MSSP CISO                             |
| Approved By (Client) | Client CISO                           |
| Classification       | Confidential – Client Restricted      |
| Review Cycle         | Annually (or upon significant change) |

---

# 2. Purpose

This document defines the **Client-Specific Incident Response Policy** for `[CLIENT-NAME]` as jointly governed by the MSSP and the client. It establishes the policy framework under which incident response activities are conducted in the client's environment, integrating the MSSP's standard IR framework with the client's specific governance, regulatory, operational, and contractual requirements.

A formal client-specific IR policy is critical because:

- the MSSP's master IR policy provides the foundational framework, but each client has unique governance and regulatory obligations
- regulatory regimes (RBI, SEBI, IRDAI, DPDP Act, sector-specific) vary significantly per client
- containment authority, escalation paths, and decision rights must be agreed in writing per client
- NIST CSF Govern (GV) and ISO 27001 Clause 5 (Leadership) require documented governance
- RBI Cyber Security Framework expects board-approved IR policies for regulated entities
- contractual SLAs and service scope must be reflected in policy
- audit and inspection (RBI, ISO, SOC 2) require client-specific policy evidence
- multi-tenant MSSP operations require strict per-client policy segregation
- joint MSSP-client responsibilities (RACI) must be policy-documented
- client risk tolerance and impact thresholds drive severity classification
- legal hold, evidence handling, and regulatory reporting authority must be defined
- client crisis management coordination must be policy-defined

This policy ensures:

- formal joint governance of IR activities between MSSP and client
- alignment between MSSP service delivery and client governance
- documented decision rights and approval authorities
- regulatory compliance per client's applicable obligations
- audit-ready evidence of joint IR governance
- escalation and crisis management protocols agreed in advance
- baseline for client-specific playbook customization
- foundation for tabletop exercises and drills
- clarity for SOC analysts on client-specific governance

Reference alignment:
`00_GOVERNANCE/00.1_Policies/IR-Policy-Master.md`
`00_GOVERNANCE/00.1_Policies/IR-Policy-RBI-Alignment.md`
`00_GOVERNANCE/00.1_Policies/IR-Policy-ISO27001-Alignment.md`
`00_GOVERNANCE/00.1_Policies/IR-Policy-NIST-Alignment.md`
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`

---

# 3. Scope

This policy applies to:

| Scope Element          | Coverage                                                           |
| ---------------------- | ------------------------------------------------------------------ |
| Client environment     | All in-scope assets per MSSP contract                              |
| Geographic scope       | All client locations covered by MSSP services                      |
| Service tier           | Per agreed service tier (Monitoring / MDR / Co-Managed / Full SOC) |
| Coverage hours         | Per agreed coverage window (24x7 / business hours / hybrid)        |
| Incident categories    | All incident categories per master IR policy                       |
| Regulatory obligations | All client-applicable regulations                                  |
| Joint operations       | All joint MSSP-client IR activities                                |
| Tabletop exercises     | All joint exercises                                                |
| Reporting              | All client-facing IR reporting                                     |

Out of scope:

- MSSP-internal IR activities not affecting client
- Non-incident operational activities (covered by SOPs)
- Client-only IR activities outside MSSP scope (e.g., physical security)

---

# 4. Definitions

| Term                  | Definition                                                               |
| --------------------- | ------------------------------------------------------------------------ |
| Client                | `[CLIENT-NAME]`, the regulated entity receiving MSSP services            |
| MSSP                  | The Managed Security Service Provider delivering services per contract   |
| Joint IR              | Incident response activities involving both MSSP and client teams        |
| Containment Authority | Authority to execute containment actions                                 |
| Material Incident     | Incident meeting client/regulatory threshold for material classification |
| Regulatory Reportable | Incident triggering mandatory regulatory notification                    |
| Decision Authority    | Authority to make binding decisions during IR                            |
| Service Tier          | Contracted service level (defines scope and SLAs)                        |
| Co-Managed            | Shared responsibility model between MSSP and client SOC                  |
| Steering Committee    | Joint governance body overseeing the engagement                          |

---

# 5. Roles and Responsibilities (Joint Governance)

## 5.1 MSSP Roles

| Role                      | Responsibilities                                           |
| ------------------------- | ---------------------------------------------------------- |
| MSSP CISO                 | Strategic oversight; policy approval; executive escalation |
| MSSP SOC Manager          | Service delivery accountability; operational governance    |
| MSSP SDM                  | Primary client liaison; policy administration              |
| MSSP IR Team Lead         | IR technical leadership; joint IR coordination             |
| MSSP SOC Lead             | Operational shift leadership; escalation point             |
| MSSP L1/L2/L3 Analysts    | Incident triage, investigation, and response               |
| MSSP Compliance Lead      | Regulatory alignment validation                            |
| MSSP Detection Engineer   | Client-specific detection capability                       |
| MSSP Threat Intel Analyst | Client-relevant threat intelligence                        |

## 5.2 Client Roles

| Role                        | Responsibilities                                          |
| --------------------------- | --------------------------------------------------------- |
| Client CISO / Security Head | Strategic oversight; policy approval; executive decisions |
| Client CIO                  | IT operational alignment                                  |
| Client Primary IR Contact   | Day-to-day MSSP liaison                                   |
| Client 24x7 On-Call         | After-hours escalation point                              |
| Client IT Operations        | Infrastructure changes; remediation execution             |
| Client Identity Operations  | Account actions; access changes                           |
| Client Network Operations   | Network actions; firewall changes                         |
| Client Application Owners   | Application-specific decisions                            |
| Client Compliance Officer   | Regulatory reporting decisions                            |
| Client Legal Counsel        | Legal hold; legal communications                          |
| Client DPO                  | Privacy/data protection decisions                         |
| Client HR                   | Insider threat coordination                               |
| Client Communications       | Internal/external/customer communications                 |
| Client Business Sponsor     | Business impact decisions; resource authorization         |
| Client CEO/MD               | Material incident decisions; regulatory sign-off          |

## 5.3 Joint Steering Committee

| Membership                                        | Frequency                    |
| ------------------------------------------------- | ---------------------------- |
| MSSP CISO + SOC Manager + SDM                     | Quarterly + on demand for P1 |
| Client CISO + Primary Contact + Executive Sponsor | Quarterly + on demand for P1 |

References:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`

---

# 6. Policy Statements (Mandatory)

## 6.1 General Principles

The MSSP and `[CLIENT-NAME]` jointly commit to:

- **Risk-based prioritization** – incidents handled per business impact
- **Timely response** – per contracted SLAs and regulatory requirements
- **Confidentiality** – client data protected throughout response
- **Evidence preservation** – chain of custody maintained for all evidence
- **Legal and regulatory compliance** – all obligations honored
- **Continuous improvement** – lessons learned drive program enhancement
- **Transparent communication** – timely, accurate updates to all stakeholders
- **Joint accountability** – shared ownership of incident outcomes

## 6.2 Authority and Decision Rights

- **Containment decisions** – per containment authority matrix (Section 9)
- **Regulatory reporting decisions** – Client retains authority (MSSP supports)
- **External communications** – Client retains authority
- **Law enforcement engagement** – Client retains authority
- **Legal counsel engagement** – Client retains authority
- **Cyber insurance engagement** – Client retains authority
- **Customer notification** – Client retains authority
- **MSSP service decisions** – MSSP retains authority within contracted scope

## 6.3 Confidentiality and Information Sharing

- All incident information classified as `[Client Classification – e.g., Confidential]`
- Cross-client information sharing strictly prohibited
- External sharing requires client written approval
- Threat intelligence sharing (sanitized) governed by separate clauses
- Regulatory disclosures per regulatory requirements only

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 7. Service Scope and SLA Summary (Mandatory)

### 7.1 Service Tier and Coverage

| Aspect              | Value                                        |
| ------------------- | -------------------------------------------- |
| Service Tier        | `[Monitoring / MDR / Co-Managed / Full SOC]` |
| Coverage Hours      | `[24x7 / Business Hours / Custom]`           |
| Coverage Days       | `[7 days / 5 days / Custom]`                 |
| Geographic Coverage | `[All client locations / specific]`          |
| Asset Scope         | Per Asset Register                           |
| Contract Reference  | `[MSA + SOW reference]`                      |

### 7.2 SLA Summary

| Severity | Acknowledgement SLA | Response SLA | Resolution Target |
| -------- | ------------------- | ------------ | ----------------- |
| P1       |                     |              |                   |
| P2       |                     |              |                   |
| P3       |                     |              |                   |
| P4       |                     |              |                   |

### 7.3 Reporting SLA

| Report Type                              | Frequency | Delivery SLA |
| ---------------------------------------- | --------- | ------------ |
| Initial Incident Report (P1)             |           |              |
| Final Incident Report                    |           |              |
| Daily Summary                            |           |              |
| Weekly Summary                           |           |              |
| Monthly Comprehensive                    |           |              |
| Quarterly Executive Briefing             |           |              |
| SLA Compliance Report                    |           |              |
| Regulatory Reports (RBI/CERT-In support) |           |              |

References:
`00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`

---

# 8. Severity Classification (Client-Specific)

The client adopts the MSSP's standard severity framework with the following client-specific considerations:

| Severity          | Standard Definition                 | Client-Specific Considerations                                                  |
| ----------------- | ----------------------------------- | ------------------------------------------------------------------------------- |
| **P1 (Critical)** | Service-impacting or material risk  | `[Add client-specific examples: e.g., core banking down, customer data breach]` |
| **P2 (High)**     | Significant impact, contained scope | `[Add client-specific examples]`                                                |
| **P3 (Medium)**   | Limited impact, manageable          | `[Add client-specific examples]`                                                |
| **P4 (Low)**      | Minimal impact, informational       | `[Add client-specific examples]`                                                |

### 8.1 Client-Specific Material Incident Definition

A "Material Incident" for `[CLIENT-NAME]` is defined as:

- `[e.g., Any incident affecting > 1000 customers]`
- `[e.g., Any incident with confirmed customer data exposure]`
- `[e.g., Any incident causing > 1 hour core banking downtime]`
- `[e.g., Any incident reportable to RBI per Cyber Security Framework]`
- `[e.g., Any incident reportable to CERT-In per 2022 Directions]`

References:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

# 9. Containment Authority Matrix (Client-Specific – Mandatory)

| Action                                          | Severity | MSSP Authority | Pre-Approved by Client? | Approval Required From (Client)      |
| ----------------------------------------------- | -------- | -------------- | ----------------------- | ------------------------------------ |
| Endpoint isolation (EDR) – single host          | P1/P2    | Yes            | Yes                     |                                      |
| Endpoint isolation (EDR) – multiple hosts (<10) | P1/P2    | Yes            | Yes                     |                                      |
| Endpoint isolation (EDR) – mass (>10)           | P1       | Joint          | No                      | Client IT Lead                       |
| Disable standard user account                   | P1/P2    | Yes            | Yes                     |                                      |
| Disable privileged user account                 | P1       | Joint          | No                      | Client Identity Lead                 |
| Disable service account                         | P1       | Joint          | No                      | Application Owner                    |
| Block IP at perimeter firewall                  | Any      | Yes            | Yes                     |                                      |
| Block IP at internal firewall                   | P1/P2    | Joint          | No                      | Client Network Lead                  |
| Block domain (DNS sinkhole)                     | Any      | Yes            | Yes                     |                                      |
| Block email sender                              | Any      | Yes            | Yes                     |                                      |
| Quarantine email                                | P1/P2    | Yes            | Yes                     |                                      |
| Disable cloud user account                      | P1       | Joint          | No                      | Client Cloud Lead                    |
| Suspend cloud workload                          | P1       | Joint          | No                      | Client Cloud Lead                    |
| Revoke API keys                                 | P1       | Joint          | No                      | Application Owner                    |
| Reset privileged credentials                    | P1       | Joint          | No                      | Client Identity Lead                 |
| Take application offline                        | P1       | Joint          | No                      | Application Owner + Business Sponsor |
| Network segment isolation                       | P1       | Joint          | No                      | Client Network Lead + CISO           |
| Disconnect site from network                    | P1       | Joint          | No                      | Client CIO + CISO                    |

References:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 10. Escalation Framework (Client-Specific – Mandatory)

The detailed escalation matrix is maintained in:
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-Escalation-Matrix.md`

### 10.1 High-Level Escalation Flow

```
Alert/Incident Detected
        │
        ▼
MSSP L1 Triage (within SLA)
        │
   ┌────┴────┐
   ▼         ▼
 P3/P4     P1/P2
   │         │
   │         ▼
   │    MSSP L2/L3 + Client Primary Contact
   │         │
   │         ▼
   │    Client Security Lead
   │         │
   │         ▼
   │    Client CISO
   │         │
   │         ▼
   │    Client Executive Sponsor (P1)
   │         │
   │         ▼
   │    Client CEO/MD (Material Incident)
   │
   ▼
Logged for routine handling
```

### 10.2 Crisis Bridge Activation

For P1 incidents, joint bridge call activated within `[X minutes]` per SLA.

References:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

---

# 11. Regulatory Reporting Framework (Client-Specific – Mandatory)

### 11.1 Applicable Regulations

| Regulation                         | Applicable (Y/N) | Reporting Authority              | Timeline         |
| ---------------------------------- | ---------------- | -------------------------------- | ---------------- |
| RBI Cyber Security Framework       | `[Y/N]`          | Client → RBI (MSSP supports)     | 2-6 hours        |
| CERT-In Directions (2022)          | `[Y/N]`          | Client → CERT-In (MSSP supports) | 6 hours          |
| NCIIPC (if CII)                    | `[Y/N]`          | Client → NCIIPC (MSSP supports)  | Per guidelines   |
| SEBI Cybersecurity Framework       | `[Y/N]`          | Client → SEBI (MSSP supports)    | Per guidelines   |
| IRDAI Information & Cyber Security | `[Y/N]`          | Client → IRDAI (MSSP supports)   | Per guidelines   |
| DPDP Act (Data Breach)             | `[Y/N]`          | Client → DPB (MSSP supports)     | Per Act timeline |
| Other                              |                  |                                  |                  |

### 11.2 Reporting Roles

| Activity                              | MSSP Role          | Client Role       |
| ------------------------------------- | ------------------ | ----------------- |
| Incident assessment for reportability | Support / Advise   | Decision          |
| Report drafting                       | Support / Drafting | Review / Sign-off |
| Report submission                     | Support            | Submit            |
| Acknowledgment tracking               | Support            | Retain            |
| Follow-up reports                     | Support / Drafting | Submit            |
| RCA report (regulatory)               | Author / Support   | Submit            |

### 11.3 Reporting Templates

References:
`07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`

---

# 12. Communication and Notification Protocols (Mandatory)

### 12.1 Internal Client Notifications

| Stakeholder       | P1                      | P2      | P3            | P4             |
| ----------------- | ----------------------- | ------- | ------------- | -------------- |
| Primary Contact   | Immediate               | <30 min | <2 hrs        | Daily summary  |
| Security Lead     | Immediate               | <30 min | <2 hrs        | Daily summary  |
| CISO              | Immediate               | <1 hr   | Daily summary | Weekly summary |
| CIO               | Immediate               | <1 hr   | Daily summary | Weekly summary |
| Executive Sponsor | <30 min                 | <2 hrs  | Daily summary | Weekly summary |
| CEO/MD            | Material incidents only | N/A     | N/A           | N/A            |

### 12.2 External Communications

| Audience          | Authority                            |
| ----------------- | ------------------------------------ |
| Customers         | Client (with MSSP support if needed) |
| Media             | Client only                          |
| Regulators        | Client (with MSSP support)           |
| Law Enforcement   | Client (with MSSP support)           |
| Public statements | Client only                          |
| Vendor partners   | Joint                                |
| Insurance carrier | Client (with MSSP support)           |

### 12.3 Bridge Call Protocol

| Trigger               | Bridge Activation                     |
| --------------------- | ------------------------------------- |
| P1 declared           | Within `[X minutes]`                  |
| P2 with escalation    | Per SOC Lead decision                 |
| Regulatory reportable | Within `[X minutes]` of determination |
| Customer-impacting    | Within `[X minutes]`                  |

References:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

---

# 13. Evidence Handling and Chain of Custody (Mandatory)

### 13.1 Evidence Handling Standards

- All evidence handled per MSSP's Chain of Custody SOP
- Client-specific storage location: `[On MSSP secure storage / Client storage / Hybrid]`
- Client right to inspect evidence: `[Yes/No per contract]`
- Data residency requirements: `[India / Specific / No restriction]`

### 13.2 Retention Periods

| Evidence Type                  | Retention Period          | Notes                      |
| ------------------------------ | ------------------------- | -------------------------- |
| Standard incident evidence     | `[X years]`               |                            |
| Regulatory-reportable evidence | `[X years]`               | Per regulatory requirement |
| Legal hold evidence            | Until legal hold released | Per legal advice           |
| Forensic images                | `[X years]`               |                            |

References:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md`

---

# 14. Legal Hold and Litigation Support (Mandatory)

- Legal hold authority: **Client Legal Counsel**
- Notification to MSSP: Within `[X hours]` of legal hold determination
- MSSP obligations during legal hold:
  - Suspend standard destruction processes
  - Preserve all related evidence
  - Document all access to held evidence
  - Coordinate with client legal counsel
- Release of legal hold: Written instruction from Client Legal Counsel

References:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

---

# 15. Crisis Management Integration (Mandatory)

### 15.1 Crisis Activation Triggers

A cyber incident triggers client crisis management when:

- `[e.g., Customer-facing service unavailable > 1 hour]`
- `[e.g., Confirmed customer data breach]`
- `[e.g., Regulatory reportable material incident]`
- `[e.g., Media inquiry received]`
- `[e.g., Law enforcement engagement required]`

### 15.2 Crisis Coordination

| Activity               | Responsibility                     |
| ---------------------- | ---------------------------------- |
| Crisis declaration     | Client CISO + Executive Sponsor    |
| Crisis bridge          | Client-led; MSSP participates      |
| Crisis communications  | Client (MSSP supports)             |
| Technical response     | Joint (MSSP-led for cyber aspects) |
| Business continuity    | Client-led                         |
| Stakeholder management | Client-led                         |

References:
`02_PLAYBOOKS/02.0_Playbook-Index.md`

---

# 16. Post-Incident Activities (Mandatory)

### 16.1 Lessons Learned

| Incident Severity | LL Session Required? | Timeline                 | Joint?      |
| ----------------- | -------------------- | ------------------------ | ----------- |
| P1                | Mandatory            | Within 5 days of closure | Yes (joint) |
| P2                | Mandatory            | Within 10 days           | Yes (joint) |
| P3 (TP)           | Recommended          | Within 20 days           | Per request |
| P4                | Optional             | N/A                      | No          |

### 16.2 Root Cause Analysis

| Incident Severity     | RCA Required? | Timeline                        | Authority                     |
| --------------------- | ------------- | ------------------------------- | ----------------------------- |
| P1                    | Mandatory     | Within 10 days                  | MSSP authors; Client approves |
| P2                    | Mandatory     | Within 15 days                  | MSSP authors; Client approves |
| P3 (TP)               | Recommended   | Within 20 days                  | MSSP authors                  |
| Regulatory reportable | Mandatory     | Per regulator (RBI: 14-30 days) | Joint                         |

### 16.3 Improvement Actions

- Actions tracked in MSSP improvement registers (tenant-scoped)
- Client-specific actions tracked in client systems (via MSSP communication)
- Quarterly improvement review with client

References:
`08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`
`08_POST-INCIDENT/08.3_Improvement-Tracking/`

---

# 17. Joint Exercises and Drills (Mandatory)

| Exercise Type              | Frequency       | Joint?        |
| -------------------------- | --------------- | ------------- |
| Tabletop exercise          | Annually        | Yes           |
| Crisis communication drill | Annually        | Yes           |
| Red/Purple team exercise   | Per agreement   | Per agreement |
| Regulatory reporting drill | Annually (BFSI) | Yes           |
| Bridge call drill          | Quarterly       | Yes           |

References:
`10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/`
`10_TRAINING-AND-EXERCISES/10.3_Drills/`

---

# 18. Compliance and Audit (Mandatory)

### 18.1 Audit Cooperation

- MSSP cooperates with client audits subject to:
  - Reasonable notice (`[X days/weeks]`)
  - Confidentiality protections
  - Multi-tenant segregation maintained
  - Access scoped to client's specific data only
- MSSP provides:
  - Audit evidence packages (tenant-scoped)
  - Sanitized policies and procedures
  - Personnel for interviews as agreed
  - Access to client-specific systems

### 18.2 Regulatory Inspection Support

- MSSP provides on-demand support for RBI/regulatory inspections
- Timelines per regulator requirements
- MSSP personnel may be required to attend

References:
`07_REPORTING/07.4_Regulatory-Reports/Audit-Evidence-Package.md`
`09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-Audit-Readiness-Checklist.md`

---

# 19. Policy Review and Maintenance (Mandatory)

| Review Type                     | Frequency             | Owner                          |
| ------------------------------- | --------------------- | ------------------------------ |
| Annual policy review            | Annually              | Joint (MSSP SDM + Client CISO) |
| Regulatory change-driven review | Per regulation change | MSSP Compliance + Client       |
| Service tier change review      | Per change            | MSSP SDM                       |
| Post-major-incident review      | Per P1                | Joint                          |
| Steering committee review       | Quarterly             | Joint                          |

---

# 20. Policy Exceptions (Mandatory)

Any deviation from this policy requires:

- Written exception request from client
- MSSP risk assessment
- Joint approval (MSSP SOC Manager + Client CISO)
- Documentation in exception register
- Defined exception expiry date
- Periodic review of active exceptions

References:
`00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`

---

# 21. Confidentiality and Data Protection (Mandatory)

### 21.1 Confidentiality

- All incident information classified as `[Client Classification]`
- NDA obligations apply continuously
- No cross-client sharing of any information
- Sanitized lessons may inform MSSP master playbooks (without client identifiers)

### 21.2 Data Protection

- All client data handled per DPA (Data Processing Agreement)
- Data residency: `[India / Specific]`
- Data processing purpose: IR services only
- Sub-processor restrictions: Per DPA
- Data subject rights: Client retains responsibility

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 22. Termination and Transition (Mandatory)

Upon engagement termination:

- All incident data handled per offboarding plan
- Evidence handled per legal/regulatory retention requirements
- Client playbooks transferred per IP terms in contract
- Knowledge transfer per offboarding plan

References:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Offboarding-Checklist.md`

---

# 23. Related Documents

| Document                          | Path                                                                                            |
| --------------------------------- | ----------------------------------------------------------------------------------------------- |
| Client Escalation Matrix          | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-Escalation-Matrix.md` |
| Client Custom Playbooks           | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-Custom-Playbooks/`    |
| Client Environment Profile        | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`                |
| Client IR Contacts                | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`                                 |
| Client Onboarding Checklist       | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Onboarding-Checklist.md`                        |
| Client Offboarding Checklist      | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Offboarding-Checklist.md`                       |
| Client-Specific Playbook Guide    | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`         |
| Client Data Segregation Policy    | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`               |
| IR Policy Master                  | `00_GOVERNANCE/00.1_Policies/IR-Policy-Master.md`                                               |
| IR Policy RBI Alignment           | `00_GOVERNANCE/00.1_Policies/IR-Policy-RBI-Alignment.md`                                        |
| IR Policy ISO27001 Alignment      | `00_GOVERNANCE/00.1_Policies/IR-Policy-ISO27001-Alignment.md`                                   |
| IR Policy NIST Alignment          | `00_GOVERNANCE/00.1_Policies/IR-Policy-NIST-Alignment.md`                                       |
| MSSP-Client SLA Template          | `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`                                    |
| MSSP-Client Responsibility Matrix | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`            |
| IRT Containment Authority Matrix  | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`            |
| MSSP Client Evidence Handling     | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md`       |
| RBI Mandatory Report Template     | `07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`                         |
| Legal Counsel Engagement SOP      | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Policy Exception Register         | `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`                                      |

---

# 24. Revision History

| Version | Date           | Author                 | Changes               |
| ------- | -------------- | ---------------------- | --------------------- |
| 1.0     | `[YYYY-MM-DD]` | MSSP SDM / Client CISO | Initial joint version |

---

# 25. Approval

**Approved by (MSSP):**

| Role             | Name | Signature | Date |
| ---------------- | ---- | --------- | ---- |
| MSSP SDM         |      |           |      |
| MSSP SOC Manager |      |           |      |
| MSSP CISO        |      |           |      |

**Approved by (Client):**

| Role                   | Name | Signature | Date |
| ---------------------- | ---- | --------- | ---- |
| Client Primary Contact |      |           |      |
| Client Security Lead   |      |           |      |
| Client CISO            |      |           |      |

---

**End of Document**
