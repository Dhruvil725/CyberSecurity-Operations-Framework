# Client Data Segregation Policy (MSSP Multi-Tenant)

---

# 1. Document Control

| Field          | Value                                               |
| -------------- | --------------------------------------------------- |
| Document Name  | Policy – Client Data Segregation                    |
| Document ID    | MSSP-MT-001                                         |
| Version        | 1.0                                                 |
| Effective Date | 30-May-2026                                         |
| Owner          | MSSP CISO / SOC Manager                             |
| Approved By    | MSSP CISO + Compliance Lead                         |
| Classification | Confidential – MSSP Internal                        |
| Review Cycle   | Annually (or upon multi-tenant architecture change) |

---

# 2. Purpose

This document defines the **Client Data Segregation Policy** governing how the MSSP maintains strict, verifiable separation of client data, configurations, telemetry, evidence, intelligence, playbooks, and communications across its multi-tenant SOC operations.

A formal client data segregation policy is critical because:

- the MSSP serves multiple regulated clients simultaneously in shared infrastructure
- cross-client data leakage represents the single greatest reputational and contractual risk to the MSSP
- NIST CSF Identify (ID.GV, ID.SC) and Protect (PR.AC, PR.DS) require multi-tenant access controls and data protection
- ISO 27001 Annex A.5.10, A.5.12, A.5.14, A.5.34, A.8.3 mandate data classification, segregation, and access control
- RBI Cyber Security Framework and outsourcing guidelines hold MSSPs accountable for tenant isolation
- DPDP Act and other privacy laws impose strict data processing controls
- contractual NDAs and DPAs require enforceable segregation
- audit and compliance reviews (SOC 2, ISO 27001, client audits) require evidence of segregation controls
- cross-client information leakage may trigger regulatory penalties for both MSSP and clients
- SOC analyst behavior (intentional or unintentional) is the primary segregation risk vector
- multi-tenant tools (SIEM, EDR, TI platforms, SOAR) require explicit tenant configuration
- threat intelligence and lessons learned require careful sanitization for cross-tenant benefit
- staff offboarding, role changes, and onboarding affect segregation continuously
- this policy is the foundation for client trust in MSSP services

This policy ensures:

- defined, enforceable principles of tenant isolation across people, process, and technology
- consistent application across all clients, tools, and operations
- clear analyst guidance on permitted and prohibited cross-tenant activities
- defined sanitization standards for legitimate cross-tenant intelligence
- audit-ready evidence of segregation controls
- incident response procedures for segregation breaches
- linkage to client onboarding, offboarding, playbook customization, and compliance

Reference alignment:
`09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-ISO27001-Controls.md`
`09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-NIST-Alignment.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Onboarding-Checklist.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Offboarding-Checklist.md`

---

# 3. Scope

This policy applies to all MSSP operations involving multiple clients:

| Scope Element         | Coverage                                   |
| --------------------- | ------------------------------------------ |
| Client telemetry      | All log sources, alerts, events            |
| Client incident data  | Tickets, investigations, evidence          |
| Client documentation  | Profiles, contacts, playbooks              |
| Client communications | Email, portals, bridge calls               |
| Client reports        | Operational, executive, regulatory         |
| Client evidence       | Forensic artifacts, CoC records            |
| Client threat intel   | IoCs, profiles, TTPs derived from client   |
| Client configurations | Detection rules, tuning, integrations      |
| Client backups        | All backup data                            |
| Multi-tenant tools    | SIEM, EDR, SOAR, TI platforms, ticketing   |
| Shared infrastructure | Compute, storage, network                  |
| Personnel access      | All SOC and IR staff                       |
| Third-party access    | Vendors, contractors, auditors             |
| MSSP knowledge bases  | Internal documentation referencing clients |

Out of scope:

- Client-internal segregation (client's responsibility)
- MSSP-internal departmental segregation (covered by MSSP IT policies)
- Generic data classification policies (covered by MSSP information security policy)

---

# 4. Definitions

| Term                 | Definition                                                           |
| -------------------- | -------------------------------------------------------------------- |
| Tenant               | Logical or physical isolation boundary for a single client           |
| Multi-Tenancy        | Architecture serving multiple clients within shared infrastructure   |
| Tenant Segregation   | Enforced isolation between client tenants                            |
| Tenant ID            | Unique identifier per client used in all systems                     |
| Cross-Tenant         | Information or access spanning multiple client tenants               |
| Sanitization         | Removal of client-identifying information before aggregation/sharing |
| Anonymization        | Permanent removal of client identification                           |
| Pseudonymization     | Replacement of client identifiers with reversible tokens             |
| Logical Segregation  | Software-enforced tenant boundaries within shared infrastructure     |
| Physical Segregation | Dedicated infrastructure per client                                  |
| RBAC                 | Role-Based Access Control                                            |
| ABAC                 | Attribute-Based Access Control                                       |
| Need-to-Know         | Access limited to specific operational requirement                   |
| Least Privilege      | Minimum access required for role function                            |
| Segregation Breach   | Unauthorized cross-tenant access or information leakage              |

---

# 5. Roles and Responsibilities

| Role                      | Responsibilities                                                |
| ------------------------- | --------------------------------------------------------------- |
| MSSP CISO                 | Owns policy; approves exceptions; reviews breaches              |
| MSSP SOC Manager          | Operational enforcement; analyst supervision; incident response |
| MSSP Compliance Lead      | Audit; control validation; regulatory alignment                 |
| MSSP IT/Platform Team     | Technical implementation of segregation controls                |
| MSSP Detection Engineer   | Tenant-scoped detection rule management                         |
| MSSP Threat Intel Analyst | Sanitization for cross-tenant TI products                       |
| MSSP SDM (per client)     | Tenant-specific client liaison                                  |
| MSSP L1/L2/L3 Analysts    | Operational adherence; report observed issues                   |
| MSSP IR Team              | Tenant-scoped IR operations                                     |
| MSSP HR                   | Training; onboarding/offboarding; disciplinary action           |
| MSSP Legal Counsel        | Contract alignment; breach legal response                       |
| External Auditors         | Validation per audit scope (with client approval)               |

---

# 6. Policy Principles (Mandatory)

The MSSP adheres to the following core principles for client data segregation:

| Principle                       | Description                                                                   |
| ------------------------------- | ----------------------------------------------------------------------------- |
| **Strict Isolation by Default** | All client data segregated unless explicit authorization for cross-tenant use |
| **Tenant-Scoped Access**        | Analysts access only assigned clients                                         |
| **Least Privilege**             | Minimum access required for role function                                     |
| **Need-to-Know**                | Information shared only with operational necessity                            |
| **Defense in Depth**            | Multiple layers of segregation controls                                       |
| **Auditability**                | All access and cross-tenant activity logged                                   |
| **Sanitization for Sharing**    | Cross-tenant intelligence must be sanitized                                   |
| **Verifiable Controls**         | Segregation controls testable and evidence-producing                          |
| **Breach Notification**         | Suspected/confirmed breaches reported immediately                             |
| **Continuous Improvement**      | Regular validation and enhancement                                            |
| **Contractual Alignment**       | Per client contract, DPA, and NDA                                             |
| **Regulatory Compliance**       | Per applicable regulations (RBI, DPDP, ISO, etc.)                             |

---

# 7. Segregation Layers (Mandatory)

Segregation is enforced across multiple layers:

```
┌────────────────────────────────────────────────────────┐
│  Layer 7: GOVERNANCE                                    │
│  Policies, contracts, training, oversight              │
├────────────────────────────────────────────────────────┤
│  Layer 6: PERSONNEL                                     │
│  Assignment, access control, behavioral standards      │
├────────────────────────────────────────────────────────┤
│  Layer 5: PROCESS                                       │
│  Workflows, approvals, sanitization, audit             │
├────────────────────────────────────────────────────────┤
│  Layer 4: APPLICATION                                   │
│  Tenant-aware tools, RBAC, multi-tenant config         │
├────────────────────────────────────────────────────────┤
│  Layer 3: DATA                                          │
│  Encryption, tenant tagging, segregated storage        │
├────────────────────────────────────────────────────────┤
│  Layer 2: NETWORK                                       │
│  Network segmentation, VLANs, dedicated paths          │
├────────────────────────────────────────────────────────┤
│  Layer 1: INFRASTRUCTURE                                │
│  Compute isolation, storage isolation, backups         │
└────────────────────────────────────────────────────────┘
```

---

# 8. Personnel Segregation Controls (Mandatory)

## 8.1 Analyst Assignment Model

| Approach           | Description                               | Applicability                          |
| ------------------ | ----------------------------------------- | -------------------------------------- |
| **Dedicated Team** | Single client per team                    | High-value or highly regulated clients |
| **Pod Model**      | Small team handling defined cluster       | Standard tiered clients                |
| **Shared Pool**    | Analysts assigned across clients per need | Generic monitoring tier                |
| **Follow-the-Sun** | 24x7 coverage across global teams         | All tiers                              |

### 8.1.1 Assignment Documentation

- Every analyst has documented client assignment(s)
- Assignment recorded in IAM system with attributes
- Assignment scope determines tool/data access
- Assignment changes follow change control

## 8.2 Access Authorization

| Control             | Requirement                                         |
| ------------------- | --------------------------------------------------- |
| RBAC enforcement    | All tools enforce role-based access                 |
| ABAC enforcement    | Where supported, attribute-based (client tenant ID) |
| Need-to-know review | Quarterly access review per analyst                 |
| Just-in-time access | Elevated/cross-tenant access via approval workflow  |
| MFA                 | Mandatory for all MSSP systems                      |
| PAM                 | Privileged access vaulted and monitored             |

## 8.3 Behavioral Standards (Mandatory)

All MSSP personnel must:

- **Never** discuss one client's information with another client's team members
- **Never** use one client's data, IoCs, or learnings for another client without sanitization
- **Never** access another client's tenant without explicit authorization
- **Never** copy/extract client data to personal devices or unauthorized storage
- **Never** discuss client information in public spaces or unsecured channels
- **Always** verify tenant context before any action
- **Always** sanitize before cross-tenant references
- **Always** report observed segregation issues immediately
- **Always** complete tenant-specific training before client assignment

## 8.4 Onboarding & Offboarding

### 8.4.1 Personnel Onboarding

- [ ] Background verification completed
- [ ] NDA signed (general + client-specific where required)
- [ ] Multi-tenant policy training completed
- [ ] Tenant assignment documented
- [ ] RBAC/ABAC configured
- [ ] Access tested
- [ ] Mentor assigned for first 30 days

### 8.4.2 Personnel Offboarding

- [ ] All access revoked within 4 hours of separation
- [ ] All tenant access verified removed
- [ ] Client-specific NDAs continuing obligations confirmed
- [ ] Equipment returned and wiped
- [ ] Access audit performed
- [ ] Knowledge handover completed

### 8.4.3 Role Changes

- [ ] Old client access revoked
- [ ] New client access provisioned per assignment
- [ ] Access audit performed within 7 days
- [ ] Training for new client(s) completed

---

# 9. Technical Segregation Controls (Mandatory)

## 9.1 Multi-Tenant Tool Configuration

### 9.1.1 SIEM

| Control             | Requirement                                      |
| ------------------- | ------------------------------------------------ |
| Tenant separation   | Per-tenant indexes / namespaces / workspaces     |
| Access control      | RBAC enforced per tenant                         |
| Query isolation     | Cross-tenant queries blocked or require approval |
| Dashboard isolation | Tenant-scoped dashboards                         |
| Alert routing       | Tenant-tagged routing                            |
| Audit logging       | All queries and access logged with tenant ID     |

### 9.1.2 EDR / XDR

| Control           | Requirement                                      |
| ----------------- | ------------------------------------------------ |
| Tenant separation | Per-tenant console / multi-tenant view with RBAC |
| Endpoint grouping | Tenant-tagged endpoint groups                    |
| Containment scope | Limited to assigned tenant endpoints             |
| Query isolation   | Per-tenant query scope                           |

### 9.1.3 SOAR / Ticketing

| Control            | Requirement                        |
| ------------------ | ---------------------------------- |
| Tenant separation  | Per-tenant workspace / project     |
| Ticket assignment  | Routed to tenant-assigned analysts |
| Playbook isolation | Tenant-scoped playbooks            |
| Auto-response      | Tenant-scoped actions              |

### 9.1.4 Threat Intelligence Platform

| Control             | Requirement                                        |
| ------------------- | -------------------------------------------------- |
| Tenant separation   | Per-tenant feeds for client-derived IoCs           |
| Shared intelligence | Sanitized cross-tenant feeds explicitly configured |
| Access control      | Tenant-scoped per analyst assignment               |

### 9.1.5 Documentation Repositories

| Control          | Requirement                  |
| ---------------- | ---------------------------- |
| Folder structure | Per-tenant top-level folders |
| Access control   | RBAC per folder              |
| Versioning       | Per-tenant version control   |
| Backup           | Tenant-scoped backups        |

## 9.2 Data Layer Controls

| Control               | Requirement                                                           |
| --------------------- | --------------------------------------------------------------------- |
| Encryption at rest    | All client data encrypted with tenant-specific keys (where supported) |
| Encryption in transit | TLS 1.2+ for all client data flows                                    |
| Tenant tagging        | All data tagged with tenant ID                                        |
| Backup segregation    | Tenant-scoped backup configurations                                   |
| Storage isolation     | Logical or physical per tenant (per criticality)                      |
| Data residency        | Per client requirement                                                |

## 9.3 Network Layer Controls

| Control               | Requirement                                 |
| --------------------- | ------------------------------------------- |
| VLAN segmentation     | Tenant-specific VLANs where feasible        |
| Dedicated VPN tunnels | Per-client site-to-site VPN                 |
| Firewall rules        | Tenant-scoped firewall policies             |
| API gateways          | Per-tenant API endpoints with rate limiting |
| DNS isolation         | Tenant-scoped DNS where applicable          |

## 9.4 Infrastructure Layer Controls

| Control             | Requirement                                                       |
| ------------------- | ----------------------------------------------------------------- |
| Compute isolation   | Logical (containers/VMs per tenant) or physical (per criticality) |
| Storage isolation   | Per-tenant storage buckets/volumes                                |
| Hypervisor controls | Verified isolation between VMs                                    |
| Container isolation | Namespace/network/storage isolation                               |

---

# 10. Process Segregation Controls (Mandatory)

## 10.1 Workflow Controls

| Process           | Segregation Requirement                               |
| ----------------- | ----------------------------------------------------- |
| Alert triage      | Tenant-tagged alerts; analyst verifies tenant context |
| Investigation     | All artifacts tenant-scoped; no cross-references      |
| Containment       | Authority and actions limited to assigned tenant      |
| Reporting         | Tenant-scoped report generation                       |
| Evidence handling | Per-tenant evidence vaults                            |
| Communication     | Tenant-specific email aliases and channels            |
| Bridge calls      | Tenant-specific bridges; never joint                  |
| Documentation     | Per-tenant folders and access                         |

## 10.2 Cross-Tenant Operations (Strictly Controlled)

Legitimate cross-tenant activities require explicit authorization:

| Activity                         | Approval Required      | Sanitization Required                     |
| -------------------------------- | ---------------------- | ----------------------------------------- |
| Threat intel sharing (sanitized) | Threat Intel Lead      | Yes                                       |
| Lessons learned aggregation      | SOC Manager            | Yes                                       |
| Detection rule cross-application | Detection Eng Lead     | Yes (logic only, not client-derived data) |
| Trend analysis                   | SOC Manager            | Yes (anonymized)                          |
| Compliance reporting             | Compliance Lead        | Per audit scope only                      |
| Audit access                     | CISO + Client approval | Per audit scope only                      |
| Knowledge base updates           | IR Team Lead           | Yes (sanitized examples)                  |

## 10.3 Sanitization Standards (Mandatory)

When cross-tenant use of client-derived information is authorized, sanitization must:

| Sanitization Element              | Requirement                                   |
| --------------------------------- | --------------------------------------------- |
| Client name removed               | Replace with generic reference                |
| Client identifiers removed        | Account IDs, hostnames, IP ranges, user names |
| Specific business context removed | Industry-specific generalization only         |
| Specific systems anonymized       | Generic system descriptions                   |
| Customer PII removed              | All personal data removed                     |
| Financial details removed         | Specific amounts/transactions removed         |
| Geographic specifics generalized  | Region-level only, not site-level             |

### 10.3.1 Sanitization Approval

- Sanitization performed by authorized analyst
- Reviewed by second person (peer review)
- Approved by appropriate lead (Threat Intel Lead, IR Team Lead, etc.)
- Logged with approver, date, original source reference

---

# 11. Specific Scenario Guidance (Mandatory)

## 11.1 Threat Intelligence Sharing

| Scenario                                                  | Permitted?      | Conditions                                                |
| --------------------------------------------------------- | --------------- | --------------------------------------------------------- |
| Sharing IoC from Client A incident to Client B            | Yes (sanitized) | Generic IoC; no Client A attribution; approved            |
| Sharing TTP analysis                                      | Yes (sanitized) | TTPs are generic by nature; no client-specific procedures |
| Sharing client-specific compromise evidence               | No              | Client-confidential evidence stays in tenant              |
| Adding generic IoC to all-tenant TI feed                  | Yes             | Per TI sharing process                                    |
| Reporting client incident to CERT-In with client approval | Yes             | Client must approve specifically                          |

References:
`08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md`

## 11.2 Detection Rule Cross-Application

| Scenario                                                 | Permitted?                       | Conditions                               |
| -------------------------------------------------------- | -------------------------------- | ---------------------------------------- |
| Apply detection logic developed for Client A to Client B | Yes (logic only)                 | Logic generic; no Client A data embedded |
| Use Client A IoCs as detection in Client B               | No (unless sanitized + approved) | Per TI sharing process                   |
| Apply tuning learnings from Client A to Client B         | Yes (logic only)                 | Sanitized rationale                      |
| Develop generic detection from multiple client patterns  | Yes (anonymized aggregate)       | No individual client attribution         |

## 11.3 Lessons Learned

| Scenario                                  | Permitted?      | Conditions                                      |
| ----------------------------------------- | --------------- | ----------------------------------------------- |
| Document LL in Client A's records         | Yes             | Tenant-scoped                                   |
| Apply generic LL to MSSP master playbooks | Yes (sanitized) | No client identifiers                           |
| Share Client A LL with Client B           | No              | Even sanitized, requires explicit authorization |
| Internal LL session referencing Client A  | Restricted      | Only assigned analysts; no recordings shared    |

## 11.4 Analyst Cross-Tenant Communication

| Scenario                                          | Permitted? | Conditions                       |
| ------------------------------------------------- | ---------- | -------------------------------- |
| Asking colleague about Client A in shared chat    | No         | Use tenant-specific channel only |
| Discussing Client A on public Slack/Teams channel | No         | Tenant-scoped channels mandatory |
| Sharing Client A screenshot in MSSP-wide meeting  | No         | Sanitize first                   |
| Mentioning Client A as case study                 | Restricted | Sanitization + approval required |

## 11.5 Documentation Cross-References

| Scenario                                         | Permitted? | Conditions              |
| ------------------------------------------------ | ---------- | ----------------------- |
| Client A playbook references Client B            | No         | Strict prohibition      |
| Master playbook references generic learnings     | Yes        | Must be fully sanitized |
| Client A folder accessible by Client B's analyst | No         | RBAC must prevent       |

## 11.6 Reporting

| Scenario                                   | Permitted?       | Conditions                          |
| ------------------------------------------ | ---------------- | ----------------------------------- |
| Aggregated MSSP metrics in board report    | Yes              | Anonymized aggregate only           |
| Client-attributed metrics in marketing     | No               | Without explicit client approval    |
| Industry-trend reports                     | Yes (anonymized) | No individual client identification |
| Audit reports referencing specific clients | Per audit scope  | With client approval                |

---

# 12. Audit and Monitoring (Mandatory)

## 12.1 Continuous Monitoring

| Activity                                          | Frequency |
| ------------------------------------------------- | --------- |
| Access logs review (cross-tenant access attempts) | Daily     |
| Tool access audit                                 | Weekly    |
| User entitlement review                           | Quarterly |
| RBAC configuration audit                          | Quarterly |
| Cross-tenant data flow audit                      | Monthly   |
| Backup segregation validation                     | Monthly   |
| Network segmentation testing                      | Quarterly |

## 12.2 Periodic Audits

| Audit Type                         | Frequency   | Owner                        |
| ---------------------------------- | ----------- | ---------------------------- |
| Internal segregation audit         | Annually    | Compliance Lead              |
| Penetration testing (multi-tenant) | Annually    | External / Internal Red Team |
| SOC 2 / ISO 27001 audits           | Annually    | External                     |
| Client-requested audits            | Per request | Compliance + SDM             |

## 12.3 Detection Use Cases (Mandatory)

The MSSP SIEM must include detections for:

- Unauthorized cross-tenant access attempts
- Privilege escalation by analysts
- Bulk data exports
- Off-hours access by terminated personnel
- Direct database access bypassing applications
- Configuration changes to RBAC/ABAC

---

# 13. Segregation Breach Response (Mandatory)

## 13.1 Breach Categories

| Category                 | Examples                                          |
| ------------------------ | ------------------------------------------------- |
| **Personnel Breach**     | Analyst accessing unassigned tenant               |
| **Process Breach**       | Cross-tenant communication; non-sanitized sharing |
| **Technical Breach**     | RBAC misconfiguration; tool bug                   |
| **Data Breach**          | Client data leakage to another client's view      |
| **Communication Breach** | Sent to wrong tenant; discussed in wrong forum    |
| **Documentation Breach** | Client A info in Client B documentation           |

## 13.2 Breach Response Procedure

| Step | Action                          | Owner              | Timeline                  |
| ---- | ------------------------------- | ------------------ | ------------------------- |
| 1    | Detection / Report              | Any personnel      | Immediate                 |
| 2    | Initial assessment              | SOC Manager        | Within 1 hour             |
| 3    | Containment                     | SOC Manager + IT   | Within 4 hours            |
| 4    | Severity classification         | CISO               | Within 4 hours            |
| 5    | Internal investigation          | Compliance + IR    | Within 24 hours           |
| 6    | Affected client(s) notification | SDM + CISO + Legal | Per contract / regulation |
| 7    | Root cause analysis             | Compliance         | Within 7 days             |
| 8    | Corrective actions              | SOC Manager        | Per action plan           |
| 9    | Post-incident review            | CISO               | Within 30 days            |
| 10   | Lessons learned (sanitized)     | Compliance         | Within 60 days            |

## 13.3 Reporting Obligations

| Severity     | Internal Reporting       | Client Reporting             | Regulatory Reporting             |
| ------------ | ------------------------ | ---------------------------- | -------------------------------- |
| **Minor**    | SOC Manager              | Per contract (typically yes) | Per regulation (typically no)    |
| **Moderate** | CISO + Legal             | Mandatory                    | Per regulation                   |
| **Major**    | CISO + Legal + Executive | Mandatory + immediate        | Mandatory per applicable laws    |
| **Critical** | Executive + Board        | Mandatory + executive level  | Mandatory immediate notification |

## 13.4 Disciplinary Actions

Personnel violations addressed per HR policy:

- Verbal warning (first minor offense)
- Written warning (repeat or moderate offense)
- Suspension pending investigation (major offense)
- Termination (critical offense)
- Legal action (intentional violation with damage)

---

# 14. Training and Awareness (Mandatory)

| Training                             | Audience                     | Frequency      | Owner             |
| ------------------------------------ | ---------------------------- | -------------- | ----------------- |
| Initial multi-tenant policy training | All new personnel            | Onboarding     | Compliance + HR   |
| Annual refresher training            | All personnel                | Annually       | Compliance        |
| Tenant assignment briefing           | Per new assignment           | Per assignment | SDM               |
| Sanitization training                | Threat Intel + Detection Eng | Annually       | Threat Intel Lead |
| Breach response drill                | SOC Management               | Annually       | Compliance        |
| Client-specific NDA training         | Per client assignment        | Per assignment | Legal + SDM       |

---

# 15. Policy Exceptions (Mandatory)

Any deviation from this policy requires:

| Step | Action                                                    |
| ---- | --------------------------------------------------------- |
| 1    | Written exception request with business justification     |
| 2    | Risk assessment by Compliance                             |
| 3    | Approval by MSSP CISO                                     |
| 4    | If client data involved: client written approval required |
| 5    | Documentation in exception register                       |
| 6    | Defined exception expiry date                             |
| 7    | Compensating controls implemented                         |
| 8    | Quarterly review of active exceptions                     |
| 9    | Closure at expiry                                         |

References:
`00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`

---

# 16. Contract and Regulatory Alignment (Mandatory)

This policy supports:

| Framework / Regulation                                | Alignment                                       |
| ----------------------------------------------------- | ----------------------------------------------- |
| ISO 27001 Annex A.5.10, A.5.12, A.5.14, A.5.34, A.8.3 | Data classification, segregation, access        |
| NIST CSF ID.GV, ID.SC, PR.AC, PR.DS                   | Governance, supply chain, access, data security |
| SOC 2 Trust Services Criteria                         | Confidentiality, Privacy                        |
| RBI Cyber Security Framework                          | Outsourcing controls                            |
| RBI Outsourcing Guidelines                            | Service provider obligations                    |
| DPDP Act                                              | Data processor obligations                      |
| Client NDA / DPA / MSA                                | Contractual confidentiality                     |

---

# 17. Quality Checklist (Annual Validation)

Before annual policy approval:

- [ ] All principles enforced operationally
- [ ] Personnel segregation verified (RBAC/ABAC audit)
- [ ] Technical segregation validated (penetration test)
- [ ] Process segregation validated (workflow audit)
- [ ] Sanitization standards followed (TI / detection review)
- [ ] Monitoring active and alerting
- [ ] Training completion ≥95%
- [ ] No unresolved breach findings from prior period
- [ ] Exceptions reviewed and current
- [ ] Aligned with current contracts
- [ ] Aligned with regulatory changes
- [ ] Aligned with multi-tenant architecture changes
- [ ] Internal audit completed
- [ ] CISO approval obtained

---

# 18. Related Documents

| Document                          | Path                                                                                      |
| --------------------------------- | ----------------------------------------------------------------------------------------- |
| Multi-Client Alert Handling       | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`            |
| Cross-Client Incident Procedure   | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`        |
| Client Onboarding Checklist       | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Onboarding-Checklist.md`                  |
| Client Offboarding Checklist      | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Offboarding-Checklist.md`                 |
| Client Environment Profile        | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`          |
| Client IR Contacts                | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`                           |
| Client-Specific Playbook Guide    | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`   |
| MSSP ISO27001 Controls            | `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-ISO27001-Controls.md`                         |
| MSSP NIST Alignment               | `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-NIST-Alignment.md`                            |
| MSSP Audit Readiness Checklist    | `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-Audit-Readiness-Checklist.md`                 |
| MSSP-Client Responsibility Matrix | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`      |
| Policy Exception Register         | `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`                                |
| IoC Output Register               | `08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md`                        |
| Threat Actor Profile Template     | `08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md`              |
| TTP Intelligence Report           | `08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md`                    |
| MSSP Client Evidence Handling     | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md` |
| Detection Improvement Log         | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`                 |
| Playbook Update Log               | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`                       |

---

# 19. Revision History

| Version | Date        | Author                  | Changes         |
| ------- | ----------- | ----------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP CISO / SOC Manager | Initial version |

---

# 20. Approval

Approved by:

| Role                 | Name | Signature | Date |
| -------------------- | ---- | --------- | ---- |
| MSSP SOC Manager     |      |           |      |
| MSSP Compliance Lead |      |           |      |
| MSSP Legal Counsel   |      |           |      |
| MSSP CISO            |      |           |      |

---

**End of Document**
